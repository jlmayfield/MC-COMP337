# FSMs for RDTs Quick Reference 

## Basic RDT Events

Events are viewed as boolean valued functions.

*   `rdt_send(msg)` - Request from system to send message `msg` 
*   `rdt_rev(pk)` - Packet `pk` has been delivered from the network.  
*   `timeout`  - Timer has runout
*   `corrupt(p)` and `notcorrupt(p)` - Packet `p` passes or fails a checksum check, i.e. data corruption is or is not detected.
*   `isACK(pk,n)` - Packet `pk` is an ACK with sequence number `n`
*   `hasseqnum(pk,n)` - Packet `pk` has sequence number `n`
*   **&#x039B;** - Always True event or free event. Typically reserved for the starting transition and a paired with initialization actions.


## Basic RDT Actions

The building block of event handlers, the things our protocols actually do.

*   `udt_send(pk)` - Transmit the packet pk on the network (multiplex and header preparation included.)
*   `pk=make_pkt(n,msg,chk)` - Construct a segment `pk` with sequence number `n`, payload `msg`, and checksum `chk`.
*   `start_timer` - Start the timer
*   `stop_timer`  - Stop the timer
*   `extract(pk,msg)` - Extract payload `msg` from the segment `pk`. Notice this works my modifying `msg`. 
*   `deliver_data(msg)` - Deliver message `msg` to the application. 
*   **&#x039B;** - Free action, aka Do nothing, aka no operations. 

## Note on Extended FSMs   

We can go beyond the basics in two ways:
1.  Add our own protocol events and actions (see Problem 3.17)
2. Extend FSMs with variables and conditionals. Our key example of this is Figures 3.20 and 3.21, the specifications of the GBN sender and receiver.  
