biasanya filenya tipe pcap pcapng
buka file dengan wireshark

### Follow TCP Stream

![[follow-stream.png]]

### file yang dikirim melalui paket (des3)

Follow TCP STREAM

![[tcp.png]]
cari paket yang isi awalnya salted di paket no 57

![[salted.png]]
File > Export Packet Bytes
![[export.png]]

kemudian di buka di console 

```bash
openssl des3 -d -salt -in saltedfile.bin -out file.txt -k supersecretpassword123
```

