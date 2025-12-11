**Tags**: #networks
**Status**: #child 

---




## Security

IPsec - Policy-Based Interception
WireGuard - Route-Based Interception



```
IPsec Flow
[App] → [IP Stack]
           ↓
      [XFRM Policy Check] ← "Does this packet match a policy?"
           ↓ YES
      [Apply Transform: Encrypt with SA]
           ↓
      [Add outer IP header]
           ↓
      [Route outer packet normally]
           ↓
      [eth0] → Network

Wireguard Flow

[App] → [IP Stack]
           ↓
      [Routing Table] ← "Where does this packet go?"
           ↓
      [wg0 interface] ← Normal route decision
           ↓
      [WireGuard: Encrypt]
           ↓
      [Send as UDP via eth0]
           ↓
      [eth0] → Network
```