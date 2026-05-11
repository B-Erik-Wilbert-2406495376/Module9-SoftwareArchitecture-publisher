7. 
a. How much data your publisher program will send to the message broker in one run?
Dalam satu kali menjalankan program publisher, aplikasi mengirim 5 message ke message broker (RabbitMQ). Setiap message berisi data `user_id` dan `user_name` dalam bentuk `UserCreatedEventMessage`, sehingga total terdapat 5 event yang dikirim ke queue `user_created`.

b. The url of “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
Karena publisher dan subscriber menggunakan URL `amqp://guest:guest@localhost:5672` yang sama, berarti keduanya terhubung ke RabbitMQ server yang sama menggunakan username, password, host, dan port yang sama. Dengan begitu, publisher dapat mengirim message ke broker dan subscriber dapat menerima message tersebut dari broker yang sama.