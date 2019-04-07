# Objects And Data Structures

Pada chapter ini kita akan membicarakan mengenai object yang kita buat dalam project dan juga data structuresnya, mengenai bagaimana pembuatan yang baik dan tujuannya untuk apa

## Data Abstraction
Contoh data abstraction adalah ketika kita melakukan implementation kepada sebuah interface, tujuannya adalah agar data utama tidak dapat diakses dengan langsung dan juga memberikan kemudahan agar kita hanya mengakses apa yang memang kita perlukan. Contohnya:
```
public interface Point {
    double getX();
    double getY();
    void setCartesian(double x, double y); double getR();
    double getTheta();
    void setPolar(double r, double theta); 
}
```
ketika kita membuat sebuah interface seperti ini, maka ini akan membuat kita dapat mengimplementasikannya kedalam banyak class tanpa perlu memikirkan ini untuk lingkaran atau persegi, karena ini sudah mencakup segala yang dibutuhkan. Contoh lain dari data asbtraction juga dapat kita lihat ketika:
```
public interface Vehicle {
    double getFuelTankCapacityInGallons(); 
    double getGallonsOfGasoline();
}
```
Tujuan kita mengetahui maksimal kapasitas dari tank dan jumlah gas yang ada didalam gas itu untuk apa? Kita ingin mengetahui tinggal berapa persen gas yang kita miliki, maka dapat saja kita langsung membuatnya menjadi:
```
public interface Vehicle {
    double getPercentFuelRemaining();
}
```
Tetapi kedua cara diatas ini dapat sama-sama diterapkan, hanya kembali lagi ketujuan yang ingin dicapai itu apa.

## Data/Object Anti-Symmetry
Object membuat data tertutup dalam enkapsulasinya dan menggunakan function untuk mengakses data mereka. Data Structure membuat datanya terbuka, tanpa menggunakan function. Data Structures yang biasa digunakan dalam procedural programming memiliki kelebihannya, begitu juga dengan Object yang digunakan dalam Object Oriented Programming. Seperti contoh procedural programming:
```
public class Square { 
    public double side;
}
public class Circle { 
    public double radius;
}
public class Geometry {
    public final double PI = 3.141592653589793;
    public double area(Object shape){
        if (shape instanceof Square) { 
            Square s = new Square(); 
            return s.side * s.side;
        }else if (shape instanceof Circle) {
            Circle c = new Circle();
            return PI * c.radius * c.radius; 
        }
    }
}
```
Dari code berikut, kelebihan yang dapat kita rasakan adalah ketika kita ingin menambahkan sebuah variable baru kesalah satu jenis shape, maka shape lain tidak harus berganti mengikuti perubahan yang terjadi pada class tersebut. Namun ketika kita ingin menambahkan sebuah shape baru, maka itu akan mempengaruhi class Geometry karna dia harus menambahkan shape baru di if elsenya. Disisi lain ada Object yang mengcover kekurangan dari ini, contohnya:
```
public class Square implements Shape {
    private double side;
    public double area() { return side*side;} 
}
public class Circle implements Shape { 
    private double radius;
    public final double PI = 3.141592653589793;
    public double area() {return PI * radius * radius;} 
}
```
Dari code berikut, kita kana lebih mudah apabila ingin menambah sebuah shape baru, karena sudah ada interface shape yang memiliki semua yang dibutuhkan dari sebuah class shape, namun akan buruk apabila kita ingin menambahkan sebuah tipe data baru ataupun functuin baru karena harus menambahkan di class Shape lalu mengimplementasikannya semua di masing-masing class yang mengimplement class Shape.
Kesimpulannya:
* Procedural membuat kita mudah untuk menambah function. Object Oriented membuat kita mudah menambah class baru
* Procedural membuat kita sulit untuk menambah sebuah data structure karna harus merubah functionnya. Object Oriented membuat kita sulit untuk menambah sebuah function baru karena harus merubah class yang mengimplementasikannya

## The Law Of Demeter
`A module should not know about the innards of the objects it manipulates`
ini adalah konsep dari Law of Demeter, dimana contohnya sebuah Object menutup data namun mengekspose functionnya, dimana artinya sebuah object tidak boleh membuka data atau internal structures mereka.
Dalam penggunaan sebuah object, biasanya kita perlu mengambil data yang cukup panjang chainingnya, seperti:
`String name = User.getName(User.queryUserById(session.getAttribute("userId")));`
Ketika dibaca ini akna cukup memusingkan dan kondisi ini biasa disebut `Train Wrecks`. Kondisi ini dapat diperbaiki dengan memecahkan atau menampungnya kesebuah variable-variable agar mudah dimengerti, seperti:
```
int UserId = session.getAttribute("UserId");
User user = User.queryUserById(UserId);
String UserName = user.getName();
```

## Hiding Structures
-- 

## Data Transfer Object
Object yang hanya berisikan Data + Constructor + Setter Getter saja, merupakan  Object yang sangat baik terutama apabila digunakan untuk berkomunikasi dengan Databse ataupun Socket. Ada juga Active Records yang merupakan DTO namun variablenya dibuka secara public, dengan ada tambahan function `save`&`find`. Biasanya active records ini merupakan bentuk dari database tablenya langsung
