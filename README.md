# Modul-9-Software-architechture-publisher

## Reflection
> How much data your publisher program will send to the message broker in one run?

Pada file main.rs, kita dapat melihat code berikut

```rs
fn main() {
    let mut p =
        CrosstownBus::new_queue_publisher("amqp://guest:guest@localhost:5672".to_owned()).unwrap();
    _ = p.publish_event(
        "user_created".to_owned(),
        UserCreatedEventMessage {
            user_id: "1".to_owned(),
            user_name: "2406400070-Amir".to_owned(),
        },
    );
    _ = p.publish_event(
        "user_created".to_owned(),
        UserCreatedEventMessage {
            user_id: "2".to_owned(),
            user_name: "2406400070-Budi".to_owned(),
        },
    );
    _ = p.publish_event(
        "user_created".to_owned(),
        UserCreatedEventMessage {
            user_id: "3".to_owned(),
            user_name: "2406400070-Cica".to_owned(),
        },
    );
    _ = p.publish_event(
        "user_created".to_owned(),
        UserCreatedEventMessage {
            user_id: "4".to_owned(),
            user_name: "2406400070-Dira".to_owned(),
        },
    );
    _ = p.publish_event(
        "user_created".to_owned(),
        UserCreatedEventMessage {
            user_id: "5".to_owned(),
            user_name: "2406400070-Emir".to_owned(),
        },
    );
}
```
Dari sini kita dapat melihat bahwa setiap kali kita run, kita akan mengirim 5 messages (`publish_event` dijalankan sebnyak 5 kali)

> The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

Hal tersebut menunjukkan bahwa program subscriber dan publsiher kita menggunakan server RabbitMQ yang sama. Maka publisher akan mengirim pesan ke queue dan subscriber akan mengambil message tersebut dari queue yang sama sehingga publisher dan subscriber dapat berjalan tanpa mengetahui keberadaan satu sama lain, mereka hanya perlu tahu server RabbitMQnya.

## Running RabbitMQ as Message Broker
![alt text](./images/running-rabbit.png)


## Sending and processing event.
![alt text](./images/run.png)

Dari screenshot diatas kita dapat melihat bahwa saya menjalankan program publisher sebanyak 2 kali. Untuk setiap kali saya ran, bisa dilihat diconsole sebelah kanan bahwa subscriber menerima 5 messages. Sehingga subscriber secara totoal menerima 10 messages. Hal ini menunjukkan bahwa komunikasi antar subscriber dan publsiher dan juga rabbitmq bekerja dengan semestinya.

## Monitoring chart based on publisher.
![alt text](./images/spike.png)

Kita dapat melihat bahwa terdapat spike yang muncul setiap kali kita menjalankan program publisher. Dari dashboard rabbitmq, kita melihat bahwa spike tersebut berada di grafik messages rates. Hal ini sesuai dengan cara kerja program karena setiap kali kita run program publisher, publisher akan mengirimkan message ke rabbitmq sehingga messages ratesnya naik. Namun karena program kita hanya berjalan satu kali (tidak continous) sehingga setelah messages dikirim, program berhenti dan messages rates turun, membuat pola spike yang kita lihat.