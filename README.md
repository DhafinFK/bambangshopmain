# BambangShop Publisher App
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
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [v] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [v] Commit: `Create Subscriber model struct.`
    -   [v] Commit: `Create Notification model struct.`
    -   [v] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [v] Commit: `Implement add function in Subscriber repository.`
    -   [v] Commit: `Implement list_all function in Subscriber repository.`
    -   [v] Commit: `Implement delete function in Subscriber repository.`
    -   [v] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [v] Commit: `Create Notification service struct skeleton.`
    -   [v] Commit: `Implement subscribe function in Notification service.`
    -   [v] Commit: `Implement subscribe function in Notification controller.`
    -   [v] Commit: `Implement unsubscribe function in Notification service.`
    -   [v] Commit: `Implement unsubscribe function in Notification controller.`
    -   [v] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [v] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [v] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [v] Commit: `Implement publish function in Program service and Program controller.`
    -   [v] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [v] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1

1. Dalam desain Observer, kebutuhan akan antarmuka atau trait ditentukan oleh kompleksitas dari sistem observer yang digunakan. Ketika observer mencakup berbagai jenis dan kelas, penggunaan trait menjadi esensial untuk memudahkan implementasi. Akan tetapi, untuk kasus BambangShop yang hanya memiliki satu kelas observer yaitu Subscriber, penggunaan trait tidak diperlukan. Sebaliknya, struktur model tunggal sudah memadai untuk mengelola pengamatan terhadap perubahan yang terjadi. Oleh karena itu, untuk BambangShop, cukup menggunakan satu Model struct tanpa perlu menambahkan antarmuka yang lain.

2. Penggunaan DashMap diperlukan untuk meningkatkan efisiensi dalam memetakan hubungan antara produk dan subscriber. Penggunaan Vec akan mengharuskan pembuatan dua Vec terpisah untuk tiap produk, yang dapat menyulitkan dalam pengelolaan data. Sebaliknya, DashMap menyediakan cara yang lebih mudah untuk mengakses dan memelihara data melalui pemetaan langsung antara produk dan subscriber.

3. Dalam bahasa pemrograman Rust, kepatuhan ketat terhadap aturan kompiler menjamin keselamatan thread dalam program. Untuk variabel statis Daftar Pelanggan (SUBSCRIBERS), penggunaan DashMap dimaksudkan untuk memastikan bahwa penggunaan HashMap aman dari masalah yang berkaitan dengan thread. Perlu dipertimbangkan apakah penggunaan DashMap masih relevan atau jika pola Singleton bisa menjadi alternatif yang layak.

#### Reflection Publisher-2

1. Dalam kerangka MVC, dimana Model berperan dalam menyimpan data serta mengatur logika bisnis, penting untuk memisahkan "Servi
ce" dan "Repository" agar sesuai dengan prinsip single responsibility. Pemisahan ini mengisolasi fungsi yang berbeda, di mana "Service" bertanggung jawab atas logika aplikasi dan "Repository" fokus pada pengelolaan akses data. Struktur ini meningkatkan modularitas dan memudahkan dalam pengembangan serta perawatan kode.

2. Mengandalkan hanya pada Model tanpa struktur tambahan lainnya akan menghasilkan tingkat ketergantungan yang tinggi dalam program. Hal ini berarti setiap kali terjadi perubahan, banyak penyesuaian yang harus dilakukan pada kode. Menggunakan hanya Model tanpa lapisan tambahan mempersulit pemeliharaan kode karena hubungan erat antar komponen, di mana perubahan pada satu bagian sering kali berdampak pada bagian lain.

3. Saya telah memperluas pengetahuan saya tentang Postman, sebuah alat yang sangat berguna untuk menguji aplikasi yang saya kembangkan. Dengan Postman, saya bisa memastikan bahwa respon aplikasi sesuai dengan ekspektasi berdasarkan permintaan yang diberikan. Saya juga dapat menyesuaikan operasi yang diperlukan, seperti operasi CRUD, untuk memastikan kebenaran data. Beberapa fitur Postman yang saya temukan sangat berguna termasuk kemampuan untuk mengelola dan menyimpan kumpulan permintaan HTTP, mengotomatisasi pengujian dengan skrip, serta menyediakan lingkungan terisolasi untuk melakukan pengujian integrasi dengan API eksternal. Saya sangat menghargai fitur pengujian otomatis yang memungkinkan saya menjalankan serangkaian tes secara teratur untuk memastikan konsistensi dan kualitas aplikasi.

#### Reflection Publisher-3
