Let’s start with the following three types of scans:
  * Null Scan
  * FIN Scan
  * Xmas Scan
## Null Scan
The null scan does not set any flag; all six flag bits are set to zero. You can choose this scan using the -sN option. A TCP packet with no flags set will not trigger any response when it reaches an open port, as shown in the figure below. Therefore, from Nmap’s perspective, a lack of reply in a null scan indicates that either the port is open or a firewall is blocking the packet.
<img width="862" height="220" alt="image" src="https://github.com/user-attachments/assets/a78f0445-0941-4a39-8b73-7321337131df" />

However, we expect the target server to respond with an RST packet if the port is closed. Consequently, we can use the lack of RST response to figure out the ports that are not closed: open or filtered.

<img width="862" height="260" alt="image" src="https://github.com/user-attachments/assets/70f7b978-a1f5-4ad1-97da-7f1901280f0d" />

Below is an example of a null scan against a Linux server. The null scan we carried out has successfully identified the six open ports on the target system. Because the null scan relies on the lack of a response to infer that the port is not closed, it cannot indicate with certainty that these ports are open; there is a possibility that the ports are not responding due to a firewall rule.

<img width="1528" height="532" alt="image" src="https://github.com/user-attachments/assets/794e770e-46e5-4442-974a-5855cd4cc177" />

Note that many Nmap options require root privileges. Unless you are running Nmap as root, you need to use sudo as in the example above using the -sN option.

## FIN Scan

The FIN scan sends a TCP packet with the FIN flag set. You can choose this scan type using the -sF option. Similarly, no response will be sent if the TCP port is open. Again, Nmap cannot be sure if the port is open or if a firewall is blocking the traffic related to this TCP port.

<img width="862" height="220" alt="image" src="https://github.com/user-attachments/assets/cc95bea8-6298-4a09-b279-e2485ac02d2e" />

However, the target system should respond with an RST if the port is closed. Consequently, we will be able to know which ports are closed and use this knowledge to infer the ports that are open or filtered. It's worth noting some firewalls will 'silently' drop the traffic without sending an RST.

<img width="862" height="260" alt="image" src="https://github.com/user-attachments/assets/b6e57668-e00e-4186-84f2-5ce3892d63dc" />

Below is an example of a FIN scan against a Linux server. The result is quite similar to the result we obtained earlier using a null scan.

<img width="1558" height="595" alt="image" src="https://github.com/user-attachments/assets/24d237e9-5af9-4366-961e-39145af3b077" />

## Xmas Scan
The Xmas scan gets its name after Christmas tree lights. An Xmas scan sets the FIN, PSH, and URG flags simultaneously. You can select Xmas scan with the option -sX.

Like the Null scan and FIN scan, if an RST packet is received, it means that the port is closed. Otherwise, it will be reported as open|filtered.

The following two figures show the case when the TCP port is open and the case when the TCP port is closed.

<img width="862" height="220" alt="image" src="https://github.com/user-attachments/assets/39b70891-9191-46bf-bc07-08c8d519a160" />

<img width="862" height="260" alt="image" src="https://github.com/user-attachments/assets/a5d9123f-ddde-439b-a911-ba7d154c293d" />

The console output below shows an example of a Xmas scan against a Linux server. The obtained results are pretty similar to that of the null scan and the FIN scan.

<img width="1558" height="583" alt="image" src="https://github.com/user-attachments/assets/053519b5-9231-434c-93e7-571ea9b6e65b" />

One scenario where these three scan types can be efficient is when scanning a target behind a stateless (non-stateful) firewall. A stateless firewall will check if the incoming packet has the SYN flag set to detect a connection attempt. Using a flag combination that does not match the SYN packet makes it possible to deceive the firewall and reach the system behind it. However, a stateful firewall will practically block all such crafted packets and render this kind of scan useless.

✅ Answer the questions below

1. In a null scan, how many flags are set to 1?
✅ . 0 [NULL (NO FLAG SET)]
2. In a FIN scan, how many flags are set to 1?
✅ . 1 (FIN)
3. In a Xmas scan, how many flags are set to 1?
✅ . 3 (FIN, PSH, URG)
4. Start the VM and load the AttackBox. Once both are ready, open the terminal on the AttackBox and use nmap to launch a FIN scan against the target VM. How many ports appear as open|filtered?
✅ . 9

<img width="902" height="603" alt="image" src="https://github.com/user-attachments/assets/abc27831-acdb-4e1a-88b1-48aa6766d7f1" />


5.Repeat your scan launching a null scan against the target VM. How many ports appear as open|filtered?
✅ . 9

<img width="936" height="626" alt="image" src="https://github.com/user-attachments/assets/bfd136c0-3845-41b6-9990-0c7b2393211c" />
