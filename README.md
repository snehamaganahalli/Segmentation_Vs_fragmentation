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
