
# 📘 Tutorial Java OOP #04: Constructor & Destructor pada Java

> *"Konstruktor adalah tempat di mana kehidupan objek dimulai; destruktor adalah tempat di mana objek mengucapkan selamat tinggal."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dan peran konstruktor dalam pemrograman berorientasi objek
- Membuat dan mengimplementasikan berbagai jenis konstruktor di Java
- Memahami konsep destruktor dan bagaimana Java menangani penghapusan objek
- Menerapkan constructor overloading dan constructor chaining dengan tepat
- Memahami perbedaan antara metode `finalize()` dan pendekatan modern untuk manajemen sumber daya
- Mengimplementasikan best practices untuk pembuatan konstruktor

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Konstruktor (Constructor)](#konstruktor-constructor)
   - [Apa itu Konstruktor?](#apa-itu-konstruktor)
   - [Default Constructor](#default-constructor)
   - [Parameterized Constructor](#parameterized-constructor)
   - [Copy Constructor](#copy-constructor)
3. [Constructor Overloading](#constructor-overloading)
4. [Constructor Chaining](#constructor-chaining)
   - [Chaining dengan `this()`](#chaining-dengan-this)
   - [Chaining dengan `super()`](#chaining-dengan-super)
5. [Destruktor dan Garbage Collection](#destruktor-dan-garbage-collection)
   - [Garbage Collection di Java](#garbage-collection-di-java)
   - [Metode `finalize()`](#metode-finalize)
   - [Limitasi `finalize()`](#limitasi-finalize)
6. [Resource Management di Java Modern](#resource-management-di-java-modern)
   - [try-with-resources](#try-with-resources)
   - [Closeable Interface](#closeable-interface)
7. [Best Practices untuk Konstruktor](#best-practices-untuk-konstruktor)
8. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
9. [Rangkuman](#rangkuman)
10. [Latihan Soal](#latihan-soal)
11. [Referensi](#referensi)

## Pendahuluan

Setiap objek memiliki siklus hidup. Objek dibuat, digunakan, dan kemudian dihancurkan. Dalam bahasa pemrograman berorientasi objek seperti Java, proses pembuatan objek dikelola melalui konstruktor (constructor), sedangkan penghancuran objek dikelola oleh Garbage Collector.

Pada tutorial ini, kita akan mempelajari lebih dalam tentang konstruktor dan bagaimana Java menangani penghapusan objek. Memahami konsep ini sangat penting untuk membuat program yang efisien dan menghindari memory leak.

## Konstruktor (Constructor)

### Apa itu Konstruktor?

**Konstruktor** adalah metode khusus yang dipanggil saat objek dari sebuah class dibuat (diinstansiasi). Konstruktor digunakan untuk menginisialisasi objek, atau dengan kata lain, menyiapkan objek agar siap digunakan.

Karakteristik konstruktor:
- Namanya harus sama dengan nama class
- Tidak memiliki return type, bahkan `void` sekalipun
- Dipanggil secara otomatis saat objek dibuat dengan operator `new`
- Dapat overloaded (memiliki beberapa versi dengan parameter berbeda)
- Tidak dapat di-override, tetapi dapat di-chain (metode konstruktor memanggil konstruktor lain)

Konstruktor digunakan untuk:
- Menginisialisasi atribut objek dengan nilai awal
- Memastikan objek dalam keadaan valid sebelum digunakan
- Mengalokasikan sumber daya yang diperlukan objek

### Default Constructor

**Default Constructor** adalah konstruktor tanpa parameter yang dibuat secara otomatis oleh Java jika tidak ada konstruktor yang didefinisikan secara eksplisit dalam class.

Contoh:
```java
public class Mahasiswa {
    private String nama;
    private String nim;
    
    // Ini adalah default constructor yang dibuat otomatis jika tidak ada konstruktor lain
    // public Mahasiswa() {
    //     // Tidak ada statement, body kosong
    // }
}
```

Contoh penggunaan:
```java
// Memanggil default constructor
Mahasiswa mhs = new Mahasiswa();
```

Jika Anda membuat konstruktor dengan parameter, maka default constructor tidak akan dibuat secara otomatis. Jika masih diperlukan, Anda harus mendefinisikannya secara eksplisit.

```java
public class Mahasiswa {
    private String nama;
    private String nim;
    
    // Konstruktor dengan parameter
    public Mahasiswa(String nama, String nim) {
        this.nama = nama;
        this.nim = nim;
    }
    
    // Default constructor harus didefinisikan secara eksplisit jika masih diperlukan
    public Mahasiswa() {
        this.nama = "Belum ada nama";
        this.nim = "Belum ada NIM";
    }
}
```

### Parameterized Constructor

**Parameterized Constructor** adalah konstruktor yang menerima satu atau lebih parameter untuk menginisialisasi objek.

Contoh:
```java
public class Produk {
    private String nama;
    private double harga;
    private int stok;
    
    // Parameterized constructor dengan 3 parameter
    public Produk(String nama, double harga, int stok) {
        this.nama = nama;
        this.harga = harga;
        this.stok = stok;
    }
    
    // Parameterized constructor dengan 2 parameter
    public Produk(String nama, double harga) {
        this.nama = nama;
        this.harga = harga;
        this.stok = 0; // Nilai default
    }
    
    // Getter methods
    public String getNama() {
        return nama;
    }
    
    public double getHarga() {
        return harga;
    }
    
    public int getStok() {
        return stok;
    }
}
```

Contoh penggunaan:
```java
// Menggunakan konstruktor dengan 3 parameter
Produk laptop = new Produk("Laptop Asus", 12000000, 10);

// Menggunakan konstruktor dengan 2 parameter
Produk mouse = new Produk("Mouse Logitech", 350000);
```

### Copy Constructor

**Copy Constructor** adalah konstruktor yang menerima objek dari class yang sama sebagai parameter dan membuat salinan (copy) objek tersebut. Java tidak menyediakan copy constructor secara otomatis, sehingga perlu didefinisikan secara manual.

Contoh:
```java
public class Mahasiswa {
    private String nama;
    private String nim;
    private double[] nilai;
    
    // Konstruktor normal
    public Mahasiswa(String nama, String nim, double[] nilai) {
        this.nama = nama;
        this.nim = nim;
        this.nilai = nilai;
    }
    
    // Copy constructor
    public Mahasiswa(Mahasiswa mahasiswaLain) {
        this.nama = mahasiswaLain.nama;
        this.nim = mahasiswaLain.nim;
        
        // Deep copy untuk array (mencegah shared reference)
        this.nilai = new double[mahasiswaLain.nilai.length];
        for (int i = 0; i < mahasiswaLain.nilai.length; i++) {
            this.nilai[i] = mahasiswaLain.nilai[i];
        }
    }
    
    // Method untuk mengubah nilai
    public void setNilai(int index, double nilai) {
        if (index >= 0 && index < this.nilai.length) {
            this.nilai[index] = nilai;
        }
    }
    
    // Method untuk menampilkan info
    public void tampilInfo() {
        System.out.println("Nama: " + nama);
        System.out.println("NIM: " + nim);
        System.out.print("Nilai: ");
        for (double n : nilai) {
            System.out.print(n + " ");
        }
        System.out.println();
    }
}
```

Contoh penggunaan copy constructor:
```java
double[] nilaiAwal = {80, 75, 90};
Mahasiswa mhs1 = new Mahasiswa("Budi", "A12345", nilaiAwal);

// Membuat salinan dari mhs1
Mahasiswa mhs2 = new Mahasiswa(mhs1);

// Mengubah nilai mhs2 tidak akan memengaruhi mhs1
mhs2.setNilai(0, 95);

mhs1.tampilInfo(); // Nilai indeks 0 tetap 80
mhs2.tampilInfo(); // Nilai indeks 0 menjadi 95
```

#### Pentingnya Deep Copy vs Shallow Copy

Perhatikan bahwa copy constructor di atas menggunakan **deep copy** untuk array `nilai`. Ini penting karena:

- **Shallow Copy**: Hanya menyalin referensi objek, sehingga kedua objek akan berbagi referensi yang sama ke array. Perubahan pada array melalui satu objek akan memengaruhi objek lainnya.
- **Deep Copy**: Membuat salinan terpisah dari objek yang direferensikan, sehingga setiap objek memiliki versinya sendiri.

```java
// Contoh shallow copy (HINDARI untuk reference types)
public Mahasiswa(Mahasiswa mahasiswaLain) {
    this.nama = mahasiswaLain.nama;
    this.nim = mahasiswaLain.nim;
    this.nilai = mahasiswaLain.nilai; // Shallow copy (berbagi referensi)
}
```

## Constructor Overloading

**Constructor Overloading** adalah teknik mendefinisikan beberapa konstruktor dengan jumlah atau tipe parameter yang berbeda dalam class yang sama. Ini memungkinkan objek dibuat dengan cara yang berbeda-beda.

Contoh:
```java
public class Mobil {
    private String merek;
    private String model;
    private int tahun;
    private String warna;
    private double harga;
    
    // Konstruktor 1 - lengkap
    public Mobil(String merek, String model, int tahun, String warna, double harga) {
        this.merek = merek;
        this.model = model;
        this.tahun = tahun;
        this.warna = warna;
        this.harga = harga;
    }
    
    // Konstruktor 2 - tanpa harga
    public Mobil(String merek, String model, int tahun, String warna) {
        this.merek = merek;
        this.model = model;
        this.tahun = tahun;
        this.warna = warna;
        this.harga = 0.0; // Nilai default
    }
    
    // Konstruktor 3 - hanya merek dan model
    public Mobil(String merek, String model) {
        this.merek = merek;
        this.model = model;
        this.tahun = 2023; // Default tahun ini
        this.warna = "Hitam"; // Default warna
        this.harga = 0.0;
    }
    
    // Konstruktor 4 - default
    public Mobil() {
        this.merek = "Tidak diketahui";
        this.model = "Tidak diketahui";
        this.tahun = 2023;
        this.warna = "Hitam";
        this.harga = 0.0;
    }
    
    // Method untuk menampilkan info
    public void tampilInfo() {
        System.out.println("Merek: " + merek);
        System.out.println("Model: " + model);
        System.out.println("Tahun: " + tahun);
        System.out.println("Warna: " + warna);
        System.out.println("Harga: " + harga);
    }
}
```

Contoh penggunaan:
```java
// Menggunakan berbagai konstruktor
Mobil mobil1 = new Mobil("Toyota", "Avanza", 2021, "Putih", 220000000);
Mobil mobil2 = new Mobil("Honda", "Civic", 2022, "Merah");
Mobil mobil3 = new Mobil("Suzuki", "Swift");
Mobil mobil4 = new Mobil();

mobil1.tampilInfo();
mobil2.tampilInfo();
mobil3.tampilInfo();
mobil4.tampilInfo();
```

## Constructor Chaining

**Constructor Chaining** adalah teknik di mana satu konstruktor memanggil konstruktor lain dalam class yang sama atau dalam superclass. Ini membantu menghindari duplikasi kode dan meningkatkan maintainability.

### Chaining dengan `this()`

Untuk memanggil konstruktor lain dalam class yang sama, gunakan `this()` dengan parameter yang sesuai.

Contoh:
```java
public class Pegawai {
    private String id;
    private String nama;
    private String departemen;
    private double gaji;
    
    // Konstruktor lengkap
    public Pegawai(String id, String nama, String departemen, double gaji) {
        this.id = id;
        this.nama = nama;
        this.departemen = departemen;
        this.gaji = gaji;
    }
    
    // Konstruktor yang memanggil konstruktor lengkap
    public Pegawai(String id, String nama, String departemen) {
        this(id, nama, departemen, 4000000); // Memanggil konstruktor lengkap
    }
    
    // Konstruktor yang memanggil konstruktor sebelumnya
    public Pegawai(String id, String nama) {
        this(id, nama, "Umum"); // Memanggil konstruktor dengan 3 parameter
    }
    
    // Konstruktor default yang memanggil konstruktor sebelumnya
    public Pegawai() {
        this("P000", "Belum ada nama"); // Memanggil konstruktor dengan 2 parameter
    }
    
    // Method untuk menampilkan info
    public void tampilInfo() {
        System.out.println("ID: " + id);
        System.out.println("Nama: " + nama);
        System.out.println("Departemen: " + departemen);
        System.out.println("Gaji: " + gaji);
    }
}
```

Contoh penggunaan:
```java
Pegawai pegawai1 = new Pegawai("P001", "Budi", "IT", 8000000);
Pegawai pegawai2 = new Pegawai("P002", "Ani", "HR");
Pegawai pegawai3 = new Pegawai("P003", "Cindy");
Pegawai pegawai4 = new Pegawai();

pegawai1.tampilInfo();
pegawai2.tampilInfo();
pegawai3.tampilInfo();
pegawai4.tampilInfo();
```

### Chaining dengan `super()`

Untuk memanggil konstruktor dari superclass, gunakan `super()` dengan parameter yang sesuai.

Contoh:
```java
// Superclass
class Kendaraan {
    protected String merek;
    protected int tahun;
    
    public Kendaraan() {
        this.merek = "Tidak diketahui";
        this.tahun = 2023;
        System.out.println("Konstruktor default Kendaraan dipanggil");
    }
    
    public Kendaraan(String merek, int tahun) {
        this.merek = merek;
        this.tahun = tahun;
        System.out.println("Konstruktor parameterized Kendaraan dipanggil");
    }
}

// Subclass
class Mobil extends Kendaraan {
    private int jumlahPintu;
    
    public Mobil() {
        // super() dipanggil secara implisit jika tidak ada panggilan eksplisit
        System.out.println("Konstruktor default Mobil dipanggil");
        this.jumlahPintu = 4;
    }
    
    public Mobil(String merek, int tahun, int jumlahPintu) {
        super(merek, tahun); // Memanggil konstruktor superclass
        this.jumlahPintu = jumlahPintu;
        System.out.println("Konstruktor parameterized Mobil dipanggil");
    }
    
    public void tampilInfo() {
        System.out.println("Merek: " + merek);
        System.out.println("Tahun: " + tahun);
        System.out.println("Jumlah Pintu: " + jumlahPintu);
    }
}
```

Contoh penggunaan:
```java
System.out.println("--- Membuat Mobil dengan konstruktor default ---");
Mobil mobil1 = new Mobil();
mobil1.tampilInfo();

System.out.println("\n--- Membuat Mobil dengan konstruktor parameterized ---");
Mobil mobil2 = new Mobil("Toyota", 2022, 2);
mobil2.tampilInfo();
```

Output:
```
--- Membuat Mobil dengan konstruktor default ---
Konstruktor default Kendaraan dipanggil
Konstruktor default Mobil dipanggil
Merek: Tidak diketahui
Tahun: 2023
Jumlah Pintu: 4

--- Membuat Mobil dengan konstruktor parameterized ---
Konstruktor parameterized Kendaraan dipanggil
Konstruktor parameterized Mobil dipanggil
Merek: Toyota
Tahun: 2022
Jumlah Pintu: 2
```

Perhatikan beberapa hal penting:
- `super()` harus menjadi statement pertama dalam konstruktor subclass
- Jika tidak ada panggilan eksplisit ke `super()`, Java secara otomatis memanggil `super()` tanpa parameter
- Jika superclass tidak memiliki konstruktor tanpa parameter, maka subclass harus secara eksplisit memanggil salah satu konstruktor superclass yang tersedia

## Destruktor dan Garbage Collection

Tidak seperti beberapa bahasa pemrograman lain (seperti C++), Java tidak memiliki destruktor dalam arti tradisional. Java menggunakan Garbage Collection (GC) untuk mengelola memori dan menghapus objek yang tidak lagi direferensikan.

### Garbage Collection di Java

**Garbage Collection** adalah proses otomatis yang mengidentifikasi dan menghapus objek yang tidak lagi dapat dijangkau (unreachable) dalam program Java. Objek menjadi tidak dapat dijangkau ketika tidak ada referensi yang menunjuk kepadanya.

Cara kerja sederhana Garbage Collector:
1. Mengidentifikasi objek yang tidak lagi direferensikan
2. Membebaskan memori yang ditempati oleh objek tersebut
3. Menjadwalkan eksekusi metode `finalize()` (jika ada) sebelum objek benar-benar dihapus

Keuntungan Garbage Collection:
- Programmer tidak perlu secara manual menghapus objek
- Mencegah memory leaks (kebocoran memori)
- Mencegah dangling references (referensi menggantung)

Namun, programmer tidak memiliki kontrol langsung kapan Garbage Collection terjadi.

### Metode `finalize()`

Metode `finalize()` adalah metode yang diwariskan dari class `Object` dan dapat di-override oleh class lain. Metode ini dipanggil oleh Garbage Collector sebelum objek dihapus dari memori.

```java
public class FileResource {
    private String filename;
    private boolean isOpen;
    
    public FileResource(String filename) {
        this.filename = filename;
        this.isOpen = true;
        System.out.println("File " + filename + " dibuka");
    }
    
    public void processFile() {
        System.out.println("Memproses file " + filename);
    }
    
    public void closeFile() {
        if (isOpen) {
            isOpen = false;
            System.out.println("File " + filename + " ditutup secara manual");
        }
    }
    
    @Override
    protected void finalize() throws Throwable {
        try {
            if (isOpen) {
                System.out.println("WARNING: File " + filename + " ditutup oleh finalize()");
                closeFile();
            }
        } finally {
            super.finalize();
        }
    }
}
```

Contoh penggunaan:
```java
public static void main(String[] args) {
    // Skenario 1: Penutupan file secara manual
    FileResource file1 = new FileResource("data1.txt");
    file1.processFile();
    file1.closeFile();
    
    // Skenario 2: File tidak ditutup secara manual
    createAndForgetFile();
    
    // Memaksa Garbage Collection (tidak dijamin akan berjalan)
    System.gc();
    
    // Jeda untuk memberi waktu GC bekerja
    try {
        Thread.sleep(1000);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}

private static void createAndForgetFile() {
    FileResource file2 = new FileResource("data2.txt");
    file2.processFile();
    // File tidak ditutup secara manual
}
```

### Limitasi `finalize()`

Meskipun metode `finalize()` terlihat seperti destruktor, ada beberapa limitasi serius:

1. **Tidak Dijamin Dipanggil**: Garbage Collector tidak menjamin kapan (atau bahkan apakah) metode `finalize()` akan dipanggil
2. **Kinerja**: Mengandalkan `finalize()` untuk pembersihan sumber daya dapat memengaruhi kinerja
3. **Tidak Dapat Diprediksi**: Urutan pemanggilan `finalize()` untuk beberapa objek tidak dapat diprediksi
4. **Penundaan Pembersihan**: Objek yang menimpa `finalize()` memerlukan setidaknya dua siklus GC untuk dihapus sepenuhnya
5. **Deprecated**: Sejak Java 9, metode `finalize()` telah ditandai sebagai deprecated

Karena masalah di atas, metode `finalize()` tidak direkomendasikan untuk pembersihan sumber daya penting. Java menyediakan mekanisme alternatif yang lebih baik.

## Resource Management di Java Modern

Java modern menyediakan mekanisme yang lebih baik untuk mengelola sumber daya daripada mengandalkan `finalize()`.

### try-with-resources

Fitur `try-with-resources` yang diperkenalkan di Java 7 adalah cara yang lebih baik untuk memastikan sumber daya ditutup dengan benar, bahkan jika terjadi exception.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileExample {
    public static void main(String[] args) {
        // Menggunakan try-with-resources
        try (BufferedReader reader = new BufferedReader(new FileReader("data.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Error membaca file: " + e.getMessage());
        }
        // BufferedReader ditutup secara otomatis di sini, bahkan jika terjadi exception
    }
}
```

### Closeable Interface

Untuk class kustom yang mengelola sumber daya, implementasikan interface `Closeable` atau `AutoCloseable`.

```java
import java.io.Closeable;
import java.io.IOException;

public class DatabaseConnection implements Closeable {
    private String connectionString;
    private boolean isConnected;
    
    public DatabaseConnection(String connectionString) {
        this.connectionString = connectionString;
        this.isConnected = true;
        System.out.println("Koneksi database dibuka: " + connectionString);
    }
    
    public void executeQuery(String query) {
        if (isConnected) {
            System.out.println("Eksekusi query: " + query);
        } else {
            throw new IllegalStateException("Koneksi database sudah ditutup");
        }
    }
    
    @Override
    public void close() throws IOException {
        if (isConnected) {
            isConnected = false;
            System.out.println("Koneksi database ditutup: " + connectionString);
        }
    }
}
```

Contoh penggunaan:
```java
public static void main(String[] args) {
    try (DatabaseConnection db = new DatabaseConnection("jdbc:mysql://localhost:3306/mydb")) {
        db.executeQuery("SELECT * FROM users");
    } catch (IOException e) {
        System.err.println("Error saat menutup koneksi: " + e.getMessage());
    }
    // DatabaseConnection ditutup secara otomatis di sini
}
```

## Best Practices untuk Konstruktor

Berikut adalah beberapa best practices dalam membuat dan menggunakan konstruktor di Java:

1. **Berikan Default Constructor jika Diperlukan**: Jika Anda menambahkan konstruktor dengan parameter, tambahkan juga default constructor jika masih diperlukan.

2. **Gunakan Overloading secara Bijak**: Sediakan beberapa konstruktor dengan parameter yang berbeda untuk fleksibilitas pembuatan objek.

3. **Gunakan Constructor Chaining**: Kurangi duplikasi kode dengan memanggil konstruktor lain menggunakan `this()`.

4. **Validasi Parameter**: Lakukan validasi parameter di dalam konstruktor untuk memastikan objek dalam keadaan valid.

   ```java
   public Siswa(String nama, int umur) {
       if (nama == null || nama.trim().isEmpty()) {
           throw new IllegalArgumentException("Nama tidak boleh kosong");
       }
       if (umur <= 0) {
           throw new IllegalArgumentException("Umur harus positif");
       }
       this.nama = nama;
       this.umur = umur;
   }
   ```

5. **Jangan Panggil Method yang Dapat Di-override**: Dalam konstruktor, hindari memanggil method yang dapat di-override oleh subclass.

   ```java
   // JANGAN lakukan ini
   public class Parent {
       public Parent() {
           initialize(); // Berbahaya jika di-override
       }
       
       public void initialize() {
           // Inisialisasi
       }
   }
   
   // Subclass dapat meng-override initialize()
   public class Child extends Parent {
       private int value;
       
       public Child() {
           super();
       }
       
       @Override
       public void initialize() {
           value = 10 / 0; // Menyebabkan exception
       }
   }
   ```

6. **Buat Konstruktor Private untuk Singleton atau Utility Class**:

   ```java
   // Utility class dengan private constructor
   public class MathUtil {
       // Private constructor mencegah instantiasi
       private MathUtil() {
           throw new AssertionError("Utility class tidak boleh diinstansiasi");
       }
       
       public static int add(int a, int b) {
           return a + b;
       }
   }
   ```

7. **Gunakan Factory Method Alih-alih Konstruktor Langsung**: Untuk kasus yang kompleks, pertimbangkan menggunakan factory method.

   ```java
   public class Produk {
       private String nama;
       private double harga;
       
       private Produk(String nama, double harga) {
           this.nama = nama;
           this.harga = harga;
       }
       
       // Factory method
       public static Produk createProduk(String nama, double harga) {
           if (harga < 0) {
               throw new IllegalArgumentException("Harga tidak boleh negatif");
           }
           return new Produk(nama, harga);
       }
   }
   ```

8. **Gunakan Constructor yang Jelas dan Deskriptif**:

   ```java
   // KURANG BAIK: Parameter tidak jelas
   Employee emp = new Employee("John", "Doe", 5000, true, 30);
   
   // LEBIH BAIK: Menggunakan Builder Pattern
   Employee emp = new Employee.Builder()
       .firstName("John")
       .lastName("Doe")
       .salary(5000)
       .isFullTime(true)
       .age(30)
       .build();
   ```

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep konstruktor dan manajemen sumber daya dengan membuat program sederhana menggunakan NetBeans IDE.

### Skenario: Sistem Manajemen Pesanan

Kita akan membuat sistem manajemen pesanan sederhana dengan beberapa kelas yang menunjukkan penggunaan berbagai jenis konstruktor, constructor chaining, dan resource management.

### Langkah 1: Buat Project Baru

1. Buka NetBeans IDE
2. Pilih **File** > **New Project**
3. Pilih **Java** > **Java Application** > **Next**
4. Beri nama project "SistemPesanan" dan tentukan lokasi penyimpanan
5. Klik **Finish**

### Langkah 2: Buat Kelas Produk

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Produk"
3. Isi dengan kode berikut:

```java
package sistempesanan;

public class Produk {
    private String kode;
    private String nama;
    private double harga;
    private int stok;
    
    // Default constructor
    public Produk() {
        this("XXXX", "Produk Baru", 0, 0);
    }
    
    // Parameterized constructor dengan 2 parameter
    public Produk(String kode, String nama) {
        this(kode, nama, 0, 0);
    }
    
    // Parameterized constructor dengan 3 parameter
    public Produk(String kode, String nama, double harga) {
        this(kode, nama, harga, 0);
    }
    
    // Parameterized constructor dengan 4 parameter (complete)
    public Produk(String kode, String nama, double harga, int stok) {
        // Validasi input
        if (kode == null || kode.trim().isEmpty()) {
            throw new IllegalArgumentException("Kode produk tidak boleh kosong");
        }
        if (nama == null || nama.trim().isEmpty()) {
            throw new IllegalArgumentException("Nama produk tidak boleh kosong");
        }
        if (harga < 0) {
            throw new IllegalArgumentException("Harga tidak boleh negatif");
        }
        if (stok < 0) {
            throw new IllegalArgumentException("Stok tidak boleh negatif");
        }
        
        this.kode = kode;
        this.nama = nama;
        this.harga = harga;
        this.stok = stok;
    }
    
    // Copy constructor
    public Produk(Produk produkLain) {
        this(produkLain.kode, produkLain.nama, produkLain.harga, produkLain.stok);
    }
    
    // Getter and Setter methods
    public String getKode() {
        return kode;
    }
    
    public String getNama() {
        return nama;
    }
    
    public void setNama(String nama) {
        if (nama == null || nama.trim().isEmpty()) {
            throw new IllegalArgumentException("Nama produk tidak boleh kosong");
        }
        this.nama = nama;
    }
    
    public double getHarga() {
        return harga;
    }
    
    public void setHarga(double harga) {
        if (harga < 0) {
            throw new IllegalArgumentException("Harga tidak boleh negatif");
        }
        this.harga = harga;
    }
    
    public int getStok() {
        return stok;
    }
    
    public void setStok(int stok) {
        if (stok < 0) {
            throw new IllegalArgumentException("Stok tidak boleh negatif");
        }
        this.stok = stok;
    }
    
    // Method untuk menambah stok
    public void tambahStok(int jumlah) {
        if (jumlah <= 0) {
            throw new IllegalArgumentException("Jumlah penambahan harus positif");
        }
        this.stok += jumlah;
    }
    
    // Method untuk mengurangi stok
    public boolean kurangiStok(int jumlah) {
        if (jumlah <= 0) {
            throw new IllegalArgumentException("Jumlah pengurangan harus positif");
        }
        if (stok >= jumlah) {
            stok -= jumlah;
            return true;
        }
        return false;
    }
    
    // Method untuk mendapatkan info produk
    public String getInfo() {
        return String.format("Produk [kode=%s, nama=%s, harga=%.2f, stok=%d]", 
                            kode, nama, harga, stok);
    }
    
    @Override
    public String toString() {
        return getInfo();
    }
}
```

### Langkah 3: Buat Kelas DetailPesanan

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "DetailPesanan"
3. Isi dengan kode berikut:

```java
package sistempesanan;

public class DetailPesanan {
    private Produk produk;
    private int jumlah;
    private double subTotal;
    
    // Constructor dengan produk dan jumlah
    public DetailPesanan(Produk produk, int jumlah) {
        if (produk == null) {
            throw new IllegalArgumentException("Produk tidak boleh null");
        }
        if (jumlah <= 0) {
            throw new IllegalArgumentException("Jumlah harus positif");
        }
        
        this.produk = new Produk(produk); // Menggunakan copy constructor
        this.jumlah = jumlah;
        this.subTotal = hitungSubTotal();
    }
    
    // Private method untuk menghitung subtotal
    private double hitungSubTotal() {
        return produk.getHarga() * jumlah;
    }
    
    // Getter methods
    public Produk getProduk() {
        return produk;
    }
    
    public int getJumlah() {
        return jumlah;
    }
    
    public double getSubTotal() {
        return subTotal;
    }
    
    // Method untuk mendapatkan info detail pesanan
    public String getInfo() {
        return String.format("%s - %d x Rp%.2f = Rp%.2f", 
                            produk.getNama(), jumlah, produk.getHarga(), subTotal);
    }
    
    @Override
    public String toString() {
        return getInfo();
    }
}
```

### Langkah 4: Buat Kelas Pesanan

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Pesanan"
3. Isi dengan kode berikut:

```java
package sistempesanan;

import java.io.Closeable;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

public class Pesanan implements Closeable {
    private static int counter = 0;
    
    private String nomorPesanan;
    private Date tanggalPesanan;
    private String namaPelanggan;
    private List<DetailPesanan> daftarItem;
    private double totalPesanan;
    private boolean isProcessed;
    
    // Static block untuk inisialisasi counter
    static {
        counter = 1000;
    }
    
    // Default constructor
    public Pesanan() {
        this("Pelanggan");
    }
    
    // Constructor dengan nama pelanggan
    public Pesanan(String namaPelanggan) {
        this.nomorPesanan = generateNomorPesanan();
        this.tanggalPesanan = new Date();
        this.namaPelanggan = namaPelanggan;
        this.daftarItem = new ArrayList<>();
        this.totalPesanan = 0;
        this.isProcessed = false;
        System.out.println("Pesanan dibuat: " + nomorPesanan);
    }
    
    // Private method untuk generate nomor pesanan
    private String generateNomorPesanan() {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMdd");
        return "ORD-" + sdf.format(new Date()) + "-" + (++counter);
    }
    
    // Method untuk menambah item pesanan
    public void tambahItem(Produk produk, int jumlah) {
        if (isProcessed) {
            throw new IllegalStateException("Pesanan sudah diproses, tidak dapat menambah item");
        }
        
        if (produk.getStok() < jumlah) {
            throw new IllegalArgumentException("Stok tidak mencukupi");
        }
        
        DetailPesanan item = new DetailPesanan(produk, jumlah);
        produk.kurangiStok(jumlah);
        daftarItem.add(item);
        totalPesanan += item.getSubTotal();
    }
    
    // Method untuk menampilkan pesanan
    public void tampilkanPesanan() {
        System.out.println("=== DETAIL PESANAN ===");
        System.out.println("Nomor Pesanan: " + nomorPesanan);
        System.out.println("Tanggal: " + tanggalPesanan);
        System.out.println("Pelanggan: " + namaPelanggan);
        System.out.println("------------------------------");
        
        for (int i = 0; i < daftarItem.size(); i++) {
            System.out.println((i + 1) + ". " + daftarItem.get(i).getInfo());
        }
        
        System.out.println("------------------------------");
        System.out.println("Total: Rp" + String.format("%.2f", totalPesanan));
        System.out.println("Status: " + (isProcessed ? "Sudah diproses" : "Belum diproses"));
    }
    
    // Method untuk memproses pesanan
    public void prosesPesanan() {
        if (daftarItem.isEmpty()) {
            throw new IllegalStateException("Pesanan kosong, tidak dapat diproses");
        }
        
        if (!isProcessed) {
            isProcessed = true;
            System.out.println("Pesanan " + nomorPesanan + " telah diproses");
        } else {
            System.out.println("Pesanan " + nomorPesanan + " sudah diproses sebelumnya");
        }
    }
    
    // Implementasi method close() dari interface Closeable
    @Override
    public void close() throws IOException {
        if (!isProcessed) {
            System.out.println("WARNING: Pesanan " + nomorPesanan + " ditutup tanpa diproses");
            isProcessed = true;
        }
        System.out.println("Pesanan " + nomorPesanan + " ditutup");
    }
    
    // Method finalize yang deprecated (contoh saja)
    @Override
    protected void finalize() throws Throwable {
        try {
            if (!isProcessed) {
                System.out.println("WARNING: Pesanan " + nomorPesanan + " dihapus tanpa diproses");
            }
        } finally {
            super.finalize();
        }
    }
    
    // Getter methods
    public String getNomorPesanan() {
        return nomorPesanan;
    }
    
    public Date getTanggalPesanan() {
        return tanggalPesanan;
    }
    
    public String getNamaPelanggan() {
        return namaPelanggan;
    }
    
    public double getTotalPesanan() {
        return totalPesanan;
    }
    
    public boolean isProcessed() {
        return isProcessed;
    }
}
```

### Langkah 5: Buat Kelas Main

1. Buka file main (biasanya `SistemPesanan.java`)
2. Ubah kode menjadi:

```java
package sistempesanan;

public class SistemPesanan {
    public static void main(String[] args) {
        // Membuat produk dengan berbagai konstruktor
        System.out.println("=== PEMBUATAN PRODUK ===");
        Produk produk1 = new Produk("P001", "Laptop Asus", 12000000, 5);
        Produk produk2 = new Produk("P002", "Mouse Logitech", 350000, 10);
        Produk produk3 = new Produk("P003", "Keyboard Mechanical");
        produk3.setHarga(750000);
        produk3.setStok(7);
        
        Produk produk4 = new Produk(); // Default constructor
        produk4.setKode("P004");
        produk4.setNama("Headset Gaming");
        produk4.setHarga(500000);
        produk4.setStok(8);
        
        Produk produk5 = new Produk(produk1); // Copy constructor
        produk5.setKode("P005");
        produk5.setNama("Laptop HP");
        
        // Menampilkan info produk
        System.out.println(produk1.getInfo());
        System.out.println(produk2.getInfo());
        System.out.println(produk3.getInfo());
        System.out.println(produk4.getInfo());
        System.out.println(produk5.getInfo());
        
        System.out.println("\n=== PEMBUATAN PESANAN ===");
        
        // Menggunakan try-with-resources untuk pesanan
        try (Pesanan pesanan1 = new Pesanan("John Doe")) {
            pesanan1.tambahItem(produk1, 1);
            pesanan1.tambahItem(produk2, 2);
            pesanan1.tambahItem(produk3, 1);
            
            pesanan1.tampilkanPesanan();
            pesanan1.prosesPesanan();
            
        } catch (Exception e) {
            System.err.println("Error pada pesanan: " + e.getMessage());
        }
        
        System.out.println("\n=== PESANAN TANPA CLOSE EKSPLISIT ===");
        createAndForgetOrder(produk4, produk5);
        
        System.out.println("\n=== STOK SETELAH PEMESANAN ===");
        System.out.println(produk1.getInfo());
        System.out.println(produk2.getInfo());
        System.out.println(produk3.getInfo());
        System.out.println(produk4.getInfo());
        System.out.println(produk5.getInfo());
    }
    
    private static void createAndForgetOrder(Produk p1, Produk p2) {
        Pesanan pesanan2 = new Pesanan("Jane Smith");
        pesanan2.tambahItem(p1, 1);
        pesanan2.tambahItem(p2, 1);
        pesanan2.tampilkanPesanan();
        // Pesanan tidak diproses dan tidak ditutup secara eksplisit
    }
}
```

### Langkah 6: Jalankan Program

1. Klik **Run** > **Run Project**
2. Atau tekan tombol F6

### Penjelasan

Dalam contoh praktik di atas, kita telah mengimplementasikan:

1. **Berbagai Jenis Konstruktor**:
   - Default constructor di kelas `Produk`
   - Parameterized constructor dengan beberapa parameter di kelas `Produk`
   - Copy constructor di kelas `Produk`

2. **Constructor Chaining**:
   - `this()` untuk memanggil konstruktor lain dalam kelas yang sama (di kelas `Produk`)

3. **Validasi Parameter**:
   - Validasi input pada konstruktor untuk memastikan objek dalam keadaan valid (di kelas `Produk` dan `DetailPesanan`)

4. **Resource Management Modern**:
   - Implementasi interface `Closeable` di kelas `Pesanan`
   - Penggunaan try-with-resources untuk memastikan pesanan ditutup dengan benar

5. **Metode `finalize()` (untuk ilustrasi)**:
   - Override metode `finalize()` untuk menunjukkan limitasinya (di kelas `Pesanan`)

Program menunjukkan siklus hidup objek dari pembuatan (melalui konstruktor) hingga penghapusan (melalui `close()` atau garbage collection). Penggunaan try-with-resources menunjukkan pendekatan modern untuk manajemen sumber daya di Java.

## Rangkuman

Dalam bab ini, kita telah mempelajari:

1. **Konstruktor di Java**:
   - Metode khusus yang dipanggil saat objek dibuat
   - Digunakan untuk menginisialisasi objek
   - Berbagai jenis: default, parameterized, dan copy constructor

2. **Constructor Overloading**:
   - Mendefinisikan beberapa konstruktor dengan parameter berbeda
   - Meningkatkan fleksibilitas pembuatan objek

3. **Constructor Chaining**:
   - Menggunakan `this()` untuk memanggil konstruktor lain dalam kelas yang sama
   - Menggunakan `super()` untuk memanggil konstruktor superclass
   - Mengurangi duplikasi kode

4. **Destruktor dan Garbage Collection**:
   - Java menggunakan Garbage Collection untuk mengelola memori secara otomatis
   - Metode `finalize()` sebagai alternatif destruktor (tetapi memiliki limitasi serius)
   - Tidak mengandalkan `finalize()` untuk pembersihan sumber daya penting

5. **Resource Management Modern**:
   - try-with-resources untuk otomatisasi pembersihan sumber daya
   - Interface `Closeable` dan `AutoCloseable` untuk pengelolaan sumber daya kustom

6. **Best Practices**:
   - Validasi parameter di konstruktor
   - Gunakan constructor chaining
   - Hindari memanggil method yang dapat di-override dalam konstruktor
   - Gunakan resource management modern alih-alih `finalize()`

Memahami konstruktor dan cara Java mengelola penghapusan objek sangat penting untuk membuat program Java yang efisien, aman, dan robust. Dengan menerapkan best practices yang telah kita pelajari, Anda dapat membuat objek yang selalu dalam keadaan valid dan mengelola sumber daya dengan benar.

## Latihan Soal

1. Jelaskan perbedaan antara default constructor dan parameterized constructor. Kapan masing-masing digunakan?

2. Apa yang terjadi jika Anda tidak menyediakan default constructor dalam sebuah class yang memiliki parameterized constructor?

3. Jelaskan konsep "constructor chaining" dan bagaimana implementasinya dalam Java.

4. Apa perbedaan antara `this()` dan `super()` dalam konteks constructor chaining?

5. Mengapa Java tidak memiliki destruktor seperti di bahasa pemrograman C++? Bagaimana Java menangani penghapusan objek?

6. Sebutkan limitasi utama metode `finalize()` dan mengapa tidak direkomendasikan untuk pembersihan sumber daya.

7. Jelaskan bagaimana try-with-resources bekerja dan keuntungannya dibandingkan dengan try-catch-finally tradisional.

8. Implementasikan sebuah class `Circle` dengan:
   - Atribut private `radius` (double)
   - Konstruktor default yang menetapkan radius ke 1.0
   - Konstruktor dengan parameter radius
   - Copy constructor
   - Method untuk menghitung luas dan keliling lingkaran

9. Perhatikan code berikut dan identifikasi masalah yang mungkin terjadi:
   ```java
   public class Parent {
       private int value;
       
       public Parent() {
           initialize();
       }
       
       public void initialize() {
           value = 10;
       }
   }
   
   public class Child extends Parent {
       private int childValue;
       
       @Override
       public void initialize() {
           childValue = 5;
           super.initialize();
       }
   }
   ```

10. Bagaimana Anda mengimplementasikan resource management yang baik untuk sebuah class yang mengelola sumber daya eksternal seperti koneksi database atau file?

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional.

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall.

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional.

5. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall.

6. Oracle. (2023). *Java Language Specification: Object Creation and Initialization*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-12.html#jls-12.5](https://docs.oracle.com/javase/specs/jls/se17/html/jls-12.html#jls-12.5)

7. Oracle. (2023). *Java Tutorial: Constructors*. [https://docs.oracle.com/javase/tutorial/java/javaOO/constructors.html](https://docs.oracle.com/javase/tutorial/java/javaOO/constructors.html)

8. Oracle. (2023). *Java Tutorial: The try-with-resources Statement*. [https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html)

9. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education.

10. Oracle. (2023). *Garbage Collection in Java*. [https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)

---

[◀️ Kembali ke Tutorial #03: Tingkat Akses Member dan Class (Modifier)](03-access-modifiers.md) | [Lanjut ke Tutorial #05: Menggunakan Method Setter dan Getter ▶️](05-setters-getters.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
