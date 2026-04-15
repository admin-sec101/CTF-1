**h4cked**

Find out what happened by analysing a .pcap file and hack your way back into the machine

https://tryhackme.com/room/h4cked

<img width="732" height="522" alt="image" src="https://github.com/user-attachments/assets/34d87d1d-9625-4132-a90c-6f232ae48139" />


Q.1: The attacker is trying to log into a specific service. What service is this?

<img width="433" height="82" alt="image" src="https://github.com/user-attachments/assets/1fc392cc-170e-489a-ae1a-6c7cd90236a8" />

<img width="1182" height="87" alt="image" src="https://github.com/user-attachments/assets/7f92c7a6-c843-420b-a9b8-70faf8d46428" />

```Answer: FTP```

Q.2: There is a very popular tool by Van Hauser which can be used to brute force a series of services. What is the name of this tool?

<img width="483" height="91" alt="image" src="https://github.com/user-attachments/assets/fc9692ed-60dd-4da6-948b-e92b1a245643" />

<img width="1192" height="104" alt="image" src="https://github.com/user-attachments/assets/1366afaf-f169-4218-89d1-ad3280fa10cf" />

```Answer: Hydra```

Q.3: The attacker is trying to log on with a specific username. What is the username?

<img width="1273" height="605" alt="image" src="https://github.com/user-attachments/assets/dba25aa5-3b58-4b72-abcf-2f82f3d29379" />

<img width="1189" height="91" alt="image" src="https://github.com/user-attachments/assets/fe409061-967d-4319-a8db-9e83301c0bf0" />


```Answer: jenny```

Q.4: What is the user’s password?

```Answer:password123```

<img width="1323" height="621" alt="image" src="https://github.com/user-attachments/assets/497c56c3-61f2-409b-b311-715dd4d13f67" />

<img width="1192" height="97" alt="image" src="https://github.com/user-attachments/assets/9f6bfeea-070e-4b31-9e16-563133c70ce4" />

```
220 Hello FTP World!

USER jenny

331 Please specify the password.

PASS 111111

530 Login incorrect.

USER jenny

331 Please specify the password.

PASS password123

230 Login successful.
```

Q.5: What is the current FTP working directory after the attacker logged in?

```Answer: /var/www/html```

<img width="1276" height="609" alt="image" src="https://github.com/user-attachments/assets/42368d4f-8801-489a-beda-dd865b33faf6" />

<img width="1180" height="93" alt="image" src="https://github.com/user-attachments/assets/8622d7d4-f8e7-4d6d-9970-f83bf4081265" />

Q.6: The attacker uploaded a backdoor. What is the backdoor’s filename?

```Answer: shell.php```

<img width="1186" height="89" alt="image" src="https://github.com/user-attachments/assets/774084a3-5500-4698-887b-1fbf1310108b" />

<img width="756" height="655" alt="image" src="https://github.com/user-attachments/assets/00693cad-4567-4f04-ba67-fc7e6af514b8" />

Q.7: The backdoor can be downloaded from a specific URL, as it is located inside the uploaded file. What is the full URL?

```Answer: http://pentestmonkey.net/tools/php-reverse-shell```
    
<img width="557" height="211" alt="image" src="https://github.com/user-attachments/assets/a275aa3d-374f-49e3-ac61-296480d19f02" />

<img width="1180" height="90" alt="image" src="https://github.com/user-attachments/assets/e90fa2f5-7d6f-475c-9b76-45fdc1497eee" />

Q.8: Which command did the attacker manually execute after getting a reverse shell?

Answer: whoami

<img width="1232" height="611" alt="image" src="https://github.com/user-attachments/assets/1e2b3aff-bbb6-4a3c-a076-b9c4ae3935a0" />

<img width="1184" height="91" alt="image" src="https://github.com/user-attachments/assets/cd1791a9-a8d6-4810-9c9c-d09d1ce91a99" />

Q.9: What is the computer’s hostname?

```Answer: wir3```

<img width="759" height="447" alt="image" src="https://github.com/user-attachments/assets/e8a76815-1a68-4e6f-91c6-bf6dbdffcb94" />

Q.10: Which command did the attacker execute to spawn a new TTY shell?

```Answer:python3 -c 'import pty; pty.spawn("/bin/bash")'```

<img width="765" height="173" alt="image" src="https://github.com/user-attachments/assets/fd0a00bc-9577-4d5c-bdf9-bb8e971c93d8" />

<img width="1186" height="97" alt="image" src="https://github.com/user-attachments/assets/781d597c-454f-4c12-be83-3810268394c6" />

Q.11: Which command was executed to gain a root shell?

<img width="764" height="241" alt="image" src="https://github.com/user-attachments/assets/6ecc722f-1bd1-48b2-bcd9-fb63db022a53" />

```Answer: sudo su```

Q.11: The attacker downloaded something from GitHub. What is the name of the GitHub project?

```Answer: Reptile```

<img width="764" height="152" alt="image" src="https://github.com/user-attachments/assets/c1a675a2-c420-4c10-b0a7-d064b39a2487" />

<img width="1191" height="105" alt="image" src="https://github.com/user-attachments/assets/6f9fa9e7-c78e-4bb2-8edf-b2087315960d" />

Q.12: The project can be used to install a stealthy backdoor on the system. It can be very hard to detect. What is this type of backdoor called?

```Answer: rootkit```
