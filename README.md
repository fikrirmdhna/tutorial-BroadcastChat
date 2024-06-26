# Tutorial-10: Broadcast Chat 
## Fikri Dhiya Ramadhana
## 2206819533
## AdvProg-C

### Reflection
1. Try to run one server, and three clients.  
![](images/image.png)  
Dapat dilihat dari gambar di atas, saat menjalankan satu server dengan tiga client, masing masing dari client akan membuat koneksi baru dengan port yang berbeda namun masih terhubung dalam satu server dan hal ini membuat setiap ada pesan yang masuk dari salah satu client akan terhubung ke dalam server dan tampilan client bahwa ada pesan dari client lain.

2. Modifying Port  
![](images/image-2.png)  
Untuk mengubah port yang ada diperlukannya untuk mengubah dua file yang berasal dari server.rs dan client.rs
* server.rs  
```rust 
let listener = TcpListener::bind("127.0.0.1:8080").await?;
```
* client.rs  
```rust 
ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:8080"))
            .connect()
            .await?;
```
Kedua kode di atas sudah menggunakan protokol WebSocket yang sama yaitu `tokio_websockets` (digunakan pada client side) yang dimana akan membuat server side dan client side berjalan dengan normal walaupun menggunakan port yang berbeda. 

3. Add some information to client  
![](images/image-3.png)  
jika ingin menambahkan informasi mengenai pesan yang berada di terminal dapat ditambahkan melalui kode println yang berada di server.rs dan client.rs, seperti:  
* server.rs  
```rust
if let Some(text) = msg.as_text() {
    println!("From client {addr:?} {text:?}");
    bcast_tx.send(format!("{addr} : {text}"))?;
}
```
```rust
    println!("New connection from Fikri's Computer {addr:?}");
```

* client.rs
```rust
if let Some(text) = msg.as_text() {
    println!("Fikri's Computer - From server: {}", text);
}
```  
Perubahan ini dilakukan agar tampilan pesan dapat menampilkan informasi tambahan yang sesuai dengan keinginan. 