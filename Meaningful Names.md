# Meaningful Names

Pada chapter ini kita akan membahas mengenai bagaimana sebuah penamaan terhadap segala hal dalam code kita dapat mempengaruhi performa dari sebuah pengerjaan project atau apps.

## Use Intention-Revealing Names & Avoid Disinformation
Kita harus memberikan nama kepada variable, method, atau apapun yang berkaitan dengan code yang kita buat sesuai dengan apa tujuan dari hal itu dibuat oleh kita. Dan terutama jangan buat penamaan yang dapat membingungkan pembaca code lainnya
Berikut contoh penamaan yang kurang baik:
```
public List<String[]> getItem(int id){
    List<String[]> list1 = new ArrayList<String[]>();
    for(String[] string : GroupOfString){
        if(string.getId == id){
            list1.add(string);
        }
    }
    return list1;
}
```
Disini akan membingungkan apabila kita hanya memberi nama "getItem()" karna terlalu luas pengertian dari "getItem()" tersebut. Dan banyak juga penamaan yang masih sangat tidak jelas seperti list1, string, dan GroupOfString. Oleh karena itu akan lebih apabila kita ganti penamaannya menjadi:
```
public List<Product> getProductByUserId(int id){
    List<Product> products = new ArrayList<Product>();
    for(Product product : catalog){
        if(product.getId == id){
            products.add(product);
        }
    }
    return products;
}
```
Dengan begini lebih jelas maksud dari method tersebut apa dan variable yang digunakan itu tujuannya apa.

## Make Meaningful Distinctions
Biasanya kita akan dihadapkan pada sebuah kondisi dimana kita harus memberi nama untuk sebuah variable yang tujuannya berbeda namun berkaitan. Seperti ketika kita perlu memberi nama untuk 2 method yang pertama berfungsi untuk mengambil sebuah data Product secara random dan yang kedua berfungsi untuk mengambil semua Product, jika kita beri nama seperti:
```
getProduct();
getProducts();
```
akan sangat membingungkan untuk dipahami oleh programmer lainnya, oleh karna itu lebih baik kita menggantinya dengan:
```
getRandomProduct();
getAllProducts();
```
## Avoid Encodings
Hindari yang namanya encoding, karena tanpa disacari kita sudah punya cukup banyak hal untuk di encoding dan tidak perlu lagi kita melakukan encoding dengan sengaja seperti memberikan keterangan jenis tipe data didepan nama sebuah variabel, dan berikut beberapa klasifikasi encoding yang harus diperhatikan.
### Hungarian Notation & Member Prefix
Hungarian Notation dulunya digunakan ketika jamannya C masih menjadi bahasa utama, gunanya untuk memberi keterangan tipe data apa yang kita berikan untuk variabel tersebut. Oleh karena itu kita tidak perlu memberi penamaan seperti `var sName` untuk menunjukkan kalau name adalah String. Kita juga tidak perlu melakukan member prefix seperti `String m_desc` karna akan lebih baik untuk langsung `String description`.
### Interfaces and Implementations
Ketika kita membuat interface dan implementasinya, ada banyak pendapat yang mengenai penamaan yang baik agar kita apat tau secara jelas interface dan implementasinya. Dari interface, ada yang berpendapat untuk memberikan nama `IProductFactory`, namun huruf `I` didepan sebenarnya tidak terlalu berpengaruh oleh karena itu lebih baik langsung `ProductFactory`. Dari implementasinya ada yang menggunakan `CProductFactory` dimana dapat lebih jelas apabila kita ganti menjadi `ProductFactoryImpl` untuk menunjukkan itu adalah implementasi dari ProductFactory.

## Avoid Mental Mapping
Biasanya ini terjadi ketika kita melakukan looping, kita sering memberi nama menggunakan 1 huruf seperti i, j, atau k. Jika looping ini masih kecil dan tidak menimbulkan konflik maka itu masih bisa diacuhkan, namun tetap saja cara ini sudah kuno dan kurang baik digunakan.

## Little Notes
1. Berikan penamaan yang mudah dibaca oleh manusia
2. Berikan penamaan yang mudah dicari oleh rekan kita seperti: `validateEmailAndPassword()` dibanding 'emailAndPasswordValidation()'
3. Penamaan untuk Class harus menggunakan kata benda (noun)
4. Penamaan untuk Menthod atau Function harus menggunakan kata kerja (verb)
5. Jangan menggunakan kata-kata yang aneh seperti `FireInTheHole` untuk melakukan delete
6. Pilih satu kata untuk mewakili sebuah konsep seperti diantara `get`,`fetch`,`retrieve` yang memiliki konsep yang sama yaitu untuk mengambil sebuah data