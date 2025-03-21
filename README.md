# advprog-module6
## REFLECTION
- Commit 1 
    - Pada commit pertama, program hanya membuat server TCP yang mendengarkan request HTTP. Pertama, program membuat server TCP pada "127.0.0.1:7878". Kemudian, server menerima koneksi baru yang dihandle dalam for loop yang melakukan call kepada function handle_connection. Function handle_connection akan mencetak raw HTTP Request yang dikirimkan oleh user pada web server. Functiona ini memiliki parameter mutable TcpStream. Dengan adanya mutable, isi dari variabel ini dapat dimodifikasi sesuai keperluan.Kemudian, TcpStream memberikan referensinya kepada BufReader. Pada method .lines() pada http_request dan buf_reader akan mengembalikan baris-baris masukan dari stream, lalu menggunakan map() untuk membongkar result dari lines(). Kemudian, function take_while mengumpulkan baris sampai menemukan baris kosong yang menandakan akhir dari HTTP Request. Collect() akan mengumpulkan baris-baris menjadi suatu Vector berisi String yang akan dicetak pada layer. 

- Commit 2
    - handle_connection pada commit kedua akan mengirimkan HTTP Response dengan status 200 OK. Kemduian akan variabel contents dengan function read_to_string akan membaca konten "hello.html" dan menyimpan dalam contents. Panjang dari contents dihitung dengan contents.len(). Hal ini berguna dalam Content-Length di HTTP Response agar browser mengetahui Panjang body dari respons. Respons tersebut dapat ditampilkan di browser kepada pengirim.
    - ![Screenshot 2025-03-20 161336](https://github.com/user-attachments/assets/01ccea0c-1fa9-4691-b0a4-77a1526c92c6)

- Commit 3
    - Pada kali ini, terdapat implementasi dari pemisahan page sesuai dengan request yang diterima. Apabila respons ditemukan akan menuju page "hello.html" dan menuju "404.html" apabila selain itu. Hal ini bisa terjadi dengan adanya `let request_line = buf_reader.lines().next().unwrap().unwrap();` yang mengambil request line. Kemudian, apabila nilai dari request line adalah `GET / HTTP/1.1` akan kembalikan status 200 OK dan menuju "hello.html". Apabila request line tidak sama dengan `GET / HTTP/1.1`  akan mengembalikan 404 NOT FOUND dan menuju "404.html". Code hasil refactor dapat dilihat dalam commit 3.
    - ![image](https://github.com/user-attachments/assets/e95db023-85f9-45ed-907f-0ed2e30737d0)
