# WeaveWorks (CNI)

- place their agents in each Node
- These agents are responsible for managing all activities between sites.
- They also keep talking to each other and are well connected.
- They communicate with each other to exchange information regarding the nodes and networks and pods within them.
- Each agent or peer stores (indistinct) of the entire setup that way they know the pods and their IPs on the other nodes.

- Weave creates its own bridge on the nodes and names. It, Weave then assigns IP address to each network.
- when a packet is sent from one pod to another on another node, Weave intercepts the packet and identifies that it's on a separate network. It then encapsulates this packet into a new one with new source and destination and sends it across the network.
- Once on the other side the other Weave agent retrieves the packet, decapsulates it and routes the packet to the right pod.