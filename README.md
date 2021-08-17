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
- | Operasi                         | Keterangan                                 |
  |---------------------------------|--------------------------------------------|
  | mget key [key ...]              | Get the values of all the given keys |
  | mset key value [key value ...]  | Set multiple keys to multiple values |