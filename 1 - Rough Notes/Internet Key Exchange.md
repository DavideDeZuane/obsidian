Fare tutta la parte di introduzione sul protocollo 




## Generating Keys
Nella parte in cui si devono generare le chiavi necessarie a proteggere crittograficamente tutte gli scambi successivi abbiamo che:

```bash
SKEYSEED = PRF(Ni|Nr, SHARED_SECRET)
```

Ovvero il seed viene derivato utilizzando la funzione di messagge authentication che di solito è HMAC utilizzando i nonce come chiave e firmando il segreto condiviso.

A questo punto il seed viene utilizzato come chiave per riuscire a derivare tutto il key material necessario per le chiavi infatti:

```bash
{ SK_d, SK_ai, SK_ar, SK_ei, SK_er, SK_pi, SK_pr } = prf+(K, S)
where:
K = SKEYSEED
S = Ni | Nr | SPIi | SPIr
```

L'output della prf è fissato infatti trattandosi di una funzione di hash, la dimensione del messagge digest è fissa. Dato che il keying material necessario è maggiore di quello di output della funzione quello che si fa è applicare la funzione in maniera iterativa fino a quando non si ha il materiale necessario per tutte le chiavi.

La maniera iterativa è la seguente.
```bash
prf+ (K,S) = T1 | T2 | T3 | T4 | ...
where:
T1 = prf (K, S | 0x01)
T2 = prf (K, T1 | S | 0x02)
T3 = prf (K, T2 | S | 0x03)
T4 = prf (K, T3 | S | 0x04)
...
```

![[PRF+.svg | center | 700]]

Questo procedimento va avanti fino a quando non si genera keymaterial a sufficenza per tutte le chiavi. In particolare la dimensione delle chiavi 

As we can see from the diagram, we have that:
1. At the iteration `0`  the input data to the `PRD` is appended a **counter**. This counter is necessary to increase the entropy and the diffusion property of the input data.
2. After the iteration `0` at each step we have to prepend to the `S` payload the outcome of the last iteration, and increment the counter. This ensure that every generated block depends on the previous output and the new data. This guarantees that the sequence of output is unique. (It's impossible to generate `T2` without knowing `T1` )
3. The iteration continues until we have enough material for all the keys 


## AUTH
The Identification payloads, denoted IDi and IDr,allow peers to assert an identity to one another. This payload are used purely to fetch the policy and authentication data related to the other party.

In minimal implementation, it might be easiest to always use KEY_ID type.  This allows the ID payload to be static.  Using an IP address has problems in environments where IP addresses are dynamically allocated


## Minimal

The minimal implementation of IKEv2 only uses the first two exchanges, called `IKE_SA_INIT` and `IKE_AUTH`

These are used to create the IKE SA and the first Child SA.  In addition to those messages, a minimal IKEv2 implementation needs to understand the CREATE_CHILD_SA request enough to generate a CREATE_CHILD_SA response containing the NO_ADDITIONAL_SAS error notify.  It needs to understand the INFORMATIONAL request enough to generate an empty INFORMATIONAL response to it..
  Minimal implementations only need to support the role of initiator,
   so it typically only sends an IKE_SA_INIT request that, when
   answered, is followed by an IKE_AUTH.  As those messages have fixed
   Message IDs (0 and 1), it does not need to keep track of its own
   Message IDs for outgoing requests after that.


