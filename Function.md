# Function
## Small!!!
Dalam pembuatan function, function itu haruslah kecil. Tidak ada rumusan yang tepat seberapa kecil function itu seharusnya dibentuk, namun dari buku Clean Code ini diberitahu untuk sebisa mungkin 2-4 line dan dapat dipahami dalam waktu paling lama 3 menit. Dan tidak mengandung nested structures 

## Do One Thing
Seperti yang sebelumnya saya bilang function haruslah kecil, hal ini dikarenakan function harusnya hanya melakukan 1 kegiatan, seperti:
```
List<Product> items;
public void addItemToList(Product product){
    items.add(product);
}
```

## One Level of Abstraction per Function
Dalam function harus memiliki 1 level abstraksi saja, untuk mendukung juga bahwa function itu hanya boleh melakukan 1 kegiatan saja. Contoh level abstraksi yang tinggi seperti `getHtml()`, dan contoh yang rendah seperti `.append('\t')`.

## Switch case
Harus dihindari untuk membuat switch case karena dengan ada switch case akan membuat function itu melakukan lebih dari 1 kegiatan. Caranya adalah dengan memasukan ke interface sehingga function atau kegiatan dari setiap switch hanya akan dibuat sekali ketika salah satu case terjadi.

## Function Arguments
Ketika membuat function pastinya ada argument yang kita terima, jumlah-jumlah function ini ternyata mempengaruhi Clean Code. Semakin sedikit argumen yang diterima oleh sebuah function akan membuat itu menjadi lebih mudah dimengerti, asalkan jumlah argumen yang diterima memang sesuai dengan kebutuhan (tidak dipaksakan semua function untuk hanya menerima 1 argumen).
### Monadic Argument (1 Argument)
Biasanya ada 2 alasan kita melempar 1 argumen kesebuah function, pertama untuk melakukan pengecekkan (`boolean isLogin(User user)`), dan yang kedua untuk mengolah suatu hal (`void getProductById(String id)`). Tipe ini paling mudah dimengerti karna tidak akan banyak mengolah data sehingga functionnya juga akan relatif kecil. Terlebih lagi jangan mengisi argumen dengan sebuah boolean seperti `login(true)`, tetapi dapat diganti dengan `login (boolean isEmailValid)`.
### Dyadic Function
Tipe ini lebih sulit dimengerti dibanding Monadic Argument karena semakin banyak argumennya maka butuh waktu yang semakin panjang untuk memahami kegunaannya seperti `writeField(output,name)`, akan lebih efektif apabila kita menggunakan `writeField(name)`. Tetapi terkadang 2 argumen ini juga lebih baik dibanding 1 argumen apabila penggunaannya tepat seperti `new Point(0,0)` akan lebih jelas dibanding `new point(0)`
### Triad Function
Tipe ini lebih sulit lagi untuk dipahami seperti misalnya `assertEquals(expected,actual,message)` oleh karena itu perlu dipikirkan matang2 untuk penggunaannya
### Object Argument
kita bisa mengganti isi argument kita dengan sebuah object apabila itu akan memudahkan seperti dari yang awalnya `register(String name, String email, String password)` menjadi `register(User user)`
### Verbs and Keywords
Penamaan yang kita berikan harus menjelaskan tujuan dari function itu, seperti `write(name)`. Namun penamaan ini dapat dikembangkan lagi menjadi `writeField(name)`, sehingga pembaca yang dari awalnya hanya berpikir "oh function ini untuk mencetak nama" akan menjadi lebih jelas dan berpikir "oh function ini untuk mencetak sebuah field dengan nama".

## Have No Side Effects
Function tidak seharusnya memberikan sebuah efek samping bagi sistem diluar dari apa yang seharusnya dia lakukan, seperti:
```
public boolean validateUsername(String username){
    User user = User.findUsername(username);
    if(user == null){
        User newUser = new User(username);
        return true;
    }
    return false
}
```
Dari snippet berikut, fuction ini akan memberikan efek samping karena seharusnya dia hanya mengecek apakah username tersebut sudah ada sebelumnya atau belum, tetapi function ini malah langsung membuat user baru. Kita bisa saja mengganti nama function ini menjadi `validateUsernameAndCreateUser(String username)`, tetapi ini akan menyalahi konsep "Do One Thing".

## Output Arguments
COntoh dari output argument adalah seperti `void appendFooter(StringBuffer report)` yang dimana function ini dimaksudnya bahwa kita ingin menambahkan footer ke dalam report. Tetapi sekarang akan lebih baik apabila kita membuatnya dengan `report.appendFooter()`, karena ketika kita menggunakan output argument maka kita membuat ada pihak eksternal yang mempengaruhi class atau state tersebut;

## Command Query Separation
Terkadang kita akan membuat sebuah function yang rancu ketika kita harus melakukan query juga didalam kegiatan tersebut dengan alasan agar lebih efisien, seperti `if(set('name','Mike')`. Dengan function ini kita bisa dengan cepat langsung melakukan set dan sambil mengecek apakah hal ini berhasil atau tidak, yang dimana apabila berhasil maka artinya name ini ada. Tetapi cara ini membingungkan dan perlu waktu untuk dipahami, oleh karena itu lebih baik apabila kita merubahnya menjadi:
```
if(nameExists("name"){
    setName("name","Mike");
}
```

## Prefer Exceptions to Returning Error Codes
Lebih baik menggunakan try/catch dibanding kita harus if else untuk menunjukkan error seperti:
```
void addUser(User user){
    if(user.Exists()){
        if(user.Active()){
            System.out.print("User exist & active");
        }
        else{
            System.out.print("User exist but not active. Recreating nre user");
            userList.addAttribute(user);
        }
    }else{
        userList.addAttribute(user);
    }
}
```
Function ini akan lebih baik apabila kita ganti menjadi:
```
void addUser(User user){
    try{
        userList.addAttribute(user);
    }catch(Exception e){
        e.printStackTrace();
    }
}
```

Tetapi try/catch seperti ini juga masih kurang bagus karna cukup membingungkan, oleh karna itu lebih baik apabila kita mengganti isinya menjadi:
```
void addUser(User user){
    try{
        addUserToList(user);
    }catch(Exception e){
        logError(e);
    }
}
```
kenapa seperti inoi? karena error handling sendiri merupakan sebuah kegiatan, dan apabila kita menerapkan konsep "Do One Thing", maka kita perlu memisahkannya lagi kedapan function lain.

## Don't Repeat Yourself
Konsep ini sering kita dengar tapi kadang tetap terlewatkan oleh kita, seperti ketika kita membuat logic dari function `addProduct` atau `addUser`, biasanya kita akan melakukan validasi dulu apakah fieldnya ada yang kosong, dan validasi lain yang akan kita ulang dikedua function tersebut. Nah disinilah kita bisa membuat sebuah function baru `validate` untuk melakukan pengecekkan terhadap hal-hal yang akan dilakukan di function `addProduct` dan `addUser`

## Structured Programming
Edsger Dijkstra mempunyai sebuah peraturan mengenai pembuatan function, yaitu
`setiap function hanya boleh punya 1 entry dan 1 exit`
maksudnya, hanya boleh ada 1 `return` dalam function tersebut, tidak ada `break` ataupun `continue` dalam looping. dan tidak ada `goto`.


## Little Notes:
1. Bikin function agar mudah dibaca dari atas kebawah
2. Gunakan nama yang menjelaskan tujuan dari function itu
3. Apabila ingin mengembalikan sebuah error, lebih baik gunakan try/catch
