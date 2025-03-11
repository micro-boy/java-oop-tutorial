# 📘 Tutorial Java OOP #05: Menggunakan Method Setter dan Getter

> *"Akses langsung ke atribut adalah seperti membiarkan orang lain langsung mengakses isi lemari Anda; menggunakan getter dan setter adalah seperti meminta izin dan mengikuti prosedur yang tepat."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep enkapsulasi dan pentingnya dalam pemrograman berorientasi objek
- Menjelaskan fungsi dan manfaat method setter dan getter
- Mengimplementasikan method setter dan getter sesuai dengan konvensi JavaBeans
- Menerapkan validasi data dalam method setter
- Membuat method getter yang aman untuk berbagai tipe data
- Mengimplementasikan property dengan akses terkontrol dalam desain class

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Konsep Enkapsulasi](#konsep-enkapsulasi)
3. [Method Getter dan Setter](#method-getter-dan-setter)
   - [Apa itu Method Getter?](#apa-itu-method-getter)
   - [Apa itu Method Setter?](#apa-itu-method-setter)
   - [Mengapa Menggunakan Getter dan Setter?](#mengapa-menggunakan-getter-dan-setter)
4. [Konvensi Penamaan (JavaBeans)](#konvensi-penamaan-javabeans)
5. [Implementasi Getter dan Setter](#implementasi-getter-dan-setter)
   - [Getter dan Setter Dasar](#getter-dan-setter-dasar)
   - [Validasi Data dalam Setter](#validasi-data-dalam-setter)
   - [Getter untuk Berbagai Tipe Data](#getter-untuk-berbagai-tipe-data)
   - [Boolean Getter: isX() vs getX()](#boolean-getter-isx-vs-getx)
6. [Property Read-Only dan Write-Only](#property-read-only-dan-write-only)
7. [Mutable vs Immutable Objects](#mutable-vs-immutable-objects)
8. [Best Practices](#best-practices)
9. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
10. [Rangkuman](#rangkuman)
11. [Latihan Soal](#latihan-soal)
12. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari tentang constructor dan destructor, yang merupakan bagian penting dalam siklus hidup objek. Pada tutorial ini, kita akan membahas cara mengontrol akses ke atribut (property) objek melalui method khusus yang disebut "getter" dan "setter".

Method getter dan setter adalah bagian fundamental dari konsep enkapsulasi dalam pemrograman berorientasi objek. Mereka memungkinkan kita mengontrol bagaimana data dalam objek diakses dan dimodifikasi, sekaligus menyembunyikan implementasi internal dari client code.

## Konsep Enkapsulasi

**Enkapsulasi** adalah salah satu dari empat pilar utama pemrograman berorientasi objek, yang bertujuan untuk menyembunyikan detail implementasi dan internal state objek dari dunia luar. Hanya fungsionalitas publik yang terdefinisi dengan baik yang dapat diakses.

Prinsip enkapsulasi meliputi:

1. **Penyembunyian Data (Data Hiding)**: Membatasi akses langsung ke atribut objek
2. **Kontrol Akses**: Menyediakan method publik tertentu untuk mengakses dan memodifikasi data
3. **Validasi Data**: Memastikan data yang disimpan selalu valid
4. **Fleksibilitas Implementasi**: Memungkinkan perubahan implementasi internal tanpa memengaruhi code yang menggunakan class

Dalam Java, enkapsulasi biasanya dicapai dengan:
- Menjadikan atribut `private`
- Menyediakan method `public` untuk mengakses (getter) dan mengubah (setter) atribut

```java
public class Mahasiswa {
    // Atribut private - tidak dapat diakses langsung dari luar
    private String nama;
    private String nim;
    private double ipk;
    
    // Getter dan setter publik - mengontrol akses ke atribut
    public String getNama() {
        return nama;
    }
    
    public void setNama(String nama) {
        this.nama = nama;
    }
    
    // Getter dan setter lainnya...
}
```

## Method Getter dan Setter

### Apa itu Method Getter?

**Method Getter** (accessor) adalah method yang digunakan untuk mengambil nilai atribut objek. Method ini tidak mengubah state objek dan biasanya mengembalikan nilai atribut.

### Apa itu Method Setter?

**Method Setter** (mutator) adalah method yang digunakan untuk mengubah nilai atribut objek. Method ini menerima parameter yang akan menjadi nilai baru atribut.

### Mengapa Menggunakan Getter dan Setter?

Ada beberapa alasan untuk menggunakan getter dan setter daripada mengakses atribut secara langsung:

1. **Kontrol Akses**: Memungkinkan Anda membatasi akses ke atribut (misalnya, read-only property)

2. **Validasi Data**: Memungkinkan Anda memvalidasi data sebelum mengubah atribut
   ```java
   public void setUmur(int umur) {
       if (umur < 0 || umur > 150) {
           throw new IllegalArgumentException("Umur harus antara 0-150");
       }
       this.umur = umur;
   }
   ```

3. **Encapsulation**: Menyembunyikan implementasi dan memungkinkan perubahan internal tanpa memengaruhi client code
   ```java
   // Versi 1: Menyimpan nama depan dan belakang terpisah
   private String namaDepan;
   private String namaBelakang;
   
   public String getNama() {
       return namaDepan + " " + namaBelakang;
   }
   
   // Versi 2: Dapat diubah untuk menyimpan nama lengkap tanpa mengubah client code
   private String nama;
   
   public String getNama() {
       return nama;
   }
   ```

4. **Lazy Initialization**: Menunda pembuatan objek yang mahal hingga benar-benar diperlukan
   ```java
   private List<Item> items;
   
   public List<Item> getItems() {
       if (items == null) {
           items = new ArrayList<>();
       }
       return items;
   }
   ```

5. **Synchronization**: Mengontrol akses ke atribut dalam lingkungan multi-thread
   ```java
   private int counter;
   
   public synchronized void incrementCounter() {
       counter++;
   }
   
   public synchronized int getCounter() {
       return counter;
   }
   ```

6. **Debugging**: Memungkinkan Anda melacak akses dan modifikasi atribut
   ```java
   public void setSaldo(double saldo) {
       System.out.println("Saldo diubah dari " + this.saldo + " menjadi " + saldo);
       this.saldo = saldo;
   }
   ```

## Konvensi Penamaan (JavaBeans)

Java memiliki konvensi yang disebut **JavaBeans** untuk penamaan getter dan setter. Konvensi ini sangat penting karena banyak framework Java (seperti Spring, Hibernate, Jackson) bergantung padanya.

Konvensi penamaan JavaBeans:

1. **Getter**:
   - Dimulai dengan prefix `get` diikuti dengan nama atribut (huruf pertama kapital)
   - Untuk tipe data boolean, sering dimulai dengan `is` diikuti dengan nama atribut
   - Tidak menerima parameter
   - Return type harus sesuai dengan tipe atribut

2. **Setter**:
   - Dimulai dengan prefix `set` diikuti dengan nama atribut (huruf pertama kapital)
   - Menerima satu parameter dengan tipe yang sesuai dengan atribut
   - Return type biasanya `void`

Contoh:
```java
public class Pegawai {
    private String nama;
    private int umur;
    private double gaji;
    private boolean aktif;
    
    // Getter
    public String getNama() {
        return nama;
    }
    
    public int getUmur() {
        return umur;
    }
    
    public double getGaji() {
        return gaji;
    }
    
    public boolean isAktif() {  // Perhatikan prefix 'is' untuk boolean
        return aktif;
    }
    
    // Setter
    public void setNama(String nama) {
        this.nama = nama;
    }
    
    public void setUmur(int umur) {
        this.umur = umur;
    }
    
    public void setGaji(double gaji) {
        this.gaji = gaji;
    }
    
    public void setAktif(boolean aktif) {
        this.aktif = aktif;
    }
}
```

## Implementasi Getter dan Setter

### Getter dan Setter Dasar

Implementasi dasar getter dan setter sangat sederhana:

```java
public class Produk {
    private String nama;
    private double harga;
    
    // Getter untuk nama
    public String getNama() {
        return nama;
    }
    
    // Setter untuk nama
    public void setNama(String nama) {
        this.nama = nama;
    }
    
    // Getter untuk harga
    public double getHarga() {
        return harga;
    }
    
    // Setter untuk harga
    public void setHarga(double harga) {
        this.harga = harga;
    }
}
```

### Validasi Data dalam Setter

Salah satu keuntungan utama dari setter adalah kemampuan untuk memvalidasi data sebelum menetapkannya ke atribut. Ini membantu menjaga integritas objek.

```java
public class Mahasiswa {
    private String nama;
    private String nim;
    private double ipk;
    
    // Setter dengan validasi
    public void setNama(String nama) {
        if (nama == null || nama.trim().isEmpty()) {
            throw new IllegalArgumentException("Nama tidak boleh kosong");
        }
        this.nama = nama;
    }
    
    public void setNim(String nim) {
        if (nim == null || !nim.matches("[A-Z]\\d{5}")) {
            throw new IllegalArgumentException("NIM harus berupa 1 huruf kapital diikuti 5 digit angka");
        }
        this.nim = nim;
    }
    
    public void setIpk(double ipk) {
        if (ipk < 0 || ipk > 4.0) {
            throw new IllegalArgumentException("IPK harus antara 0.0 - 4.0");
        }
        this.ipk = ipk;
    }
    
    // Getter standar
    public String getNama() {
        return nama;
    }
    
    public String getNim() {
        return nim;
    }
    
    public double getIpk() {
        return ipk;
    }
}
```

### Getter untuk Berbagai Tipe Data

Implementasi getter dapat bervariasi tergantung pada tipe data atribut, terutama untuk tipe referensi (seperti array, collection, object).

#### Getter untuk Primitive Type

Untuk tipe data primitif (int, double, boolean, dll), getter biasanya hanya mengembalikan nilai secara langsung:

```java
private int umur;

public int getUmur() {
    return umur;
}
```

#### Getter untuk Reference Type

Untuk tipe referensi, Anda perlu berhati-hati tentang ekspos referensi objek internal. Jika Anda mengembalikan referensi langsung ke objek yang dapat dimodifikasi, client dapat mengubah objek tersebut tanpa melalui setter.

**Pendekatan 1: Defensive Copying (untuk mutable objects)**

```java
private Date tanggalLahir; // Date adalah mutable object

// KURANG AMAN: Mengembalikan referensi langsung
public Date getTanggalLahir() {
    return tanggalLahir; // Client dapat memodifikasi tanggalLahir secara langsung
}

// LEBIH AMAN: Defensive copy
public Date getTanggalLahir() {
    return tanggalLahir != null ? new Date(tanggalLahir.getTime()) : null;
}

public void setTanggalLahir(Date tanggalLahir) {
    this.tanggalLahir = tanggalLahir != null ? new Date(tanggalLahir.getTime()) : null;
}
```

**Pendekatan 2: Unmodifiable Wrapper (untuk collections)**

```java
private List<String> hobi;

// KURANG AMAN: Mengembalikan referensi langsung
public List<String> getHobi() {
    return hobi; // Client dapat memodifikasi list secara langsung
}

// LEBIH AMAN: Unmodifiable wrapper
public List<String> getHobi() {
    return Collections.unmodifiableList(hobi);
}

// Menyediakan method khusus untuk memodifikasi
public void tambahHobi(String hobi) {
    if (this.hobi == null) {
        this.hobi = new ArrayList<>();
    }
    this.hobi.add(hobi);
}

public void hapusHobi(String hobi) {
    if (this.hobi != null) {
        this.hobi.remove(hobi);
    }
}
```

**Pendekatan 3: Immutable Objects**

Jika memungkinkan, gunakan immutable objects (objek yang tidak dapat diubah setelah dibuat):

```java
// Immutable class
public final class Koordinat {
    private final double x;
    private final double y;
    
    public Koordinat(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double getX() {
        return x;
    }
    
    public double getY() {
        return y;
    }
    
    // Tidak ada setter, hanya method yang mengembalikan instance baru
    public Koordinat withX(double x) {
        return new Koordinat(x, this.y);
    }
    
    public Koordinat withY(double y) {
        return new Koordinat(this.x, y);
    }
}
```

### Boolean Getter: isX() vs getX()

Untuk atribut bertipe boolean, ada dua konvensi penamaan getter:

1. **isX()**: Lebih umum dan sesuai dengan spesifikasi JavaBeans
2. **getX()**: Lebih konsisten dengan getter lainnya

Kedua konvensi dapat diterima, tetapi `isX()` lebih disukai untuk boolean:

```java
private boolean aktif;

// Pilihan 1: isX() (direkomendasikan untuk boolean)
public boolean isAktif() {
    return aktif;
}

// Pilihan 2: getX() (konsisten dengan getter lainnya)
public boolean getAktif() {
    return aktif;
}
```

## Property Read-Only dan Write-Only

Kadang-kadang, Anda ingin membatasi akses ke property sehingga hanya dapat dibaca (read-only) atau hanya dapat ditulis (write-only).

### Read-Only Property

Property read-only hanya dapat dibaca, tidak dapat diubah dari luar class. Ini berguna untuk value yang tidak boleh diubah setelah objek dibuat, atau yang dihitung secara dinamis.

```java
public class Lingkaran {
    private final double radius; // Final untuk immutability
    
    public Lingkaran(double radius) {
        this.radius = radius;
    }
    
    // Read-only property radius
    public double getRadius() {
        return radius;
    }
    
    // Read-only property yang dihitung
    public double getLuas() {
        return Math.PI * radius * radius;
    }
    
    public double getKeliling() {
        return 2 * Math.PI * radius;
    }
    
    // Tidak ada setter untuk radius
}
```

### Write-Only Property

Property write-only hanya dapat ditulis, tidak dapat dibaca dari luar class. Ini jarang digunakan tetapi berguna untuk informasi sensitif.

```java
public class UserAccount {
    private String username;
    private char[] password; // Menyimpan password sebagai char array adalah lebih aman
    
    public String getUsername() {
        return username;
    }
    
    public void setUsername(String username) {
        this.username = username;
    }
    
    // Write-only property untuk password
    public void setPassword(char[] password) {
        // Validasi password
        if (password == null || password.length < 8) {
            throw new IllegalArgumentException("Password harus minimal 8 karakter");
        }
        
        // Copy password untuk keamanan
        this.password = Arrays.copyOf(password, password.length);
        
        // Bersihkan input password dari memori
        Arrays.fill(password, '0');
    }
    
    // Tidak ada getter untuk password
    
    public boolean verifyPassword(char[] inputPassword) {
        boolean result = Arrays.equals(password, inputPassword);
        // Bersihkan input password dari memori
        Arrays.fill(inputPassword, '0');
        return result;
    }
}
```

## Mutable vs Immutable Objects

Penerapan getter dan setter juga terkait dengan konsep mutable dan immutable objects.

### Mutable Objects

**Mutable objects** adalah objek yang state-nya dapat diubah setelah dibuat. Class dengan setter adalah contoh mutable objects.

```java
// Mutable class
public class Pegawai {
    private String nama;
    private double gaji;
    
    // Getters and setters
    public String getNama() {
        return nama;
    }
    
    public void setNama(String nama) {
        this.nama = nama;
    }
    
    public double getGaji() {
        return gaji;
    }
    
    public void setGaji(double gaji) {
        this.gaji = gaji;
    }
}
```

### Immutable Objects

**Immutable objects** adalah objek yang state-nya tidak dapat diubah setelah dibuat. Mereka hanya memiliki getter dan tidak memiliki setter.

```java
// Immutable class
public final class Titik {
    private final int x;
    private final int y;
    
    public Titik(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    public int getX() {
        return x;
    }
    
    public int getY() {
        return y;
    }
    
    // Method untuk membuat instance baru dengan nilai berbeda
    public Titik pindah(int deltaX, int deltaY) {
        return new Titik(x + deltaX, y + deltaY);
    }
}
```

Keuntungan immutable objects:
- Thread-safe tanpa synchronization
- Dapat di-cache dan di-share dengan aman
- Tidak perlu defensive copying
- Cocok untuk key di Map atau elemen di Set

## Best Practices

Berikut adalah beberapa best practices dalam mengimplementasikan getter dan setter:

1. **Ikuti Konvensi JavaBeans**: Gunakan penamaan `getX()`, `setX()`, dan `isX()` untuk boolean

2. **Validasi Input di Setter**: Selalu validasi input sebelum mengubah state objek

3. **Hati-hati dengan Reference Types**: Gunakan defensive copying atau unmodifiable wrapper untuk mencegah ekspos referensi internal

4. **Pertimbangkan Immutability**: Jika objek tidak perlu diubah setelah dibuat, buat immutable

5. **Berikan Visibilitas Minimal**: Jangan buat semua atribut memiliki getter dan setter secara otomatis; berikan hanya yang diperlukan

6. **Gunakan Method yang Bermakna**: Untuk operasi kompleks, buat method dengan nama yang deskriptif daripada hanya getter/setter
   ```java
   // KURANG JELAS
   user.setActive(true);
   user.setLastLoginDate(new Date());
   
   // LEBIH JELAS
   user.activate();
   user.recordLogin();
   ```

7. **Builder Pattern untuk Parameter Banyak**: Pertimbangkan menggunakan Builder Pattern untuk menginisialisasi objek dengan banyak parameter
   ```java
   // RUMIT
   User user = new User();
   user.setFirstName("John");
   user.setLastName("Doe");
   user.setEmail("john@example.com");
   user.setAge(30);
   
   // LEBIH BAIK
   User user = new User.Builder()
       .firstName("John")
       .lastName("Doe")
       .email("john@example.com")
       .age(30)
       .build();
   ```

8. **Pertimbangkan Method Chaining untuk Setter**: Memungkinkan beberapa setter dipanggil dalam satu statement
   ```java
   public class Produk {
       private String nama;
       private double harga;
       
       public Produk setNama(String nama) {
           this.nama = nama;
           return this; // Mengembalikan this untuk chaining
       }
       
       public Produk setHarga(double harga) {
           this.harga = harga;
           return this; // Mengembalikan this untuk chaining
       }
   }
   
   // Penggunaan
   Produk p = new Produk()
       .setNama("Laptop")
       .setHarga(12000000);
   ```

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep getter dan setter dengan membuat program sederhana menggunakan NetBeans IDE.

### Skenario: Sistem Manajemen Perpustakaan (Lanjutan)

Kita akan melanjutkan proyek Sistem Perpustakaan dari tutorial sebelumnya, dengan fokus pada implementasi getter dan setter yang baik.

### Langkah 1: Buat Project Baru

1. Buka NetBeans IDE
2. Pilih **File** > **New Project**
3. Pilih **Java** > **Java Application** > **Next**
4. Beri nama project "PerpustakaanApp" dan tentukan lokasi penyimpanan
5. Klik **Finish**

### Langkah 2: Buat Kelas Buku

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Buku"
3. Isi dengan kode berikut:

```java
package perpustakaanapp;

import java.util.Arrays;
import java.util.Date;

public class Buku {
    // Atribut private
    private String isbn;
    private String judul;
    private String[] penulis;
    private String penerbit;
    private int tahunTerbit;
    private int jumlahHalaman;
    private String kategori;
    private boolean tersedia;
    private Date tanggalTerakhirDipinjam;
    
    // Konstruktor
    public Buku(String isbn, String judul, String[] penulis, String penerbit, int tahunTerbit) {
        setIsbn(isbn);
        setJudul(judul);
        setPenulis(penulis);
        setPenerbit(penerbit);
        setTahunTerbit(tahunTerbit);
        this.tersedia = true;
    }
    
    // Getter dan Setter dengan validasi dan defensive copy
    
    public String getIsbn() {
        return isbn;
    }
    
    public void setIsbn(String isbn) {
        if (isbn == null || !isbn.matches("\\d{3}-\\d{10}")) {
            throw new IllegalArgumentException("ISBN harus dalam format XXX-XXXXXXXXXX");
        }
        this.isbn = isbn;
    }
    
    public String getJudul() {
        return judul;
    }
    
    public void setJudul(String judul) {
        if (judul == null || judul.trim().isEmpty()) {
            throw new IllegalArgumentException("Judul tidak boleh kosong");
        }
        this.judul = judul;
    }
    
    public String[] getPenulis() {
        // Defensive copy untuk array
        return penulis != null ? Arrays.copyOf(penulis, penulis.length) : null;
    }
    
    public void setPenulis(String[] penulis) {
        if (penulis == null || penulis.length == 0) {
            throw new IllegalArgumentException("Minimal harus ada satu penulis");
        }
        // Defensive copy untuk array
        this.penulis = Arrays.copyOf(penulis, penulis.length);
    }
    
    public String getPenerbit() {
        return penerbit;
    }
    
    public void setPenerbit(String penerbit) {
        if (penerbit == null || penerbit.trim().isEmpty()) {
            throw new IllegalArgumentException("Penerbit tidak boleh kosong");
        }
        this.penerbit = penerbit;
    }
    
    public int getTahunTerbit() {
        return tahunTerbit;
    }
    
    public void setTahunTerbit(int tahunTerbit) {
        int tahunSekarang = java.util.Calendar.getInstance().get(java.util.Calendar.YEAR);
        if (tahunTerbit < 1900 || tahunTerbit > tahunSekarang) {
            throw new IllegalArgumentException("Tahun terbit harus antara 1900 dan " + tahunSekarang);
        }
        this.tahunTerbit = tahunTerbit;
    }
    
    public int getJumlahHalaman() {
        return jumlahHalaman;
    }
    
    public void setJumlahHalaman(int jumlahHalaman) {
        if (jumlahHalaman <= 0) {
            throw new IllegalArgumentException("Jumlah halaman harus positif");
        }
        this.jumlahHalaman = jumlahHalaman;
    }
    
    public String getKategori() {
        return kategori;
    }
    
    public void setKategori(String kategori) {
        this.kategori = kategori;
    }
    
    // Boolean getter menggunakan isX()
    public boolean isTersedia() {
        return tersedia;
    }
    
    // Private setter - hanya diubah melalui method pinjam() dan kembalikan()
    private void setTersedia(boolean tersedia) {
        this.tersedia = tersedia;
    }
    
    // Getter dengan defensive copy untuk Date
    public Date getTanggalTerakhirDipinjam() {
        return tanggalTerakhirDipinjam != null ? new Date(tanggalTerakhirDipinjam.getTime()) : null;
    }
    
    // Private setter untuk tanggalTerakhirDipinjam
    private void setTanggalTerakhirDipinjam(Date tanggal) {
        this.tanggalTerakhirDipinjam = tanggal != null ? new Date(tanggal.getTime()) : null;
    }
    
    // Method fungsional sebagai pengganti akses langsung ke setter
    public void pinjam() {
        if (!tersedia) {
            throw new IllegalStateException("Buku tidak tersedia untuk dipinjam");
        }
        setTersedia(false);
        setTanggalTerakhirDipinjam(new Date());
        System.out.println("Buku " + judul + " berhasil dipinjam");
    }
    
    public void kembalikan() {
        if (tersedia) {
            throw new IllegalStateException("Buku tidak sedang dipinjam");
        }
        setTersedia(true);
        System.out.println("Buku " + judul + " berhasil dikembalikan");
    }
    
    // Method untuk menampilkan informasi buku
    public void tampilInfo() {
        System.out.println("ISBN: " + isbn);
        System.out.println("Judul: " + judul);
        System.out.print("Penulis: ");
        if (penulis != null) {
            for (int i = 0; i < penulis.length; i++) {
                System.out.print(penulis[i]);
                if (i < penulis.length - 1) {
                    System.out.print(", ");
                }
            }
            System.out.println();
        } else {
            System.out.println("(Tidak ada)");
        }
        System.out.println("Penerbit: " + penerbit);
        System.out.println("Tahun Terbit: " + tahunTerbit);
        System.out.println("Jumlah Halaman: " + (jumlahHalaman > 0 ? jumlahHalaman : "Tidak diketahui"));
        System.out.println("Kategori: " + (kategori != null ? kategori : "Umum"));
        System.out.println("Status: " + (tersedia ? "Tersedia" : "Dipinjam"));
        if (tanggalTerakhirDipinjam != null) {
            System.out.println("Tanggal Terakhir Dipinjam: " + tanggalTerakhirDipinjam);
        }
    }
}
```

### Langkah 3: Buat Kelas Anggota

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama "Anggota"
3. Isi dengan kode berikut:

```java
package perpustakaanapp;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Date;
import java.util.List;

public class Anggota {
    // Constant
    public static final int BATAS_PINJAM = 3;
    
    // Atribut private
    private final String id; // Read-only (final)
    private String nama;
    private String alamat;
    private String nomorTelepon;
    private Date tanggalDaftar;
    private List<Buku> bukuDipinjam;
    private boolean aktif;
    
    // Konstruktor
    public Anggota(String id, String nama) {
        if (id == null || !id.matches("M-\\d{4}")) {
            throw new IllegalArgumentException("ID anggota harus dalam format M-XXXX");
        }
        this.id = id;
        setNama(nama);
        this.tanggalDaftar = new Date();
        this.bukuDipinjam = new ArrayList<>();
        this.aktif = true;
    }
    
    // Getter dan Setter
    
    // Read-only property (hanya getter)
    public String getId() {
        return id;
    }
    
    public String getNama() {
        return nama;
    }
    
    public void setNama(String nama) {
        if (nama == null || nama.trim().isEmpty()) {
            throw new IllegalArgumentException("Nama tidak boleh kosong");
        }
        this.nama = nama;
    }
    
    public String getAlamat() {
        return alamat;
    }
    
    public void setAlamat(String alamat) {
        this.alamat = alamat;
    }
    
    public String getNomorTelepon() {
        return nomorTelepon;
    }
    
    public void setNomorTelepon(String nomorTelepon) {
        if (nomorTelepon != null && !nomorTelepon.matches("\\d{10,15}")) {
            throw new IllegalArgumentException("Nomor telepon harus terdiri dari 10-15 digit");
        }
        this.nomorTelepon = nomorTelepon;
    }
    
    // Getter dengan defensive copy untuk Date
    public Date getTanggalDaftar() {
        return new Date(tanggalDaftar.getTime());
    }
    
    // Tidak ada setter untuk tanggalDaftar karena tidak boleh diubah
    
    // Getter dengan unmodifiable wrapper untuk collection
    public List<Buku> getBukuDipinjam() {
        return Collections.unmodifiableList(bukuDipinjam);
    }
    
    // Tidak ada setter langsung untuk bukuDipinjam, diganti dengan method fungsional
    
    // Boolean getter menggunakan isX()
    public boolean isAktif() {
        return aktif;
    }
    
    public void setAktif(boolean aktif) {
        this.aktif = aktif;
    }
    
    // Method fungsional
    public boolean pinjamBuku(Buku buku) {
        if (!aktif) {
            System.out.println("Anggota tidak aktif");
            return false;
        }
        
        if (bukuDipinjam.size() >= BATAS_PINJAM) {
            System.out.println("Mencapai batas maksimal peminjaman (" + BATAS_PINJAM + " buku)");
            return false;
        }
        
        if (!buku.isTersedia()) {
            System.out.println("Buku tidak tersedia");
            return false;
        }
        
        try {
            buku.pinjam();
            bukuDipinjam.add(buku);
            System.out.println("Anggota " + nama + " berhasil meminjam buku " + buku.getJudul());
            return true;
        } catch (Exception e) {
            System.out.println("Gagal meminjam buku: " + e.getMessage());
            return false;
        }
    }
    
    public boolean kembalikanBuku(Buku buku) {
        if (!bukuDipinjam.contains(buku)) {
            System.out.println("Buku tidak dipinjam oleh anggota ini");
            return false;
        }
        
        try {
            buku.kembalikan();
            bukuDipinjam.remove(buku);
            System.out.println("Anggota " + nama + " berhasil mengembalikan buku " + buku.getJudul());
            return true;
        } catch (Exception e) {
            System.out.println("Gagal mengembalikan buku: " + e.getMessage());
            return false;
        }
    }
    
    public int getJumlahBukuDipinjam() {
        return bukuDipinjam.size();
    }
    
    // Method untuk menampilkan informasi anggota
    public void tampilInfo() {
        System.out.println("ID Anggota: " + id);
        System.out.println("Nama: " + nama);
        System.out.println("Alamat: " + (alamat != null ? alamat : "(Belum diisi)"));
        System.out.println("Nomor Telepon: " + (nomorTelepon != null ? nomorTelepon : "(Belum diisi)"));
        System.out.println("Tanggal Daftar: " + tanggalDaftar);
        System.out.println("Status: " + (aktif ? "Aktif" : "Tidak Aktif"));
        System.out.println("Jumlah Buku Dipinjam: " + bukuDipinjam.size());
        
        if (!bukuDipinjam.isEmpty()) {
            System.out.println("Daftar Buku Dipinjam:");
            for (int i = 0; i < bukuDipinjam.size(); i++) {
                System.out.println("  " + (i + 1) + ". " + bukuDipinjam.get(i).getJudul());
            }
        }
    }
}
```

### Langkah 4: Buat Kelas Main

1. Buka file main (biasanya `PerpustakaanApp.java`)
2. Ubah kode menjadi:

```java
package perpustakaanapp;

public class PerpustakaanApp {
    public static void main(String[] args) {
        // Membuat objek buku
        Buku buku1 = new Buku("123-1234567890", "Java Programming", 
                               new String[]{"John Doe", "Jane Smith"}, "Penerbit ABC", 2020);
        buku1.setJumlahHalaman(500);
        buku1.setKategori("Programming");
        
        Buku buku2 = new Buku("456-0987654321", "Database Design", 
                               new String[]{"Alice Johnson"}, "Penerbit XYZ", 2018);
        buku2.setJumlahHalaman(350);
        buku2.setKategori("Database");
        
        // Membuat objek anggota
        Anggota anggota = new Anggota("M-1234", "Rudi Hartono");
        anggota.setAlamat("Jl. Merdeka No. 123, Jakarta");
        anggota.setNomorTelepon("0812345678");
        
        // Menampilkan informasi buku dan anggota
        System.out.println("=== INFORMASI BUKU ===");
        buku1.tampilInfo();
        System.out.println();
        buku2.tampilInfo();
        
        System.out.println("\n=== INFORMASI ANGGOTA ===");
        anggota.tampilInfo();
        
        // Demonstrasi peminjaman dan pengembalian buku
        System.out.println("\n=== PROSES PEMINJAMAN DAN PENGEMBALIAN ===");
        
        // Peminjaman buku
        anggota.pinjamBuku(buku1);
        anggota.pinjamBuku(buku2);
        
        System.out.println("\n=== INFORMASI ANGGOTA SETELAH PEMINJAMAN ===");
        anggota.tampilInfo();
        
        System.out.println("\n=== INFORMASI BUKU SETELAH PEMINJAMAN ===");
        buku1.tampilInfo();
        System.out.println();
        buku2.tampilInfo();
        
        // Pengembalian buku
        anggota.kembalikanBuku(buku1);
        
        System.out.println("\n=== INFORMASI ANGGOTA SETELAH PENGEMBALIAN ===");
        anggota.tampilInfo();
        
        System.out.println("\n=== INFORMASI BUKU SETELAH PENGEMBALIAN ===");
        buku1.tampilInfo();
        
        // Demonstrasi validasi data
        System.out.println("\n=== DEMONSTRASI VALIDASI DATA ===");
        
        try {
            // Mencoba membuat buku dengan ISBN invalid
            Buku bukuInvalid = new Buku("invalid-isbn", "Invalid Book", 
                                       new String[]{"Author"}, "Publisher", 2020);
        } catch (IllegalArgumentException e) {
            System.out.println("Error saat membuat buku: " + e.getMessage());
        }
        
        try {
            // Mencoba mengubah tahun terbit ke nilai tidak valid
            buku1.setTahunTerbit(3000);
        } catch (IllegalArgumentException e) {
            System.out.println("Error saat mengubah tahun terbit: " + e.getMessage());
        }
        
        try {
            // Mencoba meminjam buku yang sudah dipinjam
            Anggota anggota2 = new Anggota("M-5678", "Siti Nurhaliza");
            anggota2.pinjamBuku(buku2); // buku2 sudah dipinjam oleh anggota1
        } catch (Exception e) {
            System.out.println("Error saat meminjam buku: " + e.getMessage());
        }
    }
}
```

### Langkah 5: Jalankan Program

1. Klik **Run** > **Run Project**
2. Atau tekan tombol F6

### Penjelasan

Dalam contoh praktik di atas, kita telah mengimplementasikan berbagai konsep terkait getter dan setter:

1. **Enkapsulasi**: Semua atribut dijadikan `private` dan diakses hanya melalui getter dan setter

2. **Validasi Data**: Setter melakukan validasi untuk memastikan data yang disimpan valid
   - Validasi ISBN, tahun terbit, jumlah halaman, nomor telepon, dll.

3. **Defensive Copying**: Getter dan setter untuk tipe yang mutable (array, Date) menggunakan defensive copying
   - `getPenulis()` dan `setPenulis()` untuk array
   - `getTanggalTerakhirDipinjam()` dan `setTanggalTerakhirDipinjam()` untuk Date

4. **Unmodifiable Collections**: `getBukuDipinjam()` mengembalikan unmodifiable list untuk mencegah modifikasi langsung

5. **Property Read-Only**: 
   - `id` di kelas `Anggota` dideklarasikan sebagai `final` dan hanya memiliki getter
   - `tanggalDaftar` tidak memiliki setter publik

6. **Boolean Getters**: Menggunakan konvensi `isX()` daripada `getX()` untuk atribut boolean
   - `isTersedia()` dan `isAktif()`

7. **Method Fungsional**: Mengganti akses langsung dengan method yang bermakna
   - `pinjam()` dan `kembalikan()` daripada `setTersedia()`
   - `pinjamBuku()` dan `kembalikanBuku()` daripada memodifikasi `bukuDipinjam` langsung

## Rangkuman

Dalam bab ini, kita telah mempelajari:

1. **Konsep Enkapsulasi**:
   - Penyembunyian implementasi internal
   - Mengontrol akses ke data objek

2. **Method Getter dan Setter**:
   - Getter (accessor) untuk mengambil nilai atribut
   - Setter (mutator) untuk mengubah nilai atribut

3. **Alasan Menggunakan Getter dan Setter**:
   - Kontrol akses
   - Validasi data
   - Encapsulation
   - Lazy initialization
   - Synchronization
   - Debugging

4. **Konvensi Penamaan JavaBeans**:
   - `getX()` untuk getter umum
   - `isX()` untuk getter atribut boolean
   - `setX()` untuk setter

5. **Implementasi Getter dan Setter**:
   - Implementasi dasar
   - Validasi data dalam setter
   - Defensive copying untuk reference types
   - Boolean getter

6. **Property Read-Only dan Write-Only**:
   - Read-only: Hanya getter, tidak ada setter
   - Write-only: Hanya setter, tidak ada getter

7. **Mutable vs Immutable Objects**:
   - Mutable: State dapat diubah setelah dibuat
   - Immutable: State tidak dapat diubah setelah dibuat

8. **Best Practices**:
   - Ikuti konvensi JavaBeans
   - Validasi input
   - Hati-hati dengan reference types
   - Pertimbangkan immutability
   - Gunakan method yang bermakna

Memahami dan menerapkan getter dan setter dengan benar adalah komponen penting dalam membuat program berorientasi objek yang robust, fleksibel, dan dapat dipelihara. Dengan enkapsulasi yang baik, Anda dapat mengontrol bagaimana data diakses dan dimodifikasi, serta memberikan fleksibilitas untuk mengubah implementasi internal tanpa memengaruhi code client.

## Latihan Soal

1. Jelaskan konsep enkapsulasi dan bagaimana getter dan setter berperan dalam menerapkannya.

2. Apa perbedaan antara getter `getX()` dan `isX()`? Kapan sebaiknya menggunakan masing-masing?

3. Mengapa defensive copying penting dalam getter dan setter untuk reference types? Berikan contoh masalah yang dapat terjadi jika tidak menggunakan defensive copying.

4. Buatlah class `RekeningBank` dengan atribut-atribut yang sesuai dan terapkan enkapsulasi yang baik menggunakan getter dan setter. Implementasikan validasi untuk operasi deposit dan withdraw.

5. Apa keuntungan dan kerugian dari immutable objects? Berikan contoh kasus di mana immutable objects lebih disukai dibandingkan mutable objects.

6. Perhatikan code berikut dan identifikasi masalah-masalah yang terkait dengan getter dan setter:
   ```java
   public class Student {
       private String name;
       private int[] grades;
       private Date birthDate;
       
       public String getName() {
           return name;
       }
       
       public void setName(String name) {
           this.name = name;
       }
       
       public int[] getGrades() {
           return grades;
       }
       
       public void setGrades(int[] grades) {
           this.grades = grades;
       }
       
       public Date getBirthDate() {
           return birthDate;
       }
       
       public void setBirthDate(Date birthDate) {
           this.birthDate = birthDate;
       }
   }
   ```

7. Apa yang dimaksud dengan "lazy initialization" dalam konteks getter? Berikan contoh implementasinya.

8. Jelaskan kapan sebaiknya menggunakan property read-only dan write-only. Berikan contoh kasus penggunaan untuk masing-masing.

9. Implementasikan setter method untuk atribut email yang memvalidasi format email yang valid (mengandung '@' dan domain yang valid).

10. Bandingkan dan kontraskan pendekatan "JavaBeans standard" (getter/setter tradisional) dengan pendekatan yang lebih modern seperti "Fluent Interface" (method chaining) dan "Builder Pattern". Apa keuntungan dan kerugian masing-masing pendekatan?

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional.

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall.

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional.

5. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall.

6. Oracle. (2023). *JavaBeans Specification*. [https://www.oracle.com/java/technologies/javase/javabeans-spec.html](https://www.oracle.com/java/technologies/javase/javabeans-spec.html)

7. Oracle. (2023). *Java Tutorial: Classes and Objects*. [https://docs.oracle.com/javase/tutorial/java/javaOO/](https://docs.oracle.com/javase/tutorial/java/javaOO/)

8. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education.

9. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media.

10. Martin, R. C. (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall.

---

[◀️ Kembali ke Tutorial #04: Constructor & Destructor pada Java](04-constructors.md) | [Lanjut ke Tutorial #06: Memahami Kata Kunci this dan super ▶️](06-this-super.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
