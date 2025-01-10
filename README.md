# Segmentation_Vs_fragmentation


**Segmentation:**
The application can send a very big data. Eg of 4000 bytes.
But TCP cannot send this much big data. So segmentation is done. Segmentation applies to only TCP and not for UDP. UDP can send the big data also. It doesnot do any congestion
control. It means It can cause the congestion by sending the big data.

When the data comes to the TCP. It ll do the segmentation based on the MSS (Maximum segment size). This is communicated in the SYN packet (in TCP header options field) at the time of establishing the connection. And it cannot change throughout the connection.

eg: Apllication is sending 1,00,000 B (1 lakh byte) data to transport layer.
Transport layer will add 20B TCP header. = 1,00,020 B
Now Network layer (IP layer). Its header has a "total length" field. It is 16 bits. Therefore it can hold 65535 bytes (including IP header).
1st segment (65535 -20) = 65515 B (has transport header)+ network header
2nd Segment 100020-65515 = 34505 B (no transport header)+ network header

Only the first segment has the transport header. From second segment onwards there is no transport header.

**Fragmentation**
Fragmentation happens based on MTU (Maximum transmission Unit).

1) Fragmentation is not possible if DF bit is set in the IP header.
2) IPV6 will not permit fragmentation.

Routers will drop the packet and send ICMP messages if the DF bit is set and packet is larger than the MTU.

Eg: 4000B is application Data amd MTU is 1500B

4000/1500 = 2.6 => 3 fragments.

**Fragments:**
Frag1: IP header: length = 1500 (i.e. 1480 data +20 IP header) frag flag=1 offset = 0 (1st fragment always has fragment offset 0)
Frag2:                     1500                                          1          185 (1480/8) This field is always in the multiple of 8. (It ll give the start of the data in the original packet. i.e. to identify where to keep this data in the original packet. i.e. used in reassembly). 
Fragment offset is a 13 bit filed (8192 B). An IP header total length filed is 16 bits (65535 B). Also 65535/8 = 8191.8 ~8192 = 2^13 = (13 bit fragment offset). i.e. 2nd fragment is 65535 B then, fragment offset field will have 8192 (All bits set)

Frag 3: 4000-1480-1480 = 1040 length = 1040B, frag flag =1, offset = 370 (185+185)


**Note:**
If we do segmentation and fragmentation both, then two times dividing the packet will take lot of time. Hence at the segmenation time only, we usually divide the packet into 1460B i.e. 1460 +20 (TCPH) + 20(IPH) = 1500 B
