This task will cover how to perform a TCP ACK scan, a TCP window scan, and how to create your custom flag scan.

## TCP ACK Scan

Let’s start with the TCP ACK scan. As the name implies, an ACK scan will send a TCP packet with the ACK flag set. Use the -sA option to choose this scan. As we show in the figure below, the target would respond to the ACK with RST regardless of the state of the port. This behaviour happens because a TCP packet with the ACK flag set should be sent only in response to a received TCP packet to acknowledge the receipt of some data, unlike our case. Hence, this scan won’t tell us whether the target port is open in a simple setup.

<img width="862" height="260" alt="image" src="https://github.com/user-attachments/assets/f7136e6f-b364-4b6f-8b06-dc179309cc24" />

In the following example, we scanned the target VM before installing a firewall on it. As expected, we couldn’t learn which ports were open.

<img width="1562" height="405" alt="image" src="https://github.com/user-attachments/assets/efd5e419-df05-4ae8-ae41-9745153d990f" />

This kind of scan would be helpful if there is a firewall in front of the target. Consequently, based on which ACK packets resulted in responses, you will learn which ports were not blocked by the firewall. In other words, this type of scan is more suitable to discover firewall rule sets and configuration.

After setting up the target VM 10.48.129.213 with a firewall, we repeated the ACK scan. This time, we received some interesting results. As seen in the console output below, we have three ports that aren't being blocked by the firewall. This result indicates that the firewall is blocking all other ports except for these three ports.

<img width="1574" height="519" alt="image" src="https://github.com/user-attachments/assets/a58a9589-6370-4a8d-8ddd-fb5cffa913b3" />

## Window Scan

Another similar scan is the TCP window scan. The TCP window scan is almost the same as the ACK scan; however, it examines the TCP Window field of the RST packets returned. On specific systems, this can reveal that the port is open. You can select this scan type with the option -sW . As shown in the figure below, we expect to get an RST packet in reply to our “uninvited” ACK packets, regardless of whether the port is open or closed.

<img width="862" height="260" alt="image" src="https://github.com/user-attachments/assets/acaae863-45a8-409a-84d5-ef566b886c6e" />

Similarly, launching a TCP window scan against a Linux system with no firewall will not provide much information. As we can see in the console output below, the results of the window scan against a Linux server with no firewall didn’t give any extra information compared to the ACK scan executed earlier.

<img width="1566" height="404" alt="image" src="https://github.com/user-attachments/assets/df3a9393-4467-459a-8f29-b761d1f5f787" />

However, as you would expect, if we repeat our TCP window scan against a server behind a firewall, we expect to get more satisfying results. In the console output shown below, the TCP window scan pointed that three ports are detected as closed. (This is in contrast with the ACK scan that labelled the same three ports as unfiltered.) Although we know that these three ports are not closed, we realize they responded differently, indicating that the firewall does not block them.

<img width="1570" height="524" alt="image" src="https://github.com/user-attachments/assets/5f7d0a09-eb25-47a0-a120-f667c9f92436" />

## Custom Scan

If you want to experiment with a new TCP flag combination beyond the built-in TCP scan types, you can do so using --scanflags . For instance, if you want to set SYN, RST, and FIN simultaneously, you can do so using --scanflags RSTSYNFIN . As shown in the figure below, if you develop your custom scan, you need to know how the different ports will behave to interpret the results in different scenarios correctly.

<img width="862" height="262" alt="image" src="https://github.com/user-attachments/assets/314647b0-474e-44f6-abeb-cacc00fac6a7" />

Finally, it is essential to note that the ACK scan and the window scan were very efficient at helping us map out the firewall rules. However, it is vital to remember that just because a firewall is not blocking a specific port, it does not necessarily mean that a service is listening on that port. For example, there is a possibility that the firewall rules need to be updated to reflect recent service changes. Hence, ACK and window scans are exposing the firewall rules, not the services.

✅ Answer the questions below
1. In TCP Window scan, how many flags are set?
✅. 1 (ACK)
2. 
