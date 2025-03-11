# 📘 Tutorial Java OOP #01: Memahami Konsep Dasar OOP pada Java

> *"Objek adalah segala-galanya, dan segala-galanya adalah objek."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami perbedaan antara pemrograman prosedural dan berorientasi objek
- Menjelaskan konsep dasar objek dan kelas dalam Java
- Memahami empat pilar utama OOP: Enkapsulasi, Inheritance, Polimorfisme, dan Abstraksi
- Membuat program Java sederhana menggunakan pendekatan OOP

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Paradigma Pemrograman: Prosedural vs OOP](#paradigma-pemrograman-prosedural-vs-oop)
3. [Konsep Objek dan Kelas](#konsep-objek-dan-kelas)
4. [Empat Pilar OOP](#empat-pilar-oop)
5. [Implementasi OOP di Java](#implementasi-oop-di-java)
6. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
7. [Rangkuman](#rangkuman)
8. [Latihan Soal](#latihan-soal)

## Pendahuluan

Selamat datang di dunia pemrograman berorientasi objek (Object-Oriented Programming atau OOP)! 🎉

Java adalah salah satu bahasa pemrograman yang dirancang dengan paradigma OOP sejak awal. Memahami OOP tidak hanya akan membantu Anda menguasai Java, tetapi juga memudahkan Anda mempelajari bahasa pemrograman modern lainnya seperti C++, C#, Python, dan banyak lagi.

OOP bukanlah sekedar fitur tambahan dalam Java — ini adalah fondasi cara berpikir dan memecahkan masalah. Mari kita mulai perjalanan kita dalam memahami konsep yang menarik ini!

## Paradigma Pemrograman: Prosedural vs OOP

Sebelum kita membahas OOP secara mendalam, mari kita bandingkan dengan paradigma pemrograman prosedural yang mungkin sudah Anda kenal.

### Pemrograman Prosedural

Dalam pemrograman prosedural, program dipecah menjadi prosedur atau fungsi-fungsi kecil yang mengolah data. Data dan fungsi terpisah — data global dapat diakses dan dimodifikasi oleh fungsi mana pun.

**Contoh kode prosedural untuk menghitung luas persegi:**

```java
public class HitungLuas {
    public static void main(String[] args) {
        // Data
        double panjang = 5.0;
        double lebar = 3.0;
        
        // Fungsi untuk menghitung luas
        double luas = hitungLuasPersegiPanjang(panjang, lebar);
        
        System.out.println("Luas persegi panjang: " + luas);
    }
    
    public static double hitungLuasPersegiPanjang(double p, double l) {
        return p * l;
    }
}
```

Karakteristik pemrograman prosedural:
- Fokus pada fungsi dan prosedur
- Data terpisah dari fungsi
- Eksekusi berjalan secara linear (step-by-step)
- Modifikasi dan pemeliharaan program dapat menjadi rumit seiring bertambahnya ukuran program

### Pemrograman Berorientasi Objek (OOP)

OOP, sebaliknya, berfokus pada objek yang merupakan kombinasi dari data (atribut) dan fungsi (metode). Program dibuat dengan cara mendefinisikan kelas-kelas (blueprint) dan kemudian menciptakan objek-objek berdasarkan kelas tersebut.

**Contoh kode OOP untuk menghitung luas persegi:**

```java
public class PersegiPanjang {
    // Atribut (data)
    private double panjang;
    private double lebar;
    
    // Constructor
    public PersegiPanjang(double panjang, double lebar) {
        this.panjang = panjang;
        this.lebar = lebar;
    }
    
    // Metode (fungsi)
    public double hitungLuas() {
        return panjang * lebar;
    }
}

public class Main {
    public static void main(String[] args) {
        // Membuat objek dari kelas PersegiPanjang
        PersegiPanjang pp = new PersegiPanjang(5.0, 3.0);
        
        // Memanggil metode pada objek
        double luas = pp.hitungLuas();
        
        System.out.println("Luas persegi panjang: " + luas);
    }
}
```

Karakteristik OOP:
- Fokus pada objek yang menggabungkan data dan metode
- Enkapsulasi data (penyembunyian data)
- Kemudahan dalam memelihara dan memperluas program
- Pendekatan yang lebih mirip dengan cara dunia nyata bekerja

## Konsep Objek dan Kelas

### Kelas (Class)

**Kelas** adalah blueprint atau template untuk membuat objek. Kelas mendefinisikan:
- Atribut (variabel): karakteristik atau properti
- Metode (fungsi): perilaku atau kemampuan

Analoginya, jika kita membayangkan kue, maka kelas adalah resep kue tersebut. Resep menjelaskan bahan-bahan (atribut) dan langkah-langkah pembuatan (metode), tetapi bukan kue itu sendiri.

Contoh pendefinisian kelas di Java:

```java
public class Mobil {
    // Atribut
    private String merek;
    private String model;
    private int tahun;
    private double kecepatan;
    
    // Constructor
    public Mobil(String merek, String model, int tahun) {
        this.merek = merek;
        this.model = model;
        this.tahun = tahun;
        this.kecepatan = 0.0;
    }
    
    // Metode
    public void percepat(double nilaiPercepatan) {
        kecepatan += nilaiPercepatan;
        System.out.println("Mobil dipercepat menjadi " + kecepatan + " km/jam");
    }
    
    public void rem(double nilaiPerlambatan) {
        kecepatan -= nilaiPerlambatan;
        if (kecepatan < 0) {
            kecepatan = 0;
        }
        System.out.println("Mobil diperlambat menjadi " + kecepatan + " km/jam");
    }
    
    public void tampilkanInfo() {
        System.out.println("Mobil " + merek + " " + model + " (" + tahun + ")");
        System.out.println("Kecepatan saat ini: " + kecepatan + " km/jam");
    }
}
```

### Objek (Object)

**Objek** adalah instance konkret dari sebuah kelas. Jika kelas adalah resep, maka objek adalah kue yang sudah jadi berdasarkan resep tersebut. Anda bisa membuat banyak kue (objek) dari satu resep (kelas) yang sama.

Objek memiliki:
- **State**: nilai dari atribut-atributnya pada saat tertentu
- **Behavior**: apa yang dapat dilakukan objek (metode)
- **Identity**: identitas unik dalam program

Contoh pembuatan objek dari kelas Mobil:

```java
public class DemoMobil {
    public static void main(String[] args) {
        // Membuat objek mobil1
        Mobil mobil1 = new Mobil("Toyota", "Avanza", 2020);
        
        // Membuat objek mobil2
        Mobil mobil2 = new Mobil("Honda", "Jazz", 2021);
        
        // Menggunakan metode pada objek mobil1
        mobil1.tampilkanInfo();
        mobil1.percepat(20);
        mobil1.percepat(30);
        mobil1.rem(10);
        mobil1.tampilkanInfo();
        
        System.out.println("\n-----------------------\n");
        
        // Menggunakan metode pada objek mobil2
        mobil2.tampilkanInfo();
        mobil2.percepat(50);
        mobil2.rem(20);
        mobil2.tampilkanInfo();
    }
}
```

Output:
```
Mobil Toyota Avanza (2020)
Kecepatan saat ini: 0.0 km/jam
Mobil dipercepat menjadi 20.0 km/jam
Mobil dipercepat menjadi 50.0 km/jam
Mobil diperlambat menjadi 40.0 km/jam
Mobil Toyota Avanza (2020)
Kecepatan saat ini: 40.0 km/jam

-----------------------

Mobil Honda Jazz (2021)
Kecepatan saat ini: 0.0 km/jam
Mobil dipercepat menjadi 50.0 km/jam
Mobil diperlambat menjadi 30.0 km/jam
Mobil Honda Jazz (2021)
Kecepatan saat ini: 30.0 km/jam
```

## Empat Pilar OOP

OOP dibangun di atas empat konsep fondasi yang sering disebut sebagai "Empat Pilar OOP":

### 1. Enkapsulasi (Encapsulation)

**Enkapsulasi** adalah konsep menyembunyikan detail implementasi dan hanya mengekspos fungsionalitas yang dibutuhkan. Ini seperti kotak hitam yang Anda tahu cara menggunakannya tanpa perlu tahu bagaimana cara kerjanya.

Manfaat enkapsulasi:
- Melindungi data dari akses tidak sah
- Memudahkan pemeliharaan kode
- Mengurangi kompleksitas

Contoh enkapsulasi di Java dengan access modifier:

```java
public class RekeningBank {
    // Data yang dienkapsulasi (private)
    private String nomorRekening;
    private String namaPemilik;
    private double saldo;
    
    // Constructor
    public RekeningBank(String nomorRekening, String namaPemilik) {
        this.nomorRekening = nomorRekening;
        this.namaPemilik = namaPemilik;
        this.saldo = 0.0;
    }
    
    // Metode untuk mengakses dan memodifikasi data private
    public void setor(double jumlah) {
        if (jumlah > 0) {
            saldo += jumlah;
            System.out.println("Setoran berhasil. Saldo sekarang: " + saldo);
        } else {
            System.out.println("Jumlah setoran harus positif");
        }
    }
    
    public void tarik(double jumlah) {
        if (jumlah > 0) {
            if (saldo >= jumlah) {
                saldo -= jumlah;
                System.out.println("Penarikan berhasil. Saldo sekarang: " + saldo);
            } else {
                System.out.println("Saldo tidak mencukupi");
            }
        } else {
            System.out.println("Jumlah penarikan harus positif");
        }
    }
    
    public double getSaldo() {
        return saldo;
    }
    
    public String getInfoRekening() {
        return "Rekening " + nomorRekening + " atas nama " + namaPemilik;
    }
}
```

Dalam contoh di atas, atribut `nomorRekening`, `namaPemilik`, dan `saldo` dienkapsulasi dengan modifier `private`. Akses ke data ini hanya melalui metode publik (`setor`, `tarik`, `getSaldo`, `getInfoRekening`).

### 2. Inheritance (Pewarisan)

**Inheritance** memungkinkan sebuah kelas (subclass) mewarisi atribut dan metode dari kelas lain (superclass). Ini menciptakan hubungan "is-a" (adalah) antara kelas.

Manfaat inheritance:
- Mendorong penggunaan ulang kode
- Memungkinkan hierarki kelas yang natural
- Meningkatkan modularitas

Contoh inheritance di Java:

```java
// Superclass
public class Kendaraan {
    protected String merek;
    protected int tahun;
    
    public Kendaraan(String merek, int tahun) {
        this.merek = merek;
        this.tahun = tahun;
    }
    
    public void tampilkanInfo() {
        System.out.println("Kendaraan merek " + merek + " tahun " + tahun);
    }
    
    public void bergerak() {
        System.out.println("Kendaraan bergerak");
    }
}

// Subclass
public class Mobil extends Kendaraan {
    private int jumlahPintu;
    
    public Mobil(String merek, int tahun, int jumlahPintu) {
        super(merek, tahun); // Memanggil constructor superclass
        this.jumlahPintu = jumlahPintu;
    }
    
    // Override metode dari superclass
    @Override
    public void tampilkanInfo() {
        System.out.println("Mobil merek " + merek + " tahun " + tahun);
        System.out.println("Jumlah pintu: " + jumlahPintu);
    }
    
    // Metode tambahan spesifik untuk Mobil
    public void klakson() {
        System.out.println("Beep! Beep!");
    }
}
```

Dalam contoh di atas, `Mobil` mewarisi atribut dan metode dari `Kendaraan`, serta menambahkan atribut dan metode spesifik untuk mobil. `Mobil` juga meng-override metode `tampilkanInfo()` untuk memberikan informasi yang lebih spesifik.

### 3. Polimorfisme (Polymorphism)

**Polimorfisme** memungkinkan objek dari kelas yang berbeda merespons metode yang sama dengan cara berbeda. Ada dua jenis polimorfisme:
- **Compile-time polymorphism** (method overloading)
- **Runtime polymorphism** (method overriding)

Manfaat polimorfisme:
- Fleksibilitas dalam penggunaan kode
- Simplifikasi desain program
- Memudahkan perluasan

Contoh polimorfisme di Java:

```java
// Superclass
public class Bentuk {
    public void gambar() {
        System.out.println("Menggambar bentuk");
    }
    
    public double hitungLuas() {
        return 0.0; // Implementasi default
    }
}

// Subclass 1
public class Lingkaran extends Bentuk {
    private double jariJari;
    
    public Lingkaran(double jariJari) {
        this.jariJari = jariJari;
    }
    
    @Override
    public void gambar() {
        System.out.println("Menggambar lingkaran");
    }
    
    @Override
    public double hitungLuas() {
        return Math.PI * jariJari * jariJari;
    }
}

// Subclass 2
public class PersegiPanjang extends Bentuk {
    private double panjang;
    private double lebar;
    
    public PersegiPanjang(double panjang, double lebar) {
        this.panjang = panjang;
        this.lebar = lebar;
    }
    
    @Override
    public void gambar() {
        System.out.println("Menggambar persegi panjang");
    }
    
    @Override
    public double hitungLuas() {
        return panjang * lebar;
    }
}
```

Contoh penggunaan polimorfisme:

```java
public class DemoBentuk {
    public static void main(String[] args) {
        // Array of Bentuk yang berisi objek dari berbagai subclass
        Bentuk[] bentukArray = new Bentuk[3];
        bentukArray[0] = new Bentuk();
        bentukArray[1] = new Lingkaran(5.0);
        bentukArray[2] = new PersegiPanjang(4.0, 6.0);
        
        // Memanggil metode yang sama pada objek berbeda
        for (Bentuk bentuk : bentukArray) {
            bentuk.gambar();
            System.out.println("Luas: " + bentuk.hitungLuas());
            System.out.println();
        }
    }
}
```

Output:
```
Menggambar bentuk
Luas: 0.0

Menggambar lingkaran
Luas: 78.53981633974483

Menggambar persegi panjang
Luas: 24.0
```

### 4. Abstraksi (Abstraction)

**Abstraksi** adalah konsep menyembunyikan kompleksitas implementasi dan hanya menampilkan fungsionalitas esensial kepada pengguna. Abstraksi membantu kita fokus pada "apa" yang dilakukan objek, bukan "bagaimana" melakukannya.

Manfaat abstraksi:
- Menyederhanakan model pemrograman
- Mengurangi kompleksitas kode
- Memudahkan perubahan implementasi

Java mendukung abstraksi melalui:
- Interface
- Abstract class

Contoh abstraksi dengan abstract class:

```java
// Abstract class
public abstract class Hewan {
    protected String nama;
    
    public Hewan(String nama) {
        this.nama = nama;
    }
    
    // Abstract method (tidak memiliki implementasi)
    public abstract void bersuara();
    
    // Concrete method (memiliki implementasi)
    public void tidur() {
        System.out.println(nama + " sedang tidur");
    }
}

// Implementasi abstract class
public class Kucing extends Hewan {
    public Kucing(String nama) {
        super(nama);
    }
    
    @Override
    public void bersuara() {
        System.out.println(nama + " bersuara: Meow!");
    }
}

public class Anjing extends Hewan {
    public Anjing(String nama) {
        super(nama);
    }
    
    @Override
    public void bersuara() {
        System.out.println(nama + " bersuara: Woof!");
    }
}
```

Contoh penggunaan abstraksi:

```java
public class DemoHewan {
    public static void main(String[] args) {
        // Hewan hewan = new Hewan("Binatang"); // Error: tidak bisa instantiate abstract class
        
        Kucing kucing = new Kucing("Kitty");
        Anjing anjing = new Anjing("Doggy");
        
        kucing.bersuara();
        kucing.tidur();
        
        anjing.bersuara();
        anjing.tidur();
    }
}
```

Output:
```
Kitty bersuara: Meow!
Kitty sedang tidur
Doggy bersuara: Woof!
Doggy sedang tidur
```

## Implementasi OOP di Java

Java adalah bahasa pemrograman yang dirancang dengan pemikiran OOP dari awal. Beberapa implementasi OOP yang umum di Java:

1. **Class dan Object**: Semua kode Java ditulis dalam class, dan program Java berjalan berdasarkan objek
2. **Access Modifiers**: `private`, `protected`, `public`, dan default (no modifier) untuk mengontrol akses
3. **Packages**: Untuk mengorganisir class yang berkaitan
4. **Interface**: Contract yang harus diimplementasikan oleh class
5. **Abstract Class**: Class yang tidak dapat diinstansiasi langsung
6. **Extending dan Implementing**: Untuk mewarisi dan mengimplementasikan behavior

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep OOP dengan membuat program sederhana menggunakan NetBeans IDE.

### Langkah 1: Buat Project Baru

1. Buka NetBeans IDE
2. Pilih **File** > **New Project**
3. Pilih **Java** > **Java Application** > **Next**
4. Beri nama project "BelajarOOP" dan tentukan lokasi penyimpanan
5. Klik **Finish**

### Langkah 2: Buat Kelas Mahasiswa

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Mahasiswa"
3. Isi dengan kode berikut:

```java
package belajaroop;

public class Mahasiswa {
    // Atribut
    private String nim;
    private String nama;
    private String jurusan;
    private double ipk;
    
    // Constructor
    public Mahasiswa(String nim, String nama, String jurusan) {
        this.nim = nim;
        this.nama = nama;
        this.jurusan = jurusan;
        this.ipk = 0.0;
    }
    
    // Method untuk mengubah IPK
    public void setIPK(double ipk) {
        if (ipk >= 0 && ipk <= 4.0) {
            this.ipk = ipk;
        } else {
            System.out.println("IPK harus berada di antara 0 - 4.0");
        }
    }
    
    // Method untuk mendapatkan status akademik
    public String getStatusAkademik() {
        if (ipk >= 3.5) {
            return "Cumlaude";
        } else if (ipk >= 3.0) {
            return "Sangat Memuaskan";
        } else if (ipk >= 2.5) {
            return "Memuaskan";
        } else if (ipk >= 2.0) {
            return "Cukup";
        } else {
            return "Perlu Bimbingan";
        }
    }
    
    // Method untuk menampilkan info mahasiswa
    public void tampilkanInfo() {
        System.out.println("NIM: " + nim);
        System.out.println("Nama: " + nama);
        System.out.println("Jurusan: " + jurusan);
        System.out.println("IPK: " + ipk);
        System.out.println("Status: " + getStatusAkademik());
    }
    
    // Getter methods
    public String getNim() {
        return nim;
    }
    
    public String getNama() {
        return nama;
    }
    
    public String getJurusan() {
        return jurusan;
    }
    
    public double getIpk() {
        return ipk;
    }
}
```

### Langkah 3: Buat Kelas Utama

1. Buka file `BelajarOOP.java` (atau nama file utama yang dibuat otomatis)
2. Ubah kode menjadi:

```java
package belajaroop;

public class BelajarOOP {
    public static void main(String[] args) {
        // Membuat objek mahasiswa
        Mahasiswa mhs1 = new Mahasiswa("A12345", "Budi Santoso", "Teknik Informatika");
        Mahasiswa mhs2 = new Mahasiswa("B67890", "Ani Wijaya", "Sistem Informasi");
        
        // Mengatur IPK
        mhs1.setIPK(3.7);
        mhs2.setIPK(2.9);
        
        // Menampilkan informasi mahasiswa
        System.out.println("=== Informasi Mahasiswa 1 ===");
        mhs1.tampilkanInfo();
        
        System.out.println("\n=== Informasi Mahasiswa 2 ===");
        mhs2.tampilkanInfo();
    }
}
```

### Langkah 4: Jalankan Program

1. Klik **Run** > **Run Project**
2. Atau tekan tombol F6

Output:
```
=== Informasi Mahasiswa 1 ===
NIM: A12345
Nama: Budi Santoso
Jurusan: Teknik Informatika
IPK: 3.7
Status: Cumlaude

=== Informasi Mahasiswa 2 ===
NIM: B67890
Nama: Ani Wijaya
Jurusan: Sistem Informasi
IPK: 2.9
Status: Memuaskan
```

### Penjelasan

Dalam contoh praktik di atas:

1. Kita telah membuat class `Mahasiswa` yang menerapkan konsep **enkapsulasi** dengan:
   - Atribut private (`nim`, `nama`, `jurusan`, `ipk`)
   - Method public untuk mengakses atribut (`setIPK`, getter methods)

2. Program mendemonstrasikan bagaimana **objek** dibuat dari blueprint class:
   - `mhs1` dan `mhs2` adalah dua objek berbeda dari class yang sama
   - Masing-masing memiliki state (data) sendiri
   - Keduanya memiliki behavior (method) yang sama

3. Konsep OOP yang diterapkan:
   - **Abstraksi**: Mahasiswa menyederhanakan konsep mahasiswa di dunia nyata
   - **Enkapsulasi**: Atribut disembunyikan dan hanya diakses melalui method
   - (Inheritance dan Polimorfisme akan kita bahas lebih detail di bab berikutnya)

## Rangkuman

Dalam bab ini, kita telah mempelajari:

1. **Paradigma Pemrograman**: Perbedaan antara pemrograman prosedural dan OOP
2. **Konsep Objek dan Kelas**: 
   - Class sebagai blueprint
   - Object sebagai instance dari class
3. **Empat Pilar OOP**:
   - **Enkapsulasi**: Menyembunyikan implementasi dan data
   - **Inheritance**: Mewarisi properties dan methods
   - **Polimorfisme**: Satu interface, banyak implementasi
   - **Abstraksi**: Menyembunyikan kompleksitas
4. **Implementasi OOP di Java**: Bagaimana Java mendukung konsep OOP
5. **Praktik dengan NetBeans**: Membuat program sederhana yang menerapkan konsep OOP

OOP adalah paradigma pemrograman yang sangat powerful yang memungkinkan kita membuat program yang modular, dapat digunakan kembali, dan mudah dipelihara. Dengan memahami konsep dasar OOP, Anda telah memiliki fondasi yang kuat untuk menjadi programmer Java yang handal.

## Latihan Soal

1. Apa perbedaan utama antara pemrograman prosedural dan pemrograman berorientasi objek?

2. Jelaskan perbedaan antara class dan object dengan menggunakan analogi dunia nyata!

3. Sebutkan dan jelaskan secara singkat empat pilar OOP!

4. Buatlah class sederhana untuk memodelkan "Buku" dengan atribut-atribut yang sesuai dan method untuk menampilkan informasi buku!

5. Mengapa enkapsulasi penting dalam pemrograman berorientasi objek? Berikan contoh sederhana!

6. Bagaimana cara menerapkan konsep abstraksi dalam Java? Apa perbedaan antara abstract class dan interface?

7. Modifikasi program latihan praktik untuk menambahkan class "MahasiswaBerprestasi" yang mewarisi dari class "Mahasiswa" dan memiliki atribut dan method tambahan!

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional.

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall.

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional.

5. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall.

6. Oracle. (2023). *The Java™ Tutorials*. Oracle. [https://docs.oracle.com/javase/tutorial/](https://docs.oracle.com/javase/tutorial/)

7. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education.

8. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media.

9. Ullenboom, C. (2022). *Java ist auch eine Insel* (15th ed.). Rheinwerk Computing.

10. Liang, Y. D. (2019). *Introduction to Java Programming and Data Structures, Comprehensive Version* (12th ed.). Pearson.

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
