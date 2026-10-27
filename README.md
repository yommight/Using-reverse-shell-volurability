<img width="764" height="607" alt="Kali-2026-10-27-05-05-28" src="https://github.com/user-attachments/assets/83ed472a-1fee-46d8-97d7-c6571fddf041" />
<img width="764" height="607" alt="Kali-2026-10-27-04-27-51" src="https://github.com/user-attachments/assets/57fa8005-858d-44f6-9508-87dea95fb314" />
# Using-reverse-shell-volurability
This a exploit testing using reverse shell to deliver a payload to metasploit  machine 
<img width="858" height="610" alt="Kali-2026-10-27-03-38-58" src="https://github.com/user-attachments/assets/1b1ce408-5e2d-4726-b703-86efc7e551a2" />

The testing captured in the terminal screenshot identified two SSH connection issues while attempting to connect to remote hosts using the account msfadmin
SSH host key compatibility failure: The server at 192.168.217.129 offers legacy host key algorithms (ssh-rsa and ssh-dss) that the SSH client does not accept by default.
Network connectivity failure: A connection attempt to 192.168.217.128 failed with a “Network is unreachable” message.
FTP session: The screenshot also shows a successful FTP directory listing and a 221 Goodbye response, indicating that the FTP session ended normally. This does not establish that SSH access is available.
The primary finding is that SSH access to 192.168.217.129 was blocked during host key negotiation, before successful authentication could be established. The failure for 192.168.217.128 occurred at the network connectivity stage.
Analysis: The SSH client and server could not agree on a host key algorithm. Both ssh-rsa (the legacy SHA-1 signature scheme) and ssh-dss (DSA) are legacy algorithms, and modern clients commonly disable them by default.
Result: The connection failed before the screenshot could establish whether the credentials were valid.
Solution ssh -o HostKeyAlgorithms=+ssh-rsa \msfadmin@192.168.217.129 was used before the LHOST can communicate with the RHOST
Check that the target IP address is correct, both systems are connected to the intended virtual network, and the relevant network interfaces and routes are configured properly.
