
## Router vs Switch

```Router is network layer device while switches are link layer devices```

Some packet switches, called link-layer switches (examined
in Chapter 5), base their forwarding decision on values in the fields of the linklayer frame; switches are thus referred to as link-layer (layer 2) devices. Other packet switches, called routers, base their forwarding decision on the value in the networklayer field. Routers are thus network-layer (layer 3) devices. but must also implement layer 2 protocols as well, since layer 3 devices require the services of layer 2 to implement their (layer 3) functionality.

## Network layer

![network layer](images/network_layers.png)

The role of the network layer is thus deceptively simple—to move packets from a sending host to a receiving host. To do so, two important network-layer functions can be identified:

- ***Forwarding***. Forwarding refers to the router-local action of transferring a packet from an input link
interface to the appropriate output link interface.

When a packet arrives at a router’s input link, the router must move the packet to the appropriate output link. For example, a packet arriving from Host H1 to Router R1 must be forwarded to the next router on a path to H2.

- ***Routing***. Routing refers to the network-wide process that determines the end-to-end paths that packets take from source to destination.

The network layer must determine the route or path taken by packets as they flow from a sender to a receiver. The algorithms that calculate these paths are referred to as routing algorithms. A routing algorithm would determine, for example, the path along which packets flow from H1 to H2.

### Datagram networks
```Internet is a datagram networks.```

In a datagram network, each time an end system wants to send a packet, it stamps the packet with the address of the destination end system and then pops the packet into the network.

As a packet is transmitted from source to destination, it passes through a series of routers. Each of these routers uses the packet’s destination address to forward the packet. Specifically, each router has a forwarding table that maps destination addresses to link interfaces; when a packet arrives at the router, the router uses the packet’s destination address to look up the appropriate output link interface in the forwarding table. The router then intentionally forwards the packet to that output link interface.

![datagram networks](images/datagram_networks.png)

### Forwarding table

```Every router has a forwarding table.```

A router forwards a packet by examining the value of a field in the arriving packet’s header, and then using this header value to index into the router’s forwarding table. The value stored in the forwarding table entry for that header indicates the router’s outgoing link interface to which that packet is to be forwarded. Depending on the network-layer protocol, the header value could be the destination address of the packet or an indication of the connection to which the packet belongs.

![routing](images/routing.png)

With this style of forwarding table, the router matches a prefix of the packet’s destination address with the entries in the table; if there’s a match, the router forwards the packet to a link associated with the match. The router uses the **longest prefix matching rule**; that
is, it finds the longest matching entry in the table and forwards the packet to the link interface associated with the longest prefix match.

Although routers in datagram networks maintain no connection state information,
they nevertheless maintain forwarding state information in their forwarding
tables. However, the time scale at which this forwarding state information changes
is relatively slow. Indeed, in a datagram network the forwarding tables are modified
by the routing algorithms, which typically update a forwarding table every one-to five minutes or so.

## Inside a Router
```Router's main duty - forwarding function: the actual transfer of packets from a router’s incoming links to the appropriate outgoing links at that router.```

### Router Architecture:
- **Input ports** 
    - It performs the ***physical layer function*** of terminating an incoming physical link at a router.
    - An input port also performs ***link-layer functions*** needed to interoperate with the link layer at the other side of the incoming link
    - Perhaps most crucially, ***the lookup function*** is also performed at the input port; It is here that the forwarding table is consulted to determine the router output port to which an arriving packet will be forwarded via the switching fabric. ***Control packets*** (for example, packets carrying routing protocol information) are forwarded from an input port to the routing processor.
- **Switching fabric**
    - The switching fabric connects the router’s input ports to its output ports.
- **Output ports**
    - An output port stores packets received from the switching fabric and transmits these packets on the outgoing link by performing the necessary ***link-layer and physical-layer functions***.
- **Routing processor**
    - The routing processor executes the routing protocols.
    - maintains routing tables.
    - attached link state information.
    - computes the forwarding table for the router.
    - It also performs the network management functions.

![router Architecture](images/router_arch.png)

A router’s input ports, output ports, and switching fabric
together implement the forwarding function and are almost always implemented in ***hardware***. These forwarding functions are sometimes collectively referred to as the router ***forwarding data plane***.

These router control plane functions are usually implemented in ***software*** and execute on the routing processor (typically a traditional CPU).

### Input Processing
The input port’s line termination function and link-layer processing implement the
physical and link layers for that individual input link. The lookup performed in the
input port is central to the router’s operation—it is here that the router uses the forwarding
table to look up the output port to which an arriving packet will be forwarded via the switching fabric. The forwarding table is computed and updated
by the routing processor, with a ***shadow copy typically stored at each input port***. The
forwarding table is copied from the routing processor to the line cards over a separate
bus (e.g., a PCI bus) indicated by the dashed line from the routing processor to
the input line cards. Therefore, forwarding decisions can be
made ***locally***, at each input port, without invoking the centralized routing processor
on a per-packet basis and thus avoiding a centralized processing bottleneck.

![input processing](images/input_processing.png)

Four major events happen here:

- Routing table lookup.
- physical - and link-layer processing
must occur, as discussed above; 
- the packet’s version number, checksum
and time-to-live field — all must be checked
and the latter two fields rewritten
- counters used for network management
(such as the number of IP datagrams received) must be updated.

### Switching
```To ensure packets are switched (that is, forwarded) from an input port to an output port.```

There are three switching method:

- **Switching via memory**. An input port with an arriving packet
first signaled the routing processor via an interrupt. The packet was then copied from the input port into processor memory. The routing processor then extracted
the destination address from the header, looked up the appropriate output port in
the forwarding table, and copied the packet to the output port’s buffers. (memory mapped ports)
- **Switching via a bus.** In this approach, an input port transfers a packet directly to the
output port over a shared bus, without intervention by the routing processor.
- **Switching via an interconnection network.** One way to overcome the bandwidth
limitation of a single, shared bus is to use a more sophisticated interconnection network,
such as those that have been used in the past to interconnect processors in a
multiprocessor computer architecture.

![Switching method](images/switching_method.png)

### Output processing

Output port processing, takes packets that have been stored in
the output port’s memory and transmits them over the output link. This includes:

- selecting and de-queueing packets for transmission
-  performing the needed linklayer and physical-layer transmission functions.

![output processing](images/output_process.png)



## Reference 
