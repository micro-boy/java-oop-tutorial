# 📘 Tutorial Java OOP #12: Exception Handling dalam OOP

> *"Exception handling adalah jaring pengaman dalam kode Anda—memungkinkan program untuk menangani kesalahan dengan anggun dan memberikan umpan balik yang bermakna alih-alih crash tanpa peringatan."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dasar exception handling dalam Java
- Membedakan jenis-jenis exception: checked, unchecked, dan error
- Mengimplementasikan try-catch-finally blocks dengan benar
- Membuat dan menggunakan custom exception
- Memahami exception propagation dan exception chaining
- Menggunakan try-with-resources untuk resource management
- Menerapkan best practices dalam exception handling
- Mendokumentasikan exceptions dengan JavaDoc
- Menerapkan exception handling dalam aplikasi Java nyata

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Apa itu Exception?](#apa-itu-exception)
   - [Definisi dan Konsep Dasar](#definisi-dan-konsep-dasar)
   - [Error vs Exception](#error-vs-exception)
   - [Checked Exception vs Unchecked Exception](#checked-exception-vs-unchecked-exception)
3. [Hierarki Exception di Java](#hierarki-exception-di-java)
   - [Class Throwable dan Turunannya](#class-throwable-dan-turunannya)
   - [Common Exceptions di Java](#common-exceptions-di-java)
4. [Menangani Exception](#menangani-exception)
   - [Try-Catch Block](#try-catch-block)
   - [Multiple Catch Blocks](#multiple-catch-blocks)
   - [Finally Block](#finally-block)
   - [Try-with-Resources](#try-with-resources)
5. [Throwing Exceptions](#throwing-exceptions)
   - [Keyword throw](#keyword-throw)
   - [Keyword throws](#keyword-throws)
   - [Exception Propagation](#exception-propagation)
6. [Custom Exceptions](#custom-exceptions)
   - [Membuat Custom Exception Class](#membuat-custom-exception-class)
   - [Best Practices dalam Custom Exception](#best-practices-dalam-custom-exception)
7. [Exception Chaining](#exception-chaining)
   - [Konsep Exception Chaining](#konsep-exception-chaining)
   - [Mengimplementasikan Exception Chaining](#mengimplementasikan-exception-chaining)
8. [Best Practices dalam Exception Handling](#best-practices-dalam-exception-handling)
   - [Do's and Don'ts](#dos-and-donts)
   - [Exception Handling in OOP](#exception-handling-in-oop)
   - [Logging Exceptions](#logging-exceptions)
9. [Mendokumentasikan Exceptions](#mendokumentasikan-exceptions)
   - [JavaDoc untuk Exceptions](#javadoc-untuk-exceptions)
   - [Meaningful Error Messages](#meaningful-error-messages)
10. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
11. [Rangkuman](#rangkuman)
12. [Latihan Soal](#latihan-soal)
13. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari berbagai konsep pemrograman berorientasi objek (OOP) di Java, dari kelas dan objek hingga konsep-konsep lanjutan seperti polimorfisme, interface, abstract class, anonymous class, dan lambda expressions. Semua konsep ini membantu kita membuat aplikasi yang terstruktur, modular, dan mudah dipelihara.

Namun, tidak peduli seberapa baik kode kita, hal-hal yang tidak terduga tetap bisa terjadi saat runtime. Pengguna bisa memasukkan input yang tidak valid, file yang diharapkan mungkin tidak ada, koneksi jaringan bisa terputus, atau sistem bisa kehabisan memori. Situasi-situasi ini dapat menyebabkan program crash jika tidak ditangani dengan benar.

Di sinilah exception handling menjadi sangat penting. Exception handling adalah mekanisme yang memberikan cara untuk mendeteksi dan menangani situasi pengecualian (exceptional situations) selama eksekusi program. Ini memungkinkan program untuk melanjutkan atau berhenti dengan cara yang terkendali, daripada crash secara tidak terduga.

Dalam tutorial ini, kita akan mempelajari bagaimana Java mengimplementasikan exception handling dan bagaimana menggunakannya secara efektif dalam aplikasi berorientasi objek.

## Apa itu Exception?

### Definisi dan Konsep Dasar

**Exception** (pengecualian) adalah kejadian yang mengganggu aliran normal eksekusi program. Ketika exception terjadi, aliran normal program terganggu, dan jika tidak ditangani, program akan berhenti.

Exception terjadi karena berbagai alasan:
- Kesalahan pengguna (misalnya input yang tidak valid)
- Masalah hardware (misalnya disk penuh)
- Kesalahan jaringan (misalnya server tidak tersedia)
- Kesalahan pemrograman (misalnya akses array di luar batas)
- Ketidaktersediaan resource (misalnya file tidak ditemukan)

Dalam Java, exception direpresentasikan sebagai objek yang mengenkapsulasi informasi tentang situasi pengecualian, seperti jenis kesalahan, keadaan program saat kesalahan terjadi, dan pesan yang menjelaskan kesalahan tersebut.

### Error vs Exception

Java membedakan antara **Error** dan **Exception**:

- **Error**: Mewakili masalah serius yang biasanya tidak dapat dipulihkan oleh aplikasi. Errors biasanya disebabkan oleh masalah di luar kontrol aplikasi, seperti masalah di JVM itu sendiri. Contohnya adalah `OutOfMemoryError`, `StackOverflowError`, dan `NoClassDefFoundError`. Program tidak diharapkan untuk menangkap atau menangani errors.

- **Exception**: Mewakili kondisi yang mungkin dapat dipulihkan oleh aplikasi. Exceptions bisa disebabkan oleh kesalahan dalam kode aplikasi atau oleh kondisi eksternal. Program diharapkan untuk menangkap dan menangani exceptions untuk mencegah crash.

### Checked Exception vs Unchecked Exception

Java lebih lanjut membagi exceptions menjadi dua kategori utama:

1. **Checked Exceptions**:
   - Exceptions yang harus di-declare dalam klausa `throws` method atau di-catch di dalam method.
   - Kompiler memeriksa apakah method menangani checked exceptions.
   - Merupakan subclass dari `Exception` tapi bukan subclass dari `RuntimeException`.
   - Contoh: `IOException`, `SQLException`, `ClassNotFoundException`.
   - Biasanya digunakan untuk kondisi yang dapat dipulihkan dan melibatkan interaksi eksternal.

2. **Unchecked Exceptions**:
   - Exceptions yang tidak perlu di-declare atau di-catch secara eksplisit.
   - Merupakan subclass dari `RuntimeException`.
   - Contoh: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException`.
   - Biasanya digunakan untuk kesalahan pemrograman atau situasi yang seharusnya tidak terjadi.

## Hierarki Exception di Java

### Class Throwable dan Turunannya

Semua exceptions di Java berasal dari class `Throwable`. Hierarki utama exception adalah sebagai berikut:

```
Throwable
|
|-- Error (Unchecked)
|   |-- OutOfMemoryError
|   |-- StackOverflowError
|   |-- ...
|
|-- Exception (Mostly Checked)
    |-- IOException
    |-- SQLException
    |-- ClassNotFoundException
    |-- ...
    |
    |-- RuntimeException (Unchecked)
        |-- NullPointerException
        |-- ArrayIndexOutOfBoundsException
        |-- ArithmeticException
        |-- IllegalArgumentException
        |-- ...
```

### Common Exceptions di Java

Berikut adalah beberapa exceptions umum yang sering ditemui dalam pemrograman Java:

**Unchecked Exceptions (RuntimeException)**:
- `NullPointerException`: Terjadi ketika mencoba mengakses method atau field dari referensi null.
- `ArrayIndexOutOfBoundsException`: Terjadi ketika mencoba mengakses indeks array yang tidak valid.
- `ArithmeticException`: Terjadi ketika operasi aritmatika memiliki kesalahan, seperti pembagian dengan nol.
- `IllegalArgumentException`: Terjadi ketika method menerima argumen yang tidak valid.
- `IllegalStateException`: Terjadi ketika method dipanggil pada waktu yang tidak tepat.
- `ClassCastException`: Terjadi ketika mencoba melakukan cast objek ke subclass yang tidak sesuai.

**Checked Exceptions**:
- `IOException`: Terjadi saat operasi I/O gagal atau terganggu.
- `FileNotFoundException`: Terjadi ketika mencoba mengakses file yang tidak ada.
- `SQLException`: Terjadi saat ada masalah dengan database.
- `ClassNotFoundException`: Terjadi ketika JVM tidak dapat menemukan class.
- `InterruptedException`: Terjadi ketika thread terganggu saat sedang sleep, wait, atau tertahan.

## Menangani Exception

### Try-Catch Block

Cara paling umum untuk menangani exception adalah menggunakan blok `try-catch`:

```java
try {
    // Code that might throw an exception
    int result = 10 / 0;  // This will throw ArithmeticException
} catch (ArithmeticException e) {
    // Code to handle the exception
    System.err.println("Error: Division by zero is not allowed.");
    System.err.println("Exception message: " + e.getMessage());
    e.printStackTrace();  // Prints stack trace for debugging
}
```

Dalam contoh di atas:
- Kode yang mungkin throw exception ditempatkan dalam blok `try`.
- Jika exception terjadi, eksekusi blok `try` berhenti dan control pindah ke blok `catch` yang sesuai.
- Blok `catch` menangkap exception spesifik (`ArithmeticException` dalam contoh ini) dan menanganinya.

### Multiple Catch Blocks

Anda dapat memiliki beberapa blok `catch` untuk menangani berbagai jenis exception:

```java
try {
    File file = new File("nonexistent.txt");
    FileInputStream fis = new FileInputStream(file);  // Might throw FileNotFoundException
    int data = fis.read();  // Might throw IOException
    System.out.println("Data: " + data);
} catch (FileNotFoundException e) {
    System.err.println("Error: File not found.");
    e.printStackTrace();
} catch (IOException e) {
    System.err.println("Error: Problem reading from file.");
    e.printStackTrace();
} catch (Exception e) {
    // Catches any other exceptions not caught by previous catch blocks
    System.err.println("An unexpected error occurred.");
    e.printStackTrace();
}
```

**Penting**: Ketika menggunakan multiple catch blocks, blok untuk subclass harus muncul sebelum blok untuk superclass. Jika tidak, kompiler akan menampilkan error karena blok untuk superclass akan menangkap semua exceptions, membuat blok untuk subclass tidak dapat dijangkau.

Sejak Java 7, Anda juga dapat menangkap multiple exceptions dalam satu blok catch menggunakan operator `|`:

```java
try {
    // Code that might throw exceptions
} catch (FileNotFoundException | NullPointerException e) {
    // Handle both exceptions the same way
    System.err.println("Either file not found or null pointer: " + e.getMessage());
}
```

### Finally Block

Blok `finally` berisi kode yang akan dieksekusi selalu, terlepas dari apakah exception terjadi atau tidak:

```java
FileInputStream fis = null;
try {
    fis = new FileInputStream("example.txt");
    // Process file
} catch (IOException e) {
    System.err.println("Error processing file: " + e.getMessage());
} finally {
    // This block always executes
    if (fis != null) {
        try {
            fis.close();  // Close the resource
        } catch (IOException e) {
            System.err.println("Error closing file: " + e.getMessage());
        }
    }
    System.out.println("Processing complete.");
}
```

Blok `finally` sangat berguna untuk:
- Membersihkan resources (seperti menutup file atau koneksi database)
- Mengeksekusi kode yang harus dijalankan terlepas dari apakah exception terjadi atau tidak

### Try-with-Resources

Java 7 memperkenalkan try-with-resources statement, yang menyederhanakan penanganan resources yang harus ditutup setelah digunakan:

```java
try (FileInputStream fis = new FileInputStream("example.txt");
     FileOutputStream fos = new FileOutputStream("output.txt")) {
    // Process files
    int data;
    while ((data = fis.read()) != -1) {
        fos.write(data);
    }
} catch (IOException e) {
    System.err.println("Error processing files: " + e.getMessage());
}
// Resources (fis and fos) are automatically closed
```

Dalam try-with-resources:
- Resources didefinisikan dalam tanda kurung setelah keyword `try`.
- Resources harus mengimplementasikan interface `AutoCloseable` atau `Closeable`.
- Resources ditutup secara otomatis di akhir blok try (bahkan jika exception terjadi).
- Resources ditutup dalam urutan terbalik dari urutan pembuatannya.

## Throwing Exceptions

### Keyword throw

Keyword `throw` digunakan untuk eksplisit melempar exception:

```java
public void validateAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
    if (age > 150) {
        throw new IllegalArgumentException("Age cannot be greater than 150");
    }
    
    // If age is valid, continue with the method
    System.out.println("Age is valid: " + age);
}
```

### Keyword throws

Keyword `throws` digunakan dalam signature method untuk mendeklarasikan bahwa method tersebut mungkin melempar exceptions tertentu:

```java
public void readFile(String filename) throws FileNotFoundException, IOException {
    FileInputStream fis = new FileInputStream(filename);  // Might throw FileNotFoundException
    int data = fis.read();  // Might throw IOException
    // Process file
    fis.close();
}
```

Method yang memanggil method dengan deklarasi `throws` harus:
- Menangkap exceptions yang dideklarasikan, atau
- Meneruskan exceptions tersebut dengan deklarasi `throws` miliknya sendiri

**Penting**: Untuk checked exceptions, Anda harus menggunakan `throws` dalam signature method atau menangkap exception di dalam method. Untuk unchecked exceptions, `throws` bersifat opsional tapi berguna untuk dokumentasi.

### Exception Propagation

Exception propagation adalah proses di mana exception yang tidak tertangani dalam satu method diteruskan ke method pemanggil. Propagation berlanjut hingga exception ditangkap atau mencapai puncak stack call (biasanya method `main` atau method yang menangani thread).

```java
public void method3() {
    int result = 10 / 0;  // Throws ArithmeticException
}

public void method2() {
    method3();  // Exception propagates to method2
}

public void method1() {
    try {
        method2();  // Exception propagates to method1
    } catch (ArithmeticException e) {
        System.err.println("Caught in method1: " + e.getMessage());
    }
}
```

Ketika exception terjadi di `method3()`, tidak ada blok catch yang menanganinya, sehingga exception diteruskan ke `method2()`. `method2()` juga tidak menangkap exception, sehingga exception diteruskan ke `method1()`, di mana akhirnya ditangkap oleh blok catch.

## Custom Exceptions

### Membuat Custom Exception Class

Kadang-kadang exceptions standar Java tidak cukup untuk menggambarkan situasi pengecualian spesifik dalam domain aplikasi Anda. Dalam kasus ini, Anda dapat membuat custom exception class Anda sendiri:

```java
// Checked custom exception
public class InsufficientFundsException extends Exception {
    private double amount;
    
    public InsufficientFundsException(double amount) {
        super("Insufficient funds: you need " + amount + " more to complete this transaction");
        this.amount = amount;
    }
    
    public double getAmount() {
        return amount;
    }
}

// Unchecked custom exception
public class UserNotFoundException extends RuntimeException {
    private String userId;
    
    public UserNotFoundException(String userId) {
        super("User not found with ID: " + userId);
        this.userId = userId;
    }
    
    public String getUserId() {
        return userId;
    }
}
```

Penggunaan custom exceptions:

```java
public class BankAccount {
    private String accountNumber;
    private double balance;
    
    // Constructor and other methods
    
    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount <= 0) {
            throw new IllegalArgumentException("Amount must be positive");
        }
        
        if (amount > balance) {
            throw new InsufficientFundsException(amount - balance);
        }
        
        balance -= amount;
        System.out.println("Withdrawal successful. New balance: " + balance);
    }
}
```

### Best Practices dalam Custom Exception

1. **Penamaan yang Jelas**: Nama exception harus menggambarkan situasi pengecualian dengan jelas. Biasanya diakhiri dengan "Exception".
2. **Pilih Superclass yang Tepat**: Extend `Exception` untuk checked exceptions dan `RuntimeException` untuk unchecked exceptions.
3. **Sertakan Informasi Relevan**: Custom exceptions harus menyertakan informasi yang relevan tentang kesalahan. Ini bisa berupa konstruktor dengan parameter atau getter methods.
4. **Jaga Serialization**: Jika aplikasi Anda mungkin menyebarkan exceptions melalui JVM atau jaringan, pastikan exceptions adalah serializable (dengan menambahkan `serialVersionUID`).
5. **Sediakan Konstruktor yang Berguna**: Minimal, berikan konstruktor tanpa parameter dan konstruktor dengan pesan kesalahan.

## Exception Chaining

### Konsep Exception Chaining

Exception chaining adalah teknik di mana exception ditangkap dan dibungkus dalam exception lain, biasanya pada tingkat abstraksi yang lebih tinggi. Ini memungkinkan kode untuk memperlakukan kesalahan pada tingkat yang sesuai sambil mempertahankan informasi tentang penyebab awal.

### Mengimplementasikan Exception Chaining

Java mendukung exception chaining melalui konstruktor yang menerima `Throwable cause`:

```java
public void processFile(String filename) throws ServiceException {
    try {
        // Code that might throw IOException
        FileInputStream fis = new FileInputStream(filename);
        // Process file...
    } catch (IOException e) {
        // Wrap the low-level IOException in a higher-level ServiceException
        throw new ServiceException("Error processing file: " + filename, e);
    }
}

// Custom exception with chaining support
public class ServiceException extends Exception {
    public ServiceException(String message) {
        super(message);
    }
    
    public ServiceException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

Dengan exception chaining:
- Anda dapat membuat API yang bersih dengan exceptions yang bermakna untuk domain Anda.
- Anda tetap mempertahankan informasi tentang penyebab awal kesalahan dengan `getCause()`.
- Stack trace akan menampilkan keduanya, exception asli dan exception pembungkus.

## Best Practices dalam Exception Handling

### Do's and Don'ts

**Do**:
- Gunakan exceptions untuk situasi pengecualian saja, bukan untuk control flow biasa.
- Tangkap exceptions yang specific daripada menangkap `Exception` generik.
- Selalu berikan informasi yang berguna dalam pesan exception.
- Selalu tutup resources dalam blok `finally` atau gunakan try-with-resources.
- Log exceptions dengan informasi kontekstual yang cukup.
- Dokumentasikan exceptions yang mungkin dilempar oleh method publik Anda.

**Don't**:
- Jangan "swallow" exceptions (menangkap exceptions tanpa menanganinya dengan benar).
- Jangan menangkap exceptions yang tidak dapat Anda tangani.
- Jangan menggunakan exceptions untuk control flow biasa.
- Jangan mengkonversi checked exceptions menjadi unchecked exceptions tanpa alasan yang bagus.
- Jangan membuat try blocks terlalu besar; tangkap exceptions sedekat mungkin dengan sumbernya.
- Jangan menggunakan `e.printStackTrace()` dalam kode produksi; gunakan framework logging yang tepat.

### Exception Handling in OOP

Dalam OOP, exception handling harus:

1. **Mengikuti Principle of Encapsulation**: 
   - Gunakan custom exceptions untuk domain Anda.
   - Jangan menampilkan detail implementasi internal.

2. **Menghormati Interface Contracts**:
   - Dokumentasikan exceptions yang mungkin dilempar.
   - Pertimbangkan exceptions sebagai bagian dari kontrak.

3. **Menjaga Abstraction Levels**:
   - Low-level exceptions harus ditangkap dan dibungkus dalam exceptions yang bermakna bagi abstraction level method Anda.

Contoh pendekatan OOP untuk exception handling:

```java
// Domain-specific exception
public class OrderProcessingException extends Exception {
    // Constructors and methods
}

// Service interface
public interface OrderService {
    void placeOrder(Order order) throws OrderProcessingException;
}

// Service implementation
public class OrderServiceImpl implements OrderService {
    private InventoryRepository inventoryRepo;
    private PaymentGateway paymentGateway;
    
    @Override
    public void placeOrder(Order order) throws OrderProcessingException {
        try {
            // Check inventory
            if (!inventoryRepo.checkAvailability(order.getItems())) {
                throw new OrderProcessingException("Some items are out of stock");
            }
            
            // Process payment
            paymentGateway.processPayment(order.getPayment());
            
            // Other processing steps...
        } catch (InventoryException e) {
            throw new OrderProcessingException("Inventory error: " + e.getMessage(), e);
        } catch (PaymentException e) {
            throw new OrderProcessingException("Payment error: " + e.getMessage(), e);
        }
    }
}
```

### Logging Exceptions

Logging yang tepat untuk exceptions sangat penting untuk debugging dan pemecahan masalah:

```java
import java.util.logging.Logger;
import java.util.logging.Level;

public class ExceptionLoggingExample {
    private static final Logger LOGGER = Logger.getLogger(ExceptionLoggingExample.class.getName());
    
    public void processData(String data) {
        try {
            // Process data...
            if (data == null) {
                throw new IllegalArgumentException("Data cannot be null");
            }
            
            // More processing...
        } catch (IllegalArgumentException e) {
            // Log with appropriate level and context
            LOGGER.log(Level.WARNING, "Invalid data provided", e);
            // Maybe rethrow or handle differently
        } catch (Exception e) {
            // Log unexpected errors
            LOGGER.log(Level.SEVERE, "Unexpected error processing data: " + data, e);
            throw new RuntimeException("Data processing failed", e);
        }
    }
}
```

Best practices untuk logging exceptions:
- Selalu sertakan exception object dalam log (jangan hanya pesan).
- Sertakan informasi kontekstual yang cukup.
- Gunakan log level yang tepat (ERROR, WARNING, INFO, etc.).
- Pertimbangkan untuk menggunakan framework logging seperti Log4j, SLF4J, atau Logback untuk aplikasi besar.

## Mendokumentasikan Exceptions

### JavaDoc untuk Exceptions

Mendokumentasikan exceptions yang mungkin dilempar oleh method Anda:

```java
/**
 * Opens the specified file and returns an InputStream to read from it.
 * 
 * @param filename the name of the file to open
 * @return an InputStream for reading from the file
 * @throws FileNotFoundException if the file does not exist or cannot be opened
 * @throws SecurityException if a security manager exists and denies read access to the file
 */
public InputStream openFile(String filename) throws FileNotFoundException {
    return new FileInputStream(filename);
}
```

### Meaningful Error Messages

Pesan kesalahan yang baik harus:
- Jelas dan spesifik
- Memberikan informasi yang cukup untuk memahami dan menyelesaikan masalah
- Ditulis dari perspektif pengguna (jika pesan akan dilihat oleh pengguna)

Contoh pesan kesalahan yang baik:
```java
throw new IllegalArgumentException("Username must be between 3 and 20 characters");
```

vs pesan yang buruk:
```java
throw new IllegalArgumentException("Bad username");
```

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep exception handling dengan membuat aplikasi sederhana di NetBeans.

### Langkah 1: Buat Project Baru

1. Buka NetBeans
2. Pilih `File > New Project`
3. Pilih `Java with Ant > Java Application`
4. Beri nama project `ExceptionHandlingDemo` dan klik `Finish`

### Langkah 2: Buat Custom Exception Classes

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `InsufficientFundsException` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package exceptionhandlingdemo;

public class InsufficientFundsException extends Exception {
    private double shortfall;
    
    public InsufficientFundsException(double shortfall) {
        super("Insufficient funds: shortfall of $" + String.format("%.2f", shortfall));
        this.shortfall = shortfall;
    }
    
    public double getShortfall() {
        return shortfall;
    }
}
```

4. Buat class exception lainnya:

```java
package exceptionhandlingdemo;

public class InvalidAccountException extends Exception {
    private String accountId;
    
    public InvalidAccountException(String accountId) {
        super("Invalid account: " + accountId);
        this.accountId = accountId;
    }
    
    public String getAccountId() {
        return accountId;
    }
}
```

### Langkah 3: Buat Model Class

1. Buat class `BankAccount`:

```java
package exceptionhandlingdemo;

public class BankAccount {
    private String accountId;
    private String ownerName;
    private double balance;
    
    public BankAccount(String accountId, String ownerName, double initialBalance) {
        if (accountId == null || accountId.trim().isEmpty()) {
            throw new IllegalArgumentException("Account ID cannot be null or empty");
        }
        if (ownerName == null || ownerName.trim().isEmpty()) {
            throw new IllegalArgumentException("Owner name cannot be null or empty");
        }
        if (initialBalance < 0) {
            throw new IllegalArgumentException("Initial balance cannot be negative");
        }
        
        this.accountId = accountId;
        this.ownerName = ownerName;
        this.balance = initialBalance;
    }
    
    public String getAccountId() {
        return accountId;
    }
    
    public String getOwnerName() {
        return ownerName;
    }
    
    public double getBalance() {
        return balance;
    }
    
    public void deposit(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Deposit amount must be positive");
        }
        
        balance += amount;
        System.out.println("Deposited $" + String.format("%.2f", amount) + 
                         ". New balance: $" + String.format("%.2f", balance));
    }
    
    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount <= 0) {
            throw new IllegalArgumentException("Withdrawal amount must be positive");
        }
        
        if (amount > balance) {
            double shortfall = amount - balance;
            throw new InsufficientFundsException(shortfall);
        }
        
        balance -= amount;
        System.out.println("Withdrew $" + String.format("%.2f", amount) + 
                         ". New balance: $" + String.format("%.2f", balance));
    }
    
    @Override
    public String toString() {
        return "Account ID: " + accountId + 
               ", Owner: " + ownerName + 
               ", Balance: $" + String.format("%.2f", balance);
    }
}
```

### Langkah 4: Buat Service Class

1. Buat class `BankService`:

```java
package exceptionhandlingdemo;

import java.util.HashMap;
import java.util.Map;
import java.util.logging.Logger;
import java.util.logging.Level;

public class BankService {
    private static final Logger LOGGER = Logger.getLogger(BankService.class.getName());
    
    private Map<String, BankAccount> accounts;
    
    public BankService() {
        accounts = new HashMap<>();
    }
    
    public void createAccount(String accountId, String ownerName, double initialBalance) {
        try {
            if (accounts.containsKey(accountId)) {
                throw new IllegalArgumentException("Account ID already exists: " + accountId);
            }
            
            BankAccount account = new BankAccount(accountId, ownerName, initialBalance);
            accounts.put(accountId, account);
            System.out.println("Account created successfully: " + account);
        } catch (IllegalArgumentException e) {
            LOGGER.log(Level.WARNING, "Failed to create account", e);
            System.err.println("Error: " + e.getMessage());
        }
    }
    
    public BankAccount findAccount(String accountId) throws InvalidAccountException {
        BankAccount account = accounts.get(accountId);
        
        if (account == null) {
            throw new InvalidAccountException(accountId);
        }
        
        return account;
    }
    
    public void transferFunds(String fromAccountId, String toAccountId, double amount) {
        try {
            // Input validation
            if (amount <= 0) {
                throw new IllegalArgumentException("Transfer amount must be positive");
            }
            
            // Find accounts
            BankAccount fromAccount = findAccount(fromAccountId);
            BankAccount toAccount = findAccount(toAccountId);
            
            // Perform transfer
            System.out.println("Transferring $" + String.format("%.2f", amount) + 
                             " from " + fromAccount.getOwnerName() + 
                             " to " + toAccount.getOwnerName());
            
            fromAccount.withdraw(amount);
            toAccount.deposit(amount);
            
            System.out.println("Transfer completed successfully");
        } catch (InvalidAccountException e) {
            LOGGER.log(Level.WARNING, "Account not found", e);
            System.err.println("Error: " + e.getMessage());
        } catch (InsufficientFundsException e) {
            LOGGER.log(Level.WARNING, "Insufficient funds for transfer", e);
            System.err.println("Error: " + e.getMessage());
            System.err.println("You need $" + String.format("%.2f", e.getShortfall()) + " more to complete this transfer");
        } catch (IllegalArgumentException e) {
            LOGGER.log(Level.WARNING, "Invalid transfer parameters", e);
            System.err.println("Error: " + e.getMessage());
        } catch (Exception e) {
            LOGGER.log(Level.SEVERE, "Unexpected error during transfer", e);
            System.err.println("An unexpected error occurred: " + e.getMessage());
        }
    }
    
    public void displayAccountInfo(String accountId) {
        try {
            BankAccount account = findAccount(accountId);
            System.out.println(account);
        } catch (InvalidAccountException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }
    
    public void displayAllAccounts() {
        if (accounts.isEmpty()) {
            System.out.println("No accounts found");
            return;
        }
        
        System.out.println("\n==== All Accounts ====");
        for (BankAccount account : accounts.values()) {
            System.out.println(account);
        }
        System.out.println("=====================\n");
    }
}
```

### Langkah 5: Implementasi Resource Management dengan Try-with-Resources

1. Buat class `TransactionLogger`:

```java
package exceptionhandlingdemo;

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class TransactionLogger implements AutoCloseable {
    private BufferedWriter writer;
    private String filePath;
    private DateTimeFormatter formatter;
    
    public TransactionLogger(String filePath) throws IOException {
        this.filePath = filePath;
        this.writer = new BufferedWriter(new FileWriter(filePath, true));
        this.formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        
        // Write header if file is empty
        writer.write("=== Transaction Log ===\n");
        writer.flush();
    }
    
    public void logTransaction(String transactionType, String details) throws IOException {
        String timestamp = LocalDateTime.now().format(formatter);
        String logEntry = String.format("[%s] %s: %s\n", timestamp, transactionType, details);
        
        writer.write(logEntry);
        writer.flush();
    }
    
    @Override
    public void close() throws IOException {
        if (writer != null) {
            writer.close();
            System.out.println("Transaction logger closed: " + filePath);
        }
    }
}
```

### Langkah 6: Buat Main Class

1. Buka file main class (biasanya `ExceptionHandlingDemo.java`)
2. Ubah kode menjadi:

```java
package exceptionhandlingdemo;

import java.io.IOException;
import java.util.Scanner;

public class ExceptionHandlingDemo {
    private static BankService bankService = new BankService();
    private static Scanner scanner = new Scanner(System.in);
    
    public static void main(String[] args) {
        System.out.println("===== Bank System Exception Handling Demo =====\n");
        
        // Create some sample accounts
        initializeAccounts();
        
        boolean running = true;
        while (running) {
            displayMenu();
            try {
                int choice = Integer.parseInt(scanner.nextLine());
                
                switch (choice) {
                    case 1:
                        createAccount();
                        break;
                    case 2:
                        checkBalance();
                        break;
                    case 3:
                        deposit();
                        break;
                    case 4:
                        withdraw();
                        break;
                    case 5:
                        transfer();
                        break;
                    case 6:
                        bankService.displayAllAccounts();
                        break;
                    case 7:
                        logTransactions();
                        break;
                    case 8:
                        demonstrateExceptionHandling();
                        break;
                    case 9:
                        running = false;
                        System.out.println("Thank you for using the bank system. Goodbye!");
                        break;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                }
            } catch (NumberFormatException e) {
                System.err.println("Error: Please enter a valid number.");
            } catch (Exception e) {
                System.err.println("An unexpected error occurred: " + e.getMessage());
                e.printStackTrace();
            }
            
            // Pause before showing menu again
            if (running) {
                System.out.println("\nPress Enter to continue...");
                scanner.nextLine();
            }
        }
    }
    
    private static void displayMenu() {
        System.out.println("\n===== Menu =====");
        System.out.println("1. Create Account");
        System.out.println("2. Check Balance");
        System.out.println("3. Deposit");
        System.out.println("4. Withdraw");
        System.out.println("5. Transfer");
        System.out.println("6. Display All Accounts");
        System.out.println("7. Log Transactions (Try-with-Resources Demo)");
        System.out.println("8. Exception Handling Demonstrations");
        System.out.println("9. Exit");
        System.out.print("Enter your choice: ");
    }
    
    private static void initializeAccounts() {
        bankService.createAccount("A001", "John Doe", 1000.0);
        bankService.createAccount("A002", "Jane Smith", 2000.0);
        bankService.createAccount("A003", "Bob Johnson", 500.0);
    }
    
    private static void createAccount() {
        System.out.println("\n--- Create Account ---");
        
        System.out.print("Enter Account ID: ");
        String accountId = scanner.nextLine();
        
        System.out.print("Enter Owner Name: ");
        String ownerName = scanner.nextLine();
        
        double initialBalance = 0.0;
        boolean validInput = false;
        while (!validInput) {
            try {
                System.out.print("Enter Initial Balance: ");
                initialBalance = Double.parseDouble(scanner.nextLine());
                validInput = true;
            } catch (NumberFormatException e) {
                System.err.println("Error: Please enter a valid number for the balance.");
            }
        }
        
        bankService.createAccount(accountId, ownerName, initialBalance);
    }
    
    private static void checkBalance() {
        System.out.println("\n--- Check Balance ---");
        
        System.out.print("Enter Account ID: ");
        String accountId = scanner.nextLine();
        
        bankService.displayAccountInfo(accountId);
    }
    
    private static void deposit() {
        System.out.println("\n--- Deposit ---");
        
        System.out.print("Enter Account ID: ");
        String accountId = scanner.nextLine();
        
        try {
            BankAccount account = bankService.findAccount(accountId);
            
            double amount = 0.0;
            boolean validInput = false;
            while (!validInput) {
                try {
                    System.out.print("Enter Deposit Amount: ");
                    amount = Double.parseDouble(scanner.nextLine());
                    validInput = true;
                } catch (NumberFormatException e) {
                    System.err.println("Error: Please enter a valid number for the amount.");
                }
            }
            
            try {
                account.deposit(amount);
            } catch (IllegalArgumentException e) {
                System.err.println("Error: " + e.getMessage());
            }
        } catch (InvalidAccountException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }
    
    private static void withdraw() {
        System.out.println("\n--- Withdraw ---");
        
        System.out.print("Enter Account ID: ");
        String accountId = scanner.nextLine();
        
        try {
            BankAccount account = bankService.findAccount(accountId);
            
            double amount = 0.0;
            boolean validInput = false;
            while (!validInput) {
                try {
                    System.out.print("Enter Withdrawal Amount: ");
                    amount = Double.parseDouble(scanner.nextLine());
                    validInput = true;
                } catch (NumberFormatException e) {
                    System.err.println("Error: Please enter a valid number for the amount.");
                }
            }
            
            try {
                account.withdraw(amount);
            } catch (IllegalArgumentException e) {
                System.err.println("Error: " + e.getMessage());
            } catch (InsufficientFundsException e) {
                System.err.println("Error: " + e.getMessage());
                System.err.println("You need $" + String.format("%.2f", e.getShortfall()) + " more to complete this withdrawal");
            }
        } catch (InvalidAccountException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }
    
    private static void transfer() {
        System.out.println("\n--- Transfer ---");
        
        System.out.print("Enter Source Account ID: ");
        String fromAccountId = scanner.nextLine();
        
        System.out.print("Enter Destination Account ID: ");
        String toAccountId = scanner.nextLine();
        
        double amount = 0.0;
        boolean validInput = false;
        while (!validInput) {
            try {
                System.out.print("Enter Transfer Amount: ");
                amount = Double.parseDouble(scanner.nextLine());
                validInput = true;
            } catch (NumberFormatException e) {
                System.err.println("Error: Please enter a valid number for the amount.");
            }
        }
        
        bankService.transferFunds(fromAccountId, toAccountId, amount);
    }
    
    private static void logTransactions() {
        System.out.println("\n--- Log Transactions (Try-with-Resources Demo) ---");
        
        // Try-with-resources example
        try (TransactionLogger logger = new TransactionLogger("transactions.log")) {
            System.out.println("Transaction logger opened");
            
            // Log some transactions
            logger.logTransaction("VIEW", "User viewed account list");
            logger.logTransaction("DEMO", "Try-with-resources demonstration");
            
            System.out.println("Transactions logged successfully");
            
            // The logger will be closed automatically at the end of this block
        } catch (IOException e) {
            System.err.println("Error writing to transaction log: " + e.getMessage());
        }
    }
    
    private static void demonstrateExceptionHandling() {
        System.out.println("\n--- Exception Handling Demonstrations ---");
        
        // 1. Demonstrate try-catch-finally
        System.out.println("\n1. Try-Catch-Finally Example");
        try {
            System.out.println("Executing risky code...");
            int result = 10 / 0;  // This will throw ArithmeticException
            System.out.println("This line will not be executed");
        } catch (ArithmeticException e) {
            System.err.println("Caught exception: " + e.getMessage());
        } finally {
            System.out.println("Finally block always executes");
        }
        
        // 2. Demonstrate exception chaining
        System.out.println("\n2. Exception Chaining Example");
        try {
            try {
                System.out.println("Executing inner try block...");
                String nullStr = null;
                nullStr.length();  // This will throw NullPointerException
            } catch (NullPointerException e) {
                System.err.println("Inner catch: " + e.getMessage());
                throw new RuntimeException("Something went wrong", e);
            }
        } catch (RuntimeException e) {
            System.err.println("Outer catch: " + e.getMessage());
            System.err.println("Caused by: " + e.getCause().getClass().getName());
        }
        
        // 3. Demonstrate multiple catch blocks
        System.out.println("\n3. Multiple Catch Blocks Example");
        try {
            System.out.print("Enter a number to divide 10 by: ");
            String input = scanner.nextLine();
            int divisor = Integer.parseInt(input);
            int result = 10 / divisor;
            System.out.println("Result: " + result);
        } catch (NumberFormatException e) {
            System.err.println("That's not a valid number: " + e.getMessage());
        } catch (ArithmeticException e) {
            System.err.println("Arithmetic error: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Something else went wrong: " + e.getMessage());
        }
        
        // 4. Demonstrate multi-catch (Java 7+)
        System.out.println("\n4. Multi-Catch Example");
        try {
            String[] array = new String[3];
            array[5] = "Test";  // ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException | NullPointerException e) {
            System.err.println("Array operation error: " + e.getMessage());
        }
    }
}
```

### Langkah 7: Jalankan Program

1. Klik tombol Run (F6) untuk menjalankan program
2. Eksplor berbagai fitur dan perhatikan bagaimana exceptions ditangani

## Rangkuman

Dalam tutorial ini, kita telah mempelajari:

✅ **Exception Handling Basics** - Apa itu exception dan mengapa penting dalam pemrograman Java

✅ **Jenis-jenis Exception** - Checked, unchecked, dan errors; hierarki exception di Java

✅ **Try-Catch-Finally** - Cara menangkap dan menangani exceptions dengan try-catch blocks

✅ **Try-with-Resources** - Cara mengelola resources yang harus ditutup secara otomatis

✅ **Throwing Exceptions** - Cara melempar exceptions dengan `throw` dan mendeklarasikannya dengan `throws`

✅ **Custom Exceptions** - Cara membuat dan menggunakan exception classes Anda sendiri

✅ **Exception Chaining** - Cara menghubungkan exceptions untuk mempertahankan informasi penyebab

✅ **Best Practices** - Pedoman untuk exception handling yang efektif dalam OOP

✅ **Mendokumentasikan Exceptions** - Cara mendokumentasikan exceptions dengan JavaDoc dan meaningful error messages

Exception handling adalah bagian penting dari pemrograman Java yang robust. Dengan menerapkan teknik-teknik yang dipelajari dalam tutorial ini, Anda dapat membuat aplikasi yang menangani situasi kesalahan dengan anggun dan memberikan umpan balik yang bermakna kepada pengguna dan developer.

## Latihan Soal

1. Apa perbedaan antara checked exception dan unchecked exception di Java? Berikan contoh untuk masing-masing.

2. Jelaskan hierarki exception di Java. Gambarkan hubungan antara `Throwable`, `Error`, `Exception`, dan `RuntimeException`.

3. Tuliskan contoh kode penggunaan try-catch-finally block. Kapan kode dalam blok finally akan dieksekusi?

4. Apa itu try-with-resources statement? Berikan contoh penggunaannya dan jelaskan keuntungannya dibandingkan dengan try-catch-finally tradisional.

5. Buatlah custom checked exception bernama `InvalidEmailException` yang dilemparkan ketika email tidak valid. Implementasikan method `validateEmail(String email)` yang menggunakan exception ini.

6. Jelaskan konsep exception chaining dengan contoh kode. Mengapa exception chaining berguna dalam pengembangan aplikasi?

7. Apa yang dimaksud dengan "exception swallowing"? Mengapa praktik ini umumnya dianggap buruk dan bagaimana cara menghindarinya?

8. Anda memiliki method yang mungkin melempar beberapa jenis exception. Bagaimana cara terbaik untuk mendeklarasikan dan mendokumentasikan exceptions ini?

9. Implementasikan sistem login sederhana dengan custom exceptions untuk berbagai situasi kesalahan, seperti `UserNotFoundException`, `InvalidPasswordException`, dan `AccountLockedException`.

10. Dalam aplikasi banking, Anda perlu mengimplementasikan transfer antar rekening. Jelaskan bagaimana Anda akan menerapkan exception handling dalam fitur ini untuk menjaga integritas data dan memberikan umpan balik yang jelas kepada pengguna.

## Referensi

1. Horstmann, C.S. (2019). *Core Java Volume I--Fundamentals* (11th ed.). Pearson Education. Chapter 7: Exceptions, Assertions, and Logging.

2. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional. Chapter 10: Exceptions.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall. Chapter 12: Error Handling with Exceptions.

4. Oracle. (2023). *Java Language Specification: Exceptions*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-11.html](https://docs.oracle.com/javase/specs/jls/se17/html/jls-11.html)

5. Oracle. (2023). *Java Tutorial: Exceptions*. [https://docs.oracle.com/javase/tutorial/essential/exceptions/](https://docs.oracle.com/javase/tutorial/essential/exceptions/)

6. Evans, B., & Warburton, R. (2014). *Java in a Nutshell* (6th ed.). O'Reilly Media. Chapter 5: Exceptions and Error Handling.

7. Goetz, B., et al. (2006). *Java Concurrency in Practice*. Addison-Wesley Professional. Chapter 7: Cancellation and Shutdown.

8. Kalinkov, I. (2018). "Exception Handling Best Practices in Java". *DZone*. [https://dzone.com/articles/exception-handling-best-practices-in-java](https://dzone.com/articles/exception-handling-best-practices-in-java)

9. Subramaniam, V. (2014). *Functional Programming in Java*. Pragmatic Bookshelf. Chapter 10: Handling Exceptions.

10. Martin, R.C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship*. Prentice Hall. Chapter 7: Error Handling.

---

[◀️ Kembali ke Tutorial #11: Menggunakan Lambda Expression](11-lambda-expressions.md) | [Lanjut ke Tutorial #13: Collections Framework ▶️](13-collections.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
