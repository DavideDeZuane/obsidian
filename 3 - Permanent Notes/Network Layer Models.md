**Tags**: #networks 
**Status**: #done

---
## TCP/IP Model

The `TCP/IP` model stems from a more *practical approach*. In fact, even before it was formalized as a model, its component protocols had already been implemented and used in the ARPANET network. 

The main goal of this architecture was to ensure reliable communication between devices in distributed networks, even under difficult conditions, such as outages or malfunctions of some nodes. Only later, with the spread of the Internet, was the need felt to describe and organize these protocols into a more structured model, which we know today as the TCP/IP model.

 ```
It was not designed a priori as a theoretical reference, but emerged from concrete experience and the evolution of real networks.
```

## ISO/OSI Model 

While the TCP/IP protocol, developed by ARPANET, was achieving success, it was not yet a global standard. Many companies and countries, especially in Europe, were looking for a more general and formal solution, independent of the United States and the Department of Defense. 

In this context, there was a need for a guide for the development of new networks that was flexible and adaptable to emerging technologies and could support the construction of globally interoperable networks. So it was that in 1977, the **ISO** (*International Organization for Standardization*) began work on a standard model for networks. In 1984, the **OSI** (*Open Systems Interconnection*) model was officially published.

```
🎯 To create a layered model that described how data should travel through a network, regardless of the technology used.
```

### **Characteristics**

Thanks to the layering design the software stack for the computer networks is strongly structured and divided in layer. Each layer has a specific task to complete, each of them has three main concept:

- **Service to upper Layer**: is a functional description (i.e., how to use) of the services that a layer provides to the one above it. This service are essential because without them the upper layer cannot fulfill his task.
- **Protocol**: two entities at the same level in different systems cooperate and interact by means of protocols. The protocol defines the rules, syntax and semantics of communication. 
- **Addressing**: users who use the services must be identified, so that multiplexing can be carried out.

In this model we have two type of communication:

**Virtual communication**:  Each layer of the ISO/OSI model believes it communicates directly with the corresponding layer of the remote device. This is done logically, without a direct physical connection between the layers. And the way the two communicate is specified by that layer's protocol.
> Specified in red in the figure.

**Actual Communication**: Actual communication represents the actual way in which data moves across layers and the network. Data travels from *top* to *bottom* in the sender's OSI model, traversing all layers until it is physically transmitted. On the receiver, data travels *up* through the layers until it reaches the destination layer.
> Specified in blue in the figure.

![[Path.svg | center | 350]]
```
The ISO/OSI model is the reference model
```

## Layers

The two models break-down communication into a number of different layers. In fact, we can do the following comparison:

| Livello OSI    | Livello TCP/IP (5 livelli) | Funzione                                       |
| -------------- | -------------------------- | ---------------------------------------------- |
| `Application`  | `Application`              | Interface with the user                        |
| `Presentation` | -                          | Data conversion, encryption, compression       |
| `Sesssion`     | -                          | Session handling                               |
| `Transport`    | `Transport`                | Flow control, reliability, segmentation        |
| `Network`      | `Network (Internet)`       | Package routing and identification             |
| `Data Link`    | `Data Link`                | Communication with devices on the same network |
| `Physical`     | `Physical`                 | Bit over the communication channel             |

- [[Application Layer]]
- [[Transport Layer]]
- [[Network Layer]]
- [[Data-Link Layer]]
- [[Physical Layer]]