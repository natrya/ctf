### Tools
mmls dan autopsy

decompress dulu kalau di compress
tipe = file.gz

```bash
gunzip <file.gz>
gzip -d <file.gz>
```

tipe = file.bz2

```bash
bzip2 -d
```

mmls <file.img>

![[mmls.png]]
start = alamat awal partisi disk image
end = alamat akhir partisi disk image
length = size dari disk image

fsstat -o (start-offset) (file.img)

mencari flag langsung di disk image
```bash
strings -t d <file.img> | grep -iE "flag"
strings -t d <file.img> | grep -iE "LKS"
strings -t d <file.img> | grep -iE "flag.txt"
```

kalau ketemu 

![[flagtxt.png]]

dicek bagian  `204193835` dikurangi  `184549376` ( `360448 (nilai start dari partisi ) * 512`) 
`$ expr 204193835 - 184549376`
and hasilnya dibagi `1024` bytes using,
`$ expr 19644459 / 1024`
hasilnya `19184` 
`$ ifind -f ext4 -o 360448 -d 19184 disk.flag.img`
hasilnya `2363`
`$ icat -f ext4 -o 360448 disk.flag.img 2363`

![[expr.png]]
strings -t d disk.flag.img | grep -iE "flag.uni.txt"
![[flaguni.png]]
kemudian dibuka di autopsy

![[flag.png]]

### ambil ssh-private key dari image

```bash
strings -t d disk.img | grep -iE "OPENSSH PRIVATE KEY"
```

![[mmls-3.png]]
seperti cara sebelumnya

114562048 - 105906176 (start partisi 206848 * 512)

![[openssh.png]]

validasi dengan autopsy

![[autopsy.png]]

filenya di chmod 400 terlebih dahulu sebelum digunakan

![[perm.png]]
setelah bisa terkoneksi dengan ssh key bisa digunakan 

![[flag-2.png]]

### mengambil isi file yang di encryp

![[mmls-4.png]]
ditemukan perintah 

openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567

validasi dengan autopsy

![[ssh.png]]

dilihat isi filenya

![[string.png]]

validasi dengan autopsy

![[salt.png]]

file diambil dengan perintah

icat -f ext4 -o 411648 disk.flag.img 1782 > flag.txt.enc
kemudian di decrypt file dengan perintah

openssl aes256 -salt -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567

![[flag-3.png]]
