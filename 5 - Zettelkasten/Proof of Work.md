**Tags**: #Security #protocols 

---


One party (the _prover_) proves to others (the *verifiers*) that a certain amount of a specific computational effort has been expended. This mechanism must have the following characteristics:
- the computation must be moderately hard (yet feasible) on the *prover*
- but the verification part must be easy for the *verifier*

This is one way to mitigate denial of service attacks in network protocol.

> These mechanisms are used in network protocols when the request for the client is relatively simple, while creating the response requires considerable computational effort on the part of the server.


There are two classes of proof-of-work protocols.
## **Challenge-Response**

This protocols assume a direct interactive link between the requester (client) and the provider (server). The provider chooses a challenge, say an item in a set with a property, the requester finds the relevant response in the set, which is sent back and checked by the provider. As the challenge is chosen on the spot by the provider, its difficulty can be adapted to its current load.

![[Proof of Work.svg | center ]]

## **Solution–verification**

The protocols do not assume a direct interactive link.
As a result, the problem must be self-imposed before a solution is sought by the requester, and the provider must check both the problem choice and the found solution.
