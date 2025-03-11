# 📘 Tutorial Java OOP #08: Menggunakan Interface

> *"Interface adalah kontrak yang menjanjikan kemampuan tanpa mendiktekan implementasi — memungkinkan berbagai kelas untuk berperilaku sama tanpa harus berbagi warisan yang sama."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dan tujuan interface dalam pemrograman Java
- Membedakan interface dengan abstract class dan class biasa
- Mendefinisikan dan mengimplementasikan interface sendiri
- Memahami multiple interface implementation di Java
- Menggunakan default dan static methods dalam interface (Java 8+)
- Memanfaatkan interface sebagai tipe data untuk polimorfisme
- Menerapkan best practices dalam penggunaan interface

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Apa Itu Interface?](#apa-itu-interface)
   - [Definisi dan Konsep Dasar](#definisi-dan-konsep-dasar)
   - [Perbedaan Interface dengan Class dan Abstract Class](#perbedaan-interface-dengan-class-dan-abstract-class)
   - [Mengapa Kita Membutuhkan Interface?](#mengapa-kita-membutuhkan-interface)
3. [Mendefinisikan Interface](#mendefinisikan-interface)
   - [Sintaks dan Struktur](#sintaks-dan-struktur)
   - [Fields dalam Interface](#fields-dalam-interface)
   - [Methods dalam Interface](#methods-dalam-interface)
4. [Mengimplementasikan Interface](#mengimplementasikan-interface)
   - [Keyword implements](#keyword-implements)
   - [Mengimplementasikan Method Interface](#mengimplementasikan-method-interface)
   - [Multiple Interface Implementation](#multiple-interface-implementation)
5. [Fitur Modern Interface (Java 8+)](#fitur-modern-interface-java-8)
   - [Default Methods](#default-methods)
   - [Static Methods](#static-methods)
   - [Private Methods (Java 9+)](#private-methods-java-9)
6. [Interface sebagai Tipe Data](#interface-sebagai-tipe-data)
   - [Interface untuk Polimorfisme](#interface-untuk-polimorfisme)
   - [Interface sebagai Parameter dan Return Type](#interface-sebagai-parameter-dan-return-type)
7. [Nested Interface](#nested-interface)
8. [Interface Inheritance](#interface-inheritance)
9. [Functional Interface (Java 8+)](#functional-interface-java-8)
10. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
11. [Rangkuman](#rangkuman)
12. [Latihan Soal](#latihan-soal)
13. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari konsep polimorfisme yang merupakan salah satu pilar penting dalam pemrograman berorientasi objek. Polimorfisme memungkinkan kita untuk memperlakukan objek dari kelas yang berbeda secara seragam melalui tipe referensi yang sama.

Di Java, selain inheritance yang sudah kita pelajari, ada cara lain untuk mencapai polimorfisme yaitu dengan menggunakan **interface**. Interface menjadi solusi untuk kelemahan dari pewarisan tunggal (single inheritance) di Java, dimana sebuah kelas hanya bisa mewarisi dari satu kelas lain.

Dalam tutorial ini, kita akan mempelajari secara mendalam tentang interface di Java, mulai dari konsep dasar hingga fitur-fitur modern yang diperkenalkan di Java 8 dan setelahnya.

## Apa Itu Interface?

### Definisi dan Konsep Dasar

**Interface** adalah blueprint dari sebuah kelas yang hanya berisi konstanta dan deklarasi method (tanpa implementasi body) yang harus diimplementasikan oleh kelas-kelas yang menggunakannya. Interface mendefinisikan "apa" yang harus dilakukan oleh sebuah kelas, tetapi tidak mendefinisikan "bagaimana" melakukannya.

Secara sederhana, interface bertindak sebagai **kontrak** yang harus dipenuhi oleh kelas yang mengimplementasikannya. Kelas tersebut wajib menyediakan implementasi untuk semua method yang dideklarasikan dalam interface.

Analogi sederhana: Interface seperti template atau blueprint untuk konstruksi rumah. Template tersebut menentukan bahwa rumah harus memiliki pintu, jendela, dan atap, tetapi tidak menentukan bagaimana pintu, jendela, dan atap tersebut harus dibangun. Hal itu diserahkan kepada kontraktor (kelas implementasi).

### Perbedaan Interface dengan Class dan Abstract Class

| Aspek | Class | Abstract Class | Interface |
|-------|-------|---------------|-----------|
| Instantiasi | Dapat di-instantiasi langsung | Tidak dapat di-instantiasi langsung | Tidak dapat di-instantiasi langsung |
| Inheritance | Dapat mewarisi satu class | Dapat mewarisi satu class | Dapat mewarisi banyak interface |
| Methods | Dapat berisi method konkrit dan abstract | Dapat berisi method konkrit dan abstract | Secara tradisional hanya berisi abstract methods (Java 8+ mendukung default dan static methods) |
| Fields | Dapat berisi instance variables | Dapat berisi instance variables | Hanya berisi konstanta (public static final) |
| Konstruktor | Dapat memiliki konstruktor | Dapat memiliki konstruktor | Tidak memiliki konstruktor |
| Akses Modifier | Dapat menggunakan semua access modifiers | Dapat menggunakan semua access modifiers | Methods secara implisit public, fields secara implisit public static final |
| Penggunaan | Untuk objek konkrit | Untuk template partial | Untuk kontrak fungsionalitas |

### Mengapa Kita Membutuhkan Interface?

Interface menyediakan beberapa keuntungan penting dalam pengembangan aplikasi:

1. **Mengatasi Keterbatasan Single Inheritance**: Java hanya mendukung single inheritance (satu kelas hanya bisa mewarisi dari satu kelas). Interface memungkinkan kelas untuk "mewarisi" behavior dari banyak sumber.

2. **Mencapai Polymorphism**: Interface memungkinkan kita untuk memperlakukan objek dari kelas yang berbeda secara seragam, jika mereka mengimplementasikan interface yang sama.

3. **Loose Coupling**: Interface membantu menciptakan sistem yang komponennya tidak terikat erat satu sama lain (loosely coupled), yang membuat sistem lebih modular dan mudah diubah.

4. **Pemisahan Concern**: Interface memungkinkan pemisahan antara apa yang harus dilakukan (kontrak) dan bagaimana melakukannya (implementasi).

5. **Menyediakan Kontrak**: Interface memberikan jaminan bahwa kelas yang mengimplementasikan memiliki method-method tertentu.

## Mendefinisikan Interface

### Sintaks dan Struktur

Untuk mendefinisikan interface di Java, kita menggunakan keyword `interface` sebagai pengganti `class`:

```java
public interface InterfaceName {
    // Konstanta
    // Deklarasi method
}
```

### Fields dalam Interface

Fields dalam interface selalu bersifat `public`, `static`, dan `final`, meskipun tidak ditulis secara eksplisit:

```java
public interface Flyable {
    int MAX_ALTITUDE = 10000; // secara implisit: public static final
    String DEFAULT_AIRLINE = "Generic Airways"; // secara implisit: public static final
}
```

Dalam contoh di atas, `MAX_ALTITUDE` dan `DEFAULT_AIRLINE` adalah konstanta yang dapat diakses langsung melalui nama interface: `Flyable.MAX_ALTITUDE`.

### Methods dalam Interface

Secara tradisional (sebelum Java 8), methods dalam interface selalu bersifat `public` dan `abstract`:

```java
public interface Drawable {
    void draw(); // secara implisit: public abstract
    double calculateArea(); // secara implisit: public abstract
}
```

Sejak Java 8, interface juga dapat memiliki `default` dan `static` methods (akan dibahas nanti).

## Mengimplementasikan Interface

### Keyword implements

Untuk mengimplementasikan interface, kelas menggunakan keyword `implements`:

```java
public class Circle implements Drawable {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a circle with radius: " + radius);
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}
```

### Mengimplementasikan Method Interface

Ketika sebuah kelas mengimplementasikan interface, kelas tersebut **harus** menyediakan implementasi untuk semua method yang dideklarasikan dalam interface, kecuali jika kelas tersebut adalah abstract class.

```java
public interface Movable {
    void moveUp();
    void moveDown();
    void moveLeft();
    void moveRight();
}

// Implementasi lengkap
public class Car implements Movable {
    @Override
    public void moveUp() {
        System.out.println("Car moving forward");
    }
    
    @Override
    public void moveDown() {
        System.out.println("Car moving backward");
    }
    
    @Override
    public void moveLeft() {
        System.out.println("Car turning left");
    }
    
    @Override
    public void moveRight() {
        System.out.println("Car turning right");
    }
}

// Implementasi partial (kelas harus abstract)
public abstract class PartialImplementation implements Movable {
    @Override
    public void moveUp() {
        System.out.println("Moving up");
    }
    
    @Override
    public void moveDown() {
        System.out.println("Moving down");
    }
    
    // moveLeft() dan moveRight() tidak diimplementasikan,
    // sehingga kelas ini harus dideklarasikan sebagai abstract
}
```

### Multiple Interface Implementation

Salah satu keunggulan interface adalah memungkinkan sebuah kelas untuk mengimplementasikan lebih dari satu interface:

```java
public interface Drawable {
    void draw();
}

public interface Resizable {
    void resize(double factor);
}

public class Rectangle implements Drawable, Resizable {
    private double width;
    private double height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle with width: " + width + " and height: " + height);
    }
    
    @Override
    public void resize(double factor) {
        width *= factor;
        height *= factor;
        System.out.println("Resized rectangle to width: " + width + " and height: " + height);
    }
}
```

Dalam contoh di atas, kelas `Rectangle` mengimplementasikan dua interface: `Drawable` dan `Resizable`. Kelas ini harus menyediakan implementasi untuk semua method dari kedua interface tersebut.

## Fitur Modern Interface (Java 8+)

Java 8 memperkenalkan beberapa fitur baru untuk interface yang membuat interface lebih fleksibel.

### Default Methods

**Default methods** memungkinkan kita untuk menyediakan implementasi default dalam interface, yang dapat digunakan oleh kelas yang mengimplementasikan interface tanpa harus memberikan implementasi sendiri:

```java
public interface Vehicle {
    void start();
    void stop();
    
    // Default method
    default void honk() {
        System.out.println("Beep beep!");
    }
}

public class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car started");
    }
    
    @Override
    public void stop() {
        System.out.println("Car stopped");
    }
    
    // Tidak perlu mengimplementasikan honk()
    // karena sudah ada implementasi default
}
```

Default methods sangat berguna ketika kita ingin menambahkan fungsionalitas baru ke interface yang sudah ada tanpa merusak kode yang sudah mengimplementasikannya.

### Static Methods

**Static methods** dalam interface mirip dengan static methods dalam class. Mereka terkait dengan interface, bukan dengan instance dari kelas yang mengimplementasikan interface:

```java
public interface MathOperations {
    double add(double a, double b);
    double subtract(double a, double b);
    
    // Static method
    static double multiply(double a, double b) {
        return a * b;
    }
}

// Penggunaan static method
double result = MathOperations.multiply(5, 3); // Memanggil langsung dari interface
```

Static methods tidak dapat di-override oleh kelas yang mengimplementasikan interface.

### Private Methods (Java 9+)

Java 9 memperkenalkan **private methods** dalam interface, yang memungkinkan kita untuk memecah default methods yang kompleks menjadi bagian-bagian yang lebih kecil dan dapat digunakan kembali:

```java
public interface Logger {
    void logInfo(String message);
    void logError(String message);
    
    default void logWithTimestamp(String message) {
        String timestamp = generateTimestamp();
        System.out.println(timestamp + ": " + message);
    }
    
    // Private method (Java 9+)
    private String generateTimestamp() {
        return new java.util.Date().toString();
    }
}
```

Private methods hanya dapat dipanggil dari default atau static methods dalam interface yang sama.

## Interface sebagai Tipe Data

### Interface untuk Polimorfisme

Interface dapat digunakan sebagai tipe data, yang memungkinkan polimorfisme:

```java
public interface Shape {
    double calculateArea();
    double calculatePerimeter();
}

public class Circle implements Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
}

public class Rectangle implements Shape {
    private double width;
    private double height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * (width + height);
    }
}

// Penggunaan polimorfisme
public class ShapeProcessor {
    public void printShapeDetails(Shape shape) {
        System.out.println("Area: " + shape.calculateArea());
        System.out.println("Perimeter: " + shape.calculatePerimeter());
    }
}

// Memanggil method dengan berbagai implementasi Shape
ShapeProcessor processor = new ShapeProcessor();
processor.printShapeDetails(new Circle(5));
processor.printShapeDetails(new Rectangle(4, 6));
```

### Interface sebagai Parameter dan Return Type

Interface sering digunakan sebagai tipe parameter dan return type dalam method:

```java
// Interface sebagai parameter
public void sortList(Comparator<String> comparator) {
    // Implementasi sorting dengan comparator
}

// Interface sebagai return type
public Iterator<String> getIterator() {
    // Mengembalikan objek yang mengimplementasikan Iterator
    return new MyCustomIterator();
}
```

Penggunaan interface sebagai tipe data meningkatkan fleksibilitas dan loose coupling dalam desain kode.

## Nested Interface

Interface dapat didefinisikan di dalam kelas atau interface lain, yang disebut **nested interface**:

```java
public class OuterClass {
    // Nested interface dalam kelas
    public interface NestedInterface {
        void nestedMethod();
    }
}

public interface OuterInterface {
    // Nested interface dalam interface
    interface NestedInterface {
        void nestedMethod();
    }
}

// Implementasi nested interface
public class Implementation implements OuterClass.NestedInterface {
    @Override
    public void nestedMethod() {
        System.out.println("Implementing nested interface");
    }
}
```

Nested interface berguna untuk mengelompokkan interface yang terkait dengan kelas atau interface tertentu.

## Interface Inheritance

Interface dapat mewarisi (extend) dari satu atau lebih interface lain:

```java
public interface BasicShape {
    double calculateArea();
}

public interface AdvancedShape extends BasicShape {
    double calculatePerimeter();
    void draw();
}

// Implementasi interface yang mewarisi interface lain
public class Circle implements AdvancedShape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing Circle");
    }
}
```

Interface inheritance memungkinkan kita untuk mengorganisasi hierarki interface dan mempromosikan reusability.

## Functional Interface (Java 8+)

**Functional interface** adalah interface yang hanya memiliki satu abstract method. Functional interface sangat penting untuk lambda expressions di Java 8+:

```java
// Functional interface ditandai dengan anotasi @FunctionalInterface
@FunctionalInterface
public interface Printable {
    void print(String message);
    
    // Default dan static methods diperbolehkan dalam functional interface
    default void printTwice(String message) {
        print(message);
        print(message);
    }
    
    static void printLine() {
        System.out.println("----------------");
    }
}

// Implementasi functional interface dengan anonymous class
Printable anonymousPrinter = new Printable() {
    @Override
    public void print(String message) {
        System.out.println("Anonymous: " + message);
    }
};

// Implementasi functional interface dengan lambda expression
Printable lambdaPrinter = message -> System.out.println("Lambda: " + message);

// Penggunaan
anonymousPrinter.print("Hello!");
lambdaPrinter.print("World!");
```

Java 8 juga menyediakan banyak built-in functional interfaces di package `java.util.function` seperti `Predicate<T>`, `Function<T, R>`, `Consumer<T>`, dan `Supplier<T>`.

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep interface dengan membuat aplikasi sederhana untuk mengelola berbagai jenis audio player di NetBeans.

### Langkah 1: Buat Project Baru

1. Buka NetBeans
2. Pilih **File** > **New Project**
3. Pilih **Java with Ant** > **Java Application**
4. Beri nama project `AudioPlayerSystem` dan klik **Finish**

### Langkah 2: Buat Interface `MediaPlayer`

1. Klik kanan pada package project > **New** > **Java Interface**
2. Beri nama `MediaPlayer` dan klik **Finish**
3. Isi dengan kode berikut:

```java
package audioplayersystem;

public interface MediaPlayer {
    // Constants
    int MIN_VOLUME = 0;
    int MAX_VOLUME = 100;
    
    // Abstract methods
    void play();
    void pause();
    void stop();
    void setVolume(int volume);
    int getVolume();
    
    // Default method
    default void increaseVolume(int amount) {
        int newVolume = getVolume() + amount;
        if (newVolume > MAX_VOLUME) {
            newVolume = MAX_VOLUME;
        }
        setVolume(newVolume);
        System.out.println("Volume increased to: " + getVolume());
    }
    
    // Default method
    default void decreaseVolume(int amount) {
        int newVolume = getVolume() - amount;
        if (newVolume < MIN_VOLUME) {
            newVolume = MIN_VOLUME;
        }
        setVolume(newVolume);
        System.out.println("Volume decreased to: " + getVolume());
    }
    
    // Static method
    static boolean isValidVolume(int volume) {
        return volume >= MIN_VOLUME && volume <= MAX_VOLUME;
    }
}
```

### Langkah 3: Buat Interface `EqualizerControl`

1. Klik kanan pada package project > **New** > **Java Interface**
2. Beri nama `EqualizerControl` dan klik **Finish**
3. Isi dengan kode berikut:

```java
package audioplayersystem;

public interface EqualizerControl {
    void setBass(int level);
    void setTreble(int level);
    void setPreset(String preset);
    
    // Default method
    default void resetEqualizer() {
        setBass(5);
        setTreble(5);
        setPreset("Flat");
        System.out.println("Equalizer reset to default settings");
    }
}
```

### Langkah 4: Buat Interface `BluetoothEnabled`

1. Klik kanan pada package project > **New** > **Java Interface**
2. Beri nama `BluetoothEnabled` dan klik **Finish**
3. Isi dengan kode berikut:

```java
package audioplayersystem;

public interface BluetoothEnabled {
    void connectBluetooth(String deviceName);
    void disconnectBluetooth();
    boolean isBluetoothConnected();
}
```

### Langkah 5: Buat Kelas `MusicPlayer` yang Mengimplementasikan `MediaPlayer`

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama `MusicPlayer` dan klik **Finish**
3. Isi dengan kode berikut:

```java
package audioplayersystem;

public class MusicPlayer implements MediaPlayer {
    private String name;
    private boolean isPlaying;
    private int volume;
    private String currentTrack;
    
    public MusicPlayer(String name) {
        this.name = name;
        this.isPlaying = false;
        this.volume = 50; // Default volume
        this.currentTrack = "No track selected";
    }
    
    public void setCurrentTrack(String track) {
        this.currentTrack = track;
        System.out.println(name + ": Track set to " + track);
    }
    
    @Override
    public void play() {
        isPlaying = true;
        System.out.println(name + ": Playing " + currentTrack + " at volume " + volume);
    }
    
    @Override
    public void pause() {
        isPlaying = false;
        System.out.println(name + ": Paused " + currentTrack);
    }
    
    @Override
    public void stop() {
        isPlaying = false;
        System.out.println(name + ": Stopped playback");
    }
    
    @Override
    public void setVolume(int volume) {
        if (MediaPlayer.isValidVolume(volume)) {
            this.volume = volume;
        } else {
            System.out.println("Invalid volume level. Must be between " + 
                               MediaPlayer.MIN_VOLUME + " and " + 
                               MediaPlayer.MAX_VOLUME);
        }
    }
    
    @Override
    public int getVolume() {
        return volume;
    }
    
    public boolean isPlaying() {
        return isPlaying;
    }
    
    public String getName() {
        return name;
    }
}
```

### Langkah 6: Buat Kelas `AdvancedMusicPlayer` yang Mengimplementasikan `MediaPlayer` dan `EqualizerControl`

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama `AdvancedMusicPlayer` dan klik **Finish**
3. Isi dengan kode berikut:

```java
package audioplayersystem;

public class AdvancedMusicPlayer implements MediaPlayer, EqualizerControl {
    private String name;
    private boolean isPlaying;
    private int volume;
    private String currentTrack;
    private int bassLevel;
    private int trebleLevel;
    private String currentPreset;
    
    public AdvancedMusicPlayer(String name) {
        this.name = name;
        this.isPlaying = false;
        this.volume = 50; // Default volume
        this.currentTrack = "No track selected";
        this.bassLevel = 5; // Default bass
        this.trebleLevel = 5; // Default treble
        this.currentPreset = "Flat"; // Default preset
    }
    
    public void setCurrentTrack(String track) {
        this.currentTrack = track;
        System.out.println(name + ": Track set to " + track);
    }
    
    @Override
    public void play() {
        isPlaying = true;
        System.out.println(name + ": Playing " + currentTrack + " at volume " + volume);
        System.out.println("Bass: " + bassLevel + ", Treble: " + trebleLevel + 
                          ", Preset: " + currentPreset);
    }
    
    @Override
    public void pause() {
        isPlaying = false;
        System.out.println(name + ": Paused " + currentTrack);
    }
    
    @Override
    public void stop() {
        isPlaying = false;
        System.out.println(name + ": Stopped playback");
    }
    
    @Override
    public void setVolume(int volume) {
        if (MediaPlayer.isValidVolume(volume)) {
            this.volume = volume;
        } else {
            System.out.println("Invalid volume level. Must be between " + 
                               MediaPlayer.MIN_VOLUME + " and " + 
                               MediaPlayer.MAX_VOLUME);
        }
    }
    
    @Override
    public int getVolume() {
        return volume;
    }
    
    @Override
    public void setBass(int level) {
        if (level >= 0 && level <= 10) {
            this.bassLevel = level;
            System.out.println(name + ": Bass set to " + level);
        } else {
            System.out.println("Invalid bass level. Must be between 0 and 10");
        }
    }
    
    @Override
    public void setTreble(int level) {
        if (level >= 0 && level <= 10) {
            this.trebleLevel = level;
            System.out.println(name + ": Treble set to " + level);
        } else {
            System.out.println("Invalid treble level. Must be between 0 and 10");
        }
    }
    
    @Override
    public void setPreset(String preset) {
        this.currentPreset = preset;
        System.out.println(name + ": Equalizer preset set to " + preset);
    }
    
    public boolean isPlaying() {
        return isPlaying;
    }
    
    public String getName() {
        return name;
    }
}
```

### Langkah 7: Buat Kelas `BluetoothMusicPlayer` yang Mengimplementasikan Semua Interface

1. Klik kanan pada package project > **New** > **Java Class**
2. Beri nama `BluetoothMusicPlayer` dan klik **Finish**
3. Isi dengan kode berikut:

```java
package audioplayersystem;

public class BluetoothMusicPlayer implements MediaPlayer, EqualizerControl, BluetoothEnabled {
    private String name;
    private boolean isPlaying;
    private int volume;
    private String currentTrack;
    private int bassLevel;
    private int trebleLevel;
    private String currentPreset;
    private boolean bluetoothConnected;
    private String connectedDevice;
    
    public BluetoothMusicPlayer(String name) {
        this.name = name;
        this.isPlaying = false;
        this.volume = 50; // Default volume
        this.currentTrack = "No track selected";
        this.bassLevel = 5; // Default bass
        this.trebleLevel = 5; // Default treble
        this.currentPreset = "Flat"; // Default preset
        this.bluetoothConnected = false;
        this.connectedDevice = null;
    }
    
    public void setCurrentTrack(String track) {
        this.currentTrack = track;
        System.out.println(name + ": Track set to " + track);
    }
    
    @Override
    public void play() {
        if (bluetoothConnected) {
            isPlaying = true;
            System.out.println(name + ": Playing " + currentTrack + " at volume " + volume);
            System.out.println("Bass: " + bassLevel + ", Treble: " + trebleLevel + 
                              ", Preset: " + currentPreset);
            System.out.println("Streaming via Bluetooth to " + connectedDevice);
        } else {
            System.out.println(name + ": Cannot play. No Bluetooth device connected.");
        }
    }
    
    @Override
    public void pause() {
        isPlaying = false;
        System.out.println(name + ": Paused " + currentTrack);
    }
    
    @Override
    public void stop() {
        isPlaying = false;
        System.out.println(name + ": Stopped playback");
    }
    
    @Override
    public void setVolume(int volume) {
        if (MediaPlayer.isValidVolume(volume)) {
            this.volume = volume;
        } else {
            System.out.println("Invalid volume level. Must be between " + 
                               MediaPlayer.MIN_VOLUME + " and " + 
                               MediaPlayer.MAX_VOLUME);
        }
    }
    
    @Override
    public int getVolume() {
        return volume;
    }
    
    @Override
    public void setBass(int level) {
        if (level >= 0 && level <= 10) {
            this.bassLevel = level;
            System.out.println(name + ": Bass set to " + level);
        } else {
            System.out.println("Invalid bass level. Must be between 0 and 10");
        }
    }
    
    @Override
    public void setTreble(int level) {
        if (level >= 0 && level <= 10) {
            this.trebleLevel = level;
            System.out.println(name + ": Treble set to " + level);
        } else {
            System.out.println("Invalid treble level. Must be between 0 and 10");
        }
    }
    
    @Override
    public void setPreset(String preset) {
        this.currentPreset = preset;
        System.out.println(name + ": Equalizer preset set to " + preset);
    }
    
    @Override
    public void connectBluetooth(String deviceName) {
        this.bluetoothConnected = true;
        this.connectedDevice = deviceName;
        System.out.println(name + ": Connected to Bluetooth device " + deviceName);
    }
    
    @Override
    public void disconnectBluetooth() {
        if (bluetoothConnected) {
            System.out.println(name + ": Disconnected from Bluetooth device " + connectedDevice);
            this.bluetoothConnected = false;
            this.connectedDevice = null;
        } else {
            System.out.println(name + ": No Bluetooth device connected");
        }
    }
    
    @Override
    public boolean isBluetoothConnected() {
        return bluetoothConnected;
    }
    
    public String getConnectedDevice() {
        return connectedDevice;
    }
    
    public boolean isPlaying() {
        return isPlaying;
    }
    
    public String getName() {
        return name;
    }
}
```

### Langkah 8: Buat Interface Functional untuk Demonstrasi

1. Klik kanan pada package project > **New** > **Java Interface**
2. Beri nama `PlaybackControl` dan klik **Finish**
3. Isi dengan kode berikut:

```java
package audioplayersystem;

@FunctionalInterface
public interface PlaybackControl {
    void control(MediaPlayer player);
    
    // Static utility method
    static void playAll(MediaPlayer[] players) {
        for (MediaPlayer player : players) {
            player.play();
        }
    }
}
```

### Langkah 9: Buat Kelas Main

1. Buka file main (biasanya `AudioPlayerSystem.java`)
2. Ubah kode menjadi:

```java
package audioplayersystem;

public class AudioPlayerSystem {
    public static void main(String[] args) {
        System.out.println("=== BASIC MUSIC PLAYER DEMO ===");
        MusicPlayer basicPlayer = new MusicPlayer("Basic Player");
        basicPlayer.setCurrentTrack("Shape of You - Ed Sheeran");
        basicPlayer.setVolume(60);
        basicPlayer.play();
        basicPlayer.increaseVolume(15);
        basicPlayer.pause();
        basicPlayer.decreaseVolume(25);
        basicPlayer.play();
        basicPlayer.stop();
        
        System.out.println("\n=== ADVANCED MUSIC PLAYER DEMO ===");
        AdvancedMusicPlayer advancedPlayer = new AdvancedMusicPlayer("Advanced Player");
        advancedPlayer.setCurrentTrack("Bohemian Rhapsody - Queen");
        advancedPlayer.setVolume(70);
        advancedPlayer.setBass(8);
        advancedPlayer.setTreble(6);
        advancedPlayer.setPreset("Rock");
        advancedPlayer.play();
        advancedPlayer.pause();
        advancedPlayer.resetEqualizer();
        advancedPlayer.play();
        advancedPlayer.stop();
        
        System.out.println("\n=== BLUETOOTH MUSIC PLAYER DEMO ===");
        BluetoothMusicPlayer bluetoothPlayer = new BluetoothMusicPlayer("Bluetooth Player");
        bluetoothPlayer.setCurrentTrack("Believer - Imagine Dragons");
        bluetoothPlayer.setVolume(65);
        bluetoothPlayer.setBass(7);
        bluetoothPlayer.setTreble(7);
        bluetoothPlayer.setPreset("Pop");
        
        // Try to play without connecting Bluetooth
        bluetoothPlayer.play();
        
        // Connect Bluetooth and try again
        bluetoothPlayer.connectBluetooth("Sony WH-1000XM4");
        bluetoothPlayer.play();
        bluetoothPlayer.pause();
        bluetoothPlayer.disconnectBluetooth();
        
        System.out.println("\n=== INTERFACE AS TYPE DEMO ===");
        MediaPlayer[] players = {basicPlayer, advancedPlayer, bluetoothPlayer};
        
        for (MediaPlayer player : players) {
            player.setVolume(50);
            player.play();
        }
        
        EqualizerControl[] equalizerPlayers = {advancedPlayer, bluetoothPlayer};
        
        for (EqualizerControl player : equalizerPlayers) {
            player.resetEqualizer();
        }
        
        System.out.println("\n=== FUNCTIONAL INTERFACE DEMO ===");
        // Using anonymous class
        PlaybackControl playController = new PlaybackControl() {
            @Override
            public void control(MediaPlayer player) {
                player.play();
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                player.pause();
            }
        };
        
        // Using lambda expression
        PlaybackControl stopController = player -> {
            System.out.println("Lambda controlling: " + 
                              (player instanceof MusicPlayer ? ((MusicPlayer)player).getName() : "Unknown"));
            player.stop();
        };
        
        playController.control(basicPlayer);
        stopController.control(advancedPlayer);
        
        // Using static method
        System.out.println("\n=== PLAYING ALL PLAYERS ===");
        bluetoothPlayer.connectBluetooth("Sony WH-1000XM4");
        PlaybackControl.playAll(players);
    }
}
```

### Langkah 10: Jalankan Program

1. Klik **Run** > **Run Project**
2. Atau tekan tombol F6

### Penjelasan

Dalam contoh praktik di atas, kita telah mengimplementasikan berbagai aspek interface di Java:

1. **Definisi Interface**:
   - `MediaPlayer`: Interface dasar dengan abstract methods, default methods, dan static method
   - `EqualizerControl`: Interface untuk kontrol equalizer
   - `BluetoothEnabled`: Interface untuk fungsionalitas Bluetooth
   - `PlaybackControl`: Functional interface

2. **Multiple Interface Implementation**:
   - `MusicPlayer`: Mengimplementasikan `MediaPlayer`
   - `AdvancedMusicPlayer`: Mengimplementasikan `MediaPlayer` dan `EqualizerControl`
   - `BluetoothMusicPlayer`: Mengimplementasikan `MediaPlayer`, `EqualizerControl`, dan `BluetoothEnabled`

3. **Interface sebagai Tipe Data**:
   - Array `MediaPlayer[]` yang berisi objek dari berbagai kelas implementasi
   - Array `EqualizerControl[]` untuk mengelompokkan objek yang memiliki kontrol equalizer

4. **Functional Interface dan Lambda**:
   - Implementasi `PlaybackControl` dengan anonymous class
   - Implementasi `PlaybackControl` dengan lambda expression
   - Penggunaan static method dalam functional interface

## Rangkuman

Dalam bab ini, kita telah mempelajari:

✅ **Interface** adalah kontrak yang berisi deklarasi method yang harus diimplementasikan oleh kelas-kelas yang menggunakannya

✅ **Perbedaan** antara interface, abstract class, dan class biasa

✅ **Fields dalam interface** selalu bersifat `public`, `static`, dan `final`

✅ **Methods dalam interface** secara tradisional bersifat `public` dan `abstract`

✅ **Keyword `implements`** digunakan untuk mengimplementasikan interface

✅ **Multiple interface implementation** memungkinkan kelas untuk "mewarisi" behavior dari banyak sumber

✅ **Fitur modern interface** seperti default methods, static methods, dan private methods

✅ **Interface sebagai tipe data** untuk mencapai polimorfisme

✅ **Nested interface** untuk mengelompokkan interface terkait

✅ **Interface inheritance** untuk mengorganisasi hierarki interface

✅ **Functional interface** sebagai dasar untuk lambda expressions

Interface adalah komponen penting dalam pemrograman Java yang memungkinkan desain yang fleksibel, modular, dan mudah diperluas. Dengan memahami dan menggunakan interface secara efektif, Anda dapat membuat kode yang lebih bersih, lebih mudah di-maintain, dan lebih robust.

## Latihan Soal

1. Apa perbedaan utama antara interface dan abstract class di Java? Kapan sebaiknya menggunakan masing-masing?

2. Apa yang dimaksud dengan multiple interface implementation? Berikan contoh kasus penggunaan di dunia nyata.

3. Jelaskan fitur default methods dalam interface yang diperkenalkan di Java 8. Apa keuntungan dari fitur ini?

4. Bagaimana cara interface digunakan untuk mencapai polimorfisme? Berikan contoh kode.

5. Apa itu functional interface? Bagaimana hubungannya dengan lambda expressions di Java 8+?

6. Buatlah system e-commerce sederhana dengan interface `Payable` yang memiliki method `pay()`. Buat tiga implementasi berbeda: `CreditCardPayment`, `PayPalPayment`, dan `BankTransferPayment`.

7. Bagaimana cara mengatasi "diamond problem" dalam multiple inheritance menggunakan interface di Java? Berikan contoh kode.

8. Buatlah interface `Sortable` dengan method untuk mengurutkan data. Implementasikan interface ini di class `StudentList` menggunakan algoritma bubble sort dan di class `CourseList` menggunakan algoritma selection sort.

9. Jelaskan perbedaan antara `Object` class dan interface di Java. Mengapa semua class di Java secara implisit mewarisi dari `Object`?

10. Desain sebuah sistem perpustakaan dengan minimal 3 interface yang berbeda. Implementasikan sistem tersebut dengan beberapa class yang mengimplementasikan interface-interface tersebut.

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional. (Chapter 4: Interfaces, Item 20: Prefer interfaces to abstract classes)

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson. (Chapter 10: Object-Oriented Programming: Polymorphism and Interfaces)

3. Evans, B., & Warburton, R. (2018). *Java in a Nutshell: A Desktop Quick Reference* (7th ed.). O'Reilly Media. (Chapter 3: Classes and Objects, Section: Interfaces)

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional. (Chapter 1: Introduction to Design Patterns)

5. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall. (Chapter 6: Interfaces, Lambda Expressions, and Inner Classes)

6. Oracle. (2022). *Java Language Specification: Interfaces*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-9.html](https://docs.oracle.com/javase/specs/jls/se17/html/jls-9.html)

7. Oracle. (2022). *Java Tutorial: Interfaces and Inheritance*. [https://docs.oracle.com/javase/tutorial/java/IandI/index.html](https://docs.oracle.com/javase/tutorial/java/IandI/index.html)

8. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education. (Chapter 8: Interfaces)

9. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media. (Chapter 8: Interfaces and Polymorphism)

10. Urma, R.-G., Fusco, M., & Mycroft, A. (2014). *Java 8 in Action: Lambdas, Streams, and Functional-Style Programming*. Manning Publications. (Chapter 9: Default methods)

---

[◀️ Kembali ke Tutorial #07: Memahami Konsep Polimorfisme di Java](07-polymorphism.md) | [Lanjut ke Tutorial #09: Mengenal Class Abstract ▶️](09-abstract-classes.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.

