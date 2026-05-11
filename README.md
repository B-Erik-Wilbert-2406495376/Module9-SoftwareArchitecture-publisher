7. 
a. How much data your publisher program will send to the message broker in one run?
Dalam satu kali menjalankan program publisher, aplikasi mengirim 5 message ke message broker (RabbitMQ). Setiap message berisi data `user_id` dan `user_name` dalam bentuk `UserCreatedEventMessage`, sehingga total terdapat 5 event yang dikirim ke queue `user_created`.

b. The url of “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
Karena publisher dan subscriber menggunakan URL `amqp://guest:guest@localhost:5672` yang sama, berarti keduanya terhubung ke RabbitMQ server yang sama menggunakan username, password, host, dan port yang sama. Dengan begitu, publisher dapat mengirim message ke broker dan subscriber dapat menerima message tersebut dari broker yang sama.


![cargorun](asset/run.png)
Saat saya menjalankan `cargo run` pada program publisher, publisher mengirim 5 event/message ke RabbitMQ melalui queue `user_created`. Setiap event berisi data `user_id` dan `user_name`.
Pada saat yang sama, program subscriber mendengarkan queue yang sama dan menerima message yang dikirim oleh publisher melalui message broker. Subscriber kemudian memproses dan menampilkan setiap message yang diterima ke console.
Hal ini menunjukkan komunikasi asynchronous menggunakan AMQP dan RabbitMQ, di mana publisher dan subscriber tidak berkomunikasi secara langsung, tetapi melalui message broker.


![rabbitmq](asset/rabbit.png)
Saat publisher dijalankan berulang kali menggunakan `cargo run`, publisher terus mengirim event/message ke RabbitMQ. Setiap kali message dikirim, RabbitMQ menerima dan mendistribusikan message tersebut ke subscriber. 
Spike yang terlihat pada chart RabbitMQ menunjukkan adanya peningkatan aktivitas message pada queue dan message broker. Semakin sering publisher dijalankan, semakin banyak message yang dikirim dalam waktu singkat, sehingga grafik monitoring menunjukkan lonjakan (spike) pada message rate dan traffic RabbitMQ.
Hal ini membuktikan bahwa RabbitMQ secara aktif memproses event yang dikirim oleh publisher dan diterima oleh subscriber secara asynchronous.