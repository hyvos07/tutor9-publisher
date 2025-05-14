# 🦀 Advanced Programming - Event-Driven Programming

**Nama**  : Daniel Liman <br>
**NPM**   : 2306220753 <br>
**Kelas** : Pemrograman Lanjut A


## Reflection 1

>  How much data your publisher program will send to the message broker in one run?

Dari bagian kode di function `main()` pada file `main.rs`, dapat dilihat bahwa terdapat **5 message** yang akan dikirim ke message broker pada saat aplikasi dijalankan (dalam 1 kali jalan).

```rust
_ = p.publish_event(
    "user_created".to_owned(),
    UserCreatedEventMessage {
        user_id: "1".to_owned(),
        user_name: "2306220753-Amir".to_owned(),
    },
);
_ = p.publish_event(
    "user_created".to_owned(),
    UserCreatedEventMessage {
        user_id: "2".to_owned(),
        user_name: "2306220753-Budi".to_owned(),
    },
);
_ = p.publish_event(
    "user_created".to_owned(),
    UserCreatedEventMessage {
        user_id: "3".to_owned(),
        user_name: "2306220753-Cica".to_owned(),
    },
);
_ = p.publish_event(
    "user_created".to_owned(),
    UserCreatedEventMessage {
        user_id: "4".to_owned(),
        user_name: "2306220753-Dira".to_owned(),
    },
);
_ = p.publish_event(
    "user_created".to_owned(),
    UserCreatedEventMessage {
        user_id: "5".to_owned(),
        user_name: "2306220753-Emir".to_owned(),
    },
);
```

<br>

> The url of: `amqp://guest:guest@localhost:5672` is the same as in the subscriber program, what does it mean?

URL yang sama pada kode yang ada di sisi subscriber menunjukkan kalau kedua aplikasi (publisher dan subscriber) terhubung pada instance message broker yang sama, yaitu yang terletak pada `localhost:5672` dan dengan menggunakan kredensial yang sama, yaitu kredensial default dari RabbitMQ `guest:guest`. Bagian ini memastikan message broker yang terhubung dari kedua sisi aplikasi sama dan data yang dikirim dari publisher dapat diterima oleh subscriber lewat broker yang sama.

## Running RabbitMQ as Message Broker on `localhost`

<picture>
    <img src="img/rabbitmq.png">
</picture>

## Sending and Processing Event

<picture>
    <img src="img/events.png">
</picture>

Pada gambar di atas, publisher mengirim 5 event ke broker RabbitMQ agar dapat ditahan oleh broker tersebut terlebih dahulu. Hal ini terjadi dimulai dari setelah terkoneksi dengan broker, lalu publisher mengirim 5 event tersebut lalu broker pun akan mengirim event-event tersebut pada penerima yang dituju (yaitu pada kasus ini adalah si subscriber). Setelah menerima event yang diterima dari broker, barulah subscriber akan memproses dan menampilkan hasil dari apa yang ia terima.

## Monitoring Chart Based on Publisher

<picture>
    <img src="img/chart.png">
</picture>

Pada gambar di atas, terjadi lonjakan pada setiap kali RabbitMQ menerima message baru. Spike yang dihasilkan pada chart **Message rates** di atas berkaitan dengan seberapa sering publisher mengirim message baru ke broker RabbitMQ. Semakin cepat interval per message yang dikirim dan/atau semakin banyak message yang dikirim dalam setiap kali pencatatan pada chart, maka semakin tajam dan membanyak pula spike message rates nya.