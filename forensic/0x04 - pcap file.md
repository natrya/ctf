![[pcapsearch.png]]
flag bisa dicari dengan mencari hex Value / string dari flag menggunakan search menu di wireshark

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


Perintah mencari flag di UDP Stream

- Ganti \<filenya\> menjadi nama filenya
- Ganti \<penanda_flag\> menjadi penanda flagnya

nb : terkadang flagnya picoCTF{p4ck37_ 5h4rk _ 01b0a0d6} 
atau ada tambahan seperti p i c o C T F { p 4 c k 3 7 _ 5 h 4 r k _ 0 1 b 0 a 0 d 6 } 

```bash
PCAP=<filenya>; END=$(tshark -r $PCAP -T fields -e udp.stream | sort -n | tail -1); for ((i=0;i<=END;i++)); do tshark -r $PCAP -Y "udp.stream eq $i" -T fields -e data.text -o data.show_as_text:TRUE 2>/dev/null | tr -d '\n' | grep -i "penanda_flag"; if [ $? -eq 0 ]; then echo "(Stream #$i)"; fi; done
```

Perintah mencari flag di TCP Stream

```bash
PCAP=<filenya>; END=$(tshark -r $PCAP -T fields -e tcp.stream | sort -n | tail -1); for ((i=0;i<=END;i++)); do tshark -r $PCAP -Y "tcp.stream eq $i" -T fields -e data.text -o data.show_as_text:TRUE 2>/dev/null | tr -d '\n' | grep -i "<penanda_flag>"; if [ $? -eq 0 ]; then echo "(Stream #$i)"; fi; done
```


