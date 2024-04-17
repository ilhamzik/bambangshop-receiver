# BambangShop Receiver App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a Rocket web framework skeleton that you can work with.

As this is an Observer Design Pattern tutorial repository, you need to implement a feature: `Notification`.
This feature will receive notifications of creation, promotion, and deletion of a product, when this receiver instance is subscribed to a certain product type.
The notification will be sent using HTTP POST request, so you need to make the receiver endpoint in this project.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Receiver" folder.

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    ROCKET_PORT=8001
    APP_INSTANCE_ROOT_URL=http://localhost:${ROCKET_PORT}
    APP_PUBLISHER_ROOT_URL=http://localhost:8000
    APP_INSTANCE_NAME=Safira Sudrajat
    ```
    Here are the details of each environment variable:
    | variable                | type   | description                                                     |
    |-------------------------|--------|-----------------------------------------------------------------|
    | ROCKET_PORT             | string | Port number that will be listened by this receiver instance.    |
    | APP_INSTANCE_ROOT_URL   | string | URL address where this receiver instance can be accessed.       |
    | APP_PUUBLISHER_ROOT_URL | string | URL address where the publisher instance can be accessed.       |
    | APP_INSTANCE_NAME       | string | Name of this receiver instance, will be shown on notifications. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)
3.  To simulate multiple instances of BambangShop Receiver (as the tutorial mandates you to do so),
    you can open new terminal, then edit `ROCKET_PORT` in `.env` file, then execute another `cargo run`.

    For example, if you want to run 3 (three) instances of BambangShop Receiver at port `8001`, `8002`, and `8003`, you can do these steps:
    -   Edit `ROCKET_PORT` in `.env` to `8001`, then execute `cargo run`.
    -   Open new terminal, edit `ROCKET_PORT` in `.env` to `8002`, then execute `cargo run`.
    -   Open another new terminal, edit `ROCKET_PORT` in `.env` to `8003`, then execute `cargo run`.

## Mandatory Checklists (Subscriber)
-   [x] Clone https://gitlab.com/ichlaffterlalu/bambangshop-receiver to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [x] Commit: `Create Notification model struct.`
    -   [x] Commit: `Create SubscriberRequest model struct.`
    -   [x] Commit: `Create Notification database and Notification repository struct skeleton.`
    -   [x] Commit: `Implement add function in Notification repository.`
    -   [x] Commit: `Implement list_all_as_string function in Notification repository.`
    -   [x] Write answers of your learning module's "Reflection Subscriber-1" questions in this README.
-   **STAGE 3: Implement services and controllers**
    -   [x] Commit: `Create Notification service struct skeleton.`
    -   [x] Commit: `Implement subscribe function in Notification service.`
    -   [x] Commit: `Implement subscribe function in Notification controller.`
    -   [x] Commit: `Implement unsubscribe function in Notification service.`
    -   [x] Commit: `Implement unsubscribe function in Notification controller.`
    -   [x] Commit: `Implement receive_notification function in Notification service.`
    -   [x] Commit: `Implement receive function in Notification controller.`
    -   [x] Commit: `Implement list_messages function in Notification service.`
    -   [x] Commit: `Implement list function in Notification controller.`
    -   [x] Write answers of your learning module's "Reflection Subscriber-2" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Subscriber) Reflections

#### Reflection Subscriber-1

## 1. Saat memilih antara Mutex<> dan RwLock<>, pertimbangkan bagaimana akses data terjadi dalam aplikasi kita. Mutex<> memberikan akses eksklusif, sehingga hanya satu thread yang dapat mengakses data pada satu waktu. Sementara itu, RwLock<> memungkinkan pembacaan oleh beberapa thread secara bersamaan, namun hanya satu thread yang bisa menulis pada satu waktu. Jika kita menghadapi skenario di mana pembacaan notifikasi sering terjadi oleh banyak thread secara bersamaan, maka RwLock<> bisa menjadi pilihan yang tepat. RwLock<> memungkinkan pembacaan data tanpa mengalami blokade antar thread. Namun, perlu diperhatikan bahwa jika terjadi penulisan yang jarang tetapi penting, RwLock<> dapat mempengaruhi performa karena pembacaan mungkin terhenti sementara saat penulisan berlangsung. Jadi, dalam konteks di mana pembacaan notifikasi sering dilakukan oleh banyak thread secara bersamaan, RwLock<> lebih disukai karena memungkinkan pembacaan bersamaan tanpa mengorbankan keamanan data.

## 2. Di Rust, aturan tentang kepemilikan dan peminjaman dirancang untuk mencegah variabel-variabel melampaui batasan konteks awal mereka. Tujuannya adalah untuk mencegah situasi yang berpotensi berbahaya seperti perlombaan data, di mana beberapa thread bersaing untuk mengakses atau memodifikasi data yang sama secara bersamaan. Dengan menerapkan aturan ini, Rust memastikan keamanan thread dengan memastikan bahwa hanya satu thread yang bisa memodifikasi data pada satu waktu tertentu, mengurangi risiko kesalahan dan konflik yang terkait dengan thread.

#### Reflection Subscriber-2

## 1. Dari apa yang Anda temukan dalam file lib.rs, terlihat bahwa ini adalah pusat kendali dari seluruh proyek Rust ini. Di sini, Anda tidak hanya menemukan variabel global yang diinisialisasi dan struktur data yang didefinisikan, tetapi juga fungsi-fungsi penting yang mengatur alur kerja aplikasi. Lib.rs menjadi landasan dari aplikasi ini. Dari sini, segala sesuatu dimulai dan terkoordinasi. Inilah tempat di mana fondasi dibangun untuk menjalankan aplikasi dengan mulus, dan di mana struktur data yang vital ditetapkan. Jadi, dalam konteks ini, lib.rs dapat dianggap sebagai otak dari proyek Rust ini.

## 2. Dengan menerapkan pola Observer, kita dapat meminimalkan ketergantungan antara Main App dan Receiver dalam aplikasi kita. Ini berarti ketika ada perubahan atau penambahan receiver, inti dari aplikasi tidak akan terpengaruh. Tiap receiver berperan sebagai pengamat independen, sehingga mereka hanya akan diberi tahu saat ada perubahan yang berkaitan dengan mereka. Ini memberikan fleksibilitas lebih dalam mengelola dan memperluas aplikasi tanpa risiko mengganggu bagian utama aplikasi. Tidak hanya itu, penggunaan pola Observer membuat penambahan instance Main App menjadi lebih sederhana. Setiap instance Main App dapat mengelola daftar pengamatnya sendiri, sehingga tidak perlu khawatir tentang interaksi antara instance-instance tersebut. Namun, jika kita menginginkan semua pengamat menerima notifikasi dari setiap instance Main App, diperlukan logika tambahan untuk menyatukan komunikasi antar instance. Hal ini mungkin memerlukan implementasi tambahan untuk menyinkronkan informasi antara instance-instance tersebut, tetapi dapat memberikan manfaat besar dalam memperluas fungsionalitas aplikasi secara keseluruhan.

## 3. Walaupun saya belum memiliki pengalaman langsung dalam membuat tes sendiri atau mengembangkan dokumentasi pada Postman Collection, saya meyakini nilai besar dari kedua praktik tersebut. Dalam pengujian, kita dapat secara terstruktur memeriksa setiap respons dari aplikasi untuk memastikan konsistensi dan kepatuhan dengan harapan yang telah ditetapkan. Ini tidak hanya membantu mengidentifikasi masalah dengan cepat, tetapi juga memastikan bahwa setiap skenario telah diperhitungkan. Di sisi lain, pengembangan dokumentasi menggunakan Postman Collection juga memiliki manfaat yang signifikan. Dokumentasi yang jelas dan terperinci memungkinkan pengguna atau pengembang lain untuk memahami API dengan lebih baik, dengan informasi tentang setiap endpoint, parameter yang diperlukan, dan respons yang diharapkan. Meskipun saya belum menjalankan praktik ini secara langsung, saya yakin bahwa keduanya merupakan elemen penting dalam pengembangan aplikasi yang profesional. Menerapkan pengujian yang baik dan dokumentasi yang terperinci dapat meningkatkan kualitas dan kehandalan aplikasi secara keseluruhan.