# 📘 Tutorial Java OOP #02: Inheritance dan Method Overriding

> *"Dalam kehidupan nyata, kita mewarisi sifat dari orangtua kita. Dalam OOP, kelas anak mewarisi properti dan perilaku dari kelas induk."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep inheritance (pewarisan) dalam pemrograman berorientasi objek
- Menerapkan inheritance menggunakan keyword `extends` di Java
- Menjelaskan berbagai jenis inheritance dan batasan-batasannya di Java
- Mengimplementasikan method overriding untuk menyesuaikan perilaku class turunan
- Menggunakan annotation `@Override` dengan tepat
- Memahami konsep `super` untuk mengakses anggota kelas induk

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Konsep Inheritance (Pewarisan)](#konsep-inheritance-pewarisan)
3. [Implementasi Inheritance di Java](#implementasi-inheritance-di-java)
4. [Jenis-jenis Inheritance](#jenis-jenis-inheritance)
5. [Method Overriding](#method-overriding)
6. [Annotation @Override](#annotation-override)
7. [Keyword super](#keyword-super)
8. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
9. [Rangkuman](#rangkuman)
10. [Latihan Soal](#latihan-soal)
11. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari konsep dasar OOP dan empat pilar utamanya: Enkapsulasi, Inheritance, Polimorfisme, dan Abstraksi. Pada bab ini, kita akan membahas lebih mendalam tentang salah satu pilar tersebut, yaitu **Inheritance (Pewarisan)**.

Inheritance adalah salah satu konsep paling powerful dalam OOP yang memungkinkan kita membuat kelas baru berdasarkan kelas yang sudah ada. Dengan inheritance, kita dapat menghemat waktu, mengurangi duplikasi kode, dan menciptakan hierarki kelas yang baik. Mari kita pelajari lebih lanjut!

## Konsep Inheritance (Pewarisan)

### Apa itu Inheritance?

**Inheritance (Pewarisan)** adalah mekanisme di mana sebuah kelas baru (subclass/kelas turunan) dapat mewarisi atribut dan metode dari kelas yang sudah ada (superclass/kelas induk). Kelas turunan dapat menambahkan fungsionalitas baru atau memodifikasi fungsionalitas yang diwarisi sesuai kebutuhan.

### Analogi Inheritance dalam Dunia Nyata

Untuk memahami inheritance, kita bisa menganalogikan dengan pewarisan sifat dalam keluarga:

- **Orangtua (Superclass)** memiliki karakteristik dan kemampuan tertentu
- **Anak (Subclass)** mewarisi karakteristik dan kemampuan dari orangtua
- Anak juga dapat memiliki karakteristik dan kemampuan tambahan
- Beberapa karakteristik orangtua mungkin diubah atau disesuaikan oleh anak

Atau analogi lain dengan kendaraan:
- **Kendaraan (Superclass)** memiliki kemampuan dasar seperti bergerak dan berhenti
- **Mobil (Subclass)** mewarisi kemampuan dasar tersebut
- Mobil juga memiliki kemampuan tambahan seperti AC, radio, dll
- Mobil mungkin mengimplementasikan cara bergerak yang berbeda dari kendaraan pada umumnya

### Manfaat Inheritance

1. **Penggunaan Ulang Kode (Code Reusability)**: Mengurangi duplikasi kode dengan mewarisi fungsionalitas yang sudah ada
2. **Ekstensi Mudah**: Memungkinkan penambahan fitur baru tanpa mengubah kode yang sudah ada
3. **Struktur Hierarkis**: Menciptakan hubungan yang jelas dan terorganisir antar kelas
4. **Pemeliharaan Lebih Mudah**: Perubahan pada superclass otomatis tercermin pada semua subclass

## Implementasi Inheritance di Java

Di Java, inheritance diimplementasikan menggunakan keyword `extends`. Sintaksnya adalah sebagai berikut:

```java
class SuperClass {
    // Atribut dan metode superclass
}

class SubClass extends SuperClass {
    // Atribut dan metode tambahan subclass
}
```

Contoh implementasi inheritance:

```java
// Superclass
class Kendaraan {
    protected String merek;
    protected int tahun;
    
    public Kendaraan(String merek, int tahun) {
        this.merek = merek;
        this.tahun = tahun;
    }
    
    public void info() {
        System.out.println("Kendaraan merek " + merek + " tahun " + tahun);
    }
    
    public void bergerak() {
        System.out.println("Kendaraan bergerak");
    }
}

// Subclass
class Mobil extends Kendaraan {
    private int jumlahPintu;
    
    public Mobil(String merek, int tahun, int jumlahPintu) {
        super(merek, tahun); // Memanggil constructor superclass
        this.jumlahPintu = jumlahPintu;
    }
    
    public void klakson() {
        System.out.println("Beep! Beep!");
    }
}
```

Dalam contoh di atas:
- `Kendaraan` adalah superclass
- `Mobil` adalah subclass yang mewarisi `Kendaraan`
- `Mobil` mewarisi atribut `merek` dan `tahun`, serta metode `info()` dan `bergerak()`
- `Mobil` memiliki atribut tambahan `jumlahPintu` dan metode tambahan `klakson()`

### Penggunaan Subclass

```java
public class Main {
    public static void main(String[] args) {
        Mobil mobilSaya = new Mobil("Toyota", 2020, 4);
        
        // Memanggil method yang diwarisi dari Kendaraan
        mobilSaya.info();      // Output: Kendaraan merek Toyota tahun 2020
        mobilSaya.bergerak();  // Output: Kendaraan bergerak
        
        // Memanggil method khusus Mobil
        mobilSaya.klakson();   // Output: Beep! Beep!
    }
}
```

### Hal-hal yang Diwariskan dan Tidak Diwariskan

Di Java, subclass mewarisi:
- Semua metode dan atribut `public` dari superclass
- Semua metode dan atribut `protected` dari superclass
- Metode dan atribut dengan akses default (no modifier) dari package yang sama

Subclass **tidak** mewarisi:
- Constructor superclass (meskipun bisa memanggil dengan `super()`)
- Metode dan atribut `private` dari superclass
- Metode dan atribut dengan akses default dari package yang berbeda

## Jenis-jenis Inheritance

Java mendukung beberapa jenis inheritance:

### 1. Single Inheritance

Satu subclass mewarisi satu superclass. Ini adalah bentuk inheritance yang paling dasar.

```
     Kendaraan
         ↑
       Mobil
```

```java
class Kendaraan { /* ... */ }
class Mobil extends Kendaraan { /* ... */ }
```

### 2. Multilevel Inheritance

Subclass menjadi superclass untuk kelas lain, membentuk rantai inheritance.

```
     Kendaraan
         ↑
       Mobil
         ↑
    MobilSport
```

```java
class Kendaraan { /* ... */ }
class Mobil extends Kendaraan { /* ... */ }
class MobilSport extends Mobil { /* ... */ }
```

### 3. Hierarchical Inheritance

Beberapa subclass mewarisi dari satu superclass.

```
       Kendaraan
         ↑   ↑
     Mobil   Motor
```

```java
class Kendaraan { /* ... */ }
class Mobil extends Kendaraan { /* ... */ }
class Motor extends Kendaraan { /* ... */ }
```

### Batasan Inheritance di Java

Java **tidak mendukung**:

#### Multiple Inheritance untuk Class

Java tidak mengizinkan satu class mewarisi dari lebih dari satu class langsung. Ini menghindari masalah "diamond problem".

```
    KendaraanDarat   KendaraanAir
             ↑          ↑
              \        /
               Amfibi    // Tidak diizinkan di Java
```

Sebagai gantinya, Java menyediakan interface untuk mendukung fungsionalitas serupa multiple inheritance.

```java
interface KendaraanDarat { /* ... */ }
interface KendaraanAir { /* ... */ }
class Amfibi implements KendaraanDarat, KendaraanAir { /* ... */ }
```

## Method Overriding

**Method Overriding** adalah fitur yang memungkinkan subclass menyediakan implementasi spesifik untuk metode yang sudah didefinisikan di superclass. Saat method di superclass di-override, method subclass lebih diutamakan saat dipanggil dari objek subclass.

### Syarat Method Overriding

1. Nama method, parameter, dan return type di subclass harus **sama** dengan di superclass
2. Access modifier di subclass tidak boleh lebih ketat daripada di superclass
   - Jika method superclass `public`, method subclass juga harus `public`
   - Jika method superclass `protected`, method subclass bisa `protected` atau `public`
3. Method subclass tidak boleh melempar checked exception yang lebih luas dari method superclass
4. Method yang dideklarasikan sebagai `final` tidak bisa di-override
5. Method yang dideklarasikan sebagai `static` tidak bisa di-override (meskipun bisa "disembunyikan")
6. Constructor tidak bisa di-override

### Contoh Method Overriding

```java
// Superclass
class Kendaraan {
    public void bergerak() {
        System.out.println("Kendaraan bergerak");
    }
}

// Subclass
class Mobil extends Kendaraan {
    @Override
    public void bergerak() {
        System.out.println("Mobil bergerak dengan roda");
    }
}

// Subclass lain
class Pesawat extends Kendaraan {
    @Override
    public void bergerak() {
        System.out.println("Pesawat bergerak dengan terbang");
    }
}
```

Penggunaan:

```java
public class Main {
    public static void main(String[] args) {
        Kendaraan k1 = new Kendaraan();
        Kendaraan k2 = new Mobil();      // Polymorphism
        Kendaraan k3 = new Pesawat();    // Polymorphism
        
        k1.bergerak(); // Output: Kendaraan bergerak
        k2.bergerak(); // Output: Mobil bergerak dengan roda
        k3.bergerak(); // Output: Pesawat bergerak dengan terbang
    }
}
```

### Method Overriding vs Method Overloading

Sering terjadi kebingungan antara overriding dan overloading. Berikut perbedaannya:

| Method Overriding | Method Overloading |
|-------------------|-------------------|
| Dilakukan di subclass | Dilakukan di class yang sama atau subclass |
| Nama method, parameter, dan return type sama | Nama method sama, parameter berbeda |
| Runtime polymorphism | Compile-time polymorphism |
| Memodifikasi perilaku metode yang diwariskan | Menyediakan perilaku berbeda dengan signature metode berbeda |

## Annotation @Override

Annotation `@Override` digunakan untuk menandai bahwa sebuah method dimaksudkan untuk meng-override method dari superclass. Penggunaan annotation ini tidak wajib, tetapi sangat direkomendasikan karena:

1. **Keamanan Kode**: Compiler akan memeriksa apakah method benar-benar meng-override method superclass
2. **Dokumentasi**: Membuat kode lebih mudah dibaca dan dipahami
3. **Mencegah Kesalahan**: Menghindari kesalahan karena typo pada nama method atau parameter yang menyebabkan method baru dibuat daripada meng-override

Contoh penggunaan `@Override`:

```java
class Hewan {
    public void suara() {
        System.out.println("Hewan bersuara");
    }
}

class Kucing extends Hewan {
    @Override
    public void suara() {
        System.out.println("Meow!");
    }
    
    // Compiler error - tidak ada method bernama 'sound' di superclass
    // @Override
    // public void sound() {
    //     System.out.println("Meow!");
    // }
}
```

## Keyword super

Keyword `super` digunakan untuk mereferensikan superclass. Ada beberapa penggunaan `super`:

### 1. Memanggil Constructor Superclass

```java
class Kendaraan {
    protected String merek;
    
    public Kendaraan(String merek) {
        this.merek = merek;
    }
}

class Mobil extends Kendaraan {
    private int jumlahPintu;
    
    public Mobil(String merek, int jumlahPintu) {
        super(merek); // Memanggil constructor Kendaraan
        this.jumlahPintu = jumlahPintu;
    }
}
```

Beberapa hal penting:
- Panggilan `super()` harus menjadi statement pertama dalam constructor
- Jika constructor superclass tanpa parameter tidak didefinisikan secara eksplisit dan subclass tidak memanggil constructor superclass secara eksplisit, compiler akan menambahkan `super()` secara otomatis
- Jika superclass tidak memiliki constructor tanpa parameter, subclass harus secara eksplisit memanggil salah satu constructor superclass dengan `super(parameter)`

### 2. Mengakses Method Superclass yang Di-override

```java
class Kendaraan {
    public void tampilInfo() {
        System.out.println("Ini adalah kendaraan");
    }
}

class Mobil extends Kendaraan {
    @Override
    public void tampilInfo() {
        super.tampilInfo(); // Memanggil method tampilInfo() dari Kendaraan
        System.out.println("Lebih spesifik, ini adalah mobil");
    }
}
```

Penggunaan:

```java
public class Main {
    public static void main(String[] args) {
        Mobil mobil = new Mobil();
        mobil.tampilInfo();
    }
}
```

Output:
```
Ini adalah kendaraan
Lebih spesifik, ini adalah mobil
```

### 3. Mengakses Atribut Superclass

```java
class Kendaraan {
    protected int kecepatan = 0;
}

class Mobil extends Kendaraan {
    private int kecepatan = 10; // Variabel dengan nama sama di subclass
    
    public void tampilKecepatan() {
        System.out.println("Kecepatan mobil: " + this.kecepatan);
        System.out.println("Kecepatan kendaraan: " + super.kecepatan);
    }
}
```

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep inheritance dan method overriding dengan membuat program sederhana menggunakan NetBeans IDE.

### Skenario: Sistem Manajemen Pegawai

Kita akan membuat sistem manajemen pegawai sederhana dengan kelas Pegawai sebagai superclass dan dua subclass: PegawaiTetap dan PegawaiKontrak.

### Langkah 1: Buat Project Baru

1. Buka NetBeans IDE
2. Pilih **File** > **New Project**
3. Pilih **Java** > **Java Application** > **Next**
4. Beri nama project "SistemPegawai" dan tentukan lokasi penyimpanan
5. Klik **Finish**

### Langkah 2: Buat Kelas Pegawai (Superclass)

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Pegawai"
3. Isi dengan kode berikut:

```java
package sistempegawai;

public class Pegawai {
    // Atribut
    protected String id;
    protected String nama;
    protected String alamat;
    protected int tahunMasuk;
    
    // Constructor
    public Pegawai(String id, String nama, String alamat, int tahunMasuk) {
        this.id = id;
        this.nama = nama;
        this.alamat = alamat;
        this.tahunMasuk = tahunMasuk;
    }
    
    // Method untuk menghitung gaji (akan di-override)
    public double hitungGaji() {
        return 0.0; // Implementasi default
    }
    
    // Method untuk menghitung masa kerja
    public int hitungMasaKerja(int tahunSekarang) {
        return tahunSekarang - tahunMasuk;
    }
    
    // Method untuk menampilkan info pegawai
    public void tampilInfo() {
        System.out.println("ID Pegawai: " + id);
        System.out.println("Nama: " + nama);
        System.out.println("Alamat: " + alamat);
        System.out.println("Tahun Masuk: " + tahunMasuk);
    }
    
    // Getter methods
    public String getId() {
        return id;
    }
    
    public String getNama() {
        return nama;
    }
    
    public String getAlamat() {
        return alamat;
    }
    
    public int getTahunMasuk() {
        return tahunMasuk;
    }
}
```

### Langkah 3: Buat Kelas PegawaiTetap (Subclass)

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "PegawaiTetap"
3. Isi dengan kode berikut:

```java
package sistempegawai;

public class PegawaiTetap extends Pegawai {
    // Atribut tambahan
    private double gajiPokok;
    private double tunjangan;
    
    // Constructor
    public PegawaiTetap(String id, String nama, String alamat, int tahunMasuk, 
                         double gajiPokok, double tunjangan) {
        super(id, nama, alamat, tahunMasuk); // Memanggil constructor superclass
        this.gajiPokok = gajiPokok;
        this.tunjangan = tunjangan;
    }
    
    // Override method hitungGaji
    @Override
    public double hitungGaji() {
        return gajiPokok + tunjangan;
    }
    
    // Override method tampilInfo
    @Override
    public void tampilInfo() {
        super.tampilInfo(); // Memanggil method superclass
        System.out.println("Status: Pegawai Tetap");
        System.out.println("Gaji Pokok: " + gajiPokok);
        System.out.println("Tunjangan: " + tunjangan);
        System.out.println("Total Gaji: " + hitungGaji());
    }
    
    // Getter methods
    public double getGajiPokok() {
        return gajiPokok;
    }
    
    public double getTunjangan() {
        return tunjangan;
    }
}
```

### Langkah 4: Buat Kelas PegawaiKontrak (Subclass)

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "PegawaiKontrak"
3. Isi dengan kode berikut:

```java
package sistempegawai;

public class PegawaiKontrak extends Pegawai {
    // Atribut tambahan
    private double upahHarian;
    private int jumlahHariKerja;
    private int lamaKontrak; // dalam bulan
    
    // Constructor
    public PegawaiKontrak(String id, String nama, String alamat, int tahunMasuk,
                          double upahHarian, int jumlahHariKerja, int lamaKontrak) {
        super(id, nama, alamat, tahunMasuk); // Memanggil constructor superclass
        this.upahHarian = upahHarian;
        this.jumlahHariKerja = jumlahHariKerja;
        this.lamaKontrak = lamaKontrak;
    }
    
    // Override method hitungGaji
    @Override
    public double hitungGaji() {
        return upahHarian * jumlahHariKerja;
    }
    
    // Override method tampilInfo
    @Override
    public void tampilInfo() {
        super.tampilInfo(); // Memanggil method superclass
        System.out.println("Status: Pegawai Kontrak");
        System.out.println("Upah Harian: " + upahHarian);
        System.out.println("Jumlah Hari Kerja: " + jumlahHariKerja);
        System.out.println("Lama Kontrak: " + lamaKontrak + " bulan");
        System.out.println("Total Gaji: " + hitungGaji());
    }
    
    // Getter methods
    public double getUpahHarian() {
        return upahHarian;
    }
    
    public int getJumlahHariKerja() {
        return jumlahHariKerja;
    }
    
    public int getLamaKontrak() {
        return lamaKontrak;
    }
    
    // Method tambahan spesifik untuk PegawaiKontrak
    public void perpanjangKontrak(int tambahan) {
        lamaKontrak += tambahan;
        System.out.println("Kontrak diperpanjang. Lama kontrak sekarang: " + lamaKontrak + " bulan");
    }
}
```

### Langkah 5: Buat Kelas Utama

1. Buka file `SistemPegawai.java` (atau nama file utama yang dibuat otomatis)
2. Ubah kode menjadi:

```java
package sistempegawai;

public class SistemPegawai {
    public static void main(String[] args) {
        // Membuat objek pegawai tetap
        PegawaiTetap pt = new PegawaiTetap("PT001", "Budi Santoso", "Jakarta", 2015, 
                                           5000000, 1500000);
        
        // Membuat objek pegawai kontrak
        PegawaiKontrak pk = new PegawaiKontrak("PK001", "Ani Wijaya", "Bandung", 2020,
                                               200000, 22, 12);
        
        // Menampilkan informasi pegawai
        System.out.println("=== INFORMASI PEGAWAI TETAP ===");
        pt.tampilInfo();
        System.out.println("Masa Kerja: " + pt.hitungMasaKerja(2023) + " tahun");
        
        System.out.println("\n=== INFORMASI PEGAWAI KONTRAK ===");
        pk.tampilInfo();
        System.out.println("Masa Kerja: " + pk.hitungMasaKerja(2023) + " tahun");
        
        // Memanggil method spesifik PegawaiKontrak
        pk.perpanjangKontrak(6);
        
        // Demonstrasi polymorphism
        System.out.println("\n=== DEMONSTRASI POLYMORPHISM ===");
        Pegawai[] pegawaiArray = new Pegawai[2];
        pegawaiArray[0] = pt;
        pegawaiArray[1] = pk;
        
        for (Pegawai pegawai : pegawaiArray) {
            pegawai.tampilInfo();
            System.out.println("Gaji: " + pegawai.hitungGaji());
            System.out.println("-------------------");
        }
    }
}
```

### Langkah 6: Jalankan Program

1. Klik **Run** > **Run Project**
2. Atau tekan tombol F6

Output:
```
=== INFORMASI PEGAWAI TETAP ===
ID Pegawai: PT001
Nama: Budi Santoso
Alamat: Jakarta
Tahun Masuk: 2015
Status: Pegawai Tetap
Gaji Pokok: 5000000.0
Tunjangan: 1500000.0
Total Gaji: 6500000.0
Masa Kerja: 8 tahun

=== INFORMASI PEGAWAI KONTRAK ===
ID Pegawai: PK001
Nama: Ani Wijaya
Alamat: Bandung
Tahun Masuk: 2020
Status: Pegawai Kontrak
Upah Harian: 200000.0
Jumlah Hari Kerja: 22
Lama Kontrak: 12 bulan
Total Gaji: 4400000.0
Masa Kerja: 3 tahun
Kontrak diperpanjang. Lama kontrak sekarang: 18 bulan

=== DEMONSTRASI POLYMORPHISM ===
ID Pegawai: PT001
Nama: Budi Santoso
Alamat: Jakarta
Tahun Masuk: 2015
Status: Pegawai Tetap
Gaji Pokok: 5000000.0
Tunjangan: 1500000.0
Total Gaji: 6500000.0
Gaji: 6500000.0
-------------------
ID Pegawai: PK001
Nama: Ani Wijaya
Alamat: Bandung
Tahun Masuk: 2020
Status: Pegawai Kontrak
Upah Harian: 200000.0
Jumlah Hari Kerja: 22
Lama Kontrak: 18 bulan
Total Gaji: 4400000.0
Gaji: 4400000.0
-------------------
```

### Penjelasan

Dalam contoh praktik di atas:

1. Kita membuat kelas `Pegawai` sebagai superclass dengan:
   - Atribut protected yang diwariskan ke subclass
   - Method `hitungGaji()` yang akan di-override oleh subclass
   - Method umum seperti `hitungMasaKerja()` dan `tampilInfo()`

2. Kita membuat dua subclass: `PegawaiTetap` dan `PegawaiKontrak` yang:
   - Mewarisi semua atribut dan method `Pegawai`
   - Memiliki atribut dan method tambahan sesuai kebutuhan
   - Meng-override method `hitungGaji()` dengan implementasi khusus
   - Meng-override method `tampilInfo()` sambil tetap memanggil implementasi superclass

3. Program mendemonstrasikan:
   - Inheritance: Subclass mewarisi atribut dan method dari superclass
   - Method Overriding: Implementasi method berbeda di setiap subclass
   - Polymorphism: Objek berbeda memberikan respons berbeda pada method yang sama

## Rangkuman

Dalam bab ini, kita telah mempelajari:

1. **Konsep Inheritance (Pewarisan)**:
   - Memungkinkan subclass mewarisi atribut dan method dari superclass
   - Menciptakan hubungan "is-a" antara kelas
   - Mendorong penggunaan ulang kode dan ekstensi mudah

2. **Implementasi Inheritance di Java**:
   - Menggunakan keyword `extends`
   - Mendukung single inheritance untuk class
   - Atribut/method yang diwariskan tergantung pada access modifier

3. **Jenis-jenis Inheritance**:
   - Single Inheritance
   - Multilevel Inheritance
   - Hierarchical Inheritance
   - Java tidak mendukung multiple inheritance untuk class

4. **Method Overriding**:
   - Memungkinkan subclass menyediakan implementasi spesifik
   - Memiliki syarat-syarat tertentu (nama, parameter, return type sama)
   - Berbeda dengan method overloading

5. **Annotation @Override**:
   - Menandai method yang meng-override method superclass
   - Menjamin keamanan kode dan dokumentasi yang baik

6. **Keyword super**:
   - Memanggil constructor superclass
   - Mengakses method superclass yang di-override
   - Mengakses atribut superclass

Inheritance adalah konsep OOP yang sangat penting yang memungkinkan kita menciptakan hierarki kelas yang baik, mengurangi duplikasi kode, dan memudahkan perluasan fungsionalitas. Dengan memahami inheritance dan method overriding, Anda telah memperkuat fondasi Anda dalam pemrograman berorientasi objek.

## Latihan Soal

1. Apa yang dimaksud dengan inheritance dalam pemrograman berorientasi objek? Sebutkan manfaatnya!

2. Jelaskan perbedaan antara method overriding dan method overloading!

3. Mengapa Java tidak mendukung multiple inheritance untuk class? Bagaimana cara Java menyediakan fungsionalitas serupa?

4. Buatlah hierarki kelas untuk sebuah sistem perpustakaan dengan kelas `Item` sebagai superclass dan `Buku`, `Majalah`, dan `DVD` sebagai subclass!

5. Apa yang terjadi jika subclass memiliki method dengan nama yang sama dengan method di superclass, tetapi dengan parameter berbeda?

6. Jelaskan kegunaan dari keyword `super` di Java! Berikan contoh penggunaannya!

7. Perhatikan kode berikut:
   ```java
   class A {
       void show() { System.out.println("A"); }
   }
   
   class B extends A {
       void show() { System.out.println("B"); }
   }
   
   class C extends A {
       void show() { System.out.println("C"); }
   }
   ```
   Apa output dari kode berikut?
   ```java
   A obj1 = new B();
   A obj2 = new C();
   obj1.show();
   obj2.show();
   ```

8. Buat program yang memanfaatkan inheritance dan method overriding untuk sistem manajemen bentuk geometri dengan kelas `BentukGeometri` sebagai superclass dan minimal dua subclass!

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional.

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall.

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional.

5. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall.

6. Oracle. (2023). *Java Language Specification: Inheritance, Overriding, and Hiding*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-8.html#jls-8.4.8](https://docs.oracle.com/javase/specs/jls/se17/html/jls-8.html#jls-8.4.8)

7. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education.

8. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media.

9. Martin, R. C. (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall.

10. Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley Professional.

---

[◀️ Kembali ke Tutorial #01: Memahami Konsep Dasar OOP pada Java](01-oop-basic-concepts.md) | [Lanjut ke Tutorial #03: Tingkat Akses Member dan Class (Modifier) ▶️](03-access-modifiers.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
