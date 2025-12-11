
To see information about the ipv4 and ipv6 configuration in linux use:
```bash
# IPv4 fragment settings
$ sysctl -a | grep ipfrag
...
net.ipv4.ipfrag_high_thresh = 4194304    # 4MB max memory for fragments
net.ipv4.ipfrag_low_thresh = 3145728     # 3MB threshold
net.ipv4.ipfrag_time = 30                # 30 second timeout
net.ipv4.ipfrag_max_dist = 64            # Max fragment queue size
...
```

### References

- https://grokipedia.com/page/IP_fragmentation_attack


# Introduction

In the Internet Protocol (IP), fragmentation occurs when a packet exceeds the maximum transmission unit (MTU) size of a network link, prompting the sender or an intermediate router to divide it into smaller fragments for transmission. This process begins with the source host or router examining the packet's total length against the outgoing interface's MTU; if exceeded, the packet is split into fragments, each carrying a copy of the original IP header with modifications to specific fields. The Total Length field is adjusted for each fragment to reflect its individual size, the Fragment Offset is set to indicate the position of the fragment's data relative to the original packet (expressed in multiples of 8 bytes), and the More Fragments (MF) flag is set to 1 for all but the last fragment, signaling that additional pieces follow. The Identification field remains identical across all fragments to enable later reassembly, while the Header Checksum is recalculated for each modified header. This mechanism, defined in the IPv4 specification, ensures that oversized datagrams can traverse diverse network paths with varying MTU limits without requiring the source to know all intermediate constraints in advance.


Reassembly is performed exclusively at the destination [host](https://grokipedia.com/page/Host), where incoming fragments are buffered and reconstructed into the original packet using the shared Identification field to group related pieces. The receiving system sorts the fragments by their [offset](https://grokipedia.com/page/Offset) values, concatenating the [data](https://grokipedia.com/page/Data) payloads in sequence while ignoring the [IP](https://grokipedia.com/page/IP) headers after the first fragment's [offset](https://grokipedia.com/page/Offset) reaches zero. Reassembly completes when a fragment arrives with the MF flag set to 0, indicating the end of the [datagram](https://grokipedia.com/page/Datagram); if fragments are missing, the entire set is discarded after a reassembly [timer](https://grokipedia.com/page/Timer) expires, typically between 15 and 60 seconds, to prevent indefinite buffering of incomplete packets. During this process, the destination verifies the integrity of the reassembled [datagram](https://grokipedia.com/page/Datagram), including recalculating the [checksum](https://grokipedia.com/page/Checksum) on the full [payload](https://grokipedia.com/page/Payload), and handles any out-of-order arrivals by holding fragments until the sequence is complete. This end-to-end approach offloads the complexity from routers, which only fragment but do not reassemble, thereby minimizing processing overhead in transit.2

In normal operations, error handling during fragmentation involves the generation of Internet Control Message Protocol (ICMP) messages to inform the source of issues, such as when a router cannot forward a fragmented packet due to a smaller downstream MTU. Specifically, the router sends an ICMP "Fragmentation Needed" message (Type 3, Code 4) back to the source, including the next-hop MTU in the unused field to suggest path MTU discovery adjustments. The source can then reduce its packet size accordingly to avoid future fragmentation. If reassembly fails at the destination due to lost fragments, no explicit feedback is provided to the source, relying instead on higher-layer protocols like TCP to detect and retransmit lost data. These mechanisms promote robust transmission across heterogeneous networks.

The mechanics of fragmentation and reassembly introduce [performance](https://grokipedia.com/page/Performance) considerations, particularly in terms of [resource](https://grokipedia.com/page/Resource) utilization and [latency](https://grokipedia.com/page/Latency). Reassembly at the destination imposes CPU overhead for buffering, sorting, and [checksum](https://grokipedia.com/page/Checksum) verification, which can become significant in high-traffic environments where multiple concurrent datagrams require simultaneous handling, potentially leading to [memory](https://grokipedia.com/page/Memory) exhaustion if fragment queues grow unchecked. In IPv4 networks, fragmentation can increase [end-to-end delay](https://grokipedia.com/page/End-to-end_delay) due to the additional processing and the risk of fragment loss, which discards entire packets rather than individual segments, amplifying inefficiency compared to unfragmented transmission. To mitigate these impacts, modern networks encourage [path MTU discovery](https://grokipedia.com/page/Path_MTU_Discovery) to minimize fragmentation occurrences, though it remains essential for compatibility with legacy or variable-MTU links.



### Fragmentation for Network Evasion
Attackers exploit [IP fragmentation](https://grokipedia.com/page/IP_fragmentation) to evade network intrusion detection systems (IDS) and firewalls by splitting malicious [payloads](https://grokipedia.com/page/Payload) across multiple fragments, ensuring that individual fragments appear benign while the fully reassembled packet reveals the attack.

This vulnerability stemmed from discrepancies between how IDS reassembled packets and how end-hosts did so, enabling evasion without detection.
Modern [deep packet inspection](https://grokipedia.com/page/Deep_packet_inspection) (DPI) systems mitigate this by performing full reassembly before analysis, though legacy or misconfigured devices remain susceptible.

As of 2025, these [IPv6](https://grokipedia.com/page/IPv6) vulnerabilities persist, with attackers abusing extension headers for evasion in high-speed networks, prompting ongoing research into adaptive detection

#### Resource Exhaustatoin

This mechanism exploits the stateless nature of IP fragmentation, where each fragment arrival triggers [buffer](https://grokipedia.com/page/Buffer) allocation without immediate validation of completeness, resulting in sustained resource holdover

To amplify the attack's effectiveness, perpetrators often employ IP spoofing to masquerade fragment sources, distributing the load across numerous apparent origins and evading source-based filtering, akin to amplification techniques in UDP-based floods like Fraggle but adapted to fragmented IP traffic. This distributed approach enables a single attacker or botnet to simulate traffic from diverse endpoints, multiplying the volume of incomplete fragments and complicating traceback efforts. In practice, such spoofing allows for volumetric scaling, where even modest per-source rates accumulate to saturate inbound links
These effects disrupt network availability, with devices prioritizing fragment processing over normal operations, thereby amplifying the attack's reach in both [enterprise](https://grokipedia.com/page/Enterprise) and [edge](https://grokipedia.com/page/Edge) deployments


## Mitigation
To mitigate IP fragmentation attacks, routers can be configured to enable [Path MTU Discovery](https://grokipedia.com/page/Path_MTU_Discovery) (PMTUD), which allows endpoints to dynamically adjust packet sizes and reduce the need 3 fragmentation along the path.