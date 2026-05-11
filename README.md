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