Uriel Maimon first described this scan in 1996. In this scan, the FIN and ACK bits are set. The target should send an RST packet as a response. However, certain BSD-derived systems drop the packet if it is an open port exposing the open ports. This scan won’t work on most targets encountered in modern networks; however, we include it in this room to better understand the port scanning mechanism and the hacking mindset. To select this scan type, use the -sM option.

Most target systems respond with an RST packet regardless of whether the TCP port is open. In such a case, we won’t be able to discover the open ports. The figure below shows the expected behaviour in the cases of both open and closed TCP ports.

<img width="862" height="280" alt="image" src="https://github.com/user-attachments/assets/87d1843a-34f8-4da5-92a5-b7f42ba137ee" />

The console output below is an example of a TCP Maimon scan against a Linux server. As mentioned, because open ports and closed ports are behaving the same way, the Maimon scan could not discover any open ports on the target system.

<img width="1564" height="368" alt="image" src="https://github.com/user-attachments/assets/02c1af25-9a5f-4d29-ae59-a5abaa184267" />

This type of scan is not the first scan one would pick to discover a system; however, it is important to know about it as you don’t know when it could come in handy.

✅Answer the questions below

1. In the Maimon scan, how many flags are set?

✅. 2 FIN/ACK
