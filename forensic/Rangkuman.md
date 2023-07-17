pengecekan file dengan tools berikut

file <filename>
untuk mengetahui tipe file

strings <filename>
untuk mengecek isi yang berupa string yang bisa dibaca

cat <filename> | grep -i "LKS"
untuk langsung cek apakah ada keynya

exiftool <filename>

zsteg -a -v <filename>

tipe file dan perlakuan berikutnya

- tipe = "shell archive text"
chmod +x <filename> supaya file bisa dieksekusi di terminal

- tipe = "current ar archive" / "gzip compressed data"
binwalk -e <filename>
cd <filename.extracted> 

- tipe = "lzip compressed data"
lzip -d -k <filename>

- tipe = "LZ4 compressed data"
lz4 -d <filename> <output>

- tipe = "LZMA compressed data"
lzma -d -k <filename>

- tipe = "LZOP compressed data"
lzop -d -k <filename> -o <output>

- tipe = "XZ compressed data"
xz -d -k <filename>

- tipe = "ASCII text"
cat <filename>
paste di cyberchef

- tipe = "PDF file"
dibuka menggunakan microsoft word untuk bisa lihat isi yang disembunyikan
