# Go-Back-N
Disclaimer : I do not own any of the progra. This README has been written after reading and appreciating tomerismis' (https://github.com/tomersimis) work on Go-Back-N (https://github.com/tomersimis/Go-Back-N).

Simple implementation of the Go-Back-N protocol using UDP (Java).
This is an implementation of UDP send receive of data following the Go Back N protocol.
The description of the classes used are given below.


RDTAck class is the class that represents Acknowledgements. It has a member variable called packet which is basically the serial number of the packet that the receiver expects next.


RDTPacket class represents the packet that is sent from the sender  to the receiver. It contains the following member variables.

a. seq which is the sequence number of the packet being sent(int)

b. data is a byte in size and contains one byte of information

c. a boolean variable last to signify whether the corresponding packet is the last to be sent.


The Sender class is used to emulate a UDP sending agent follwing the Go Back N protocol. 

A probability is set that defines the success rate of the transmission, the window size and the timer(time before re sending all non acknowledged packets) is also set.
There is a sending loop that keeps sending the packets as long as the number of acknowledgements yet to be received is less than the window size.

There is also a timeout handling module that, when invoked, sends all the sent but non Acknowledged packets.


The Receiver class is used to emulate a UDP receiving agent following the Go Back N protocol.

It has its own marker variable (waitingfor) that reprresents the sequence number of the packet that it is waiting for. If the value of the marker matches the sequence number of the packet, it adds the packet to its buffer and increments its marker. Else, it simply ignores that packet. In both cases, the receiver sends the value of its marker to the Sender denoting the sequence number of the packet that it is expecting.

In this class also, there is a probability variable that defines the prbability of the ACK reaching the Sender successfully. In both the classes, the PROBABILITY variable is used to manually insert errors in transmission.


The Serializer class is used to convert bytes to objects and vice versa.

