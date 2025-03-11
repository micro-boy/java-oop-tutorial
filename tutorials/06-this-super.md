# 📘 Tutorial Java OOP #06: Memahami Kata Kunci this dan super

> *"Kata kunci this dan super adalah seperti navigasi dalam dunia objek — this menunjuk ke diri sendiri, sementara super mengarahkan ke induk yang telah memberikan warisan."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dan penggunaan kata kunci `this` dalam Java
- Memahami konsep dan penggunaan kata kunci `super` dalam Java
- Mengidentifikasi kasus-kasus penggunaan yang tepat untuk masing-masing kata kunci
- Menerapkan kata kunci `this` dan `super` untuk mengatasi masalah variable shadowing
- Menggunakan `this()` dan `super()` dalam konstruktor dengan benar
- Menghindari kesalahan umum dalam penggunaan `this` dan `super`

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Kata Kunci this](#kata-kunci-this)
   - [Pengertian this](#pengertian-this)
   - [Penggunaan this untuk Mereferensikan Instance Variabel](#penggunaan-this-untuk-mereferensikan-instance-variabel)
   - [Penggunaan this untuk Memanggil Konstruktor Lain](#penggunaan-this-untuk-memanggil-konstruktor-lain)
   - [Penggunaan this untuk Memanggil Method pada Instance Sekarang](#penggunaan-this-untuk-memanggil-method-pada-instance-sekarang)
   - [Penggunaan this sebagai Parameter Method](#penggunaan-this-sebagai-parameter-method)
   - [Penggunaan this sebagai Return Value](#penggunaan-this-sebagai-return-value)
3. [Kata Kunci super](#kata-kunci-super)
   - [Pengertian super](#pengertian-super)
   - [Penggunaan super untuk Mengakses Variabel Superclass](#penggunaan-super-untuk-mengakses-variabel-superclass)
   - [Penggunaan super untuk Memanggil Method Superclass](#penggunaan-super-untuk-memanggil-method-superclass)
   - [Penggunaan super untuk Memanggil Konstruktor Superclass](#penggunaan-super-untuk-memanggil-konstruktor-superclass)
4. [Perbedaan this vs super](#perbedaan-this-vs-super)
5. [Kasus Khusus dan Batasan](#kasus-khusus-dan-batasan)
   - [Batasan dalam Static Context](#batasan-dalam-static-context)
   - [this dan super dalam Anonymous Class](#this-dan-super-dalam-anonymous-class)
   - [this dan super dalam Nested Class](#this-dan-super-dalam-nested-class)
6. [Common Pitfalls](#common-pitfalls)
7. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
8. [Rangkuman](#rangkuman)
9. [Latihan Soal](#latihan-soal)
10. [Referensi](#referensi)

## Pendahuluan

Dalam perjalanan mempelajari pemrograman berorientasi objek di Java, kita telah membahas konsep dasar, inheritance, access modifier, konstruktor, serta method getter dan setter. Pada tutorial ini, kita akan mempelajari dua kata kunci penting dalam Java: `this` dan `super`.

Kata kunci `this` dan `super` adalah referensi khusus yang membantu navigasi dalam hierarki objek. Mereka memungkinkan akses ke variabel dan method instance saat ini (`this`) dan superclass (`super`). Memahami kedua kata kunci ini sangat penting untuk bekerja dengan inheritance dan pemrograman berorientasi objek secara efektif.

## Kata Kunci this

### Pengertian this

Kata kunci `this` adalah referensi ke objek saat ini — instance dari class di mana `this` digunakan. Secara sederhana, `this` adalah cara sebuah objek mereferensikan dirinya sendiri.

Analogi sederhana: Bayangkan Anda berada dalam sebuah kelompok dan ingin menunjuk diri sendiri, Anda akan mengatakan "saya" (dalam bahasa pemrograman, ini adalah `this`).

### Penggunaan this untuk Mereferensikan Instance Variabel

Salah satu penggunaan paling umum dari `this` adalah untuk membedakan antara instance variable (atribut) dan parameter lokal atau variabel lokal yang memiliki nama sama.

```java
public class Mahasiswa {
    private String nama; // Instance variable
    
    public void setNama(String nama) { // Parameter lokal
        // Tanpa 'this', nama di sisi kiri akan mereferensikan parameter lokal
        // bukan instance variable
        this.nama = nama; // this.nama mereferensikan instance variable
    }
}
```

Dalam contoh di atas, `this.nama` mereferensikan instance variable `nama`, sementara `nama` saja (tanpa `this`) mereferensikan parameter local yang diberikan ke method `setNama()`.

Fenomena di mana variabel lokal/parameter memiliki nama yang sama dengan instance variable disebut **variable shadowing**. Kata kunci `this` membantu mengatasi masalah ini.

**Contoh tanpa variable shadowing** (tidak memerlukan `this`):

```java
public class Pegawai {
    private String namaPegawai;
    
    public void setNamaPegawai(String inputNama) {
        namaPegawai = inputNama; // Tidak perlu this karena tidak ada variable shadowing
    }
}
```

**Contoh dengan variable shadowing** (memerlukan `this`):

```java
public class Pegawai {
    private String nama;
    
    public void setNama(String nama) {
        this.nama = nama; // Perlu this untuk membedakan instance variable dan parameter
    }
}
```

### Penggunaan this untuk Memanggil Konstruktor Lain

Kata kunci `this` juga dapat digunakan untuk memanggil konstruktor lain dalam class yang sama. Ini disebut juga **constructor chaining**.

```java
public class Produk {
    private String kode;
    private String nama;
    private double harga;
    
    // Konstruktor dengan 3 parameter
    public Produk(String kode, String nama, double harga) {
        this.kode = kode;
        this.nama = nama;
        this.harga = harga;
    }
    
    // Konstruktor dengan 2 parameter, memanggil konstruktor dengan 3 parameter
    public Produk(String kode, String nama) {
        this(kode, nama, 0.0); // Memanggil konstruktor di atas
    }
    
    // Konstruktor tanpa parameter, memanggil konstruktor dengan 2 parameter
    public Produk() {
        this("UNKN", "Produk Baru"); // Memanggil konstruktor di atas
    }
}
```

Beberapa aturan penting saat menggunakan `this()` untuk constructor chaining:
- Pemanggilan `this()` harus menjadi statement pertama dalam konstruktor
- Hanya satu pemanggilan `this()` yang diperbolehkan dalam satu konstruktor
- Recursive constructor invocation (konstruktor memanggil dirinya sendiri secara langsung atau tidak langsung) tidak diperbolehkan

### Penggunaan this untuk Memanggil Method pada Instance Sekarang

Kata kunci `this` dapat digunakan untuk memanggil method lain dalam instance yang sama.

```java
public class Lingkaran {
    private double radius;
    
    public void setRadius(double radius) {
        this.radius = radius;
        this.hitungProperties(); // Memanggil method lain dari class yang sama
    }
    
    private void hitungProperties() {
        double luas = Math.PI * radius * radius;
        double keliling = 2 * Math.PI * radius;
        System.out.println("Radius: " + radius);
        System.out.println("Luas: " + luas);
        System.out.println("Keliling: " + keliling);
    }
}
```

Sebenarnya, dalam contoh di atas, penggunaan `this` untuk memanggil method adalah opsional. Anda bisa langsung menulis `hitungProperties()` tanpa `this.` dan hasilnya akan sama. Namun, penggunaan `this` kadang-kadang membantu membuat kode lebih jelas.

### Penggunaan this sebagai Parameter Method

Kata kunci `this` juga dapat digunakan sebagai parameter saat memanggil method dari class lain. Ini berguna ketika method tersebut memerlukan referensi ke objek pemanggil.

```java
public class Mahasiswa {
    private String nama;
    private String nim;
    
    public Mahasiswa(String nama, String nim) {
        this.nama = nama;
        this.nim = nim;
    }
    
    public void daftarKelas(Kelas kelas) {
        kelas.tambahMahasiswa(this); // Passing referensi diri sendiri
    }
    
    public String getNama() {
        return nama;
    }
    
    public String getNim() {
        return nim;
    }
}

public class Kelas {
    private String kodeKelas;
    private ArrayList<Mahasiswa> daftarMahasiswa;
    
    public Kelas(String kodeKelas) {
        this.kodeKelas = kodeKelas;
        this.daftarMahasiswa = new ArrayList<>();
    }
    
    public void tambahMahasiswa(Mahasiswa mahasiswa) {
        daftarMahasiswa.add(mahasiswa);
        System.out.println("Mahasiswa " + mahasiswa.getNama() 
                          + " telah ditambahkan ke kelas " + kodeKelas);
    }
}
```

### Penggunaan this sebagai Return Value

Kata kunci `this` juga dapat digunakan sebagai return value untuk method, yang memungkinkan method chaining (pemanggilan beberapa method secara berurutan).

```java
public class StringBuilder {
    private String value;
    
    public StringBuilder() {
        this.value = "";
    }
    
    public StringBuilder append(String str) {
        this.value += str;
        return this; // Mengembalikan instance saat ini
    }
    
    public StringBuilder appendSpace() {
        this.value += " ";
        return this; // Mengembalikan instance saat ini
    }
    
    public String build() {
        return this.value;
    }
}
```

Penggunaan:

```java
StringBuilder builder = new StringBuilder();
String result = builder.append("Hello")
                      .appendSpace()
                      .append("World")
                      .appendSpace()
                      .append("!")
                      .build();
System.out.println(result); // Output: Hello World !
```

## Kata Kunci super

### Pengertian super

Kata kunci `super` adalah referensi ke superclass (parent class) dari class saat ini. Ini memungkinkan subclass untuk mengakses anggota (variabel dan method) dari superclass yang mungkin telah ditutupi atau di-override.

Analogi sederhana: Jika `this` adalah "saya", maka `super` adalah "orang tua saya".

### Penggunaan super untuk Mengakses Variabel Superclass

Kata kunci `super` berguna ketika subclass memiliki variabel dengan nama yang sama dengan variabel di superclass (variable shadowing).

```java
public class Kendaraan {
    protected String merek = "Merek Kendaraan";
    
    public void tampilMerek() {
        System.out.println("Merek kendaraan: " + merek);
    }
}

public class Mobil extends Kendaraan {
    private String merek = "Merek Mobil"; // Nama variabel sama dengan superclass
    
    public void tampilMerek() {
        System.out.println("Merek kendaraan dari superclass: " + super.merek);
        System.out.println("Merek mobil dari subclass: " + this.merek);
        System.out.println("Merek mobil tanpa kualifikasi: " + merek); // Sama dengan this.merek
    }
}
```

Tanpa kata kunci `super`, subclass hanya bisa mengakses variabelnya sendiri yang memiliki nama yang sama, bukan variabel dari superclass.

### Penggunaan super untuk Memanggil Method Superclass

Kata kunci `super` juga digunakan untuk memanggil method dari superclass yang telah di-override oleh subclass.

```java
public class Hewan {
    public void suara() {
        System.out.println("Hewan bersuara");
    }
}

public class Kucing extends Hewan {
    @Override
    public void suara() {
        super.suara(); // Memanggil method suara() dari class Hewan
        System.out.println("Kucing: Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        Kucing kucing = new Kucing();
        kucing.suara();
    }
}
```

Output:
```
Hewan bersuara
Kucing: Meow!
```

Ini berguna ketika Anda ingin memperluas fungsionalitas method yang diwarisi, alih-alih menggantinya sepenuhnya.

### Penggunaan super untuk Memanggil Konstruktor Superclass

Kata kunci `super` dapat digunakan dalam konstruktor subclass untuk memanggil konstruktor dari superclass.

```java
public class Kendaraan {
    protected String merek;
    protected int tahun;
    
    public Kendaraan(String merek, int tahun) {
        this.merek = merek;
        this.tahun = tahun;
        System.out.println("Konstruktor Kendaraan dipanggil");
    }
}

public class Mobil extends Kendaraan {
    private int jumlahPintu;
    
    public Mobil(String merek, int tahun, int jumlahPintu) {
        super(merek, tahun); // Memanggil konstruktor Kendaraan
        this.jumlahPintu = jumlahPintu;
        System.out.println("Konstruktor Mobil dipanggil");
    }
    
    public void tampilInfo() {
        System.out.println("Merek: " + merek);
        System.out.println("Tahun: " + tahun);
        System.out.println("Jumlah Pintu: " + jumlahPintu);
    }
}
```

Beberapa aturan penting saat menggunakan `super()` untuk memanggil konstruktor superclass:
- Pemanggilan `super()` harus menjadi statement pertama dalam konstruktor subclass
- Jika konstruktor subclass tidak secara eksplisit memanggil konstruktor superclass, Java akan secara otomatis memanggil konstruktor default (tanpa parameter) dari superclass
- Jika superclass tidak memiliki konstruktor default, maka subclass harus secara eksplisit memanggil salah satu konstruktor yang tersedia menggunakan `super()`

## Perbedaan this vs super

Berikut adalah perbandingan langsung antara kata kunci `this` dan `super`:

| Aspek | `this` | `super` |
|-------|--------|---------|
| Referensi | Mereferensikan instance saat ini dari class | Mereferensikan superclass dari class saat ini |
| Memanggil Konstruktor | `this()` memanggil konstruktor lain dalam class yang sama | `super()` memanggil konstruktor dari superclass |
| Mengakses Variabel | `this.variabel` mereferensikan variabel instance dari class saat ini | `super.variabel` mereferensikan variabel dari superclass |
| Memanggil Method | `this.method()` memanggil method dari class saat ini | `super.method()` memanggil method dari superclass |
| Penggunaan | Mengatasi variable shadowing, constructor chaining, method chaining | Mengakses anggota superclass yang di-override, memanggil konstruktor superclass |
| Lokasi Penggunaan | Tidak dapat digunakan dalam static context | Tidak dapat digunakan dalam static context |

## Kasus Khusus dan Batasan

### Batasan dalam Static Context

Kedua kata kunci `this` dan `super` tidak dapat digunakan dalam static context (static method atau static block). Ini karena static member terkait dengan class, bukan dengan instance tertentu dari class.

```java
public class Contoh {
    private static int staticVar = 10;
    private int instanceVar = 20;
    
    public static void staticMethod() {
        // Kode berikut akan menyebabkan error kompilasi
        // System.out.println(this.instanceVar);
        // System.out.println(super.toString());
        
        // Yang benar:
        System.out.println(staticVar); // OK
        System.out.println(Contoh.staticVar); // OK
    }
    
    public void instanceMethod() {
        // Semua kode berikut valid:
        System.out.println(this.instanceVar);
        System.out.println(this.staticVar);
        System.out.println(super.toString());
    }
}
```

### this dan super dalam Anonymous Class

Dalam anonymous class, `this` mereferensikan instance anonymous class itu sendiri, bukan class enclosing. Untuk mengakses instance dari enclosing class, Anda perlu menggunakan kualifikasi tambahan.

```java
public class OuterClass {
    private int outerVar = 10;
    
    public void testMethod() {
        // Anonymous inner class
        Runnable r = new Runnable() {
            private int innerVar = 20;
            
            @Override
            public void run() {
                System.out.println("Inner var: " + this.innerVar); // 'this' mereferensikan anonymous class
                System.out.println("Outer var: " + OuterClass.this.outerVar); // Mengakses enclosing class
            }
        };
        
        r.run();
    }
}
```

### this dan super dalam Nested Class

Java memungkinkan definisi class di dalam class lain (nested class). Ada beberapa jenis nested class, dan penggunaan `this` dan `super` bervariasi:

**Inner Class (Non-static Nested Class)**:
```java
public class Outer {
    private int outerVar = 10;
    
    public class Inner {
        private int innerVar = 20;
        
        public void display() {
            System.out.println("Outer var: " + Outer.this.outerVar); // Referensi ke enclosing instance
            System.out.println("Inner var: " + this.innerVar); // Referensi ke inner instance
        }
    }
}
```

**Static Nested Class**:
```java
public class Outer {
    private static int staticOuterVar = 10;
    private int instanceOuterVar = 20;
    
    public static class StaticNested {
        private int nestedVar = 30;
        
        public void display() {
            System.out.println("Static outer var: " + staticOuterVar); // OK
            // System.out.println("Instance outer var: " + instanceOuterVar); // Error: tidak dapat mengakses non-static
            System.out.println("Nested var: " + this.nestedVar); // Referensi ke nested instance
        }
    }
}
```

## Common Pitfalls

Berikut adalah beberapa kesalahan umum saat menggunakan `this` dan `super`:

1. **Memanggil `this()` dan `super()` secara bersamaan**: Anda tidak dapat memanggil `this()` dan `super()` dalam konstruktor yang sama, karena keduanya harus menjadi statement pertama.

   ```java
   public class IniSalah extends SuperClass {
       public IniSalah() {
           super(); // OK
           this(10); // Error: Call to this must be first statement in constructor
       }
       
       public IniSalah(int x) {
           this(); // OK
           super(); // Error: Call to super must be first statement in constructor
       }
   }
   ```

2. **Penggunaan `this` dan `super` dalam static context**:

   ```java
   public class IniSalah {
       private int instanceVar = 10;
       
       public static void staticMethod() {
           System.out.println(this.instanceVar); // Error: 'this' cannot be used in static context
       }
   }
   ```

3. **Recursive constructor calls**:

   ```java
   public class IniSalah {
       public IniSalah() {
           this(); // Error: Recursive constructor invocation
       }
   }
   ```

4. **Tidak memanggil konstruktor superclass yang sesuai**:

   ```java
   public class SuperClass {
       // Tidak ada default constructor
       public SuperClass(int x) {
           // konstruktor dengan parameter
       }
   }
   
   public class IniSalah extends SuperClass {
       public IniSalah() {
           // Error: Tidak ada panggilan eksplisit ke konstruktor SuperClass,
           // dan SuperClass tidak memiliki default constructor
       }
   }
   ```

5. **Shadowing variabel dan method tanpa sadar**:

   ```java
   public class SuperClass {
       protected int value = 10;
       
       public void setValue(int value) {
           this.value = value;
       }
   }
   
   public class SubClass extends SuperClass {
       private int value = 20; // Shadowing variable dari SuperClass
       
       @Override
       public void setValue(int value) {
           this.value = value; // Hanya mengubah value di SubClass, bukan di SuperClass
       }
       
       public void printValues() {
           System.out.println("SubClass value: " + this.value);
           System.out.println("SuperClass value: " + super.value);
       }
   }
   ```

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep `this` dan `super` dengan membuat program sederhana menggunakan NetBeans IDE.

### Skenario: Sistem Manajemen Karyawan

Kita akan membuat sistem manajemen karyawan sederhana dengan hierarki kelas untuk mendemonstrasikan penggunaan `this` dan `super`.

### Langkah 1: Buat Project Baru

1. Buka NetBeans IDE
2. Pilih **File** > **New Project**
3. Pilih **Java** > **Java Application** > **Next**
4. Beri nama project "SistemKaryawan" dan tentukan lokasi penyimpanan
5. Klik **Finish**

### Langkah 2: Buat Kelas Dasar Karyawan

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Karyawan"
3. Isi dengan kode berikut:

```java
package sistemkaryawan;

public class Karyawan {
    // Atribut
    protected String id;
    protected String nama;
    protected double gajiPokok;
    
    // Konstruktor
    public Karyawan(String id, String nama, double gajiPokok) {
        this.id = id;
        this.nama = nama;
        this.gajiPokok = gajiPokok;
        System.out.println("Konstruktor Karyawan dipanggil");
    }
    
    // Konstruktor dengan default gaji
    public Karyawan(String id, String nama) {
        this(id, nama, 4000000); // Memanggil konstruktor lain menggunakan this()
    }
    
    // Method untuk menghitung gaji
    public double hitungGaji() {
        return gajiPokok;
    }
    
    // Method untuk menampilkan informasi
    public void tampilInfo() {
        System.out.println("ID Karyawan: " + id);
        System.out.println("Nama: " + nama);
        System.out.println("Gaji Pokok: " + gajiPokok);
        System.out.println("Total Gaji: " + hitungGaji());
    }
}
```

### Langkah 3: Buat Kelas Manajer

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Manajer"
3. Isi dengan kode berikut:

```java
package sistemkaryawan;

public class Manajer extends Karyawan {
    // Atribut tambahan
    private double tunjangan;
    private String departemen;
    
    // Konstruktor
    public Manajer(String id, String nama, double gajiPokok, double tunjangan, String departemen) {
        super(id, nama, gajiPokok); // Memanggil konstruktor superclass
        this.tunjangan = tunjangan;
        this.departemen = departemen;
        System.out.println("Konstruktor Manajer dipanggil");
    }
    
    // Method yang mengoverride hitungGaji di superclass
    @Override
    public double hitungGaji() {
        return super.hitungGaji() + tunjangan; // Memanggil method superclass
    }
    
    // Method yang mengoverride tampilInfo di superclass
    @Override
    public void tampilInfo() {
        super.tampilInfo(); // Memanggil method superclass
        System.out.println("Tunjangan: " + tunjangan);
        System.out.println("Departemen: " + departemen);
    }
    
    // Method spesifik untuk Manajer
    public void aturRapat(String agenda) {
        System.out.println("Manajer " + this.nama + " mengatur rapat dengan agenda: " + agenda);
    }
}
```

### Langkah 4: Buat Kelas Sales

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Sales"
3. Isi dengan kode berikut:

```java
package sistemkaryawan;

public class Sales extends Karyawan {
    // Atribut tambahan
    private double komisi;
    private int jumlahPenjualan;
    
    // Konstruktor
    public Sales(String id, String nama, double gajiPokok, double komisi) {
        super(id, nama, gajiPokok); // Memanggil konstruktor superclass
        this.komisi = komisi;
        this.jumlahPenjualan = 0;
        System.out.println("Konstruktor Sales dipanggil");
    }
    
    // Method untuk menambah penjualan
    public Sales tambahPenjualan(int jumlah) {
        this.jumlahPenjualan += jumlah;
        return this; // Mengembalikan instance ini untuk method chaining
    }
    
    // Method yang mengoverride hitungGaji di superclass
    @Override
    public double hitungGaji() {
        return super.hitungGaji() + (komisi * jumlahPenjualan); // Memanggil method superclass
    }
    
    // Method yang mengoverride tampilInfo di superclass
    @Override
    public void tampilInfo() {
        super.tampilInfo(); // Memanggil method superclass
        System.out.println("Komisi per penjualan: " + komisi);
        System.out.println("Jumlah Penjualan: " + jumlahPenjualan);
        System.out.println("Total Komisi: " + (komisi * jumlahPenjualan));
    }
}
```

### Langkah 5: Buat Kelas Builder sebagai Contoh Method Chaining

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "KaryawanBuilder"
3. Isi dengan kode berikut:

```java
package sistemkaryawan;

// Contoh penggunaan return this untuk method chaining
public class KaryawanBuilder {
    private String id;
    private String nama;
    private double gajiPokok;
    private String departemen;
    private double tunjangan;
    private double komisi;
    
    public KaryawanBuilder() {
        // Inisialisasi default
        this.id = "K000";
        this.nama = "Unnamed";
        this.gajiPokok = 4000000;
    }
    
    public KaryawanBuilder setId(String id) {
        this.id = id;
        return this; // Mengembalikan instance saat ini untuk chaining
    }
    
    public KaryawanBuilder setNama(String nama) {
        this.nama = nama;
        return this;
    }
    
    public KaryawanBuilder setGajiPokok(double gajiPokok) {
        this.gajiPokok = gajiPokok;
        return this;
    }
    
    public KaryawanBuilder setDepartemen(String departemen) {
        this.departemen = departemen;
        return this;
    }
    
    public KaryawanBuilder setTunjangan(double tunjangan) {
        this.tunjangan = tunjangan;
        return this;
    }
    
    public KaryawanBuilder setKomisi(double komisi) {
        this.komisi = komisi;
        return this;
    }
    
    public Karyawan buildKaryawan() {
        return new Karyawan(id, nama, gajiPokok);
    }
    
    public Manajer buildManajer() {
        if (departemen == null) {
            throw new IllegalStateException("Departemen harus diatur untuk Manajer");
        }
        return new Manajer(id, nama, gajiPokok, tunjangan, departemen);
    }
    
    public Sales buildSales() {
        if (komisi <= 0) {
            throw new IllegalStateException("Komisi harus diatur untuk Sales");
        }
        return new Sales(id, nama, gajiPokok, komisi);
    }
}
```

### Langkah 6: Buat Inner Class sebagai Contoh Penggunaan this pada Nested Class

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "KaryawanReport"
3. Isi dengan kode berikut:

```java
package sistemkaryawan;

import java.util.ArrayList;
import java.util.List;

public class KaryawanReport {
    private List<Karyawan> daftarKaryawan;
    private String namaPerusahaan;
    
    public KaryawanReport(String namaPerusahaan) {
        this.daftarKaryawan = new ArrayList<>();
        this.namaPerusahaan = namaPerusahaan;
    }
    
    public void tambahKaryawan(Karyawan karyawan) {
        this.daftarKaryawan.add(karyawan);
    }
    
    // Inner class yang menggunakan this dan outer this
    public class ReportGenerator {
        private String formatTanggal;
        
        public ReportGenerator(String formatTanggal) {
            this.formatTanggal = formatTanggal;
        }
        
        public void generateReport() {
            System.out.println("===== LAPORAN KARYAWAN =====");
            System.out.println("Perusahaan: " + KaryawanReport.this.namaPerusahaan); // Mengakses outer class
            System.out.println("Format Tanggal: " + this.formatTanggal); // Mengakses inner class
            System.out.println("Jumlah Karyawan: " + KaryawanReport.this.daftarKaryawan.size());
            System.out.println("------------------------");
            
            for (Karyawan k : KaryawanReport.this.daftarKaryawan) {
                k.tampilInfo();
                System.out.println("------------------------");
            }
        }
    }
    
    // Method untuk membuat ReportGenerator
    public ReportGenerator createReportGenerator(String formatTanggal) {
        return this.new ReportGenerator(formatTanggal);
    }
}
```

### Langkah 7: Buat Kelas Main

1. Buka file main (biasanya `SistemKaryawan.java`)
2. Ubah kode menjadi:

```java
package sistemkaryawan;

public class SistemKaryawan {
    public static void main(String[] args) {
        // Demonstrasi Konstruktor Chaining dan Inheritance
        System.out.println("=== Membuat objek Karyawan ===");
        Karyawan karyawan1 = new Karyawan("K001", "Budi");
        
        System.out.println("\n=== Membuat objek Manajer ===");
        Manajer manajer1 = new Manajer("M001", "Diana", 8000000, 3000000, "IT");
        
        System.out.println("\n=== Membuat objek Sales ===");
        Sales sales1 = new Sales("S001", "Eko", 4500000, 100000);
        
        // Demonstrasi Override Method dan super
        System.out.println("\n=== Informasi Karyawan ===");
        karyawan1.tampilInfo();
        
        System.out.println("\n=== Informasi Manajer ===");
        manajer1.tampilInfo();
        manajer1.aturRapat("Review Proyek");
        
        System.out.println("\n=== Informasi Sales ===");
        sales1.tambahPenjualan(5).tambahPenjualan(3); // Demonstrasi method chaining
        sales1.tampilInfo();
        
        // Demonstrasi Builder Pattern (penggunaan return this)
        System.out.println("\n=== Menggunakan KaryawanBuilder ===");
        KaryawanBuilder builder = new KaryawanBuilder();
        
        Manajer manajer2 = builder.setId("M002")
                                .setNama("Farhan")
                                .setGajiPokok(9000000)
                                .setTunjangan(4000000)
                                .setDepartemen("Finance")
                                .buildManajer();
        
        Sales sales2 = builder.setId("S002")
                            .setNama("Gita")
                            .setGajiPokok(4800000)
                            .setKomisi(150000)
                            .buildSales();
        
        manajer2.tampilInfo();
        System.out.println();
        sales2.tampilInfo();
        
        // Demonstrasi Inner Class dan this pada Nested Class
        System.out.println("\n=== Menggunakan Inner Class ReportGenerator ===");
        KaryawanReport report = new KaryawanReport("PT Example Indonesia");
        report.tambahKaryawan(karyawan1);
        report.tambahKaryawan(manajer1);
        report.tambahKaryawan(sales1);
        report.tambahKaryawan(manajer2);
        report.tambahKaryawan(sales2);
        
        KaryawanReport.ReportGenerator generator = report.createReportGenerator("dd/MM/yyyy");
        generator.generateReport();
    }
}
```

### Langkah 8: Jalankan Program

1. Klik **Run** > **Run Project**
2. Atau tekan tombol F6

### Penjelasan

Dalam contoh praktik di atas, kita telah mengimplementasikan berbagai penggunaan kata kunci `this` dan `super`:

1. **Penggunaan `this` untuk mereferensikan instance variable**:
   - `this.id = id` di konstruktor `Karyawan`
   - `this.tunjangan = tunjangan` di konstruktor `Manajer`

2. **Penggunaan `this()` untuk constructor chaining**:
   - `this(id, nama, 4000000)` di konstruktor `Karyawan`

3. **Penggunaan `super()` untuk memanggil konstruktor superclass**:
   - `super(id, nama, gajiPokok)` di konstruktor `Manajer` dan `Sales`

4. **Penggunaan `super` untuk memanggil method superclass**:
   - `super.hitungGaji()` di method `hitungGaji()` pada `Manajer` dan `Sales`
   - `super.tampilInfo()` di method `tampilInfo()` pada `Manajer` dan `Sales`

5. **Penggunaan `this` sebagai return value untuk method chaining**:
   - `return this` di method `tambahPenjualan()` pada `Sales`
   - Semua method setter di `KaryawanBuilder`

6. **Penggunaan `this` dalam nested class**:
   - `this.formatTanggal` mereferensikan variabel di inner class `ReportGenerator`
   - `KaryawanReport.this.namaPerusahaan` mereferensikan variabel di outer class `KaryawanReport`

## Rangkuman

Dalam bab ini, kita telah mempelajari:

1. **Kata Kunci `this`**:
   - Mereferensikan instance saat ini dari class
   - Mengatasi variable shadowing
   - Memanggil konstruktor lain dalam class yang sama
   - Memanggil method pada instance yang sama
   - Digunakan sebagai parameter method
   - Digunakan sebagai return value untuk method chaining

2. **Kata Kunci `super`**:
   - Mereferensikan superclass dari class saat ini
   - Mengakses variabel superclass yang di-shadow oleh variabel subclass
   - Memanggil method superclass yang di-override oleh subclass
   - Memanggil konstruktor superclass

3. **Perbedaan dan Batasan**:
   - Tidak dapat digunakan dalam static context
   - Pemanggilan `this()` dan `super()` harus menjadi statement pertama dalam konstruktor
   - Hanya satu pemanggilan yang diperbolehkan dalam satu konstruktor

4. **Kasus Khusus**:
   - Penggunaan dalam anonymous class
   - Penggunaan dalam nested class

5. **Common Pitfalls**:
   - Memanggil `this()` dan `super()` bersamaan
   - Penggunaan dalam static context
   - Recursive constructor calls
   - Tidak memanggil konstruktor superclass yang sesuai
   - Shadowing variabel dan method tanpa sadar

Kata kunci `this` dan `super` adalah komponen penting dalam navigasi hierarki objek Java. Dengan memahami cara mereka bekerja, Anda dapat menulis kode yang lebih bersih, lebih terstruktur, dan lebih mudah dipelihara.

## Latihan Soal

1. Jelaskan apa yang dimaksud dengan variable shadowing dan bagaimana kata kunci `this` membantu mengatasi masalah ini.

2. Apa perbedaan antara penggunaan `this()` dan `super()` dalam konstruktor? Berikan contoh kode yang menunjukkan penggunaan keduanya.

3. Mengapa pemanggilan `this()` atau `super()` harus menjadi statement pertama dalam konstruktor?

4. Anda memiliki class `Hewan` dengan method `makan()`. Subclass `Kucing` juga memiliki method `makan()` yang meng-override method di superclass. Bagaimana cara memanggil method `makan()` dari `Hewan` di dalam method `makan()` dari `Kucing`?

5. Perhatikan kode berikut:
   ```java
   public class A {
       private int value = 10;
       
       public int getValue() {
           return value;
       }
   }
   
   public class B extends A {
       private int value = 20;
       
       public int getValue() {
           return value;
       }
       
       public void printValues() {
           System.out.println(value);
           System.out.println(this.value);
           System.out.println(super.value); // Apakah ini valid?
           System.out.println(this.getValue());
           System.out.println(super.getValue());
       }
   }
   ```
   Apa output dari method `printValues()`? Jika ada error, perbaiki kode tersebut.

6. Buatlah class `Bentuk` dengan atribut `warna` dan `luas`, konstruktor yang sesuai, serta method `hitungLuas()` yang mengembalikan 0. Kemudian buat class `Lingkaran` yang mewarisi `Bentuk` dengan atribut tambahan `radius`. Override method `hitungLuas()` dan gunakan kata kunci `super` untuk mengakses atribut dari class `Bentuk`.

7. Implementasikan builder pattern untuk class `Person` dengan atribut `name`, `age`, `address`, dan `phone`. Gunakan `this` sebagai return value untuk method chaining.

8. Apa yang terjadi jika Anda mencoba menggunakan `this` atau `super` dalam static method? Jelaskan alasannya.

9. Perhatikan kode berikut:
   ```java
   public class Outer {
       private int outerValue = 10;
       
       public class Inner {
           private int innerValue = 20;
           
           public void display() {
               int localValue = 30;
               
               System.out.println(outerValue);
               System.out.println(this.innerValue);
               System.out.println(Outer.this.outerValue);
           }
       }
   }
   ```
   Jelaskan perbedaan antara `outerValue`, `this.innerValue`, dan `Outer.this.outerValue` dalam method `display()`.

10. Buatlah class `BankAccount` dengan method `transfer(BankAccount destination, double amount)` yang menggunakan `this` sebagai parameter untuk method lain.

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional.

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall.

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional.

5. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall.

6. Oracle. (2023). *Java Language Specification: This*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.8.3](https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.8.3)

7. Oracle. (2023). *Java Language Specification: Super*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.11.2](https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.11.2)

8. Oracle. (2023). *Java Tutorial: Using the this Keyword*. [https://docs.oracle.com/javase/tutorial/java/javaOO/thiskey.html](https://docs.oracle.com/javase/tutorial/java/javaOO/thiskey.html)

9. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education.

10. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media.

---

[◀️ Kembali ke Tutorial #05: Menggunakan Method Setter dan Getter](05-setters-getters.md) | [Lanjut ke Tutorial #07: Memahami Konsep Polimorfisme di Java ▶️](07-polymorphism.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
