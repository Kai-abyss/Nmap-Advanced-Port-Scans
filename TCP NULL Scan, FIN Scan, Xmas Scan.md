Let’s start with the following three types of scans:
  * Null Scan
  * FIN Scan
  * Xmas Scan
## Null Scan
The null scan does not set any flag; all six flag bits are set to zero. You can choose this scan using the -sN option. A TCP packet with no flags set will not trigger any response when it reaches an open port, as shown in the figure below. Therefore, from Nmap’s perspective, a lack of reply in a null scan indicates that either the port is open or a firewall is blocking the packet.
<img width="862" height="220" alt="image" src="https://github.com/user-attachments/assets/a78f0445-0941-4a39-8b73-7321337131df" />
However, we expect the target server to respond with an RST packet if the port is closed. Consequently, we can use the lack of RST response to figure out the ports that are not closed: open or filtered.
