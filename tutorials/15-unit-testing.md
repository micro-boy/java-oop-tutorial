# 📘 Tutorial Java OOP #15: Unit Testing untuk Kode OOP

> *"Kode tanpa pengujian seperti ilmu tanpa eksperimen—mungkin benar, tetapi kita tidak pernah cukup yakin. Unit testing memberikan landasan konkret yang membuat kita yakin bahwa kode kita benar-benar berfungsi seperti yang diharapkan."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dan pentingnya unit testing dalam pengembangan aplikasi berorientasi objek
- Menerapkan framework JUnit untuk menulis dan menjalankan unit test
- Merancang test case yang efektif untuk berbagai komponen OOP
- Menggunakan pendekatan Test-Driven Development (TDD)
- Mengimplementasikan teknik mocking untuk mengisolasi unit yang diuji
- Mengorganisasi test suites untuk maintainability
- Menerapkan best practices dalam penulisan unit test
- Menggunakan code coverage tools untuk mengukur efektivitas pengujian
- Mengintegrasikan unit testing ke dalam proses pengembangan software
- Mengatasi kesulitan khusus dalam pengujian kode OOP

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Konsep Dasar Unit Testing](#konsep-dasar-unit-testing)
   - [Apa itu Unit Testing?](#apa-itu-unit-testing)
   - [Mengapa Unit Testing Penting?](#mengapa-unit-testing-penting)
   - [Karakteristik Unit Test yang Baik](#karakteristik-unit-test-yang-baik)
   - [Unit Testing vs. Jenis Pengujian Lainnya](#unit-testing-vs-jenis-pengujian-lainnya)
3. [JUnit: Framework Unit Testing untuk Java](#junit-framework-unit-testing-untuk-java)
   - [Pengenalan JUnit](#pengenalan-junit)
   - [JUnit Annotations](#junit-annotations)
   - [Assert Methods](#assert-methods)
   - [Test Lifecycle](#test-lifecycle)
4. [Menulis Unit Test dengan JUnit](#menulis-unit-test-dengan-junit)
   - [Setup Project dengan JUnit](#setup-project-dengan-junit)
   - [Struktur Unit Test](#struktur-unit-test)
   - [Naming Conventions](#naming-conventions)
   - [Test Grouping](#test-grouping)
5. [Test-Driven Development (TDD)](#test-driven-development-tdd)
   - [Prinsip TDD: Red, Green, Refactor](#prinsip-tdd-red-green-refactor)
   - [Manfaat TDD](#manfaat-tdd)
   - [Menerapkan TDD dalam Project Java](#menerapkan-tdd-dalam-project-java)
6. [Menguji Komponen OOP](#menguji-komponen-oop)
   - [Testing Classes dan Objects](#testing-classes-dan-objects)
   - [Testing Inheritance](#testing-inheritance)
   - [Testing Polymorphism](#testing-polymorphism)
   - [Testing Interfaces dan Implementations](#testing-interfaces-dan-implementations)
   - [Testing Exception Handling](#testing-exception-handling)
7. [Mock Objects dan Dependency Injection](#mock-objects-dan-dependency-injection)
   - [Konsep Mocking](#konsep-mocking)
   - [Mockito Framework](#mockito-framework)
   - [Membuat Mocks](#membuat-mocks)
   - [Stubbing Method Calls](#stubbing-method-calls)
   - [Verifying Interactions](#verifying-interactions)
8. [Testing Patterns dan Best Practices](#testing-patterns-dan-best-practices)
   - [FIRST Principles](#first-principles)
   - [Arrange-Act-Assert Pattern](#arrange-act-assert-pattern)
   - [Test Doubles: Stubs, Mocks, Fakes](#test-doubles-stubs-mocks-fakes)
   - [Dealing with Legacy Code](#dealing-with-legacy-code)
9. [Code Coverage](#code-coverage)
   - [Apa itu Code Coverage?](#apa-itu-code-coverage)
   - [Jenis-jenis Code Coverage](#jenis-jenis-code-coverage)
   - [Tools untuk Mengukur Coverage](#tools-untuk-mengukur-coverage)
   - [Interpreting Coverage Reports](#interpreting-coverage-reports)
10. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
    - [Setup Project](#setup-project)
    - [Testing Model Classes](#testing-model-classes)
    - [Testing Service Classes](#testing-service-classes)
    - [Testing dengan Mocks](#testing-dengan-mocks)
    - [Menjalankan dan Menganalisis Tests](#menjalankan-dan-menganalisis-tests)
11. [Rangkuman](#rangkuman)
12. [Latihan Soal](#latihan-soal)
13. [Referensi](#referensi)

## Pendahuluan

Selamat datang di Tutorial #15 dari seri Pemrograman Berorientasi Objek dengan Java! Setelah mempelajari konsep-konsep OOP dan mengimplementasikannya dalam proyek sederhana, kini kita akan membahas aspek penting lainnya dalam pengembangan perangkat lunak berkualitas tinggi: unit testing.

Seorang pengembang software tidak hanya bertanggung jawab untuk menulis kode yang berfungsi, tetapi juga memastikan bahwa kode tersebut benar-benar melakukan apa yang seharusnya dilakukan. Unit testing adalah salah satu praktik terbaik dalam pengembangan software yang memungkinkan kita untuk memverifikasi bahwa kode kita berfungsi dengan benar dan tetap berfungsi seiring waktu.

Unit testing menjadi semakin penting dalam paradigma OOP karena kompleksitas interaksi antar objek dan hierarki class. Dalam tutorial ini, kita akan mempelajari bagaimana menulis dan mengorganisasi unit test untuk kode OOP, menggunakan JUnit—framework unit testing standard untuk Java. Kita juga akan membahas teknik lanjutan seperti mocking dan pendekatan Test-Driven Development.

Mari kita mulai perjalanan untuk membuat kode OOP yang lebih robust dan terpercaya melalui unit testing!

## Konsep Dasar Unit Testing

### Apa itu Unit Testing?

**Unit testing** adalah proses pengujian komponen terkecil dari aplikasi secara terpisah. Dalam konteks OOP, "unit" biasanya mengacu pada sebuah class, atau bahkan method individual. Tujuan utama unit testing adalah memastikan bahwa setiap unit berfungsi dengan benar secara terpisah sebelum diintegrasikan dengan unit lainnya.

Unit test adalah potongan kode yang ditulis oleh developer untuk menguji fungsionalitas unit tertentu. Test ini biasanya diotomatisasi dan dapat dijalankan berulang kali untuk memastikan bahwa unit terus berfungsi sesuai harapan, meskipun kode mengalami perubahan.

### Mengapa Unit Testing Penting?

Unit testing memberikan banyak manfaat dalam pengembangan software:

1. **Menemukan Bug Lebih Awal**: Membantu menemukan bug pada tahap awal pengembangan, ketika biaya perbaikan masih rendah.

2. **Mendokumentasikan Kode**: Unit test berfungsi sebagai dokumentasi hidup tentang bagaimana sebuah unit seharusnya bekerja.

3. **Memfasilitasi Refactoring**: Memberikan jaring pengaman saat melakukan refactoring, memastikan bahwa perubahan tidak merusak fungsionalitas yang ada.

4. **Meningkatkan Desain**: Menulis unit test sering mendorong desain kode yang lebih baik dan lebih modular.

5. **Memudahkan Integrasi**: Ketika semua unit telah diuji dengan baik, proses integrasi menjadi lebih smooth dan predictable.

6. **Memberikan Kepercayaan Diri**: Developer dapat membuat perubahan dengan lebih percaya diri, karena adanya suite test yang akan mendeteksi regresi.

### Karakteristik Unit Test yang Baik

Unit test yang baik memiliki karakteristik berikut:

- **Automated**: Dapat dijalankan tanpa intervensi manual
- **Thorough**: Menguji berbagai skenario termasuk kasus normal dan edge cases
- **Reliable**: Memberikan hasil yang konsisten (tidak flaky)
- **Independent**: Tidak bergantung pada urutan eksekusi atau test lain
- **Fast**: Berjalan dengan cepat untuk memungkinkan feedback loop yang cepat
- **Readable**: Mudah dipahami tujuan dan logika test
- **Maintainable**: Mudah diperbarui ketika kode aplikasi berubah

### Unit Testing vs. Jenis Pengujian Lainnya

Penting untuk memahami posisi unit testing dalam spektrum pengujian software:

| Jenis Testing | Fokus | Cakupan | Kecepatan | Tujuan |
|---------------|-------|---------|-----------|--------|
| **Unit Testing** | Komponen individual | Sangat kecil | Sangat cepat | Memastikan functionality unit tertentu |
| **Integration Testing** | Interaksi antar komponen | Medium | Medium | Memastikan komponen bekerja bersama dengan baik |
| **System Testing** | Seluruh sistem | Luas | Lambat | Memastikan sistem memenuhi requirements |
| **Acceptance Testing** | User requirements | End-to-end | Lambat | Memastikan sistem dapat diterima oleh pengguna |

Unit testing adalah fondasi dari testing pyramid, yang berarti kita harus memiliki lebih banyak unit test dibandingkan jenis test lainnya.

## JUnit: Framework Unit Testing untuk Java

### Pengenalan JUnit

**JUnit** adalah framework unit testing paling populer untuk Java. Ini adalah bagian dari keluarga framework xUnit dan menyediakan cara yang sederhana dan elegant untuk menulis, mengorganisir, dan menjalankan unit test.

JUnit 5 (versi terbaru) terdiri dari beberapa modul:
- **JUnit Platform**: Fondasi untuk meluncurkan testing frameworks di JVM
- **JUnit Jupiter**: API baru untuk menulis test di JUnit 5
- **JUnit Vintage**: Mendukung menjalankan test yang ditulis dengan JUnit 3 dan JUnit 4

### JUnit Annotations

JUnit menggunakan annotations untuk mendefinisikan test methods dan konfigurasi:

| Annotation | Deskripsi |
|------------|-----------|
| `@Test` | Menandai method sebagai test method |
| `@BeforeEach` | Method dijalankan sebelum setiap test method |
| `@AfterEach` | Method dijalankan setelah setiap test method |
| `@BeforeAll` | Method statis dijalankan sekali sebelum semua test methods di class |
| `@AfterAll` | Method statis dijalankan sekali setelah semua test methods di class |
| `@Disabled` | Menonaktifkan test method atau class |
| `@DisplayName` | Memberikan nama custom untuk test |
| `@Tag` | Menandai test untuk difilter |
| `@Timeout` | Menetapkan batas waktu eksekusi |
| `@ParameterizedTest` | Menandai method sebagai parameterized test |
| `@RepeatedTest` | Menandai method untuk diulang beberapa kali |

### Assert Methods

JUnit menyediakan beragam static methods di class `Assertions` untuk memverifikasi hasil test:

```java
import static org.junit.jupiter.api.Assertions.*;

// Basic assertions
assertEquals(expected, actual);
assertNotEquals(expected, actual);
assertTrue(condition);
assertFalse(condition);
assertNull(object);
assertNotNull(object);

// Array assertions
assertArrayEquals(expectedArray, actualArray);

// Exception assertions
assertThrows(ExpectedException.class, () -> { methodThatShouldThrow(); });

// Grouped assertions (all are executed even if some fail)
assertAll(
    () -> assertEquals(2, 1 + 1),
    () -> assertTrue(4 > 3)
);

// Advanced assertion with message
assertEquals(expected, actual, "Custom failure message");

// Assertion with supplier for lazy message evaluation
assertEquals(expected, actual, () -> "Failure with computed value: " + computeValue());
```

### Test Lifecycle

JUnit mengikuti lifecycle berikut untuk setiap test:

1. **Instantiate test class**: Sebuah instance baru dibuat untuk setiap test method
2. **@BeforeAll**: Method statis dijalankan sekali sebelum semua test
3. **@BeforeEach**: Dijalankan sebelum setiap test method
4. **@Test**: Test method dijalankan
5. **@AfterEach**: Dijalankan setelah setiap test method
6. **@AfterAll**: Method statis dijalankan sekali setelah semua test

Lifecycle ini memastikan bahwa setiap test dimulai dengan kondisi yang bersih dan tidak dipengaruhi oleh test sebelumnya.

## Menulis Unit Test dengan JUnit

### Setup Project dengan JUnit

Untuk mulai menggunakan JUnit 5 di project Java Anda, Anda perlu menambahkan dependencies yang sesuai. Berikut cara mengatur JUnit di project Maven atau Gradle.

**Maven (pom.xml)**:
```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.8.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

**Gradle (build.gradle)**:
```groovy
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.8.2'
}

test {
    useJUnitPlatform()
}
```

**Di NetBeans** dengan proyek Ant:
1. Klik kanan pada project
2. Pilih "Properties"
3. Pilih "Libraries"
4. Klik "Add Library" dan pilih "JUnit"

### Struktur Unit Test

Struktur dasar dari test class JUnit:

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.AfterEach;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
    
    private Calculator calculator;
    
    @BeforeEach
    public void setUp() {
        calculator = new Calculator();
    }
    
    @Test
    public void testAdd() {
        assertEquals(5, calculator.add(2, 3), "2 + 3 should equal 5");
    }
    
    @Test
    public void testMultiply() {
        assertEquals(6, calculator.multiply(2, 3), "2 * 3 should equal 6");
    }
    
    @Test
    public void testDivide() {
        assertEquals(2.0, calculator.divide(6, 3), "6 / 3 should equal 2");
    }
    
    @Test
    public void testDivideByZero() {
        assertThrows(ArithmeticException.class, () -> calculator.divide(1, 0),
                    "Division by zero should throw ArithmeticException");
    }
    
    @AfterEach
    public void tearDown() {
        calculator = null;
    }
}
```

### Naming Conventions

Nama test yang baik sangat penting untuk memahami tujuan dan konteks test:

1. **Nama Class Test**: Biasanya nama class yang diuji diikuti dengan "Test"
   - Contoh: `Calculator` → `CalculatorTest`

2. **Nama Method Test**: Beberapa konvensi umum:
   - `test<MethodName>`: Contoh `testAdd()`
   - `<methodName>_<state>_<expectedBehavior>`: Contoh `add_positiveNumbers_returnsSum()`
   - BDD style: `should<ExpectedBehavior>When<State>`: Contoh `shouldReturnSumWhenAddingPositiveNumbers()`

Kunci dari penamaan test yang baik adalah membuat nama yang deskriptif sehingga ketika test gagal, Anda langsung tahu apa yang seharusnya terjadi dan apa yang gagal.

### Test Grouping

Untuk proyek besar, pengelompokan test sangat penting:

1. **Package Structure**: Menempatkan test dalam package yang sama dengan kode yang diuji, tetapi di direktori test
   - Contoh: `com.example.app.model` → `com.example.app.model` (dalam direktori test)

2. **Test Suites**: Menggunakan `@Nested` untuk mengelompokkan test terkait dalam satu class

```java
import org.junit.jupiter.api.Nested;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
    
    @Nested
    class AdditionTests {
        @Test
        void testPositiveNumbers() { ... }
        
        @Test
        void testNegativeNumbers() { ... }
        
        @Test
        void testZero() { ... }
    }
    
    @Nested
    class MultiplicationTests {
        @Test
        void testPositiveNumbers() { ... }
        
        @Test
        void testNegativeNumbers() { ... }
        
        @Test
        void testZero() { ... }
    }
}
```

3. **Tags**: Menggunakan `@Tag` untuk mengategorikan test dan memungkinkan running subset test tertentu

```java
@Test
@Tag("slow")
void testComplexCalculation() { ... }

@Test
@Tag("fast")
void testSimpleAddition() { ... }
```

## Test-Driven Development (TDD)

### Prinsip TDD: Red, Green, Refactor

**Test-Driven Development (TDD)** adalah pendekatan pengembangan software di mana Anda menulis test terlebih dahulu, sebelum menulis kode yang sebenarnya. TDD mengikuti siklus yang dikenal sebagai "Red, Green, Refactor":

1. **Red**: Tulis test yang gagal untuk fungsionalitas yang ingin diimplementasikan
2. **Green**: Tulis kode minimal yang cukup untuk membuat test lulus
3. **Refactor**: Perbaiki kode tanpa mengubah behavior-nya

TDD membalik pendekatan tradisional di mana biasanya developer menulis kode terlebih dahulu dan baru kemudian menulis test (jika ada).

### Manfaat TDD

Adopsi TDD memberikan beberapa manfaat:

1. **Code Quality**: Mendorong desain yang lebih baik dan lebih modular
2. **Test Coverage**: Secara alami menghasilkan test coverage yang tinggi
3. **Fewer Bugs**: Mendeteksi masalah sejak awal pengembangan
4. **Living Documentation**: Tests berfungsi sebagai spesifikasi executable
5. **Increased Confidence**: Memudahkan refactoring dan perubahan
6. **Faster Feedback Loop**: Memberikan feedback instan tentang perubahan kode

### Menerapkan TDD dalam Project Java

Mari kita lihat contoh penerapan TDD untuk mengimplementasikan fungsionalitas sederhana:

**Langkah 1: Tulis Test yang Gagal (Red)**

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class StringUtilsTest {
    @Test
    public void testReverseString() {
        StringUtils utils = new StringUtils();
        assertEquals("cba", utils.reverse("abc"), "Should reverse 'abc' to 'cba'");
    }
}
```

Pada titik ini, `StringUtils` class dan method `reverse` belum ada, sehingga test akan gagal.

**Langkah 2: Tulis Kode Minimal untuk Lulus Test (Green)**

```java
public class StringUtils {
    public String reverse(String input) {
        return new StringBuilder(input).reverse().toString();
    }
}
```

Sekarang test akan lulus.

**Langkah 3: Refactor Kode (Refactor)**

Dalam kasus ini, implementasi sudah cukup baik. Tetapi jika perlu, kita bisa meningkatkan performa, readability, atau aspek lain tanpa mengubah behavior.

**Langkah 4: Tambahkan Test untuk Edge Cases**

```java
@Test
public void testReverseEmptyString() {
    StringUtils utils = new StringUtils();
    assertEquals("", utils.reverse(""), "Should handle empty string");
}

@Test
public void testReverseNull() {
    StringUtils utils = new StringUtils();
    assertThrows(NullPointerException.class, () -> utils.reverse(null),
                "Should throw NullPointerException for null input");
}
```

**Langkah 5: Perbaiki Kode untuk Menangani Edge Cases**

```java
public String reverse(String input) {
    if (input == null) {
        throw new NullPointerException("Input cannot be null");
    }
    return new StringBuilder(input).reverse().toString();
}
```

Ini adalah siklus TDD dasar. Anda akan mengulangi siklus ini untuk setiap fitur atau aspek baru dari sistem Anda.

## Menguji Komponen OOP

Pengujian komponen OOP memiliki tantangan unik karena sifat dari konsep OOP seperti encapsulation, inheritance, dan polymorphism. Mari kita bahas bagaimana menguji berbagai aspek OOP.

### Testing Classes dan Objects

Saat menguji class, fokus pada pengujian:

1. **Constructors**: Memastikan objek diinisialisasi dengan benar
2. **Getters dan Setters**: Memverifikasi encapsulated state
3. **Business Methods**: Menguji logika bisnis
4. **Object State**: Memastikan object state berubah sesuai harapan setelah operasi

Contoh:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class BankAccountTest {
    
    @Test
    public void testConstructor() {
        BankAccount account = new BankAccount("123456", "John Doe", 1000.0);
        assertEquals("123456", account.getAccountNumber());
        assertEquals("John Doe", account.getOwnerName());
        assertEquals(1000.0, account.getBalance());
    }
    
    @Test
    public void testDeposit() {
        BankAccount account = new BankAccount("123456", "John Doe", 1000.0);
        account.deposit(500.0);
        assertEquals(1500.0, account.getBalance());
    }
    
    @Test
    public void testWithdraw() {
        BankAccount account = new BankAccount("123456", "John Doe", 1000.0);
        account.withdraw(300.0);
        assertEquals(700.0, account.getBalance());
    }
    
    @Test
    public void testWithdrawInsufficientFunds() {
        BankAccount account = new BankAccount("123456", "John Doe", 1000.0);
        assertThrows(InsufficientFundsException.class, 
                   () -> account.withdraw(1500.0));
    }
}
```

### Testing Inheritance

Saat menguji class yang menggunakan inheritance:

1. **Test Behavior yang Diwarisi**: Pastikan subclass mewarisi behavior superclass dengan benar
2. **Test Override Methods**: Verifikasi bahwa method yang di-override berfungsi dengan benar
3. **Test Superclass Contract**: Pastikan subclass tidak melanggar kontrak yang didefinisikan oleh superclass

Contoh:

```java
// Superclass
public class Shape {
    protected String color;
    
    public Shape(String color) {
        this.color = color;
    }
    
    public String getColor() {
        return color;
    }
    
    public double calculateArea() {
        return 0.0; // To be overridden by subclasses
    }
}

// Subclass
public class Circle extends Shape {
    private double radius;
    
    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }
    
    public double getRadius() {
        return radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

// Test
public class CircleTest {
    
    @Test
    public void testInheritedBehavior() {
        Circle circle = new Circle("Red", 5.0);
        assertEquals("Red", circle.getColor()); // Inherited from Shape
    }
    
    @Test
    public void testOverriddenMethod() {
        Circle circle = new Circle("Red", 5.0);
        assertEquals(Math.PI * 25, circle.calculateArea(), 0.001);
    }
    
    @Test
    public void testCircleSpecificMethod() {
        Circle circle = new Circle("Red", 5.0);
        assertEquals(5.0, circle.getRadius());
    }
}
```

### Testing Polymorphism

Untuk menguji polymorphic behavior:

1. **Test dengan Reference Type Superclass**: Panggil methods melalui reference superclass
2. **Test di Context yang Menggunakan Polymorphism**: Verifikasi behavior dalam context yang menggunakan polymorphism

Contoh:

```java
// Test class for polymorphic behavior
public class ShapeTest {
    
    @Test
    public void testPolymorphicBehavior() {
        // Using superclass reference to subclass objects
        Shape circle = new Circle("Red", 5.0);
        Shape rectangle = new Rectangle("Blue", 4.0, 6.0);
        
        assertEquals(Math.PI * 25, circle.calculateArea(), 0.001);
        assertEquals(24.0, rectangle.calculateArea());
    }
    
    @Test
    public void testShapeProcessor() {
        Circle circle = new Circle("Red", 5.0);
        Rectangle rectangle = new Rectangle("Blue", 4.0, 6.0);
        
        ShapeProcessor processor = new ShapeProcessor();
        assertEquals(Math.PI * 25 + 24.0, processor.getTotalArea(Arrays.asList(circle, rectangle)), 0.001);
    }
}

// Class that uses polymorphism
class ShapeProcessor {
    public double getTotalArea(List<Shape> shapes) {
        return shapes.stream()
                    .mapToDouble(Shape::calculateArea)
                    .sum();
    }
}
```

### Testing Interfaces dan Implementations

Saat menguji interface dan implementasinya:

1. **Test Implementasi Individual**: Setiap implementasi harus diuji secara terpisah
2. **Test Contract Compliance**: Pastikan semua implementasi memenuhi kontrak interface
3. **Test Interchangeability**: Verifikasi bahwa client dapat bekerja dengan implementasi yang berbeda

Contoh:

```java
// Interface
public interface PaymentProcessor {
    boolean processPayment(double amount);
}

// Test for contract compliance
public class PaymentProcessorTest {
    
    @Test
    public void testCreditCardProcessor() {
        PaymentProcessor processor = new CreditCardProcessor();
        testPaymentProcessorContract(processor);
    }
    
    @Test
    public void testPayPalProcessor() {
        PaymentProcessor processor = new PayPalProcessor();
        testPaymentProcessorContract(processor);
    }
    
    // Helper method to test contract compliance
    private void testPaymentProcessorContract(PaymentProcessor processor) {
        assertTrue(processor.processPayment(100.0), "Should process valid payment");
        assertFalse(processor.processPayment(-50.0), "Should reject negative amounts");
    }
    
    // Testing client code with different implementations
    @Test
    public void testPaymentService() {
        PaymentService service = new PaymentService();
        
        service.setProcessor(new CreditCardProcessor());
        assertTrue(service.makePayment(100.0));
        
        service.setProcessor(new PayPalProcessor());
        assertTrue(service.makePayment(100.0));
    }
}

// Client class
class PaymentService {
    private PaymentProcessor processor;
    
    public void setProcessor(PaymentProcessor processor) {
        this.processor = processor;
    }
    
    public boolean makePayment(double amount) {
        return processor.processPayment(amount);
    }
}
```

### Testing Exception Handling

Pengujian exception handling adalah aspek penting dari unit testing:

1. **Verifikasi Exception Type**: Pastikan tipe exception yang benar dilempar
2. **Verifikasi Exception Message**: Pastikan message exception informatif
3. **Verifikasi Exception Timing**: Pastikan exception dilempar pada kondisi yang tepat

Contoh:

```java
@Test
public void testInvalidAmount() {
    BankAccount account = new BankAccount("123456", "John Doe", 1000.0);
    
    Exception exception = assertThrows(IllegalArgumentException.class, 
                                     () -> account.deposit(-100.0));
    assertEquals("Deposit amount must be positive", exception.getMessage());
}

@Test
public void testInsufficientFunds() {
    BankAccount account = new BankAccount("123456", "John Doe", 1000.0);
    
    InsufficientFundsException exception = assertThrows(InsufficientFundsException.class, 
                                                      () -> account.withdraw(1500.0));
    assertEquals("Insufficient funds: needed 500.0 more", exception.getMessage());
    assertEquals(500.0, exception.getAmountShort());
}
```

## Mock Objects dan Dependency Injection

### Konsep Mocking

**Mocking** adalah teknik dimana kita mengganti dependencies yang sesungguhnya dengan objek tiruan yang kita kontrol. Ini sangat berguna untuk mengisolasi unit yang sedang diuji dari dependencies eksternalnya.

Manfaat mocking:
1. **Isolation**: Memastikan bahwa test hanya menguji satu unit
2. **Speed**: Menghindari operasi yang lambat seperti I/O atau network
3. **Determinism**: Menghilangkan non-determinism dari external systems
4. **State Simulation**: Mensimulasikan berbagai state dari dependencies
5. **Verifikasi Interaksi**: Memastikan unit berinteraksi dengan dependencies secara benar

### Mockito Framework

**Mockito** adalah framework mocking populer untuk Java. Untuk menggunakannya, tambahkan dependency:

**Maven**:
```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>4.5.1</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-junit-jupiter</artifactId>
    <version>4.5.1</version>
    <scope>test</scope>
</dependency>
```

### Membuat Mocks

Cara dasar membuat mock dengan Mockito:

```java
import static org.mockito.Mockito.*;

// Creating a mock
PaymentGateway mockGateway = mock(PaymentGateway.class);

// Alternative using annotation
@Mock
PaymentGateway mockGateway;

// Initialize mocks with annotations
@BeforeEach
void setUp() {
    MockitoAnnotations.openMocks(this);
}
```

### Stubbing Method Calls

Menetapkan behavior untuk mock objects:

```java
// Stubbing void methods
doNothing().when(mockGateway).connect();

// Stubbing methods with return value
when(mockGateway.processPayment(100.0)).thenReturn(true);
when(mockGateway.processPayment(anyDouble())).thenReturn(false);

// Returning different values on consecutive calls
when(mockGateway.getStatus())
    .thenReturn("CONNECTED")
    .thenReturn("PROCESSING")
    .thenReturn("COMPLETED");

// Throwing exceptions
when(mockGateway.processPayment(-100.0)).thenThrow(new IllegalArgumentException());
```

### Verifying Interactions

Memverifikasi bahwa mock dipanggil dengan cara yang benar:

```java
// Basic verification
verify(mockGateway).connect();
verify(mockGateway).processPayment(100.0);

// Verifying number of invocations
verify(mockGateway, times(2)).getStatus();
verify(mockGateway, never()).disconnect();
verify(mockGateway, atLeastOnce()).processPayment(anyDouble());

// Verifying order of invocations
InOrder inOrder = inOrder(mockGateway);
inOrder.verify(mockGateway).connect();
inOrder.verify(mockGateway).processPayment(anyDouble());
inOrder.verify(mockGateway).disconnect();
```

Contoh penggunaan lengkap Mockito:

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
public class PaymentServiceTest {
    
    @Mock
    private PaymentGateway mockGateway;
    
    @Test
    public void testSuccessfulPayment() {
        // Setup
        PaymentService service = new PaymentService(mockGateway);
        when(mockGateway.processPayment(100.0)).thenReturn(true);
        
        // Act
        boolean result = service.makePayment(100.0);
        
        // Assert
        assertTrue(result);
        verify(mockGateway).processPayment(100.0);
    }
    
    @Test
    public void testFailedPayment() {
        // Setup
        PaymentService service = new PaymentService(mockGateway);
        when(mockGateway.processPayment(anyDouble())).thenReturn(false);
        
        // Act
        boolean result = service.makePayment(50.0);
        
        // Assert
        assertFalse(result);
        verify(mockGateway).processPayment(50.0);
    }
    
    @Test
    public void testPaymentWorkflow() {
        // Setup
        PaymentService service = new PaymentService(mockGateway);
        when(mockGateway.processPayment(100.0)).thenReturn(true);
        
        // Act
        service.processPaymentWithNotification(100.0, "test@example.com");
        
        // Verify correct workflow
        InOrder inOrder = inOrder(mockGateway);
        inOrder.verify(mockGateway).connect();
        inOrder.verify(mockGateway).processPayment(100.0);
        inOrder.verify(mockGateway).sendReceipt("test@example.com");
        inOrder.verify(mockGateway).disconnect();
    }
}

// Class under test
class PaymentService {
    private PaymentGateway gateway;
    
    public PaymentService(PaymentGateway gateway) {
        this.gateway = gateway;
    }
    
    public boolean makePayment(double amount) {
        return gateway.processPayment(amount);
    }
    
    public void processPaymentWithNotification(double amount, String email) {
        gateway.connect();
        if (gateway.processPayment(amount)) {
            gateway.sendReceipt(email);
        }
        gateway.disconnect();
    }
}

interface PaymentGateway {
    void connect();
    boolean processPayment(double amount);
    void sendReceipt(String email);
    void disconnect();
    String getStatus();
}
```

## Testing Patterns dan Best Practices

### FIRST Principles

Unit tests yang baik mengikuti prinsip FIRST:

- **F**ast: Test harus berjalan cepat
- **I**ndependent: Test tidak boleh bergantung pada test lain
- **R**epeatable: Test harus memberikan hasil yang sama setiap kali dijalankan
- **S**elf-validating: Test harus memberikan hasil pass/fail tanpa interpretasi manual
- **T**horough: Test harus mencakup semua skenario termasuk edge cases

### Arrange-Act-Assert Pattern

Pattern "Arrange-Act-Assert" (atau "Given-When-Then" dalam BDD) membantu membuat test yang terstruktur:

1. **Arrange**: Setup preconditions dan inputs
2. **Act**: Panggil method yang diuji
3. **Assert**: Verifikasi hasil

```java
@Test
public void testWithdraw() {
    // Arrange
    BankAccount account = new BankAccount("123456", "John Doe", 1000.0);
    double withdrawAmount = 300.0;
    
    // Act
    account.withdraw(withdrawAmount);
    
    // Assert
    assertEquals(700.0, account.getBalance());
}
```

### Test Doubles: Stubs, Mocks, Fakes

Ada beberapa jenis test doubles:

1. **Stub**: Menyediakan jawaban hard-coded untuk calls
2. **Mock**: Objek yang memverifikasi calls yang dibuat kepadanya
3. **Fake**: Implementasi ringan dari interface yang bekerja, tetapi tidak sesuai untuk production
4. **Spy**: Objek nyata yang sebagian methodnya telah di-stub
5. **Dummy**: Objek yang dilempar tapi tidak pernah benar-benar digunakan

Contoh penggunaan:

```java
// Stub example
EmailService stubEmailService = new StubEmailService();
stubEmailService.sendConfirmationEmail("user@example.com");
// No actual email sent, just returns success

// Mock example with Mockito
EmailService mockEmailService = mock(EmailService.class);
when(mockEmailService.sendConfirmationEmail("user@example.com")).thenReturn(true);
verify(mockEmailService).sendConfirmationEmail("user@example.com");

// Fake example
EmailService fakeEmailService = new InMemoryEmailService();
// Uses an in-memory list instead of actually sending emails

// Spy example
EmailService realEmailService = new SmtpEmailService();
EmailService spyEmailService = spy(realEmailService);
// Some methods are real, some are stubbed
```

### Dealing with Legacy Code

Testing legacy code yang tidak dirancang untuk testability bisa menjadi tantangan:

1. **Identify Seams**: Temukan titik di mana Anda dapat "menyisipkan" test
2. **Extract Method**: Refactor untuk mengekstrak logika yang ingin diuji
3. **Extract Interface**: Buat interface untuk dependencies dan kemudian mock
4. **Break Dependencies**: Gunakan dependency injection untuk memutus dependencies yang sulit
5. **Characterization Tests**: Tulis test yang mendokumentasikan behavior saat ini, meskipun mungkin bukan behavior yang ideal

## Code Coverage

### Apa itu Code Coverage?

**Code Coverage** adalah metrik yang menunjukkan persentase kode source yang dieksekusi oleh test. Ini membantu mengidentifikasi bagian kode yang belum diuji.

### Jenis-jenis Code Coverage

Ada beberapa tipe code coverage:

1. **Statement Coverage**: Persentase statements yang dieksekusi
2. **Branch Coverage**: Persentase branches (seperti if/else) yang dieksekusi
3. **Path Coverage**: Persentase paths yang mungkin melalui kode yang dieksekusi
4. **Function Coverage**: Persentase functions/methods yang dipanggil
5. **Line Coverage**: Persentase executable lines yang dieksekusi
6. **Condition Coverage**: Persentase boolean sub-expressions yang dievaluasi true dan false

### Tools untuk Mengukur Coverage

Beberapa tools populer untuk mengukur code coverage di Java:

1. **JaCoCo**: Java Code Coverage, terintegrasi baik dengan build tools
2. **OpenClover**: Sebelumnya Atlassian Clover
3. **Cobertura**: Tool coverage yang sudah lebih lama

Dengan Maven dan JaCoCo:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.7</version>
            <executions>
                <execution>
                    <goals>
                        <goal>prepare-agent</goal>
                    </goals>
                </execution>
                <execution>
                    <id>report</id>
                    <phase>test</phase>
                    <goals>
                        <goal>report</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

### Interpreting Coverage Reports

Memahami laporan coverage adalah keterampilan penting:

1. **100% Coverage Bukan Tujuan Akhir**: Coverage tinggi tidak menjamin kualitas test yang baik
2. **Identifikasi Hotspots**: Fokus pada area kritis dengan coverage rendah
3. **Trend Coverage**: Pantau trend coverage dari waktu ke waktu
4. **Kombinasikan dengan Code Reviews**: Coverage adalah alat, bukan pengganti review
5. **Pertimbangkan ROI**: Usahakan balance antara effort dan value

Pedoman umum:
- Coverage 70-80% umumnya dianggap baik untuk sistem produksi
- Coverage 90%+ untuk kode yang sangat kritikal
- Lebih penting untuk memastikan skenario-skenario yang signifikan tercakup, daripada sekadar mengejar angka

## Latihan Praktik dengan NetBeans

Mari kita praktikkan unit testing dengan contoh kode dari proyek Inventory Management System yang kita buat di tutorial sebelumnya.

### Setup Project

1. Buka NetBeans
2. Buka proyek Inventory Management System atau buat proyek baru
3. Tambahkan JUnit 5 ke project:
   - Klik kanan pada project
   - Pilih "Properties"
   - Pilih "Libraries"
   - Klik "Add Library" dan pilih "JUnit"

### Testing Model Classes

Mari menguji class `Product` dari proyek kita:

1. Klik kanan pada `Product.java`
2. Pilih "Tools > Create Tests"
3. Atau buat manual test class di direktori test

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;
import static org.junit.jupiter.api.Assertions.*;

public class ProductTest {
    
    private Product product;
    
    @BeforeEach
    public void setUp() {
        // Initialize product with test data
        product = new Product("P001", "Test Product", "Test Description", 
                           "C001", 100.0, 50, "S001");
    }
    
    @Test
    public void testConstructor() {
        assertEquals("P001", product.getProductId());
        assertEquals("Test Product", product.getName());
        assertEquals("Test Description", product.getDescription());
        assertEquals("C001", product.getCategoryId());
        assertEquals(100.0, product.getPrice());
        assertEquals(50, product.getStockQuantity());
        assertEquals("S001", product.getSupplierId());
    }
    
    @Test
    public void testIncreaseStock() {
        product.increaseStock(10);
        assertEquals(60, product.getStockQuantity());
    }
    
    @Test
    public void testIncreaseStockNegativeQuantity() {
        assertThrows(IllegalArgumentException.class, () -> {
            product.increaseStock(-10);
        });
    }
    
    @Test
    public void testDecreaseStock() {
        product.decreaseStock(20);
        assertEquals(30, product.getStockQuantity());
    }
    
    @Test
    public void testDecreaseStockNegativeQuantity() {
        assertThrows(IllegalArgumentException.class, () -> {
            product.decreaseStock(-10);
        });
    }
    
    @Test
    public void testDecreaseStockInsufficientQuantity() {
        assertThrows(IllegalStateException.class, () -> {
            product.decreaseStock(100);
        });
    }
    
    @Test
    public void testIsLowStock() {
        assertTrue(product.isLowStock(60));  // 50 < 60
        assertFalse(product.isLowStock(40)); // 50 > 40
        assertTrue(product.isLowStock(50));  // 50 == 50
    }
}
```

### Testing Service Classes

Untuk service classes, kita biasanya perlu menggunakan mocking untuk mengisolasi dari dependencies:

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.InjectMocks;
import org.mockito.junit.jupiter.MockitoExtension;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import java.util.Arrays;
import java.util.List;
import java.util.Optional;

@ExtendWith(MockitoExtension.class)
public class ProductServiceImplTest {
    
    @Mock
    private ProductDAO productDAO;
    
    @InjectMocks
    private ProductServiceImpl productService;
    
    @Test
    public void testAddProduct() {
        // Arrange
        Product product = new Product("P001", "Test Product", "Description", 
                                    "C001", 100.0, 50, "S001");
        when(productDAO.add(product)).thenReturn(true);
        
        // Act
        boolean result = productService.addProduct(product);
        
        // Assert
        assertTrue(result);
        verify(productDAO).add(product);
    }
    
    @Test
    public void testGetProductById() {
        // Arrange
        Product product = new Product("P001", "Test Product", "Description", 
                                    "C001", 100.0, 50, "S001");
        when(productDAO.findById("P001")).thenReturn(Optional.of(product));
        
        // Act
        Optional<Product> result = productService.getProductById("P001");
        
        // Assert
        assertTrue(result.isPresent());
        assertEquals(product, result.get());
    }
    
    @Test
    public void testGetProductByIdNotFound() {
        // Arrange
        when(productDAO.findById("P999")).thenReturn(Optional.empty());
        
        // Act
        Optional<Product> result = productService.getProductById("P999");
        
        // Assert
        assertFalse(result.isPresent());
    }
    
    @Test
    public void testIncreaseStock() {
        // Arrange
        Product product = new Product("P001", "Test Product", "Description", 
                                    "C001", 100.0, 50, "S001");
        when(productDAO.findById("P001")).thenReturn(Optional.of(product));
        when(productDAO.update(any(Product.class))).thenReturn(true);
        
        // Act
        boolean result = productService.increaseStock("P001", 10);
        
        // Assert
        assertTrue(result);
        assertEquals(60, product.getStockQuantity());
        verify(productDAO).update(product);
    }
    
    @Test
    public void testIncreaseStockNegativeQuantity() {
        // Act
        boolean result = productService.increaseStock("P001", -10);
        
        // Assert
        assertFalse(result);
        verify(productDAO, never()).findById(anyString());
        verify(productDAO, never()).update(any(Product.class));
    }
    
    @Test
    public void testDecreaseStock() {
        // Arrange
        Product product = new Product("P001", "Test Product", "Description", 
                                    "C001", 100.0, 50, "S001");
        when(productDAO.findById("P001")).thenReturn(Optional.of(product));
        when(productDAO.update(any(Product.class))).thenReturn(true);
        
        // Act
        boolean result = productService.decreaseStock("P001", 10);
        
        // Assert
        assertTrue(result);
        assertEquals(40, product.getStockQuantity());
        verify(productDAO).update(product);
    }
    
    @Test
    public void testGetLowStockProducts() {
        // Arrange
        List<Product> lowStockProducts = Arrays.asList(
            new Product("P001", "Low Stock 1", "Description", "C001", 100.0, 5, "S001"),
            new Product("P002", "Low Stock 2", "Description", "C001", 200.0, 3, "S001")
        );
        when(productDAO.findLowStock(10)).thenReturn(lowStockProducts);
        
        // Act
        List<Product> result = productService.getLowStockProducts(10);
        
        // Assert
        assertEquals(2, result.size());
        assertEquals(lowStockProducts, result);
    }
}
```

### Testing dengan Mocks

Mari kita uji class `TransactionServiceImpl` yang bergantung pada beberapa dependencies:

```java
@ExtendWith(MockitoExtension.class)
public class TransactionServiceImplTest {
    
    @Mock
    private TransactionDAO transactionDAO;
    
    @Mock
    private ProductService productService;
    
    @Mock
    private UserService userService;
    
    @InjectMocks
    private TransactionServiceImpl transactionService;
    
    @Test
    public void testCreateInboundTransaction() {
        // Arrange
        String productId = "P001";
        int quantity = 10;
        String notes = "Restock";
        
        Product product = new Product(productId, "Test Product", "Description", 
                                    "C001", 100.0, 50, "S001");
        User user = new User("U001", "testuser", "password", "Test User", Role.STAFF);
        
        when(userService.getCurrentUser()).thenReturn(Optional.of(user));
        when(productService.getProductById(productId)).thenReturn(Optional.of(product));
        when(productService.increaseStock(productId, quantity)).thenReturn(true);
        when(transactionDAO.add(any(Transaction.class))).thenReturn(true);
        
        // Act
        boolean result = transactionService.createInboundTransaction(productId, quantity, notes);
        
        // Assert
        assertTrue(result);
        verify(productService).increaseStock(productId, quantity);
        verify(transactionDAO).add(any(InboundTransaction.class));
    }
    
    @Test
    public void testCreateInboundTransactionNoUser() {
        // Arrange
        String productId = "P001";
        int quantity = 10;
        String notes = "Restock";
        
        when(userService.getCurrentUser()).thenReturn(Optional.empty());
        
        // Act
        boolean result = transactionService.createInboundTransaction(productId, quantity, notes);
        
        // Assert
        assertFalse(result);
        verify(productService, never()).increaseStock(anyString(), anyInt());
        verify(transactionDAO, never()).add(any(Transaction.class));
    }
    
    @Test
    public void testCreateOutboundTransaction() {
        // Arrange
        String productId = "P001";
        int quantity = 10;
        String notes = "Sale";
        
        Product product = new Product(productId, "Test Product", "Description", 
                                    "C001", 100.0, 50, "S001");
        User user = new User("U001", "testuser", "password", "Test User", Role.STAFF);
        
        when(userService.getCurrentUser()).thenReturn(Optional.of(user));
        when(productService.getProductById(productId)).thenReturn(Optional.of(product));
        when(productService.decreaseStock(productId, quantity)).thenReturn(true);
        when(transactionDAO.add(any(Transaction.class))).thenReturn(true);
        
        // Act
        boolean result = transactionService.createOutboundTransaction(productId, quantity, notes);
        
        // Assert
        assertTrue(result);
        verify(productService).decreaseStock(productId, quantity);
        verify(transactionDAO).add(any(OutboundTransaction.class));
    }
    
    @Test
    public void testCreateOutboundTransactionInsufficientStock() {
        // Arrange
        String productId = "P001";
        int quantity = 100;
        String notes = "Sale";
        
        Product product = new Product(productId, "Test Product", "Description", 
                                    "C001", 100.0, 50, "S001");
        User user = new User("U001", "testuser", "password", "Test User", Role.STAFF);
        
        when(userService.getCurrentUser()).thenReturn(Optional.of(user));
        when(productService.getProductById(productId)).thenReturn(Optional.of(product));
        when(productService.decreaseStock(productId, quantity)).thenReturn(false);
        
        // Act
        boolean result = transactionService.createOutboundTransaction(productId, quantity, notes);
        
        // Assert
        assertFalse(result);
        verify(productService).decreaseStock(productId, quantity);
        verify(transactionDAO, never()).add(any(Transaction.class));
    }
}
```

### Menjalankan dan Menganalisis Tests

Untuk menjalankan tests di NetBeans:

1. Klik kanan pada project atau test class
2. Pilih "Test" atau "Run File"
3. Melihat hasil test di Output window
4. Menganalisis coverage jika plugin code coverage diaktifkan

Tips untuk menganalisis test results:
1. Identifikasi tests yang gagal dan alasannya
2. Periksa code coverage untuk mengidentifikasi area yang belum diuji
3. Fokus pada edge cases dan complex conditional logic

## Rangkuman

Dalam tutorial ini, kita telah mempelajari:

✅ **Konsep Dasar Unit Testing** - Apa, mengapa, dan karakteristik unit test yang baik

✅ **JUnit Framework** - Cara menggunakan JUnit untuk menulis dan menjalankan unit test di Java

✅ **Test-Driven Development** - Pendekatan "Red, Green, Refactor" untuk pengembangan software

✅ **Testing OOP Components** - Teknik untuk menguji inheritance, polymorphism, dan concepts OOP lainnya

✅ **Mock Objects** - Menggunakan Mockito untuk mengisolasi unit yang diuji dari dependencies eksternal

✅ **Testing Patterns** - Pattern dan best practices untuk menulis unit test yang efektif

✅ **Code Coverage** - Tools dan teknik untuk mengukur seberapa baik test suite Anda menguji kode

Unit testing adalah komponen penting dalam pengembangan software yang berkualitas tinggi. Dengan menerapkan praktik-praktik yang telah kita pelajari, Anda dapat meningkatkan kualitas, reliability, dan maintainability kode Anda. Ingat bahwa unit testing bukanlah tujuan akhir, melainkan alat untuk membantu Anda membangun software yang lebih baik.

## Latihan Soal

1. Jelaskan apa yang dimaksud dengan unit test dan mengapa unit testing penting dalam pengembangan aplikasi berorientasi objek.

2. Buatlah test class untuk class `BankAccount` dengan fitur deposit, withdraw, dan transfer. Pastikan Anda menguji berbagai skenario termasuk happy path dan edge cases.

3. Bagaimana prinsip TDD (Test-Driven Development) dapat diterapkan dalam pengembangan aplikasi Java? Berikan contoh sederhana.

4. Jelaskan perbedaan antara stub, mock, dan fake dalam konteks unit testing. Kapan sebaiknya menggunakan masing-masing?

5. Buatlah unit test untuk class `ShoppingCart` yang memiliki method untuk menambah item, menghapus item, dan menghitung total. Gunakan Mockito untuk mock dependencies yang diperlukan.

6. Bagaimana cara menguji exception handling dalam JUnit? Berikan contoh test untuk method yang melempar exception.

7. Apa yang dimaksud dengan code coverage dan mengapa itu penting? Jelaskan jenis-jenis code coverage yang umum digunakan.

8. Buatlah unit test untuk class inheritance. Pilih contoh class hierarchy (misalnya `Vehicle` → `Car`, `Motorcycle`) dan tulis test untuk behavior yang diwarisi dan di-override.

9. Jelaskan bagaimana Anda menguji class dengan dependencies eksternal seperti database atau web service. Berikan contoh penggunaan mock objects.

10. Rancang test suite untuk subsistem autentikasi yang terdiri dari classes `User`, `UserService`, dan `AuthenticatedService`. Bagaimana Anda akan menstrukturkan test Anda dan dependency apa yang perlu di-mock?

## Referensi

1. Fowler, M. (2006). *Mocks Aren't Stubs*. [https://martinfowler.com/articles/mocksArentStubs.html](https://martinfowler.com/articles/mocksArentStubs.html)

2. Beck, K. (2002). *Test-Driven Development: By Example*. Addison-Wesley Professional.

3. Koskela, L. (2013). *Effective Unit Testing: A Guide for Java Developers*. Manning Publications.

4. Freeman, S., & Pryce, N. (2009). *Growing Object-Oriented Software, Guided by Tests*. Addison-Wesley Professional.

5. JUnit Team. (2022). *JUnit 5 User Guide*. [https://junit.org/junit5/docs/current/user-guide/](https://junit.org/junit5/docs/current/user-guide/)

6. Mockito Team. (2022). *Mockito Documentation*. [https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html)

7. Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship*. Prentice Hall. Chapter 9: Unit Tests.

8. Osherove, R. (2013). *The Art of Unit Testing: With Examples in .NET*. Manning Publications.

9. Feathers, M. (2004). *Working Effectively with Legacy Code*. Prentice Hall.

10. Meszaros, G. (2007). *xUnit Test Patterns: Refactoring Test Code*. Addison-Wesley Professional.

---

[◀️ Kembali ke Tutorial #14: Implementasi Proyek Sederhana](14-simple-project.md) | [Selesai! 🎉]

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
