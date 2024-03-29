# Packetify

Packetify is a wrapper over tcpdump utility which is a powerful command-line packet analyzer on UNIX/Linux platforms.

With normal tcpdump command, as a system admin, you need to collect all the public IP addresses configured on the server and set the port you want with long arguments/flags.

Using packetify, you only need to pass the port numbers as arguments, rest will be taken care by packetify.

### Prerequisites
- tcpdump

#### Install tcpdump on an rpm based machine.
```
# yum install tcpdump -y
```
#### Install tcpdump on a debian based machine.
```
# apt install tcpdump -y
```



### Install packetify
```
curl -o packetify https://raw.githubusercontent.com/vjwilson1987/packetify/master/packetify.py
chmod +x packetify
sudo install -m 755 packetify /usr/local/bin
```

### Usage

```
  --ports PORTS [PORTS ...]
                        List of ports to monitor
  --version             Check the version
```
#### Sample output

```
# packetify
usage: packetify [--ports PORTS [PORTS ...] | --version]

packetify is a wrapper over tcpdump utility to monitor network traffic on specific ports. It is
designed to run on Linux systems

options:
  --ports PORTS [PORTS ...]
                        List of ports to monitor
  --version             Check the version
```

```
# packetify --ports 80

Target ports are: 80

Command to run:

		tcpdump -nn -tttt -A -i eth0 "(dst host 59.x.x.x) and (dst port 80)"

Proceed? yes|y / no|n: n

Chose to exit. Goodbye.
```

```
# packetify --ports 80 443

Target ports are: 80 443

Command to run:

		tcpdump -nn -tttt -A -i eth0 "(dst host 59.x.x.x) and (dst port 80 or dst port 443)"

Proceed? yes|y / no|n: y
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
2024-03-10 19:43:58 UTC - packetify - INFO - 2024-03-10 19:43:57.539949 IP 81.x.x.x.56629 > 59.x.x.x.443: Flags [S], seq 3466351037, win 65535, options [mss 1460,nop,wscale 6,nop,nop,TS val 137554078 ecr 0,sackOK,eol], length 0
2024-03-10 19:43:58 UTC - packetify - INFO - E..@....4..G...`_....5....Q.........Lo.............
2024-03-10 19:43:58 UTC - packetify - INFO - .2..........
2024-03-10 19:43:58 UTC - packetify - INFO - 2024-03-10 19:43:57.541997 IP 81.x.x.x.56630 > 59.x.x.x.443: Flags [S], seq 4093737496, win 65535, options [mss 1460,nop,wscale 6,nop,nop,TS val 1533796160 ecr 0,sackOK,eol], length 0
2024-03-10 19:43:58 UTC - packetify - INFO - E..@....4..G...`_....6....z........................
2024-03-10 19:43:58 UTC - packetify - INFO - [k.@........
2024-03-10 19:43:58 UTC - packetify - INFO - 2024-03-10 19:43:57.554493 IP 81.x.x.x.56629 > 59.x.x.x.443: Flags [.], ack 1631265285, win 2053, options [nop,nop,TS val 137554093 ecr 1524608929], length 0
2024-03-10 19:43:58 UTC - packetify - INFO - E..4....4..S...`_....5....Q.a;"......Y.....
2024-03-10 19:43:58 UTC - packetify - INFO - .2..Z...
2024-03-10 19:43:58 UTC - packetify - INFO - 2024-03-10 19:43:57.554494 IP 81.x.x.x.56630 > 59.x.x.x.443: Flags [.], ack 1004221362, win 2053, options [nop,nop,TS val 1533796175 ecr 1524608929], length 0
2024-03-10 19:43:58 UTC - packetify - INFO - E..4....4..S...`_....6....z.;.3.....rp.....
2024-03-10 19:43:58 UTC - packetify - INFO - [k.OZ...
2024-03-10 19:43:58 UTC - packetify - INFO - 2024-03-10 19:43:57.555606 IP 81.x.x.x.56629 > 59.x.x.x.443: Flags [P.], seq 0:576, ack 1, win 2053, options [nop,nop,TS val 137554093 ecr 1524608929], length 576
2024-03-10 19:43:58 UTC - packetify - INFO - E..t....4......`_....5....Q.a;"............
2024-03-10 19:43:58 UTC - packetify - INFO - .2..Z.......;...7...o...S.....($..2L`S..1y...`R]... <.....)..C?..2.Ls |..z.]"^$...r\. .........+./.,.0............./.5....jj.........................+.................#...
2024-03-10 19:43:58 UTC - packetify - INFO - .
```

### Logging
By default it logs everything to a file named **tcpdump.log** with the system date, time and timezone which is created on the same location you run this script.
