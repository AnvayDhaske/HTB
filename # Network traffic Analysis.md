# Intro to Network traffic Analysis

## Workflow
1. What is the issue?
	-Suspected breach? Networking issue?
2. Define our scope and the goal (what are we looking for? which time period?)
	-target: multiple hosts potentially downloading a malicious file from bad.example.com
	-when: within the last 48 hours + 2 hours from now.
	-supporting info: filenames/types 'superbad.exe' 'new-crypto-miner.exe'
3. Define our target(s) (net / host(s) / protocol)
	-scope: 192.168.100.0/24 network protocols used were HTTP and FTP.
4. Capture network traffic
	-plug into a link with access to the 192.168.100.0/24 network to capture live traffic to try and grab one of the executables in transfer. See if an admin can pull PCAP and/or netflow 	data from our SIEM for the historical data.
5. Identification of required network traffic components (filtering)
	-once we have traffic, filter out any traffic not needed for this investigation to include; any traffic that matches our common baseline and keep anything relevant to the scope.`HTTP 	and FTP from the subnet, anything transferring or containing a GET request for the suspected executable files.
6. An understanding of captured network traffic
	-Once we have filtered out the noise, it's time to dig for our targets—filter on things like ftp-data to find any files transferred and reconstruct them. For HTTP, we can filter on - 	http.request.method == "GET" to see any GET requests that match the filenames we are searching for. This can show us who has acquired the files and potential other transfers internal 	to the network on the same protocols.
7. Note-taking and mind mapping of the found results.
	-Annotating everything we do, see, or find throughout the investigation is crucial. Ensure we are taking ample notes, including:
	-Timeframes we captured traffic during.
	-Suspicious hosts within the network.
	-Conversations containing the files in question. ( to include timestamps and packet numbers)
8. Summary of the analysis (what did we find?)
	-Finally, summarize what has been found, explaining the relevant details so that superiors can make an informed decision to quarantine the affected hosts or perform more significant 	incident response.
	-Our analysis will affect decisions made, so it is essential to be as clear and concise as possible.

## TCPdump
commandline packet sniffer for unix based operating systems. windump is a similar tool but for windows.
Filter	Result
host	host will filter visible traffic to show anything involving the designated host. Bi-directional
src / dest	src and dest are modifiers. We can use them to designate a source or destination host or port.
net	net will show us any traffic sourcing from or destined to the network designated. It uses / notation.
proto	will filter for a specific protocol type. (ether, TCP, UDP, and ICMP as examples)
port	port is bi-directional. It will show any traffic with the specified port as the source or destination.
portrange	portrange allows us to specify a range of ports. (0-1024)
less / greater "< >"	less and greater can be used to look for a packet or protocol option of a specific size.
and / &&	and && can be used to concatenate two different filters together. for example, src host AND port.
or	or allows for a match on either of two conditions. It does not have to meet both. It can be tricky.
not	not is a modifier saying anything but x. For example, not UDP.


IP :- https://datatracker.ietf.org/doc/html/rfc791
ICMP :- https://datatracker.ietf.org/doc/html/rfc792
TCP :- https://datatracker.ietf.org/doc/html/rfc793
UDP :- https://datatracker.ietf.org/doc/html/rfc768
all proto :- https://en.wikipedia.org/wiki/List_of_RFCs#Topical_list


## Termshark
Termshark is a Text-based User Interface (TUI) application that provides the user with a Wireshark-like interface right in your terminal window.
https://github.com/gcla/termshark.git

## Wireshark
some useful wireshark filters:-

| Capture Filter                 | Result                                                                 |
|-------------------------------|------------------------------------------------------------------------|
| `host x.x.x.x`                | Capture only traffic pertaining to a certain host                      |
| `net x.x.x.x/24`              | Capture traffic to or from a specific network (using slash notation)   |
| `src/dst net x.x.x.x/24`      | Capture traffic sourcing from or destined to the specified network     |
| `port #`                      | Filter all traffic **except** the specified port                       |
| `not port #`                  | Capture everything **except** the specified port                       |
| `port # and #`                | Use **AND** to combine multiple specified ports                        |
| `portrange x-x`               | Capture all traffic within the specified port range                    |
| `ip` / `ether` / `tcp`        | Capture only traffic from the specified protocol header                |
| `broadcast` / `multicast` / `unicast` | Capture based on traffic type: one-to-one, one-to-many, or one-to-all |

| Display Filter                    | Result                                                                 |
|----------------------------------|------------------------------------------------------------------------|
| `ip.addr == x.x.x.x`             | Capture only traffic pertaining to a certain host (OR logic)           |
| `ip.addr == x.x.x.x/24`          | Capture traffic pertaining to a specific network (OR logic)            |
| `ip.src` / `ip.dst == x.x.x.x`   | Capture traffic to or from a specific host                             |
| `dns` / `tcp` / `ftp` / `arp` / `ip` | Filter traffic by a specific protocol                                 |
| `tcp.port == x`                  | Filter by a specific TCP port                                          |
| `tcp.port` / `udp.port != x`     | Capture everything **except** the specified port                       |
| `and` / `or` / `not`             | Combine filters: AND = both, OR = either, NOT = exclude                |

ftp.request.command - Will show any commands sent across the ftp-control channel ( port 21 )
We can look for information like usernames and passwords with this filter. It can also show us filenames for anything requested.

https://www.wireshark.org/docs/dfref/f/ftp.html










