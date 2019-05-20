# System

## Separate Constructing a System from Using It
Kita perlu memisahkan proses ketika kita membangun aplikasi itu dan ketika apliaksi itu berjalan. Tapi tidak jarang hal ini tidak diperhatikan, sehingga ada logic yang digunakan untuk membangun apps tersebut namun masuk ke logic ketika apps itu berjalan. Contohnya:
```
public Service getService() { 
    if (service == null)
        service = new MyServiceImpl(...);
    return service;
}
```
Hal ini biasanya disebut Lazy Initialization, bagusnya adalah startup timenya bisa lebih cepat, dan kita hanya akan membuat object jika object itu dibutuhkan. Tapi buruknya adalah ini terkesan kita me-"hard-code" dependensi ini, dan kits harus memperhatikannya setiap kali kita menjalankan apps kita meskipun kita belum tentu menggunakannya.

### Separation of main
Salah satu cara agar bagian yang kita gunakan tidak berjalan ketika tidak digunakan adalah dnegan cara menggunakan `main`atau function yang disebut `main` dan membuat sisa aplikasinya dengan anggapan object yang dibutuhkan sudah dibuat dan disambungkan dengan baik. Sehingga flow kerjanya jelas dan main function hanya akan membuat object yang memang dibutuhkan dan nantinya akan dikirimkan ke aplikasi.
### Factories
Ketika kita membuat object tentunya aplikasi akan kena dampaknya, seperti misalnya ketika kita ingin membuat `LineItems` untuk mengisi Order. Kita bisa menggunakan Abstract Factory untuk mengatur kapan dibuatnya LineItems
### Dependencies Injection
Dependency Injection merupakan bentuk aplikasi dari Inversion of Control untuk dependency management, dimana IoC sendiri memindahkan responsibilities kedua ke object lain yang lebih fokus untuk tujuan tersebut. Dependency management yang dimaksud disini adalah dengan memberikan tanggung jawab kepada mekanisme yang lebih berwewenang untuk mendeklarasikan dependency itu sendiri. Jadi class tersebut akan benar-benar passive, dan hanya menyediakan constructor ataupun setter yang akan digunakan untuk meng-"inject" dependency tersebut

## Java Proxies
Java proxies cocok digunakan untuk kondisi yang simple, seperti untuk membungkus panggilan method pada sebuah class atau object. Tetapi dynamic proxies yang disediakan dalam JDK hanya berfungsi dengan interface. Untuk melakukan proxy pada sebuah class kita membutuhkan byte-code manipulation library seperti CGLIB, ASM, atau Javassist.

## Optimize Decision Making
Modularitas dan pemisahan masalah memungkinkan manajemen dan pengambilan keputusan dilakukan secara terdesentralisasi. Dalam pembuatan keputusan tidak bisa dilakukan oleh 1 orang aja, kita tau bahwa akan lebih baik apabila kita berikan kepada orang yang tepat. Kita juga perlu tau bahwa terkadang akan lebih baik apabila kita menunda keputusan tersebut hingga waktu terakhir yang ada, sehingga kita bisa mencari dan mengolah data yang kita miliki sebaik mungkin






