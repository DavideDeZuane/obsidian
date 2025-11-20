These are computer security exploits that crash, hang, or otherwise interfere with the targeted program or system. They are a form of [denial-of-service attack](https://en.wikipedia.org/wiki/Denial-of-service_attack "Denial-of-service attack")


## Connection Depletion Attacks

This is a Denial of Service where an attacker try to saturate all available connections of a server or network device, thereby preventing other legitimate clients from establishing new connections. 

These attacks exploit the fact that the server must allocate resources for each new connection, consuming **available memory, CPU, or sockets** until they are completely exhausted. Examples are the followings:

- **Session Exhaustion Attack:** The attacker establishes a large number of valid sessions with the server without releasing them, consuming available resources.
- **Zombie Connections:** The attacker creates a valid and complete connection with the server but then keeps it idle, taking up resources and preventing new legitimate connections. Otherwise the attacker can  initiates the connection but never completes it, leaving the server waiting until timeout.
