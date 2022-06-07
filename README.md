# Assignment 4
1. Consider a broadcast channel with N nodes and a transmission rate of R bps. Suppose the broadcast channel uses polling (with an additional polling node) for multiple access. Suppose the amount of time from when a node completes transmission until the subsequent node is permitted to transmit (that is, the polling delay) is 𝑑poll. Suppose that within a polling round, a given node is allowed to transmit at most Q bits. What is the maximum throughput of the broadcast channel?
```
Polling round = N((Q / R) + dpoll)
Max throughput = (NQ) / (N((Q / R) + dpoll))
= Q / ((Q / R) + dpoll)
= Q / ((Q / R) + (Rdpoll / R))
= Q / ((Q + Rdpoll) / R)
= QR / (Q + Rdpoll)
```

![image](https://user-images.githubusercontent.com/25465133/172308598-c4eebd93-2e4b-4744-b126-fb64a22a44c3.png)
2. Consider three LANs interconnected by two routers, as shown in Figure 1.
  - Assign IP addresses to all of the interfaces. For Subnet 1 use addresses of the form 192.168.1.xxx; for Subnet 2 uses addresses of the form 192.168.2.xxx; and for Subnet 3 use addresses of the form 192.168.3.xxx.
```
Router 1-1: 192.168.1.1
A: 192.168.1.3
B: 192.168.1.4

Router 2-1: 192.168.3.1
E: 192.168.3.3
F: 192.168.3.4

Router 1-2: 192.168.2.1
Router 2-2: 192.168.2.2
C: 192.168.2.3
D: 192.168.2.4
```

  - Assign MAC addresses to all of the adapters.
```
Router 1-1: 00:00:00:00:00:00
A: 00:00:00:00:00:05
B: 00:00:00:00:00:06

Router 2-1: 00:00:00:00:00:03
E: 00:00:00:00:00:09
F: 00:00:00:00:00:0A

Router 1-2: 00:00:00:00:00:02
Router 2-2: 00:00:00:00:00:04
C: 00:00:00:00:00:07
D: 00:00:00:00:00:08
```
  - Consider sending an IP datagram from Host E to Host B. Suppose all of the ARP tables are up to date. Enumerate all the steps.
```
1. According to the forwarding table for host E, the IP datagram must be routed from 192.168.3.3 to 192.168.3.1
2. The interface for host E creates and sends an ethernet frame with a source of 00:00:00:00:00:09 and a destination of 00:00:00:00:00:03.
3. The Router 2-1 interface receives the frame and it is unpacked into a datagram.
4. According to the forwarding table for router 2, the datagram must be routed from 192.168.2.2 to 192.168.2.1
5. The Router 2-2 interface creates and sends an ethernet frame with a source of 00:00:00:00:00:04 and a destination of 00:00:00:00:00:02.
6. The Router 1-2 interface receives the frame and it is unpacked into a datagram.
7. According to the forwarding table for router 1, the datagram must be routed from 192.168.1.1 to 192.168.1.3
8. The Router 1-1 interface creates and sends an ethernet frame with a source of 00:00:00:00:00:00 and a destination of 00:00:00:00:00:06.
9. The Router 1-2 interface receives the frame and it is unpacked into a datagram.
```

  - Repeat (c), now assuming that the ARP table in the sending host is empty (and the other tables are up to date).
```
1. Host E broadcast a newly generated ARP frame, requesting the destination address of B.
2. Interface Router 2-1 receives the frame and has the corresponding destination address so a reply frame is generated.
3. Interface Router 2-1 responds back, using a destination address of host E.
4. Host E receives the reply frame and updates the ARP cache with the newly received information.
```

3. Consider the figure in Problem 4 above. Provide MAC addresses and IP addresses for the interfaces at Host A, both routers, and Host F. Suppose Host A sends a datagram to Host F. Give the source and destination MAC addresses in the frame encapsulating this IP datagram as the frame is transmitted (i) from A to the left router, (ii) from the left router to the right router, (iii) from the right router to F. Also give the source and destination IP addresses in the IP datagram encapsulated within the frame at each of these points in time.
```
1. A to Router 1-1
Source MAC: 00:00:00:00:00:05
Dest. MAC: 00:00:00:00:00:00
Source IP: 192.168.1.3
Dest. IP: 192.168.1.1

2. Router 1-2 to Router 2-2
Source MAC: 00:00:00:00:00:02
Dest. MAC: 00:00:00:00:00:04
Source IP: 192.168.2.1
Dest. IP: 192.168.2.2

3. Router 2-1 to F
Source MAC: 00:00:00:00:00:03
Dest. MAC: 00:00:00:00:00:0A
Source IP: 192.168.3.1
Dest. IP: 192.168.3.4
```

4. Given the following data 𝐷 = 1011110111 and generator 𝐺 = 1001 please compute:
  - The redundancy data 𝑅
```
1011110111000
1001
 010110111000
 0000
  10110111000
  1001
   0100111000
   0000
    100111000
    1001
     00011000
     0000
      0011000
      0000
       011000
       0000
        11000
        1001
         1010
         1001
          011
Redundancy = 011
```

  - Verify < 𝐷, 𝑅 > using both approaches discussed in class (hint: think twice before you work too hard).
```
…
11011
1001
  1001
  1001
    000
Remained = 0 => no error
```
  - Now, verify that < 𝐷 ′, 𝑅 > with 𝐷 ′ = 1010110111 indeed contains an error when received.
```
1010110111011
1001
 011110111011
 0000
  11110111011
  1001
   1100111011
   1001
    101111011
    1001
     01011011
     0000
      1011011
      1001
       010011
       0000
        10011
        1001
         0001
         0000
          001
Remainder = 001 => error
```

5. (Bonus) Compute the RSA signatures for the given message 𝑥 with the given key pair of (𝑛,𝑒) = (1739,17) and (𝑑) = (1169). Verify your results by verifying the computed signature.
  - x = 54
```
C = xe % N
= 5417 % 1739
= 1604

x = Cd % N
= 16041169 % 1739
= 54
```

  - x = 19
```
C = xe % N
= 1917 % 1739
= 590

x = Cd % N
= 5901169 % 1739
= 19
```
