**Tags**: #[[Network]]
Status: #child

---

The main goal of a network is to let communicate two computer. The communication must adhere to a communication protocol; if it does not, two devices may not be able to interpret the received messages correctly, leading to errors in communication.
# Protocol

A **communication protocol** is a system of rules that allows two or more entities of a communications system to transmit information. The protocol defines:
- **Rules** of communication: 
>   Determine how the devices should interact, how they should handle responses, how they should deal with errors, how they should be synchronized during transmission, and so on.
- **Syntax** of communication:  
>   Concerns the **structure** and **format** of transmitted *messages*, that is, how the data should be organized and represented. (what fields should be present, and how the data should be encoded.)
- **Semantics** of communication: 
>   Concerns the meaning and interpretation of data transmitted over the network. (what the exchanged messages mean, that is, what a message is intended to communicate to the receiver.)

```
The protocol ensures that both peers speak the same language
```

---

# Layering

The communication task may see easy but there are a lot of problem, in fact is not only limited to determining the path for two entities to communicate, but must manage many other aspects of communication to ensure that it takes place in a **reliable**, **efficient**, and **structured** manner. 

 Dividing the communication task into multiple layers is the best way to handle the complexity of communication between different systems, this is possible by **Layering**: is a design principle that divides the protocol design task into smaller steps, each of which accomplishes a specific part, interacting with the other parts of the protocol only in a small number of well-defined ways.
 
**Protocol layering** refers to the the organization of network protocols into distinct layer, where each layer is responsible for a specific part of communication. 

![[Architettura.svg| center | 300]]
```
A single, complex protocols is decomposed into simpler, cooperating protocols. Each protocol layers solve a distinct class of communication problems.
```

## Main Model

The two main models used to understand and structure network communications are the `ISO/OSI` model and the` TCP/IP` model. Both define how data should be transmitted across a network, but they do so in slightly different ways. 

## References
- [[Understanding Network Layer Models]]
