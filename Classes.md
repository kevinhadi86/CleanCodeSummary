# Classes

Class harusnya dimulai dari variable-variable yang dibutuhkan, terlebih lagi apabila ada public static constant baru private static variables, dan instance variables. Ketika kita ingin membuat private fucntion, lebih baik kita buat setelah dipanggil oleh public function yang menggunakannya, sehingga akan memudahkan programmer lain untuk membacanya seperti koran.
Sering banget kita denger kalau kita harus sering-sering private isi dari class tersebut, mulai dair variable hingga function didalamnya. Tetapi terkadang kita juga harus membuatnya menjadi protected agar dapat diakses oleh sebuah test. 

## Class Should be Small
Sebelumnya ketika kita membahas mengenai function, dikatakan juga kalao function harus kecil dan kita mengukurnya dengan satuan line of code. Class juga haruslah kecil, namun satuan yang kita gunakan untuk mengukurnya adalah resposibility atau bisa dihitung dari apakah benar method yang berada disana adalah method yang benar-benar dibutuhkan dan tidak berlebihan. Biasanya untuk membantu kita mengukur ukuran dari class tersebut, penamaan dari class itu sangat membantu karena itu akan mendeskripsikan seberapa kecil ukuran class itu.

## The Single Responsibility Principle
Single Responsibility Principle berkata bahwa class ataupun function hanya boleh punya 1 alasan untuk berubah. Principle ini membantu kita mendeskripsikan ukuran dari responsibility dan juga ukuran dari class tersebut. Contohnya adalah seperti:
```
public class SuperDashboard extends JFrame implements MetaDataUser {
    public Component getLastFocusedComponent()
    public void setLastFocused(Component lastFocused)
    public int getMajorVersionNumber()
    public int getMinorVersionNumber()
    public int getBuildNumber() 
}
```
class diatas ini belum cukup untuk memenuhi Single Responsibility Principle, karena ada 3 function yang dapat dipisah dari class tersebut menjadi:
```
public class Version {
    public int getMajorVersionNumber() 
    public int getMinorVersionNumber() 
    public int getBuildNumber()
}
```

## Cohesion
Class harus memiliki instance variable yang sedikit, dan function-functionnya harus menggunakan setidaknya 1 atau lebih dari variable tersebut sehingga class tersebut menjadi semakin cohesive. Kita harus sebisa mungkin membuat class itu menjadi se-cohesive mungkin, karena dengan begitu kita membuat function dan variable didalam class ini menjadi lebih bersatu.

## Organizing for changes
Setiap clas ahrus siap untuk perubahan, dimana perubahan itu harus berdasarkan principle-principle yang memang mendukung. Seperti:
```
public class Sql {
    public Sql(String table, Column[] columns)
    public String create()
    public String insert(Object[] fields)
    public String selectAll()
    public String select(Column column, String pattern)
    public String select(Criteria criteria)
    private String columnList(Column[] columns)
    private String valuesList(Object[] fields, final Column[] columns) 
    private String selectWithCriteria(String criteria)
    private String placeholderList(Column[] columns)
}
```
Class ini harus berubah nanti ketika kita ada mengganti isi dari salah satu functionnya atau ketika kita melihat isi dari `selectWithCriteria` dimana ini sedikit menyalahi Single Responsibility Principle dimana function ini hanya berpengaruh/bergantung kepada function `select`. Sehingga class ini perlu diubah menjadi:
```
abstract public class Sql {
    public Sql(String table, Column[] columns) 
    abstract public String generate();
}
public class CreateSql extends Sql {
    public CreateSql(String table, Column[] columns) 
    @Override public String generate()
}
public class SelectSql extends Sql {
    public SelectSql(String table, Column[] columns) 
    @Override public String generate()
}
public class InsertSql extends Sql {
    public InsertSql(String table, Column[] columns, Object[] fields) 
    @Override public String generate()
    private String valuesList(Object[] fields, final Column[] columns)
}
public class SelectWithCriteriaSql extends Sql { 
    public SelectWithCriteriaSql(String table, Column[] columns, Criteria criteria) 
    @Override public String generate()
}
public class SelectWithMatchSql extends Sql { 
    public SelectWithMatchSql(String table, Column[] columns, Column column, String pattern)
    @Override public String generate()
}
public class Where {
    public Where(String criteria) 
    public String generate()
}
public class ColumnList {
    public ColumnList(Column[] columns) 
    public String generate()
}
```
Dengan begini ukuran setiap class menjadi cukup kecil dan jadi mudah dimengerti, terlebih lagi ketika kita ingin menambahkan sebuah kegiatan baru seperti `update` kita tidak perlu merubah sebuah class besar melainkan cukup menambahkan class baru.

## Isolating from Change
Code yang kita buat bisa jadi selalu berubah setiap kali ada permintaan baru baik secara bisnis ataupun teknis. Seperti contohnya kita membuat aplikasi untuk investasi, maka akan ada class Portofolio dan kita juga akan menghubungkan aplikasi kita dengan API dari luar. Akan sangat menyusahkan apabila kita harus memanggil API tersebut secara terus menerus. Oleh karena itu kita bikin interface untuk menjadi perantaranya, yang memiliki method:
```
public interface StockExchange { 
    Money currentPrice(String symbol);
}
```
Dimana dengan ini, maka isi dari Portofolio dapat berupa:
```
public Portfolio {
    private StockExchange exchange;
    public Portfolio(StockExchange exchange) {
        this.exchange = exchange; 
    }
    // ... 
}
```
Sehingga dengan ini class Portofolio tidak perlu selalu bergantung/memanggil API dari luar.





