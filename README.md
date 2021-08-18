# learn-redis

**Apa Itu Key-Value Database?**
- Redis adalah sistem basis data berbasis key-value
- aradigma key-value adalah paradigma dimana data disimpan dalam bentuk pair (key-value)
- Key mirip dengan primary key dari data, sedangkan value adalah isi dari datanya

**Apa Itu In-Memory Database?**
- Redis menyimpan datanya di memory, namun kita bisa memintanya untuk menyimpan datanya secara regular permanen di disk.
- Data di disk hanya dijadikan backup ketika redis berjalan ulang, selama redis berjalan, redis hanya akan melakukan manipulasi data ke memory

**Database**
- Redis memiliki konsep database seperti pada relational database mysql atau postgre
- Namun sedikit berbeda, jika di relational database kita bisa membuat database dengan menggunakan nama database, di redis kita hanya bisa menggunakan angka sebagai database
- Secara default database di redis adalah 0 (nol)

**String**
- Redis sebenarnya mendukung struktur data yang banyak, seperti String, List, Set, dan lain-lain

**Operasi Data String**
- | Operasi             | Keterangan                                 |
  |---------------------|--------------------------------------------|
  | set key value       | Set the string value of a key              |
  | get key             | Get the value of a key                     |
  | exists key          | Determine if a key exists                  |
  | del key [key ...]   | Delete a key                               |
  | append key value    | Append a value to a key                    |
  | keys pattern        | Find all keys matching the given pattern   |

**Operasi Range Data String**
- | Operasi                   | Keterangan                                                         |
  |---------------------------|--------------------------------------------------------------------|
  | setrange key offset value | Overwrite part of a string at key starting at the specified offset |
  | getrange key start end    | Get a substring of the string stored at a key                      |

**Operasi Range Data String**
- | Operasi                         | Keterangan                           |
  |---------------------------------|--------------------------------------|
  | mget key [key ...]              | Get the values of all the given keys |
  | mset key value [key value ...]  | Set multiple keys to multiple values |

**Expiration**
- Secara default saat kita menyimpan data ke redis, redis akan menyimpannya secara permanent sampai kita menghapusnya
- Kadang kita mendapatkan kasus ingin menghapus data di redis secara otomatis dalam waktu tertentu
- Misal kita menyimpan data cache di redis selama 10 menit, setelah 10 menit kita akan query ulang ke database untuk mendapatkan data terbaru
- Hal ini bisa dilakukan di redis, redis memiliki fitur expiration secara otomatis pada data yang kita simpan di redis

**Operasi Expiration Data String**
- | Operasi                   | Keterangan                           |
  |---------------------------|--------------------------------------|
  | expire key seconds        | Set a key's time to live in seconds  |
  | setex key seconds value   | Set the value and expiration of a key|
  | ttl key                   | Get the time to live for a key       |

**Increment & Decrement**
- Operasi Increment & Decrement sekilas sangat mudah dilakukan, hanya tinggal mengupdate data yang di redis dengan data baru (data lama ditambah 1 atau dikurangi 1)
- Namun jika operasi dilakukan secara paralel dan dalam waktu yang sangat cepat, hal ini bisa memungkinkan race condition
- Untungnya redis memiliki operasi untuk melakukan increment dan decrement

**Operasi Increment & Decrement**
- | Operasi                | Keterangan                                              |
  |-----------------------|----------------------------------------------------------|
  | incr key              | Increment the integer value of a key by one              |
  | decr key              | Decrement the integer value of a key by one              |
  | incrby key increment  | Increment the integer value of a key by the given amount |
  | decrby key increment  | Decrement the integer value of a key by the given amount |

**Flush**
- Kadang kita butuh mengosongkan seluruh data di redis, misal ketika terjadi kesalahan kode sehingga menyebabkan data di redis salah
- Menghapus data di redis satu-satu menggunakan operasi delete bukanlah hal yang bijak
- Redis memiliki fitur untuk menghapus seluruh data di database redis, yaitu operasi flush

**Operasi Flush**
- | Operasi   | Keterangan                                |
  |-----------|-------------------------------------------|
  | flushdb   | Remove all keys from the current database |
  | flushall  | Remove all keys from all databases        |

**Pipeline**
- Perintah yang dikirim dari client ke server redis menggunakan Request/Response protocol, artinya tiap request yang dikirim ke server redis, maka redis akan membalasnya secara langsung
- Kadang ada kebutuhan kita mengirim data ke redis dalam jumlah besar, misal ketika ada kasus memindahkan data dari database mysql ke redis
- Jika kita mengirim satu per satu datanya, maka akan butuh waktu lama untuk selesai
- Redis mendukung operasi bulk via pipeline, dimana kita bisa mengirim beberapa perintah sekaligus dalam satu request
- Namun perlu diketahui, server redis tidak akan membalas tiap perintah yang dikirim via pipeline
- redis-cli --pipeline