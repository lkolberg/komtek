# Trace a route to a remote server using tracer(traceroute MacOs terminal)
Hver linje som blir returnert representerer et hopp fra en router til en annen.
En Router er en liten datamskin designet for å dirigere trafikk på internet. 
Når vi bruker traceroute på et domene så får vi returnert hele ruten fra vår pc
til den serveren som dette domenet peker på. Dette blir på en måte en veibeskrivelse 
til denne serveren fra hvor vi er nå. 

Eksempel på Traceroute kall til www.cisco.com i terminalen:
>~$ traceroute www.cisco.com <br> 
traceroute to e144.dscb.akamaiedge.net (23.5.49.120), 64 hops max, 52 byte packets
 >1.  10.0.1.1 (10.0.1.1)  1.601 ms  1.208 ms  1.107 ms
 >2.  10.243.0.1 (10.243.0.1)  7.033 ms  8.402 ms  7.858 ms
 >3.  cm-84.208.41.70.getinternet.no (84.208.41.70)  15.675 ms  10.222 ms  15.760 ms
 >4.  a23-5-48-1.deploy.static.akamaitechnologies.com (23.5.48.1)  15.918 ms  14.903 ms  15.858 ms
 >5.  a23-5-49-120.deploy.static.akamaitechnologies.com (23.5.49.120)  17.009 ms  16.544 ms  15.710 ms
 
Every router has it's own IP adress. The traceroute tool shows the route a package has to travel before it reaches
it's final destination. Three packages are sent and these are used to measure min, max and average latency for each
hop(This means that three packages are sent for every single hop) of the way until our final destination which is the www.cisco.com server in our example above. 
The hop 2(point number 2) is the ISP's POP (Point Of Presence) router. Every ISP has several POP routers that
are located at the end of their network, and this is where the customers connect to the Internet. We can see
from the terminal that the packet travels on the getinternet ISP on the 3 hop and jumps to static.akamaitechnologies
on the 4 hop. This is a critical travel in the trace bacause sometimes there is packet loss in the transition 
between two IPS's or one of the IPS's are slower than the other. 

The formate of each line is as follows:<br>
>Hop RTT1 RTT2 RTT3 Domain Name [IP Adress]<br>
>- RTT1, RTT2 and RTT3 is the roundtrip it takes for a package to get to a hop and back to your computer 
(in milliseconds). The travel is inconsistent if the three package latency numbers vary alot.  

_________
**whois** can be used to determine what ISP is on a particular domain. 

>~$ whois 23.5.48.1<br>
[Akamai International, BV AIBV (NET-23-5-48-0-1) 23.5.48.0 - 23.5.63.255](https://whois.arin.net/rest/nets;q=23.5.48.1?showDetails=true&showARIN=false&showNonArinTopLevelNet=false&ext=netref2)
#
## Examine the traceroute for www.afrinic.net
> ~ $ traceroute www.afrinic.net
traceroute to www.afrinic.net (196.216.2.6), 64 hops max, 52 byte packets
 >1.  10.0.1.1 (10.0.1.1)  1.670 ms  1.214 ms  1.125 ms
 >2.  10.243.0.1 (10.243.0.1)  6.146 ms  7.729 ms  8.105 ms
 >3.  cm-84.208.41.68.getinternet.no (84.208.41.68)  10.443 ms  8.485 ms  7.748 ms
 >4.  ae10-0.poh-pe1.stv.no.ip.tdc.net (93.124.128.162)  7.918 ms  8.790 ms  14.361 ms
 >5.  ae0-0.san-peer2.osl.no.ip.tdc.net (85.19.120.129)  15.542 ms  16.581 ms  14.491 ms
 >6.  4.68.72.25 (4.68.72.25)  15.695 ms  15.342 ms  15.536 ms
 >7.  ae-228-3604.edge3.london1.level3.net (4.69.166.158)  38.191 ms  51.901 ms
    ae-226-3602.edge3.london1.level3.net (4.69.166.150)  37.870 ms
 >8.  internet-so.edge3.london1.level3.net (195.50.124.34)  41.399 ms  40.679 ms  40.724 ms
 >9.  168.209.0.177 (168.209.0.177)  225.873 ms  234.537 ms  310.096 ms
>10.  168.209.0.177 (168.209.0.177)  304.353 ms  306.709 ms  307.168 ms
>11.  196.26.0.68 (196.26.0.68)  205.613 ms  205.424 ms  203.128 ms
>12.  196.37.155.172 (196.37.155.172)  235.932 ms  307.010 ms  307.039 ms
>13.  196.216.3.131 (196.216.3.131)  307.189 ms  258.175 ms  307.593 ms
>14.  www.afrinic.net (196.216.2.6)  306.994 ms  273.710 ms  307.201 ms

**What happens at hop 7?**<br>
It looks like the travel time is inconsistent. The RTT2 package uses more time than the other two.
One of the packages is actually sendt to a different IP adress <br>

# Qustions from the introduction to networking book 1.3.1.3 Part 2
**What happens at hop 7?**<br>
All three packages are received at the exact same time. 

