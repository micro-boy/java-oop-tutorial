# 📘 Tutorial Java OOP #03: Tingkat Akses Member dan Class (Modifier)

> *"Memahami akses modifier adalah seperti memahami sistem keamanan sebuah gedung—menentukan siapa yang boleh masuk ke area mana."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep encapsulation (enkapsulasi) dan hubungannya dengan access modifier
- Menjelaskan perbedaan antara public, private, protected, dan default access modifier
- Menerapkan access modifier yang tepat untuk atribut dan metode dalam class
- Memahami dan mengimplementasikan non-access modifier seperti static, final, dan abstract
- Mendesain class dengan prinsip information hiding yang baik
- Memilih modifier yang sesuai berdasarkan kebutuhan desain dan keamanan

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Konsep Enkapsulasi dan Information Hiding](#konsep-enkapsulasi-dan-information-hiding)
3. [Access Modifiers di Java](#access-modifiers-di-java)
   - [Public Access Modifier](#public-access-modifier)
   - [Private Access Modifier](#private-access-modifier)
   - [Protected Access Modifier](#protected-access-modifier)
   - [Default (No-Modifier) Access](#default-no-modifier-access)
   - [Ringkasan Access Modifiers](#ringkasan-access-modifiers)
4. [Non-Access Modifiers](#non-access-modifiers)
   - [Static Modifier](#static-modifier)
   - [Final Modifier](#final-modifier)
   - [Abstract Modifier](#abstract-modifier)
   - [Synchronized Modifier](#synchronized-modifier)
   - [Transient Modifier](#transient-modifier)
   - [Volatile Modifier](#volatile-modifier)
5. [Best Practices Penggunaan Modifier](#best-practices-penggunaan-modifier)
6. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
7. [Rangkuman](#rangkuman)
8. [Latihan Soal](#latihan-soal)
9. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah membahas tentang inheritance dan method overriding. Kali ini, kita akan mempelajari tentang access modifiers dan non-access modifiers di Java. Dengan memahami topik ini, Anda akan dapat mendesain class yang lebih aman, lebih terstruktur, dan lebih mudah dipelihara.

Access modifiers dan non-access modifiers merupakan komponen penting dalam encapsulation—salah satu dari empat pilar OOP yang kita pelajari di tutorial pertama. Modifier ini memungkinkan Anda mengontrol visibilitas dan perilaku class, atribut, dan metode dalam program Java.

## Konsep Enkapsulasi dan Information Hiding

Sebelum kita membahas modifier secara detail, penting untuk memahami konsep enkapsulasi dan information hiding yang menjadi dasar penggunaan access modifier.

### Enkapsulasi (Encapsulation)

**Encapsulation** adalah konsep membungkus (mengenkapsulasi) data (atribut) dan kode yang memanipulasi data tersebut (metode) dalam satu unit. Di Java, unit ini adalah class.

Prinsip utama enkapsulasi adalah:
1. Menyembunyikan data (state) dari akses langsung dari luar
2. Menyediakan metode publik untuk mengakses dan memodifikasi data tersebut
3. Memastikan keadaan objek selalu valid dengan kontrol akses

### Information Hiding

**Information hiding** adalah prinsip menyembunyikan implementasi internal dan hanya mengekspos antarmuka yang diperlukan. Ini memiliki beberapa keuntungan:

1. **Keamanan Data**: Mencegah modifikasi data yang tidak diinginkan
2. **Pemeliharaan**: Perubahan implementasi internal tidak memengaruhi kode klien
3. **Pengujian**: Lebih mudah untuk menguji komponen secara terpisah
4. **Penggunaan Ulang**: Komponen dapat digunakan kembali tanpa khawatir tentang dependensi

Analogi dalam kehidupan nyata:
- Mesin mobil dienkapsulasi di bawah kap. Anda tidak perlu mengetahui cara kerja mesin secara detail untuk mengemudikan mobil.
- Antarmuka pengguna (setir, pedal gas, rem) adalah "antarmuka publik" untuk mengontrol mobil.
- Komponen internal mobil "disembunyikan" dan hanya dapat diakses oleh mekanik yang berwenang.

## Access Modifiers di Java

Java memiliki empat tingkat akses yang diatur oleh access modifier:

### Public Access Modifier

Keyword: `public`

**Definisi**: 
Class, atribut, atau metode yang dideklarasikan sebagai `public` dapat diakses dari mana saja.

**Karakteristik**:
- Visibilitas maksimum
- Dapat diakses oleh class dalam package yang sama dan dari package lain
- Untuk class, hanya class `public` yang dapat diimpor dari package lain

**Contoh**:
```java
public class Mobil {
    public String merek;
    
    public void klakson() {
        System.out.println("Beep! Beep!");
    }
}
```

**Penggunaan**:
```java
// Di class lain dalam package yang sama atau berbeda
Mobil mobilku = new Mobil();
mobilku.merek = "Toyota"; // Akses legal ke atribut public
mobilku.klakson();       // Akses legal ke metode public
```

### Private Access Modifier

Keyword: `private`

**Definisi**: 
Class, atribut, atau metode yang dideklarasikan sebagai `private` hanya dapat diakses dalam class yang sama.

**Karakteristik**:
- Visibilitas minimum
- Tidak dapat diakses dari class lain, bahkan subclass
- Metode private tidak dapat di-override
- Mendorong encapsulation

**Contoh**:
```java
public class RekeningBank {
    private String nomorRekening;
    private double saldo;
    
    public RekeningBank(String nomorRekening, double saldoAwal) {
        this.nomorRekening = nomorRekening;
        this.saldo = saldoAwal;
    }
    
    private void validasiJumlah(double jumlah) {
        if (jumlah <= 0) {
            throw new IllegalArgumentException("Jumlah harus positif");
        }
    }
    
    public void setor(double jumlah) {
        validasiJumlah(jumlah); // Memanggil metode private
        saldo += jumlah;
    }
    
    public void tarik(double jumlah) {
        validasiJumlah(jumlah);
        if (saldo >= jumlah) {
            saldo -= jumlah;
        } else {
            System.out.println("Saldo tidak mencukupi");
        }
    }
    
    public double getSaldo() {
        return saldo;
    }
}
```

**Penggunaan**:
```java
// Di class lain
RekeningBank rekeningku = new RekeningBank("123456", 1000000);
rekeningku.setor(500000);
// rekeningku.saldo = 0;        // Error: saldo memiliki akses private
// rekeningku.validasiJumlah(100); // Error: validasiJumlah() memiliki akses private
```

### Protected Access Modifier

Keyword: `protected`

**Definisi**: 
Class, atribut, atau metode yang dideklarasikan sebagai `protected` dapat diakses dalam package yang sama dan oleh subclass (bahkan jika subclass berada di package yang berbeda).

**Karakteristik**:
- Visibilitas sedang
- Memberikan akses ke subclass, mendukung inheritance
- Lebih aman daripada public tetapi memungkinkan ekstensi

**Contoh**:
```java
// Dalam package 'kendaraan'
package kendaraan;

public class Kendaraan {
    protected int kecepatan;
    
    protected void tingkatkanKecepatan(int nilaiTambah) {
        kecepatan += nilaiTambah;
    }
}

// Dalam package 'transportasi'
package transportasi;

import kendaraan.Kendaraan;

public class Mobil extends Kendaraan {
    public void akselerasi() {
        tingkatkanKecepatan(10); // Akses legal ke metode protected
        System.out.println("Kecepatan sekarang: " + kecepatan); // Akses legal ke atribut protected
    }
}
```

**Penggunaan**:
```java
// Di class lain yang bukan subclass, dalam package berbeda
Kendaraan k = new Kendaraan();
// k.kecepatan = 100;        // Error: kecepatan memiliki akses protected
// k.tingkatkanKecepatan(10); // Error: tingkatkanKecepatan() memiliki akses protected

// Di class lain dalam package yang sama
// (jika class tersebut ada dalam package 'kendaraan')
Kendaraan k = new Kendaraan();
k.kecepatan = 100;         // Akses legal (dalam package yang sama)
k.tingkatkanKecepatan(10); // Akses legal (dalam package yang sama)
```

### Default (No-Modifier) Access

Ketika tidak ada modifier yang ditentukan (no modifier).

**Definisi**: 
Class, atribut, atau metode tanpa access modifier eksplisit memiliki akses "default" atau "package-private"—dapat diakses hanya dalam package yang sama.

**Karakteristik**:
- Sering disebut "package-private"
- Membatasi akses ke package yang sama
- Berguna untuk komponen yang hanya digunakan dalam package tersebut

**Contoh**:
```java
// Dalam package 'utilitas'
package utilitas;

class Kalkulator {
    int tambah(int a, int b) {
        return a + b;
    }
}

class AplikasiKalkulator {
    void proses() {
        Kalkulator calc = new Kalkulator();
        int hasil = calc.tambah(5, 3); // Akses legal (dalam package yang sama)
    }
}
```

**Penggunaan**:
```java
// Di class dalam package berbeda
import utilitas.Kalkulator; // Error: Kalkulator tidak visible

// Bahkan jika impor berhasil:
Kalkulator calc = new Kalkulator(); // Error: Kalkulator memiliki akses default
```

### Ringkasan Access Modifiers

Berikut adalah tabel ringkasan visibilitas berbagai access modifiers:

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| public | Ya | Ya | Ya | Ya |
| protected | Ya | Ya | Ya | Tidak |
| default (no-modifier) | Ya | Ya | Tidak | Tidak |
| private | Ya | Tidak | Tidak | Tidak |

Keterangan:
- **Class**: Apakah dapat diakses dari dalam class yang sama
- **Package**: Apakah dapat diakses dari class lain dalam package yang sama
- **Subclass**: Apakah dapat diakses dari subclass (bahkan di package berbeda)
- **World**: Apakah dapat diakses dari class mana pun

## Non-Access Modifiers

Selain access modifiers, Java juga memiliki non-access modifiers yang memengaruhi perilaku class, atribut, dan metode tanpa mengubah aksesibilitasnya.

### Static Modifier

Keyword: `static`

**Definisi**:
Menandai bahwa anggota (atribut atau metode) adalah milik class, bukan instance/objek. Artinya, anggota tersebut dapat diakses tanpa membuat objek dari class tersebut.

**Karakteristik**:
- **Static Variable**: Shared di antara semua instance class, hanya ada satu copy
- **Static Method**: Dapat dipanggil tanpa membuat objek, tidak dapat mengakses non-static members secara langsung
- **Static Block**: Dieksekusi saat class dimuat, sebelum konstruktor

**Contoh**:
```java
public class Matematika {
    // Static variable
    public static final double PI = 3.14159;
    private static int jumlahOperasi = 0;
    
    // Static method
    public static int tambah(int a, int b) {
        jumlahOperasi++;
        return a + b;
    }
    
    // Static method
    public static int kali(int a, int b) {
        jumlahOperasi++;
        return a * b;
    }
    
    // Static method untuk mengakses static variable
    public static int getJumlahOperasi() {
        return jumlahOperasi;
    }
    
    // Static block
    static {
        System.out.println("Class Matematika dimuat");
    }
}
```

**Penggunaan**:
```java
// Tanpa membuat objek
double luasLingkaran = Matematika.PI * radius * radius;
int hasil = Matematika.tambah(5, 3);
System.out.println("Jumlah operasi: " + Matematika.getJumlahOperasi());
```

### Final Modifier

Keyword: `final`

**Definisi**:
Menandai bahwa entity (class, metode, atau variable) tidak dapat diubah atau di-override.

**Karakteristik**:
- **Final Class**: Tidak dapat disubclass (diturunkan)
- **Final Method**: Tidak dapat di-override oleh subclass
- **Final Variable**: Tidak dapat diubah nilainya setelah inisialisasi (konstanta)

**Contoh**:
```java
// Final class
public final class KonstantaMatematika {
    // Final variable (konstanta)
    public static final double PI = 3.14159;
    public static final double E = 2.71828;
}

// Class normal dengan final method
public class Bentuk {
    // Final method
    public final void gambar() {
        System.out.println("Menggambar bentuk dasar");
    }
}

// Subclass
public class Lingkaran extends Bentuk {
    private double radius;
    
    // Final variable di level instance
    private final String nama = "Lingkaran";
    
    // Ini akan menyebabkan error saat kompilasi
    // @Override
    // public void gambar() { 
    //     System.out.println("Menggambar lingkaran");
    // }
}
```

**Penggunaan**:
```java
KonstantaMatematika.PI; // Dapat diakses
// KonstantaMatematika.PI = 3.14; // Error: final variable tidak dapat diubah

// Tidak dapat membuat subclass dari KonstantaMatematika
// class TurunanKonstanta extends KonstantaMatematika { } // Error: final class
```

### Abstract Modifier

Keyword: `abstract`

**Definisi**:
Menandai class atau metode yang tidak lengkap dan harus dilengkapi oleh subclass.

**Karakteristik**:
- **Abstract Class**: Tidak dapat diinstansiasi, hanya dapat disubclass
- **Abstract Method**: Tidak memiliki implementasi, harus di-override oleh non-abstract subclass

**Contoh**:
```java
// Abstract class
public abstract class Bentuk {
    // Atribut biasa
    protected String warna;
    
    // Constructor
    public Bentuk(String warna) {
        this.warna = warna;
    }
    
    // Abstract method
    public abstract double hitungLuas();
    
    // Abstract method
    public abstract double hitungKeliling();
    
    // Concrete method
    public void tampilkanInfo() {
        System.out.println("Bentuk berwarna " + warna);
        System.out.println("Luas: " + hitungLuas());
        System.out.println("Keliling: " + hitungKeliling());
    }
}

// Concrete subclass
public class Lingkaran extends Bentuk {
    private double radius;
    
    public Lingkaran(String warna, double radius) {
        super(warna);
        this.radius = radius;
    }
    
    // Implementasi abstract method
    @Override
    public double hitungLuas() {
        return Math.PI * radius * radius;
    }
    
    // Implementasi abstract method
    @Override
    public double hitungKeliling() {
        return 2 * Math.PI * radius;
    }
}
```

**Penggunaan**:
```java
// Bentuk bentuk = new Bentuk("Merah"); // Error: abstract class tidak dapat diinstansiasi
Bentuk lingkaran = new Lingkaran("Biru", 5.0); // Valid: polymorphism
lingkaran.tampilkanInfo(); // Memanggil metode concrete
```

### Synchronized Modifier

Keyword: `synchronized`

**Definisi**:
Menandai metode atau blok kode yang hanya dapat diakses oleh satu thread pada satu waktu, digunakan untuk menghindari race condition.

**Karakteristik**:
- Mencegah multiple thread mengakses resource yang sama secara bersamaan
- Meningkatkan thread safety
- Dapat mempengaruhi kinerja karena thread harus menunggu

**Contoh**:
```java
public class KonterBersama {
    private int nilai = 0;
    
    // Synchronized method
    public synchronized void increment() {
        nilai++;
    }
    
    // Metode dengan synchronized block
    public void incrementDenganBlock() {
        // Operasi non-sinkron dapat dilakukan di sini
        
        // Hanya blok ini yang dieksekusi secara sinkron
        synchronized(this) {
            nilai++;
        }
        
        // Operasi non-sinkron lainnya
    }
    
    public int getNilai() {
        return nilai;
    }
}
```

### Transient Modifier

Keyword: `transient`

**Definisi**:
Menandai atribut yang tidak akan diserialisasi (disimpan) saat objek tersebut diserialisasi.

**Karakteristik**:
- Digunakan untuk menandai field yang tidak perlu atau tidak seharusnya diserialisasi
- Berguna untuk informasi sensitif atau data sementara
- Nilai field transient menjadi nilai default saat deserialisasi (0, false, null, dll.)

**Contoh**:
```java
import java.io.Serializable;

public class Pengguna implements Serializable {
    private String username;
    private transient String password; // Tidak akan diserialisasi
    
    public Pengguna(String username, String password) {
        this.username = username;
        this.password = password;
    }
    
    public void tampilkanInfo() {
        System.out.println("Username: " + username);
        System.out.println("Password: " + password);
    }
}
```

### Volatile Modifier

Keyword: `volatile`

**Definisi**:
Menandai variable yang nilainya mungkin diubah oleh multiple thread, memaksa Java untuk selalu membaca nilainya dari main memory, bukan dari thread-local cache.

**Karakteristik**:
- Memastikan visibilitas perubahan variable di antara thread
- Mencegah reordering optimasi oleh compiler
- Tidak menyediakan atomisitas operasi (use synchronized for that)

**Contoh**:
```java
public class StatusPengecekan {
    private volatile boolean berhenti = false;
    
    public void setBerhenti(boolean nilai) {
        berhenti = nilai;
    }
    
    public boolean isBerhenti() {
        return berhenti;
    }
    
    public void proses() {
        while (!berhenti) {
            // Melakukan pengecekan
            // ...
        }
    }
}
```

## Best Practices Penggunaan Modifier

Berikut adalah beberapa best practices dalam penggunaan modifier di Java:

### Access Modifier Best Practices

1. **Buat atribut private**: Sebisa mungkin, deklarasikan atribut sebagai private untuk encapsulation yang baik
2. **Gunakan getter dan setter**: Sediakan metode public untuk mengakses dan memodifikasi atribut private
3. **Batasi penggunaan protected**: Gunakan protected hanya jika subclass benar-benar perlu akses langsung
4. **Pertimbangkan package-private**: Untuk komponen yang hanya digunakan dalam satu package
5. **Ekspor hanya yang diperlukan**: Buat public hanya kelas dan metode yang perlu diakses dari luar package

### Non-Access Modifier Best Practices

1. **Gunakan static untuk utility methods**: Metode yang tidak tergantung pada state objek
2. **Gunakan final untuk constants**: Deklarasikan konstanta sebagai `static final`
3. **Gunakan final untuk immutability**: Class atau metode yang tidak boleh diubah
4. **Gunakan abstract dengan bijak**: Untuk template method pattern dan framework desain
5. **Minimalkan synchronized**: Gunakan hanya jika benar-benar diperlukan karena berpengaruh pada kinerja

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep access modifier dan non-access modifier dengan membuat program sederhana menggunakan NetBeans IDE.

### Skenario: Sistem Perpustakaan

Kita akan membuat sistem perpustakaan sederhana dengan beberapa kelas yang menunjukkan penggunaan berbagai modifier.

### Langkah 1: Buat Project Baru

1. Buka NetBeans IDE
2. Pilih **File** > **New Project**
3. Pilih **Java** > **Java Application** > **Next**
4. Beri nama project "SistemPerpustakaan" dan tentukan lokasi penyimpanan
5. Klik **Finish**

### Langkah 2: Buat Package

1. Klik kanan pada Source Packages > **New** > **Java Package**
2. Buat dua package:
   - `model`: untuk kelas-kelas model data
   - `utils`: untuk kelas-kelas utilitas

### Langkah 3: Buat Kelas Buku dalam Package 'model'

1. Klik kanan pada package 'model' > **New** > **Java Class**
2. Beri nama "Buku"
3. Isi dengan kode berikut:

```java
package model;

public class Buku {
    // Private attributes - hanya dapat diakses dalam kelas ini
    private String isbn;
    private String judul;
    private String penulis;
    private int tahunTerbit;
    private boolean dipinjam;
    
    // Protected attribute - dapat diakses oleh subclass
    protected String kategori;
    
    // Public constructor
    public Buku(String isbn, String judul, String penulis, int tahunTerbit) {
        this.isbn = isbn;
        this.judul = judul;
        this.penulis = penulis;
        this.tahunTerbit = tahunTerbit;
        this.dipinjam = false;
        this.kategori = "Umum";
    }
    
    // Public methods (getters & setters)
    public String getIsbn() {
        return isbn;
    }
    
    public String getJudul() {
        return judul;
    }
    
    public void setJudul(String judul) {
        this.judul = judul;
    }
    
    public String getPenulis() {
        return penulis;
    }
    
    public void setPenulis(String penulis) {
        this.penulis = penulis;
    }
    
    public int getTahunTerbit() {
        return tahunTerbit;
    }
    
    public void setTahunTerbit(int tahunTerbit) {
        this.tahunTerbit = tahunTerbit;
    }
    
    public boolean isDipinjam() {
        return dipinjam;
    }
    
    // Public methods untuk operasi pinjam & kembalikan
    public void pinjam() {
        if (!dipinjam) {
            dipinjam = true;
            System.out.println("Buku " + judul + " berhasil dipinjam");
        } else {
            System.out.println("Buku " + judul + " sedang dipinjam");
        }
    }
    
    public void kembalikan() {
        if (dipinjam) {
            dipinjam = false;
            System.out.println("Buku " + judul + " berhasil dikembalikan");
        } else {
            System.out.println("Buku " + judul + " tidak sedang dipinjam");
        }
    }
    
    // Private method - hanya dapat digunakan dalam kelas ini
    private String generateKodeBuku() {
        return judul.substring(0, 2).toUpperCase() + "-" + tahunTerbit;
    }
    
    // Public method yang menggunakan private method
    public String getKodeBuku() {
        return generateKodeBuku();
    }
    
    // Public method untuk menampilkan info buku
    public void tampilInfo() {
        System.out.println("ISBN: " + isbn);
        System.out.println("Judul: " + judul);
        System.out.println("Penulis: " + penulis);
        System.out.println("Tahun Terbit: " + tahunTerbit);
        System.out.println("Status: " + (dipinjam ? "Dipinjam" : "Tersedia"));
        System.out.println("Kode Buku: " + getKodeBuku());
    }
}
```

### Langkah 4: Buat Subclass BukuReferensi

1. Klik kanan pada package 'model' > **New** > **Java Class**
2. Beri nama "BukuReferensi"
3. Isi dengan kode berikut:

```java
package model;

public class BukuReferensi extends Buku {
    // Private attribute tambahan
    private boolean dapatDipinjam;
    
    // Public constructor
    public BukuReferensi(String isbn, String judul, String penulis, int tahunTerbit) {
        super(isbn, judul, penulis, tahunTerbit);
        this.dapatDipinjam = false;
        this.kategori = "Referensi"; // Mengakses protected attribute dari superclass
    }
    
    // Override method pinjam
    @Override
    public void pinjam() {
        if (dapatDipinjam) {
            super.pinjam();
        } else {
            System.out.println("Maaf, buku referensi tidak dapat dipinjam");
        }
    }
    
    // Getter dan setter untuk dapatDipinjam
    public boolean isDapatDipinjam() {
        return dapatDipinjam;
    }
    
    public void setDapatDipinjam(boolean dapatDipinjam) {
        this.dapatDipinjam = dapatDipinjam;
    }
    
    // Override method tampilInfo
    @Override
    public void tampilInfo() {
        super.tampilInfo();
        System.out.println("Jenis: Buku Referensi");
        System.out.println("Dapat Dipinjam: " + (dapatDipinjam ? "Ya" : "Tidak"));
    }
}
```

### Langkah 5: Buat Kelas KatalogBuku

1. Klik kanan pada package 'model' > **New** > **Java Class**
2. Beri nama "KatalogBuku"
3. Isi dengan kode berikut:

```java
package model;

import java.util.ArrayList;

public class KatalogBuku {
    // Private static attribute - shared oleh semua instance
    private static int jumlahKatalog = 0;
    
    // Private attributes
    private ArrayList<Buku> daftarBuku;
    private final String namaPerpustakaan;
    
    // Public constructor
    public KatalogBuku(String namaPerpustakaan) {
        this.daftarBuku = new ArrayList<>();
        this.namaPerpustakaan = namaPerpustakaan;
        jumlahKatalog++;
    }
    
    // Public method untuk menambah buku
    public void tambahBuku(Buku buku) {
        daftarBuku.add(buku);
        System.out.println("Buku " + buku.getJudul() + " berhasil ditambahkan ke katalog");
    }
    
    // Public method untuk mencari buku
    public Buku cariBuku(String isbn) {
        for (Buku buku : daftarBuku) {
            if (buku.getIsbn().equals(isbn)) {
                return buku;
            }
        }
        return null;
    }
    
    // Public method untuk menampilkan semua buku
    public void tampilkanSemuaBuku() {
        System.out.println("===== KATALOG BUKU " + namaPerpustakaan + " =====");
        if (daftarBuku.isEmpty()) {
            System.out.println("Katalog kosong");
        } else {
            for (int i = 0; i < daftarBuku.size(); i++) {
                System.out.println("\nBuku #" + (i+1));
                daftarBuku.get(i).tampilInfo();
                System.out.println("-----------------------");
            }
        }
    }
    
    // Public static method untuk melihat jumlah katalog
    public static int getJumlahKatalog() {
        return jumlahKatalog;
    }
    
    // Getter untuk namaPerpustakaan (final attribute)
    public String getNamaPerpustakaan() {
        return namaPerpustakaan;
    }
}
```

### Langkah 6: Buat Kelas Utilitas

1. Klik kanan pada package 'utils' > **New** > **Java Class**
2. Beri nama "PerpustakaanUtils"
3. Isi dengan kode berikut:

```java
package utils;

import java.text.SimpleDateFormat;
import java.util.Date;

public class PerpustakaanUtils {
    // Public constants (static final)
    public static final int DURASI_PINJAM_DEFAULT = 7; // dalam hari
    public static final double DENDA_PER_HARI = 2000.0;
    
    // Private constructor - mencegah instantiasi
    private PerpustakaanUtils() {
        // Utility class tidak seharusnya diinstansiasi
    }
    
    // Public static methods
    public static String getTanggalHariIni() {
        SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy");
        return sdf.format(new Date());
    }
    
    public static String getTanggalJatuhTempo() {
        return getTanggalJatuhTempo(DURASI_PINJAM_DEFAULT);
    }
    
    public static String getTanggalJatuhTempo(int durasiHari) {
        // Implementasi sederhana
        return "Implementasi penghitungan tanggal jatuh tempo";
    }
    
    public static double hitungDenda(int hariKeterlambatan) {
        return hariKeterlambatan * DENDA_PER_HARI;
    }
}
```

### Langkah 7: Buat Kelas Main

1. Buka file main (biasanya `SistemPerpustakaan.java`)
2. Ubah kode menjadi:

```java
package sistemperpustakaan;

import model.Buku;
import model.BukuReferensi;
import model.KatalogBuku;
import utils.PerpustakaanUtils;

public class SistemPerpustakaan {
    public static void main(String[] args) {
        // Membuat katalog
        KatalogBuku katalog = new KatalogBuku("Perpustakaan Kota");
        
        // Membuat beberapa buku
        Buku buku1 = new Buku("978-1234", "Java Programming", "John Doe", 2020);
        Buku buku2 = new Buku("978-5678", "Database Design", "Jane Smith", 2019);
        BukuReferensi bukuRef = new BukuReferensi("978-9012", "Encyclopedia of Science", "Science Team", 2018);
        
        // Tambahkan buku ke katalog
        katalog.tambahBuku(buku1);
        katalog.tambahBuku(buku2);
        katalog.tambahBuku(bukuRef);
        
        // Tampilkan semua buku
        katalog.tampilkanSemuaBuku();
        
        // Coba akses method dan pinjam buku
        System.out.println("\n=== PEMINJAMAN BUKU ===");
        System.out.println("Tanggal pinjam: " + PerpustakaanUtils.getTanggalHariIni());
        System.out.println("Durasi pinjam: " + PerpustakaanUtils.DURASI_PINJAM_DEFAULT + " hari");
        
        buku1.pinjam();
        buku1.pinjam(); // Coba pinjam buku yang sudah dipinjam
        
        bukuRef.pinjam(); // Coba pinjam buku referensi
        bukuRef.setDapatDipinjam(true);
        bukuRef.pinjam(); // Coba pinjam setelah diizinkan
        
        // Kembalikan buku
        System.out.println("\n=== PENGEMBALIAN BUKU ===");
        buku1.kembalikan();
        
        // Demonstrasi static method
        System.out.println("\n=== INFO TAMBAHAN ===");
        System.out.println("Jumlah katalog yang dibuat: " + KatalogBuku.getJumlahKatalog());
        System.out.println("Contoh denda 5 hari: " + PerpustakaanUtils.hitungDenda(5));
    }
}
```

### Langkah 8: Jalankan Program

1. Klik **Run** > **Run Project**
2. Atau tekan tombol F6

### Penjelasan

Dalam contoh praktik di atas, kita telah mengimplementasikan berbagai jenis modifier:

#### Access Modifiers:
- **Private**: Atribut seperti `isbn`, `judul` di kelas `Buku` untuk encapsulation
- **Protected**: Atribut `kategori` di kelas `Buku` yang diakses oleh subclass `BukuReferensi`
- **Public**: Method seperti `pinjam()`, `kembalikan()` untuk interface public
- **Default (Package-Private)**: (Tidak digunakan dalam contoh untuk kejelasan)

#### Non-Access Modifiers:
- **Static**: Method `getJumlahKatalog()` di `KatalogBuku` dan konstanta di `PerpustakaanUtils`
- **Final**: Atribut `namaPerpustakaan` di `KatalogBuku` yang tidak dapat diubah setelah inisialisasi
- **Final Class**: (Tidak digunakan, tetapi bisa diterapkan pada `PerpustakaanUtils` untuk mencegah extends)

Contoh menunjukkan prinsip-prinsip enkapsulasi:
1. Atribut dibuat **private** untuk menyembunyikan implementasi internal
2. **Getter dan setter** digunakan untuk mengontrol akses
3. **Protected member** digunakan untuk inheritance
4. **Static member** digunakan untuk fungsi dan konstanta global
5. **Final member** digunakan untuk nilai yang tidak boleh diubah

## Rangkuman

Dalam bab ini, kita telah mempelajari:

1. **Konsep Enkapsulasi dan Information Hiding**:
   - Membungkus data dan metode dalam satu unit
   - Menyembunyikan implementasi internal
   - Menyediakan interface publik yang terkontrol

2. **Access Modifiers di Java**:
   - **Public**: Dapat diakses dari mana saja
   - **Private**: Hanya dapat diakses dalam class yang sama
   - **Protected**: Dapat diakses dalam package yang sama dan subclass
   - **Default (No-Modifier)**: Hanya dapat diakses dalam package yang sama

3. **Non-Access Modifiers**:
   - **Static**: Milik class, bukan instance
   - **Final**: Tidak dapat diubah atau di-override
   - **Abstract**: Tidak lengkap, harus dilengkapi oleh subclass
   - **Synchronized**: Thread-safe, hanya satu thread yang dapat mengakses pada satu waktu
   - **Transient**: Tidak diserialisasi
   - **Volatile**: Selalu dibaca dari main memory

4. **Best Practices**:
   - Buat atribut private
   - Gunakan getter dan setter
   - Batasi penggunaan protected
   - Gunakan static untuk utility methods
   - Gunakan final untuk constants

5. **Implementasi Praktis**:
   - Sistem perpustakaan dengan berbagai kelas dan modifier
   - Demonstrasi access control dan encapsulation

Access modifiers dan non-access modifiers merupakan komponen penting dari Java yang memungkinkan Anda membuat program yang well-encapsulated, aman, dan mudah dipelihara. Dengan memahami dan menerapkan modifier yang tepat, Anda dapat membuat desain OOP yang lebih baik dan lebih terstruktur.

## Latihan Soal

1. Jelaskan perbedaan antara enkapsulasi dan information hiding dalam pemrograman berorientasi objek!

2. Apa perbedaan antara `protected` dan `default (no-modifier)` access level? Berikan contoh kasus penggunaan yang tepat untuk masing-masing!

3. Sebutkan dan jelaskan situasi di mana Anda harus menggunakan modifier `private` untuk method!

4. Apa perbedaan antara variabel yang dideklarasikan sebagai `static final` dan hanya `final`? Berikan contoh penggunaan untuk masing-masing!

5. Perhatikan kode berikut dan identifikasi masalah terkait access modifier:
   ```java
   // File: Mahasiswa.java
   package universitas;
   
   class Mahasiswa {
       private String nim;
       String nama; // default access
       protected int usia;
       public String jurusan;
       
       public void setNim(String nim) {
           this.nim = nim;
       }
   }
   
   // File: SistemAkademik.java
   package akademik;
   
   import universitas.Mahasiswa;
   
   public class SistemAkademik {
       public void prosesData() {
           Mahasiswa mhs = new Mahasiswa(); // Error?
           mhs.setNim("12345"); // Error?
           mhs.nama = "Budi"; // Error?
           mhs.usia = 20; // Error?
           mhs.jurusan = "Informatika"; // Error?
       }
   }
   ```

6. Jelaskan mengapa kita lebih sering menggunakan utility methods sebagai `static` methods! Berikan contoh situasi di mana method sebaiknya tidak dibuat static!

7. Buatlah class `BankAccount` dengan empat access level berbeda dan jelaskan alasan penggunaan setiap access level tersebut!

8. Jelaskan kapan kita perlu menggunakan modifier `synchronized` dan dampaknya terhadap kinerja program!

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional.

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall.

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional.

5. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall.

6. Oracle. (2023). *Java Language Specification: Defining Methods*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-8.html#jls-8.4](https://docs.oracle.com/javase/specs/jls/se17/html/jls-8.html#jls-8.4)

7. Oracle. (2023). *Java Tutorial: Controlling Access to Members of a Class*. [https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html](https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html)

8. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education.

9. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media.

10. Martin, R. C. (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall.

---

[◀️ Kembali ke Tutorial #02: Inheritance dan Method Overriding](02-inheritance.md) | [Lanjut ke Tutorial #04: Constructor & Destructor pada Java ▶️](04-constructors.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
