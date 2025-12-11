
https://grokipedia.com/page/Path_MTU_Discovery


PMTUD promotes robust, efficient data transfer by ensuring packets are tailored to the narrowest constraint in the path. This endpoint-driven approach aligns with the [end-to-end principle](https://grokipedia.com/page/End-to-end_principle) of the [Internet](https://grokipedia.com/page/Internet), placing responsibility for path adaptation on the communicating hosts rather than intermediate devices.

Path MTU Discovery is a mechanism that determines the maximum transmission unit (MTU) size on the network path between two IP hosts. This prevents fragmentation by finding the largest packet size that can traverse the path without being broken up.


Convergence to the correct MTU can be slower, especially in high-loss networks, due to reliance on transport-specific loss detection, which may require multiple retransmissions or timeouts.



Application can also control PMTUD behavoiur

```c
// C socket programming example
int val = IP_PMTUDISC_DO;  // Enable PMTUD
setsockopt(sock, IPPROTO_IP, IP_MTU_DISCOVER, &val, sizeof(val));

// Query discovered MTU
int mtu;
socklen_t len = sizeof(mtu);
getsockopt(sock, IPPROTO_IP, IP_MTU, &mtu, &len);
```

tracepath to find the pmtu 


Problema del PMTUD è che alcuni dispositvi applicano filtering ICMP quindi non abbiamo risposta al traffico e non siamo in grado di determinare il valore 

routers silently discard oversized IP packets that have the Don't Fragment (DF) bit set, without transmitting the required ICMP "Destination Unreachable—Fragmentation Needed" message to inform the sender of the MTU restriction. This lack of feedback prevents the source host from adjusting its packet size downward, resulting in persistent transmission attempts with the same oversized packets that continue to be dropped.


Nel caso questo sia bloccato si utilizza un'altra alternativa ovvero il Packetization Layer 


