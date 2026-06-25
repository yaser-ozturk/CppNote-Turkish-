
## Basic oper:

/ %(mod) ++ -- += -= *= /= %=

a = i++ önce i nin degerini a'ya ta sonra i yi 1 arttır
a = ++i önce i yi 1 arttır sonra i nin degerini ata

Logical operatörler:
&& (and)  orn 5 > 3 && 5 < 10 = true
|| (or)   orn 5 > 3 || 5 < 10 = true
! (not)   orn !(5 > 3) = false

Bitwise operatörler:
& (and)  orn 1010 & 1100 = 1000 5 & 6 = 4
| (or)   orn 1010 | 1100 = 1110 5 | 6 = 7
^ (xor)  orn 1010 ^ 1100 = 0110 5 ^ 6 = 3
~ (not)  orn ~1010 = 0101 ~5 = -6 ikiye tümleyen
<< (left shift)  orn 1010 << 1 = 10100 5 << 1 = 10 sayırı 2 katına çıkarır
>> (right shift) orn 1010 >> 1 = 0101 5 >> 1 = 2 sayıyı 2 ye böler

## Loops:

```cpp

for (int i = 0; i < 10; i++)
    {
        cout << i << endl;
    }

while (true)
{
	cout << "sonsuz döngü" << endl;
}

do
{
	cout << "sonsuz döngü" << endl; 
} while (true);

```



## Functions

```cpp

dönüşdegeri fonksiyonAdi(parametreler); //  = fonksiyon prototipi


dönüşdegeri fonksiyonAdi(parametreler)
    {
        //fonksiyon içeriği
    }
```

### Lamda Fonksşyonları:

C++'ta lambda fonksiyonları, anonim (ismi olmayan) fonksiyonlar yazmak için kullanılır ve genellikle kısa, geçici işlemler için tercih edilir.

captureedList
`&` → Dış değişkenlere referansla erişim sağlar (değiştirilebilir).  
`=` → Dış değişkenleri kopyalayarak kullanır (orijinali değişmez).

```cpp
auto isim = [captureedList](parametreler) 
        {
            //fonksiyon içeriği
        };
```

### Inline

Normalde bir fonksiyon çağrıldığında:

1. **Stack'e** dönüş adresi, parametreler ve diğer değişkenler eklenir.
2. Fonksiyonun koduna dallanılır (jump yapılır).
3. İşlem tamamlanınca çağıran fonksiyona geri dönülür.

Bu işlem küçük fonksiyonlar için bile **belli bir maliyet** yaratır. `inline` ile derleyiciye **fonksiyon çağırmak yerine kodu doğrudan çağrıldığı yere yapıştır** demiş oluruz.

-  Küçük ve sık kullanılan fonksiyonlarda (`getter`, `setter`, matematiksel işlemler vb.)
-  Döngüler içinde sık çağrılan kısa fonksiyonlarda
-  Makro yerine **type-safe** ve **debug-friendly** bir alternatif olarak

```cpp
#include <iostream>
using namespace std;

inline int kare(int x) {  
    return x * x;  
}

int main() {
    int a = 5;
    cout << "a^2 = " << kare(a) << endl;
    return 0;
}

```

`are(5)` çağrıldığında, `return 5 * 5;` şeklinde doğrudan kod içine yerleştirilir.
- Daha  hızlı çalışır

## Data Type

int 4 byte
float 4 byte
char 1 byte
bool 1 byte

arrays = int a[5] = {1,2,3,4,5}; aynı tipte veriler

### Pointers:

```cpp
int num = 42
int* pnum = &num; // num adresini pnum a ata

void addOne(int* num) {  
	(*num) += 1;
}
            
int main() {
	int x = 10;
	addOne(&x);
	std::cout << x;  // Çıktı: 11
}
```


### Refrerences:

Fonksiyon değişkeni orijinal haliyle değiştirir.genelde de bunun için kullanılır zaten.

```cpp
int num = 42;
int& rnum = num; num adresini rnum a ata

void addOne(int& num) {  
	num += 1;
}

int main() {
	int x = 10;
	addOne(x);
	std::cout << x;  // Çıktı: 11
}

```


### Struct :

```cpp
struct Ogrenci
{
	std:: isim;
	int yas;
};

Ogrenci p1 = {"ali", 20};
p1.isim = "veli";
```


### Union:

Önemli not uninion sadece bir tane değeri tutabilir.

```cpp
union Sayi
{
	int x;
	float y;
};

Sayi s;
s.x = 10;

union ExampleUnion {
	int a;
	float b;
	char c;
};

int main() {
	union ExampleUnion u;

	u.a = 10;
	printf("a: %d\n", u.a);

	u.b = 5.5;  // 'a' değeri artık geçersiz
	printf("b: %f\n", u.b);
```



### Class :

```cpp
class Person {
	public:
		std::string name;
		int age;

	void print() { // Metod
		std::cout << name << " " << age << std::endl;
	}
};
```

### Static Type:

Bir değişken **derleme zamanında (compile-time)** belirli bir türe sahipse ve bu tür **çalışma zamanında (runtime)** değiştirilemiyorsa, buna **statik tür** denir.  
C++'ta **normal değişkenler statik türdedir** ve türü bir kez belirlendikten sonra değiştirilemez.
Cpp de static olarak tür atarnırsa değiştirilemez

```cpp
int x = 5;  // x bir int değişkenidir
x = 10;     //Değer değiştirilebilir
x = 3.14;   //HATA! double türündeki bir değeri int değişkene atayamazsın

// Burada `x` değişkeninin **türü her zaman `int` olarak kalır**. Farklı bir tür atanamaz. Yani C++’ta normal değişkenler static type'dır. Tür değiştiremezsin!

```


### Dynamic Type:

Bir değişkenin **çalışma zamanında (runtime) türü değiştirilebiliyorsa**, buna **dinamik tür (dynamic type)** denir. C++'ta **dinamik tür kullanmanın iki yaygın yolu vardır:**

- `void*` (Ham İşaretçi - "Type Erasure")
- `std::any` (C++17 ile gelen dinamik tip)

void* :

```cpp
#include <iostream>

int main() {
    int sayi = 42;
    void* ptr = &sayi;  // herhangi bir veri türünü tutabilir
    
    // Tekrar int'e çevirmek gerekiyor:
    int* intPtr = static_cast<int*>(ptr);
    std::cout << *intPtr << std::endl;  // Çıktı: 42
    
    return 0;
	//`void*`, **her türü kabul eder**, ancak **hangi türü tuttuğunu bilemezsin**.Bu yüzden **cast işlemi (tür dönüşümü)** yapman gerekir.
}

```

std::any :

```cpp
#include <iostream>
#include <any>

int main() {
    std::any veri = 10;  // Başlangıçta int
    std::cout << std::any_cast<int>(veri) << std::endl;  // Çıktı: 10

    veri = 3.14;  // Şimdi double oldu
    std::cout << std::any_cast<double>(veri) << std::endl;  // Çıktı: 3.14

    veri = std::string("Merhaba!");  // Şimdi string oldu
    std::cout << std::any_cast<std::string>(veri) << std::endl;  // Çıktı: Merhaba!

    return 0;
}

```

## Pointer and Referances

```cpp
int a = 1;
int *ptr = &a;

int main() {
    std::cout << "a: " << a << std::endl;
	std::cout << "ptr: " << ptr << std::endl;    // adres
	std::cout << "*ptr: " << *ptr << std::endl; // deger
	return 0;

}
```

### Function pointers:

```cpp
int add(int a, int b) {
    return a + b;
}

int main() {
	int a ;
	int (*fcnpointer) (int, int) = add;
	a = fcnpointer(1, 2);
	std::cout << fcnpointer(1, 2) << std::endl;
} 
```

### Const

```cpp
// veri değişmez
const int x = 10;
const int* ptr = &x;  // İşaret edilen veri sabit, değiştirilemez
*ptr = 20;  //  HATA! Değiştirilemez


// adress değişmez
int x = 10, y = 20;
int* const ptr = &x;  // ptr, sadece x’i gösterebilir
ptr = &y;  //  HATA! Pointer adresi değiştirilemez

const int x = 10;
const int* const ptr = &x;  // Hem adres hem de içerik değiştirilemez

```

### Pointer to Pointer

Pointerin adresini tutan pointerlardır.

```cpp
int x = 42;
int* p = &x;
int** pp = &p;  // p'nin adresini tutar
std::cout << **pp;  // Çıktı: 42

```

### std::unique_ptr

**Bellek sızıntısını önler**. `delete` çağırmaya gerek yoktur, çünkü otomatik temizlenir.

```cpp
#include <memory>
std::unique_ptr<int> ptr = std::make_unique<int>(10);
std::cout << *ptr;  // Çıktı: 10

```

### std::shared_ptr

**Bir nesneye birden fazla pointer sahip olabilir**.

```cpp
#include <memory>
std::shared_ptr<int> p1 = std::make_shared<int>(10);
std::shared_ptr<int> p2 = p1;  // p1 ve p2 aynı adresi gösterir

```

### std::weak_ptr

Nesneyi sahiplenmez ama izler.

```cpp
#include <memory>
std::shared_ptr<int> p1 = std::make_shared<int>(10);
std::weak_ptr<int> wp = p1;  // wp, p1'i takip eder ama referans sayısını artırmaz

```



Refrerences :

        Aşağıdaki örnek bence çok hoş normalde fonksiyonun içine giren değişkeninin
        degerş tutulamamktadır ama referans ile bu değişkenin değeri değiştirilebilir.

        void swap(int& a, int& b) {
            int temp = a;
            a = b;
            b = temp;
        }

        int main() {
        int x = 5, y = 10;
        std::cout << "Before Swap: x = " << x << " y = " << y << std::endl; // Outputs 5 10
        
        swap(x, y);
        std::cout << "After Swap: x = " << x << " y = " << y << std::endl;  // Outputs 10 5
        }

## Memory Model

C++ programı çalışırken bellek **farklı bölgelere ayrılır**. Ana bölümler:

1. Code Segment (Kod Segmenti)
    - Derlenmiş **makine kodlarını (binary kodlar)** içerir.
    -  `main()` ve diğer fonksiyonlar burada bulunur.
    -  **Salt okunur (read-only)** olup, değiştirilemez.
1. **Data Segment (Veri Segmenti)**
    - `.data` (Başlangıç değeri atanmış global değişkenler)
    - `.bss` (Başlangıç değeri atanmamış global değişkenler)
2. **Stack Segment (Yığın Bellek)**
3. Heap Segment (Öbek Bellek)
### Stack memory

**Derleme (compile) zamanında** tahsis edilir.

```cpp
void functionExample() {
	int x = 10; // x is stored in the stack memory
}
```

```cpp
#include <iostream>

// Global değişken (Data Segment)
int globalVar = 100;  

void func() {
    // Static değişken (Data Segment)
    static int staticVar = 200;  
    std::cout << staticVar << std::endl;
}

int main() {
    // Yerel değişken (Stack Belleği)
    int localVar = 10;  

    func();
}


```

- `globalVar` → Program sonuna kadar bellekte kalır.
- `staticVar` → İlk kez çağrıldığında bellekte tutulur, fonksiyon bitince kaybolmaz.
- `localVar` → Stack bellekte tutulur, fonksiyon bitince kaybolur.
### Heap memory

Heap memory is used for dynamic storage duration variables, such as objects created using the new keyword. The programmer has control over the allocation and deallocation of heap memory using new and delete operators. Heap memory is a larger pool of memory than the stack, but has a slower access time.

**Çalışma (runtime) zamanında** tahsis edilir.

```cpp
void functionExample() {
		int* p = new int; // dynamically allocated int in heap memory
		*p = 10;
		// more code
		delete p; // deallocate memory
	}
```


## Life Time

### **Static Storage Duration (Statik Depolama Süresi)**

- `static int a;` veya `int a;` (küresel değişken) olarak tanımlanan değişkenler programın başında bellekte yer alır ve program bitene kadar yaşamaya devam eder.
- Bellekte **data segment** (BSS veya Data bölümü) içinde saklanır.
- Eğer başlatılmazsa, varsayılan olarak **0** değerini alır.
- `static` anahtar kelimesi, bir değişkenin fonksiyon çağrıları arasında değerini korumasını sağlar.

```cpp
#include <iostream>

static int x = 10; // Statik ömürlü değişken
void func() {
    static int y = 20; // İlk çağrıldığında bellekte yer alır ve program bitene kadar saklanır.
    std::cout << y << std::endl;
    y++;
}

int main() {
    func(); // 20 yazdırır
    func(); // 21 yazdırır
    return 0;
}

```

### **Thread Storage Duration (İş Parçacığı Depolama Süresi)**

- **C++11** ile gelen `thread_local` anahtar kelimesi kullanılarak tanımlanır.
- Her **thread (iş parçacığı)** kendi kopyasını oluşturur.
- Thread sona erdiğinde, değişken de silinir.

```cpp
#include <iostream>
#include <thread>

thread_local int tls_var = 0; // Her thread kendi kopyasını alır.

void threadFunc() {
    tls_var++;
    std::cout << "Thread ID: " << std::this_thread::get_id() << ", tls_var: " << tls_var << std::endl;
}

int main() {
    std::thread t1(threadFunc);
    std::thread t2(threadFunc);

    t1.join();
    t2.join();

    return 0;
}
```

```
Output:
Thread ID: 12345, tls_var: 1
Thread ID: 67890, tls_var: 1

```

    Automatic Storage Duration:
        fonksiyonun içindeli lokal değişken fonksiyon ölünce ölüyor degilmi ???

    Dynamic Storage Duration:
        new ve delete ile oluşturulan değişkenlerdir.
        malloc da oluyor 
        manuel elle silmen lazım
        heapde depolanır


Raw pointers

    NEW - Delete 

    Aşağıdaki örnek gayet uygun fakat arreyler için [n],ve []' ler yerine değişkeni keyword
    o zamanda değişkenler için oluyor.

    int n = 10;
    int* arr = new int[n]; // Dynamically allocates an array of 10 integers on the heap

    // Set some values in the array
    for (int i = 0; i < n; i++) {
    arr[i] = i;
    }

    delete[] arr; // Deallocates the memory assigned to the array

    Memory leak

        bu durumda delete işlemi yapılmazsa bellek sızıntısı olur ve programın bellek kullanımı artar.

        On numara örnek :
            std::shared_ptr<int[]> ptr = std::make_shared<int[]>(100); 
            // Heap'te 100 elemanlı bir int dizisi oluşturuluyor
            // shared_ptr otomatik bellek yönetimi sağlıyor


Unique Pointer (unique_ptr)


Bu kısma devam edicem ama şuan degil bu iş zor


---------------------------------------------------------------------


Structuring Codebase:

    Namespaces 
        namespace MyNamespace {
            int aFunction() {
                // function implementation
            }
        }
        // to use the function
        MyNamespace::aFunction();

    
----------------------------------------------
Bitirme için bak yaser

        MCR MAtlab

        grpc haberleşme için

----------------------------------------------

Clases an Structers

    ÖRNEK :

    data memberlar age ve name
    member functionlar ise bark
    aşağıdaki gibi bir classes yazılabilmektedir

    class Dog {
        public:
            std::string name;
            int age;
        
            void bark() {
                std::cout << name << " barks!" << std::endl;
            }
        };
    
    class üyelerinin görünürüğü public, private ve protected olabilir.
        public: Herkes tarafından erişilebilir.
        private: Sadece sınıfın kendi üyeleri tarafından erişilebilir.
        protected: Sadece sınıfın kendi üyeleri ve türetilmiş sınıflar tarafından erişilebilir.

    Inheritance 

        : ile kullanılmaktadır diğer bir sınıfın özelliklerini almak için kullanılır.
        aşağdaki örnek bir multiple Inheritance örneğidir.

        class Animal {
            public:
                void breathe() {
                    std::cout << "I can breathe" << std::endl;
                }
            };
            
        class Dog : public Animal {
        public:
            void bark() {
                std::cout << "Dog barks!" << std::endl;
            }
        };

        Dog myDog;
        myDog.breathe(); // Output: I can breathe
        myDog.bark(); // Output: Dog barks

        Diamond Inheritance: ise bir sınıfın birden fazla sınıf tarafından türetilmesi durumudur.


    Polymorphism: ???????
        aynı fonksiyonun farklı sınıflarda farklı davranışlar göstermesine olanak tanır.
        
        Static Polymorphism:

            Function overloding:
                aynı isimde farklı parametrelerle fonksiyon tanımlanmasıdır.

                void print(int x) {
                    std::cout << x << std::endl;
                }
                
                void print(float x) {
                    std::cout << x << std::endl;
                }

                int main() {
                    print(5); // Output: 5
                    print(5.5); // Output: 5.5
                }

            Template:
                template <typename T>
                void print(const T& x) {
                    std::cout << x << std::endl;
                }

                int main() {
                    std::cout << add(1, 2) << std::endl; // Output: 3
                    std::cout << add(1.1, 2.2) << std::endl; // Output: 3.3
                }

        Dynamic Polymorphism:

                hangi fonksiyonu çağırabileceğini şeçebiliyorusun çok karışık bence direkt örnege bak :
                
                Virtual kullanılarak :

                #include <iostream>

                // Base class
                class Shape {
                public:
                    virtual void draw() {
                        std::cout << "Drawing a shape" << std::endl; 
                    }
                };

                // Derived class 1
                class Circle : public Shape {
                public:
                    void draw() override {
                        std::cout << "Drawing a circle" << std::endl; 
                    }
                };

                // Derived class 2
                class Rectangle : public Shape {
                public:
                    void draw() override {
                        std::cout << "Drawing a rectangle" << std::endl;
                    }
                };

                int main() {
                    Shape* shape;
                    Circle circle;
                    Rectangle rectangle;

                    // Storing the address of circle
                    shape = &circle;

                    // Call circle draw function
                    shape->draw();

                    // Storing the address of rectangle
                    shape = &rectangle;

                    // Call rectangle draw function
                    shape->draw();

                    return 0;
                }

----------------------------------------------------------------------------------

Exeption Handling:

    try - cath : 
    hata yakalamak için kullanılır.

    try {
        // bu kısımda hata olabilecek kodlar yazılır
    } catch (const std::exception& e) {
        // hata olursa burası çalışır
    }

    throw :
        Eğer try bloğu içinde bir hata oluşursa, throw anahtar kelimesi kullanılarak belirli bir istisna (exception) türü oluşturulabilir.
        Bu istisna, ilgili catch bloğu tarafından yakalanarak işlenir.

        try {
            if (b == 0) {
                throw std::runtime_error("Division by zero is not allowed!"); 
                // Hata oluşursa istisna (exception) fırlat
            }
            result =  a / b;  // Bölme işlemi
            std::cout << "Result: " << result << std::endl;

        } catch (const std::exception& e) { 
            // Hata yakalanır ve ekrana yazdırılır
            std::cerr << "Error: " << e.what() << std::endl;
        }

        çıktı = Enter two numbers: 8 0
                Error: Division by zero is not allowed!

    Standard Exceptions

        std::exception sınıfı tüm standart C++ istisnalarının temel sınıfıdır.
        std::logic_error sınıfı, mantıksal hataları
        std::runtime_error sınıfı, çalışma zamanı hatalarını

        ornek:
        } catch (const std::exception& e) {
            std::cerr << "Error: " << e.what() << std::endl;
        }

    Exit :
        ile koddan çıkılır retun 0 gibi



---------------------------------------------------------------------------------

Standart Libraries :

    <CHRONO> : zaman işlemleri için kullanılır. zaman süresü tutar

            Duration :
                std::chrono::seconds sec(10); // 
                
            Time Point : 
                std::chrono::systemclock::system_clock //  gerçek zamanı tutar
                std::chrono::steady_clock // zamanı tutar bi kodun ne kadar zaman aldığnğ ölçümler
                std::chrono::high_resolution_clock // en yüksek çözünürlükte zamanı tutar
            
            Clock : 
                time_point // zamandaki sipesifik bir nokta
                duration // zaman aralığı
                now() // şu anki zamanı döndürür

                std::chrono::system_clock::time_point one_hour_from_now = now + std::chrono::hours(1);
            
            Converting Time Points to Calendar Time :
                insan trafından okunabilir zamanı döndürür
                    std::chrono::system_clock::time_point now = std::chrono::system_clock::now();
                    std::time_t now_c = std::chrono::system_clock::to_time_t(now);
                    std::cout << "Current time: " << std::ctime(&now_c) << std::endl;
                    
----------------------------------------------------------------------------------------------------------------                  
Language Concepts in C+++ :

        Automatic Type Deduction :
            auto keywordü ile değişkenin türü otomatik olarak belirlenir.
            auto ile tenımlama mutlaka bir ilk degere sahip olmalıdır.
            auto x = 5; // x is an integer
            auto y = 5.5; // y is a double
            auto z = "Hello"; // z is a const char*

            C++14 ile fonyksiyonlar da tanımlanabilir hale geldi.

        Arrays and vectors :

            int marks[5] = {10, 20, 30, 40, 50}; // Array
            std::vector<int> marks = {10, 20, 30, 40, 50}; // Vector

        Type Casting:

                C-style casting:
                    int a = 10;
                    float b = (float)a; // C-style casting

                Static casting:

                -- Derleme (compile-time) sırasında dönüşüm yapar.
                -- Hızlıdır, ancak yanlış tür dönüşümüne karşı kontrol yapmaz.
                -- İlişkili türler arasında dönüşüm sağlar (örneğin, türetilmiş sınıfı temel sınıfa çevirmek).
                -- Güvensiz olabilir, çünkü yanlış tür dönüşümü yaparsan hata almazsın ama beklenmeyen davranışlar oluşabilir.


                    int a = 10;
                    float b = static_cast<float>(a); // Static casting

                Dynamic casting:

                -- Çalışma zamanı (runtime) sırasında dönüşüm yapar.
                -- virtual fonksiyon içeren polimorfik sınıflar için kullanılır.
                -- Güvenlidir, çünkü yanlış tür dönüşümünü nullptr ile kontrol edebilirsin.
                -- Derleme zamanında değil, çalışma zamanında kontrol yapar, bu yüzden static_cast'e göre biraz daha yavaştır.
                
                genelde sınıf hiyerarşisinde temel (base) ve türetilmiş (derived) sınıflar arasındaki işaretçi ve referans dönüşümlerini güvenli bir şekilde yapmak için özel olarak kullanılır.
                ornek :


                class Base {};
                class Derived : public Base {};

                Base* base_ptr = new Derived();
                Derived* derived_ptr = dynamic_cast<Derived*>(base_ptr);  // dynamic_cast from Base* to Derived*

                Reinterpret casting

                -- reinterpret_cast, bellekteki bitleri değiştirmeden veri türlerini dönüştürür.
                -- İşaretçileri ve tamsayıları birbirine çevirmek için kullanılır.
                -- Yanlış kullanımda program çökebilir, dikkatli olunmalıdır.
                -- Düşük seviyeli sistem programlama ve donanım erişimi için uygundur. 

                ornek:

                int main() {
                    int x = 10;
                    int* ptr = &x;
                    
                    uintptr_t addr = reinterpret_cast<uintptr_t>(ptr); // Pointer → Integer dönüşümü
                    std::cout << "Pointer Address: " << addr << std::endl;
                    
                    return 0;
                }

                Const Casting

                -- const niteliğini kaldırarak değişkeni değiştirilebilir (mutable) hale getirir.
                -- Genellikle önerilmez, çünkü const olan bir şeyi değiştirmek programın beklenmeyen davranış göstermesine neden olabilir.
                -- Sadece const veya volatile niteliklerini kaldırabilir, başka dönüşüm yapama
                
                ornek : 

                void print(char* str) {
                    std::cout << "String: " << str << std::endl;
                }
                
                int main() {
                    const char* message = "Hello, World!";
                    print(const_cast<char*>(message)); // const_cast ile `const` kaldırıldı
                    return 0;
                }

        Undifinedfined behavior : 

                Uninitialized Variables 

                    değer atamadan değişkeni başlatma
                    ornek :

                    int x ; 
                    int x{}; // x otomatik olarak 0'a ayarlanır C++11

                Out-of-bounds Memory Access;

                    Sınırın dşındaki bir degere erişmek istersen bu şekil bir hata oluşabilir.
                    
                    ornek :

                    int arr[5] = {1, 2, 3, 4, 5};
                    std::cout << arr[5] << std::endl; // Out-of-bounds access


                Null Pointers Dereference

                    nullptr ile işaretçiye erişmeye çalışmak

                    int* ptr = nullptr;
                    *ptr = 10; // Dereferencing a null pointer

                Division by Zero

                    int a = 10;
                    int b = 0;
                    int c = a / b; // Division by zero

        Argument Dependent lookup (ADL)

                ???????????????????????????????

        Name Mangaling :
                C++ aynı siimli fonksiyonlara izin veriri bu özelliğe name Mangaling Dereference


                #include <iostream>

                void func(int x) { std::cout << "int version\n"; }
                void func(double x) { std::cout << "double version\n"; }

                int main() {
                    func(10);    // int olan fonksiyon çağrılır
                    func(3.14);  // double olan fonksiyon çağrılır
                    return 0;
                }


        Macrolar : 

        Makrolar, C++’ta derleme öncesinde (preprocessing) yapılan metin değiştirme işlemleridir.

        -- #define direktifi ile tanımlanır.
        -- Derleyiciye ulaşmadan önce preprocessor tarafından işlenir.
        -- Bellekte yer kaplamaz, sadece metin değişimi yapar.
        -- Sabitler,fonksiyon benzeri işlemler ve koşullu derleme için kullanılabilir.
              
            Constant Macros:
                #define PI 3.14159  // PI adlı bir sabit makro tanımlandı

            Function like Macros :
        
                #define SQUARE(x) ((x) * (x)) // x'in karesini hesaplayan makro

            Conditional Compilation:

            Kodun belirli bölümlerini sadece belirli koşullarda dahil etmek için #ifdef, #ifndef, #if, #else, #endif gibi direktifler kullanılır.

                ornek : 
                #include <iostream>

                #define DEBUG_MODE  // Bu satır yorum satırına alınırsa, sadece normal kod çalışır.

                int main() {
                    #ifdef DEBUG_MODE
                        std::cout << "Debugging mode is ON!" << std::endl;
                    #else
                        std::cout << "Normal mode." << std::endl;
                    #endif
                        return 0;
                    }

            Include Guard:

            Makrolar, başlık dosyalarının (.h) birden fazla kez eklenmesini önlemek için kullanılır.

            #ifndef ve # pragma once kullanılır

            Ornek ifndef :
                #ifndef MY_HEADER_H
                #define MY_HEADER_H

                // Bu başlık dosyası sadece bir kez dahil edilecek
                void myFunction();

                #endif // MY_HEADER_H

            Ornek #pragma once 

                   #pragma once
                    void myFunction();


---------------------------------------------------------------------------------------

Templates :

    C++’ta template, türden bağımsız kod yazmak için kullanılır. 
    Template, aynı kodu farklı türlerle kullanılmasını sağlamaktadır.
    Not!! şablon kullanılıyorsa her şey bir dosyada tanımlı olmalıdır.    
    
    Fonksiyon Templates:

    fonk çağrılırken a y ve b yi float versem veya integer versemde farketmez
    ornek :
        template <typename T>
        T add(T a, T b) {
            return a + b;
        }

        add<int>(1, 2); // 3
        add(1, 2); // 3
        add<float>(1.1, 2.2); // 3.3
        add(1.1, 2.2); // 3.3


    Class Templates:

        template <typename T>
        class Pair {
            private:
                T first, second;
            public:
                Pair(T a, T b) { 
                    first = a;
                    second = b;
                }
                T bigger();
        };

        template <typename T> // clasın dışındatanımlanana fonksiyonlar için tekrar tanımlama yapılmalıdır.
        T Pair<T>::bigger() { // böyle de garip bi şekilde tanımlanır.
            return (first > second ? first : second);
        }

        int main() {
            Pair<int> p(10, 20); // Pair clası integer olarak tanımlanır . ve 10 ve 20 değerleri atanır
            std::cout << p.bigger() << std::endl; // Output: 20
            return 0;
        }

    Variadic Template:

        Herhangi bir sayıda argüman almasında kullanılır aslında gayet kullanışlı
    
        template <typename T>
        void print(T value) {
            std::cout << value << std::endl;
        }

        template <typename T, typename... Args>
        void print(T first, Args... args) {
            std::cout << first << std::endl;
            print(args...);
        }

        int main() {
            print(1, 2, 3, 4, 5);
            return 0;
        }
        

 

    Template Specialization:

        template <typename T>
        T add(T a, T b) {
            return a + b;
        }

        template <>
        std::string add(std::string a, std::string b) {
            return a + " " + b;
        }

        int main() {
            std::cout << add(1, 2) << std::endl; // Output: 3
            std::cout << add("Hello", "World") << std::endl; // Output: Hello World
            return 0;
        }

    Non-type Template Parameters:

        template <typename T, int N>
        class Array {
            private:
                T arr[N];
            public:
                void set(int index, T value) {
                    arr[index] = value;
                }
                T get(int index) {
                    return arr[index];
                }
        };

        int main() {
            Array<int, 5> arr;
            arr.set(0, 10);
            std::cout << arr.get(0) << std::endl; // Output: 10
            return 0;
        }

    Variadic Templates:

        template <typename T>
        void print(T value) {
            std::cout << value << std::endl;
        }

        template <typename T, typename... Args>
        void print(T first, Args... args) {
            std::cout << first << std::endl;
            print(args...);
        }

        int main() {
            print(1, 2, 3, 4, 5);
            return 0;
        }

---------------------------------------------------------------------------------

Conteiners :

    C++’ta veri yapıları, verileri depolamak ve işlemek için kullanılır. 
    Standart kütüphane, birçok veri yapısını destekler ve bunlar genellikle şablonlar (templates) ile uygulanır.

    Array :

        std::array, sabit boyutlu bir dizi veri yapısıdır. 
        Array, C dizilerine benzer, ancak boyutu çalışma zamanında değiştirilemez.

        std::array<int, 5> arr = {1, 2, 3, 4, 5}; // Array of 5 integers
        std::array<std::string, 3> names = {"Alice", "Bob", "Charlie"}; // Array of 3 strings

    Vector :
    
        std::vector, dinamik boyutlu bir dizi veri yapısıdır. 
        Vector, boyutu çalışma zamanında değiştirilebilir ve bellekte otomatik olarak yönetilir.

        std::vector<int> vec = {1, 2, 3, 4, 5}; // Vector of integers
        std::vector<std::string> names = {"Alice", "Bob", "Charlie"}; // Vector of strings

    List : 
     
        std::list, çift yönlü bağlı liste veri yapısını temsil eder. 
        List, elemanları sıralı bir şekilde depolar ve elemanlar arasında hızlı ekleme ve silme işlemleri yapılabilir.

        std::list<int> list = {1, 2, 3, 4, 5}; // List of integers
        std::list<std::string> names = {"Alice", "Bob", "Charlie"}; // List of strings













































## Const

C++'ta `constexpr` gibi çeşitli **sabit (`const`) türleri** vardır. Bunlar, derleme zamanında veya çalışma zamanında sabit olup olmadıklarına göre farklılık gösterir. İşte bazı önemli sabit türleri:

### **1. `const` (Çalışma Zamanı Sabiti)**

- Değeri **çalışma zamanında** belirlenir.
- Değiştirilemez ama **derleme zamanında hesaplanmak zorunda değildir**.
- Bellekte bir alan kaplar.

cpp

CopyEdit

`const int x = 10;  // Çalışma zamanında sabit int arr[x];  // Hata! x derleme zamanında bilinmiyor`

---

### **2. `constexpr` (Derleme Zamanı Sabiti)**

- Değeri **derleme zamanında hesaplanabilen** bir sabittir.
- `constexpr` olarak işaretlenmiş bir değişken, **mutlaka derleme zamanında** değerlendirilebilir olmalıdır.
- Daha çok sabit ifadeler (`constant expressions`) oluşturmak için kullanılır.

cpp

CopyEdit

`constexpr int y = 20;  // Derleme zamanında hesaplanır int arr[y];  // Doğru! y derleme zamanında biliniyor`

- `constexpr` fonksiyonlar, derleme zamanında çalıştırılabilir:

cpp

CopyEdit

`constexpr int kare(int x) {     return x * x; }  constexpr int sonuc = kare(5);  // Derleme zamanında hesaplanır`

---

### **3. `consteval` (Sadece Derleme Zamanı)**

- C++20 ile gelmiştir.
- `consteval` fonksiyonları **sadece derleme zamanında çağrılabilir**.
- Çalışma zamanında çağrılmaya çalışılırsa hata oluşur.

cpp

CopyEdit

`consteval int kup(int x) {     return x * x * x; }  constexpr int sonuc = kup(3);  // Derleme zamanında hesaplanır int y = 4; // int hata = kup(y);  // Hata! Çalışma zamanında çağrılamaz`

---

### **4. `constinit` (Derleme Zamanında Başlatılan Sabitler)**

- C++20 ile gelmiştir.
- Değişkenin **derleme zamanında başlatılmasını** garanti eder, ancak çalışma zamanında değişebilir.
- **Sabit olarak değil, sadece sabit başlatma garantisi olarak kullanılır**.

cpp

CopyEdit

`constinit int global = 42;  // Derleme zamanında başlatılmalı global = 50;  // Çalışma zamanında değiştirilebilir`

---

### **Farkları Özetleyelim**

| Tür         | Derleme Zamanı mı? | Çalışma Zamanında Değiştirilebilir mi? | Kullanım Alanı                                               |
| ----------- | ------------------ | -------------------------------------- | ------------------------------------------------------------ |
| `const`     | **Zorunlu değil**  | Hayır                                  | Çalışma zamanı sabitleri, fonksiyon parametreleri            |
| `constexpr` | **Evet**           | Hayır                                  | Derleme zamanı sabitleri, sabit ifadeler                     |
| `consteval` | **Evet (Sadece)**  | Hayır                                  | Derleme zamanında **zorunlu olarak** hesaplanan fonksiyonlar |
| `constinit` | **Evet**           | **Evet**                               | Derleme zamanında başlatılma garantisi ama sabit değil       |

Eğer **bir değişkenin tamamen sabit** olmasını istiyorsan `constexpr`,  
**derleme zamanında hesaplanmasını zorunlu kılmak** istiyorsan `consteval`,  
**sadece derleme zamanında başlatılmasını sağlamak** istiyorsan `constinit` kullanabilirsin.

Hangi durum için ne gerektiğine bağlı olarak seçim yapabilirsin.


## Class

### Inherites
Klasik bir kalıtım örneği aşagıda verilmiştir bir clasın tüm özellikleri bir kalıtım fonksiyonuna atanabilir.

Protected belirteci ise taban sınıfından ve türetilmiş sınıftan bu özellikleri erişilebilir kılar. diğer türlü erişemessin.

Kalıtım Belirteci public ise :
Base'in private degiskeni asla derived nesneden erişilemez.

Kalıtım Belirteci protected ise (private olarak alsanda aynı) :

Base'nin taban sınıfındaki public bile mainden çagrılamaz.
Derived içinden Basenin protected ve public özelliklere de erişilebilir ama private yine olmaz

Peki private ile protected almanın ne farkı var ? şimdi derived ın derivedını oluştursak ve bir öncekini derivedı protected olarak atasak taban sınfın public ozellıgıne erişebilirim ama private atasam erişemem.

Örnek aşağıda verilmiştir :

```cpp
#include <iostream>  
#include <utility>  
  
class human{  
    protected:  
    std::string tc{};  
    std::string name{};  
    std::string srname{};  
  
    public:  
  
    explicit human(std::string tc = "", std::string name = "", std::string srname =""):tc(std::move(tc)),name(std::move(name)),srname(std::move(srname)){}  
  
    std::string get_tc(){return tc;}  
    std::string get_name(){return name;}  
    std::string get_srname(){ return srname;}  
  
    void set_tc(const std::string &tc_){tc=tc_;}  
    void set_name(const std::string &name_){name=name_;}  
    void set_srname(const std::string &srname_){srname=srname_;}  
  
  
};  
  
  
class student:public human {  
    private:  
    std::string student_num{};  
    public:  
    explicit student(std::string student_num = "" ,std::string tc = "", std::string name = "", std::string srname ="" ):student_num(std::move(student_num)),human(std::move(tc),std::move(name),std::move(srname)){}  
  
    std::string get_student_num(){return student_num;}  
    void set_student_num(const std::string &num_){student_num=num_;}  
};  
  
int main() {  
  
    human ali("26666666","Ali","atabak");  
  
    student student1("200223041","26666666","Mehmet");  
  
    std::cout << student1.get_student_num() << std::endl;  
    std::cout << student1.get_tc() << std::endl;  
    std::cout << student1.get_name() << std::endl;  
    std::cout << student1.get_srname() << std::endl;  
  
}
```

NOT :

std::move() :

explicit :



#### Override

Taban sınıfta üretilmiş bir özellik veya metodu aynı isimle kulanırsan onun üzerine Override etmiş olursun.

Metodlar özellikleri özelliklerde metodları ezebilir sıkıntı yok

```cpp
#include <iostream>  
#include <utility>  
  
  
class Base {  
    public:  
        int data[100]{};  
        int size{};  
        int x{0};  
  
        Base():size(0){};  
  
    void add(int value) {  
        data[size] = value;  
        size++;  
    }  
  
    void print()const {  
        std::cout<<"Base data : " <<std::endl;  
        for (int i = 0; i < size; i++) {  
            std::cout << data[i] << " ";  
        }  
    }  
};  
  
class Derived : public Base {  
public:  
    float data[100]{};  
    int size{};  
  
    Derived():size(0.0){};  
  
    void x() { // metod özelliği ezdi  
        std::cout << "hello world" << std::endl;  
    }  
  
    void add(float value) { // metod ezdim  
        data[size] = value;  
        size++;  
    }  
  
    void print()const { //Metod ezdim  
        Base::print(); // basin içindeki printi çagır bu sınıfın besine ekleme yapmadan olmaz normal base farklı bu sınıfın base i farklı  
        std::cout << "Derived data: " << std::endl;  
        for (int i = 0; i < size; i++) {  
            std::cout << data[i] << " ";  
        }  
    }  
  
    void addInt(int value) {  
        Base::add(value); // bu sınıfın basine ekleme yapıyoruz  
    }  
  
  
};  
  
  
  
int main() {  
  
    Base b;  
    b.add(1);  
    b.add(2);  
    b.add(3);  
    b.print();  
    std::cout << std::endl;  
    std::cout << std::endl;  
  
    Derived d ;  
    d.add(1.3);  
    d.add(2.3);  
    d.add(3.4);  
    d.print();  
  
    std::cout << std::endl;  
    std::cout << std::endl;  
  
    d.addInt(4);  
    d.addInt(5);  
    d.addInt(3);  
    d.print();  
  
    // std::cout << d.x << std::endl; // hata cunku artuk bi metod  
  
    // peki burada x i özellik olarak nasıl kullanacagız tabikide casting ile  
    std::cout << std::endl;  
    std::cout << std::endl;  
    std::cout << "Tip degistirme :" <<std::endl;  
    Base* ptr = &d;  
    ptr->x = 2;  
    std::cout << ptr->x;  
  
  
  
}
```

```
OUT :

Base data :
1 2 3

Base data :
Derived data:
1.3 2.3 3.4

Base data :
4 5 3 Derived data:
1.3 2.3 3.4

Tip degistirme :
2
```



association
	aggregation
		composition
	     dependency	

has a relationship



## Operator overloading

C++ dilinde bir sınıf nesnesi bir operatörün operandı olduğunda derleyici dilin kurallarına göre operatörün operandı olmuş sınıf nesnesi ifadesini bir fonksiyon çağrısına dönüştürüyoryani ortada doğrudan fonksiyon çağrı operatörü yok ama kodun anlamı derleyicinin bir fonksiyona çağrı yapması bunlara operator functions deniliyor

a + b ifadesi olsun a ve b bir sınıf türünden nesneler olsun bu durumda tanımlanmış bir fonksiyon varsa derleyici a + b ifadesini bir operatör fonksiyonuna yapılan çağrı ifadesine dönüştürüyor peki burada çağırılan fonksiyon global function mı yoksa sınıfın non-static member functionı mı ? HER İKİSİDE OLABİLİR

SORU:run time'a yönelik bir mekanizma mı compiler time'a mı? compile time'a yönelik bir mekanizma çünkü derleyici hangi fonksiyonun çağırıldığını derleme zamanında anlıyor

- operatör fonksiyonları static member function olamaz.
- operatör overloadingten faydalanabilmemiz için intuitive olmamız gerekiyor.

1)operatör overloadingten bahsedebilmemiz için operatörün operandı olan ifadelerden en az birinin bir sınıf türünden yada bir enumaration türünden olması gerekiyor

2)overload edilecek operatörün C++ dilinin operatör kümesinde olması gerekiyor
örneğin @ C++ dilinin operatör kümesinde yok

3)operatör overloading fonksiyonlarını istediğimiz gibi isimlendiremiyoruz hangi operatörü overload ediyorsak onu belirtmemiz gerekiyor operator+ ,operator[] gibi

4)dilin bütün operatörleri overload edilemiyor bazı operatörler için overloading mekanizması yasaklanmış
-  sizeof
-  :: scope resolution operatörü
-  . member access operatörü
-  .* pointer to member operatörü
-  ? : conditional operatörü
-  ->* pointer to member operatörü
- typeid

5)operatör fonksiyonlarının bazıları free function olarak tanımlanamıyor member function olmak zorundalar
-  () function call operatörü
-  [] subscript operatörü
-   -> member access operatörü
-  = assignment operatörü
- type cast operatörleri

6)tüm operatör fonksiyonları istisnasız isimleriylede çağırılabilir
```cpp
class Myclass{};

int main()
{
Myclass m1,m2;
m1.operator=(m2); // m1 = m2 
}

```


7)function call () operatörü hariç diğer operatör overloading mekanizmasında kullanılan fonksiyonlar default argument alamazlar

8)operatör overloading mekanizmasında ki operatörlerin (arity) değiştirilemez yani operatörün unary yada binary olması

#### Binary operators

- x * y // binary bir operatörü olduğu için buna uygun sentaksla overload edilecek bu overloading free functionla yapılıyorsa bu durumda

- çarpma oepratörünün sol operandı ve sağ operandıda o fonksiyonun parametrelerine argüman olarak gönderiliyor

- derleyici x * y ifadesini operator*(x,y) ifadesine dönüştürücek bu global fonksiyonun 2 tane parametre değişkeni olmalı bunun dışında başka bir parametre olursa sentaks hatası olur derleyici sol operandı 1.ci parametresini sağ operandı 2.ci parametresine geçiyor

```cpp
class Matrix{
public:

};

bool operator<(const Matrix& ,const Matrix&)

```

fakat binary operatörünü overload edicek fonksiyon member function ise o member function binary operatörünün sol operandı için çağırılıyor,

this pointerı sol operand olan nesnenin adresi x > y ifadesini derleyici x.operator>(y) ifadesine dönüştürüyor bu functionlar tek parametre olmak zorundalar bunun dışında
başka bir parametre olursa sentaks hatası olur
```cpp
class String{
public:
bool operator<(const String&) const;
}

```


#### Unary operators
!ptr// unary opeartör olduğu için buna uygun sentaksla yazılması gerek

unary operator olan ifade global function ise derleyici operatör ifadesini operator!(ptr) ifadesine yapılan bir çağrıya dönüştürücek operatörün operandı olan sınıf nesnesinide
bu fonksiyona yapılan çağrıda argüman olarak kullanıcak tek parametre almak zorundalar bunun dışında sentaks hatası olur
```cpp
class SmartPtr{};
bool operator!(const SmartPtr&)const;
```


unary operator bir member function ise parametresi olmaz zaten o nesne için çağırılır.
```cpp
class SmartPtr{
public:
bool operator!() const;
};
```



SORU:sentaks hatası mı değil mi?

```cpp
class Myclass
{
public:
Myclass operator+(); // sentaks hatası değil çünkü bu toplama operatörünü overload etmiyor sign operatörünü overload ediyor
Myclass operator+(Myclass) const; // toplama operatörünü overload ediyor
}

```


## Paterns

#### Singleton patern

Bir classtan sadece bir instance yapmanı sağlar . Başka bir örnke üretemezsin.

-  You can be sure that a class has only a single instance.
-  You gain a global access point to that instance.
-  The singleton object is initialized only when it’s requested for the first time.

![[Screenshot from 2026-06-11 14-59-15.png]]

Ornek kod.

```cpp
class MyClass {

public:

    // Tekerişim noktası
    static MyClass& instance() {
        static MyClass inst;
        return inst;
    }

    // Kopyalamayı engelle — başka nesne oluşturulmasın
    MyClass(const MyClass&)            = delete;
    MyClass& operator=(const MyClass&) = delete;

private:
    // dışarıdan oluşturulamaz.
    MyClass(){};

};


// Kullanım 

MyClass::instance().do_something();

```

#### Singleton patern

```


```

```
Singleton → Observer → Strategy → Factory
     ↓
Builder → Command → Decorator
     ↓
Proxy → State → Composite

```



## Namespaces

İsimalanı, global isimalanında oluşturabileceğimiz ve isimlerin birbirleriyle karışmasını engellemeye yönelik ve bu isimleri birarada tutan bir paket/container gibi bir yapı.

İsimalanında bildirilen isimler özel bir scope ait.Bu namespace scope.
İsimlerin birbirleriyle çakışmasını engellemeye yönelik bir mekanizma bu.

C de olsaydı, include edilen kütüphaneden gelen isimler global isimalanına enjekte edilecekti ve bunların çakışma riski var. Bir global alan var ve herkes oraya yazıyordu.

C++ ta ise bu isimleri doğrudan enjekte etmek yerine biz bu namespacelere boşaltıyoruz. isimler aynı olsa namespace ler farklı olsa bile
isimler çakışmıyor.

Pc lerdeki farklı dizinlerde varolan aynı isimli dosyalar gibi düşün.

c:\cdr\ali.txt
c:\cdr\folder\ali.txt   dosyalar aynı isimli ama çakışma yok.Aynı isimalanları/namespaces gibi.

Artık file scope diye birşey yok.
Global namespace var. tüm namespacelerde bunun içerisinde.
Nested namespacelerde olabilir. Erişim ise scope resolution :: operatörleri ile yapılıyor. 

Tüm standart kütüphaneden egelen isimler ismi std olan bir namespace içinde.
Genellikle namespace kullanmayacağız ama kullandığımız kütüphaneler namespace içinde olduğundan bilmemeiz gerekiyor.
Bazende bizim yazmamız gerekecek.

SENTAKS

```cpp
namespace Nec{

}

// Unnamed Namespace
namespace {

}

```

Sonda ; yok. Koyarsakta hata olmaz çünkü null statement olmuş olur.Ama standart sentaksta yok.

Namespace içinde func tanımı, değişken tanımı class tanımı... herşey mümkün.

Dikkat aşağıdaki a ismi aynı scopeta iki defa kullanılmış.Farklı namespacelerde hata olmazdı.

```cpp
namespace nec{
	int a = 10;
	double a = 20.2;   
}
```


```cpp
namespace nec{
	int a = 10;
}

namespace ali{
	double a = 20.2;   // LEGAL. GEÇERLİ ARTIK.
}
```

Farklı scopelar func overloading olmaz:

```cpp
namespace Ali{
	void func(int);
}

namespace Nec{
	void func(double); // Overloading yok.
}   
```

Aynı isimli isimalanları birleşir farklı yerde tanımlanmış olsalar bile. Çümkü derleyici bir namespaceden sonra tekrar aynı tanımı görürse bunları otomatik birleştirir. Yani namespacelerde kümülatif etki var

```cpp
namespace Nec{
	void func(int);
}

namespace Nec{
	void func(double); // Func OVerloading burası
	}
```

```cpp
namespace ali{
	int x = 10;
}

namespace ali{
	int x = 21;  SENTAKA HSTASI. Aynı namespacede aynı tanım 2 defa yapılmış.
}
```

İsim alanındaki ismi bulmak için scope resolution operatörü kullanılır.

```cpp
int g = 20;

namespace Nec{
	int g =10;
}

int main()
{
	int g = 30;

	g;        değeri 30 olan ilk bulunan g bu.
	nec::g;   Bu şekilde nec namespace e erişilir.
	::g;      Buda global namespacede arar.
}

```

NOT: NAMESPACE LERDE PUBLIV PRIVATE PROTECTED YOK.



```cpp
namespace Nec{
	namespace Ali{
			namespace Veli{
				int x = 10;
			}
	}

}

int main()
{
	Nec::Ali::Veli::x = 23;  // bu şekilde erişilir. Çok yaygın std library kullanıyor.
}

```

---

```cpp
//.h
namespace prog{
	class Nec{
		void func();
		void foo();
	};
}

#include "///.h"

```

1. ihtimal cpp filedan aşağıdaki gibi tanımlıyoruz.
```cpp
void prog::Nec::func()
{
	//
}
```

2. ihtimal ise cp file da da bunu prog namespace içinde tanımlayabiliriz.
Bildirim ile tanım aynı namespace içinde oluyor artık bu durumda.

```cpp
namespace prog{
	void Nec::func()
	{
	///
	}
}

```

---

Nested namespace ler çok kullanılıyor.

```cpp
namespace nec{
	namespace pro{
	}
}
```

C++17 de ekleme yapıldı dile. eskiden şöyleydi

```cpp
namespace A{
	namespace B{
		namespace C{

		}
	}
}
```

Yenisi

```cpp
namespace A::B::C{
	int x = 10;  // x burada a nın içindeki b nin içindeki c nin içinde :DD:D:
}

namespace A::B{
	int y;
}

namespace A{
	int z;
}

int main()
{
	A::z = 10;
	A::B::y = 20;
	A::B::C::x = 123;
}
```

---
Bir namespace içindeki isimlerin, bir namespace ismiyle nitelenmeden ilgili namespace te aranıp bulunmasını sağlayan 3 adet araç var.

1 - Using Decleration
2 - Using Namespace Decleration
3 - ADL(Argument Depended Lookup)

**1 - USING DECLERATION**

NOT :
- En uygunu hiç kullanmamak.
- Kullanılacaksa local (en dar) scopeta kullanmak
- En son ihtimnal namespace scopeta kullanmak.

NOT :
Başlık dosyası içinde asla using bildirimi veya using namespace bildirimi yapmayın.
Bunu include eden herkeste de bu bildirim olur.Bu durumda da namespace lerin varlık sebebi ortadan kalkar.

Bu çok yerde overload edilmiş bir keyword.Farklı amaçlarlada kullanılıyor.
Biz type alias olarak kullanıldığını gördük

```cpp
using word = int;
```


using in yapıp typedef in yapamadığı şeyler var. bunlar tempalte lerde ve generic programlamada önemli oluyor.

Bir de using in sınıf içinde kullanımı var.

```cpp
class{
	using base::x;
};
```

Sentaks :

```cpp
using namespace_name::object_name;

```

Bu artık namespace nin içindeki objenin direk ismi ile kullanılabilmesini sağlıyor.


```cpp
namespace Ali{
	int x;
}

using Ali::x; // artık x yazınca Ali::x e erişiriz.

int main()
{
	x = 5;
}

```

---

using bildiriminin bir kapsamı var. using bildiriminin kapsamı, namespace içinde kullanılırsa namespace scope, block içinde kullanılırsa block scopetur.

```cpp
namespace Ali{
	int x;
}

using Ali::x; // artık x yazınca Ali::x e erişiriz. 

void func()
{
	x = 35;
}

void foo()
{
	x = 22;
}


int main()
{
	x = 5;
}
```

hepsinde x e erişilir.Derleyici isim aramayla using bildirimini görecek.Bunun ali namespace i içinde olan x olduğunu anlayacak.

```cpp
namespace Ali{
	int x;
}


void func()
{
	using Ali::x;
	x = 35; BU SCOPETA x BULUNUR. LEGAL KOD.
}

void foo()
{
	x = 22; SENTAKS HATASI
}


int main()
{
	x = 5; SENTAKS HATASI
}
```

Using bildirimini block veya namespace scopeta yapılabilir. blockta yapılırsa ilgili blockta o isme ulaşılır global yapılırsa heryerden ulaşılabilir.

---

Using bildirimninin 2. önemli özelliği, bildirilen isim, bildirimin yapıldığı isim alanına inject ediyor.
Enjekte etmesi nedemek?

```cpp
namespace Ali{
	int x;
}

void func()
{
	using Ali::x;
	int x = 25;	// burası doğrudan SENTAKS HATASI.Zaten x değişkeni var. using sanki bu scopeta x i bildirmiş gibi davranıyor
}
```

Aşağıdaki gibi olsaydı sorun yoktu.

```cpp
namespace Ali{
	int x;
}

using Ali::x;
void func()
{
	int x = 25;	// Burası geçerli.
	x = 44;	//ismi bulacak ve arama yerel değişken olan x e yapıldı.içerideki x dışarıdakini maskeledi.
	
	Ali::x = 55; yine kullanılabilir.
}
```

Başka bir örnek. 

``` cpp
namespace Ali {
	int x;
}

int x = 25;	
using Ali::x; // Bu bildirim artık hata oldu.

void func()
{

}
```

---

```cpp
namespace Ali {
	int x;
	int y;
}

Eskiden
using Ali::x;
using Ali::y

YENİ - C++17
using Ali::x,Ali::y;

int main()
{
	x = 23;
	y = 98;
}
```

---

**2 - USING NAMESPACE BİLDİRİMİ**
Aşağıdaki isimlerin herbirini nitelemeden kullanmak istiyoruz

```cpp
namespace Ali{
	int x;
	int y;
	int z;
	////
}
```

2 yol var.
1 - tek tek using bildirimi.
2 - using namespace i kullanmak.

```cpp
namespace Ali{
	int x;
	int y;
	double z;
}

using namespace Ali; // Bunu yazınca artık, nerede bu bildirim yapıldıysa, o scopeta x,y ve z direkt olarak görünür durumda.

void func()
{
	x = 5;
}

void foo()
{
	x = 56;
}

int main()
{
	x = 234;
}
```

Sanki Ali namespace i yorum satırı yapıldı ve içindekiler dışarı çıkartımış gibi.

---

```cpp
namespace Ali{
	int x;
	int y;
	double z;
}


void func()
{
	using namespace Ali; // func scope ta artık ali namespace içindeki isimlere ulaşırım.
	x = 5;
}

void foo()
{
	x = 56; //SENTAKS HATASI. Bu scope ta değil. bunu kapsayan scope tada değil.o yüzden sentaks hatası
}

int main()
{
	x = 234; //SENTAKS HATASI. Yukarıdaki ile aynı.
}
```

DİKKAT!!!!!!!!!!!!!!!!!
BURADA  USİNG BİLDİRİMİ İLE FARKLI DAVRANIYOR inject olmuyor yani. !!!!!!!!!!!
DİKKAT ET !!!!!!!!!

```cpp
namespace Ali{
	int x;
	int y;
	double z;
}


void func()
{
	using namespace Ali; 
	int x = 10;	// HATA YOK.Buradaki x diğerini maskeliyor.  using Ali::x; olsaydı 186. satırdaki gibi. SENTAKS HATASI.
	x = 5; // buda yerel x

	Ali::x; burada da Alideki x e erişiyoruz.
}
```

!!USING BILDIRIMLERI BOL KESEDEN KULLANILMAMALI çünkü.

```cpp
#include module_a
#include module_b

a dan gelen 
namespace a{
	int ax;
	int x;
}

b den gelen
namespace b
{
	int bx;
	int x;
}

using namespace A;
using namespace B;

int main()
{
	ax++;
	bx--; //ikiside nitelemeden kullanılabilir.
	
	x; //Burada ambigiuty hatası olur. İkisinde de x var.

	A::x;
	B::x; // ile bunlar aşılabilir.
}
```


```cpp
class Myclass
{
	void func()
	{
		using namespace std;   // belki böyle kullanılır ama önermiyor hoca.
	}
}
```

NOT : CLASS DEFIBITION İÇİNDE USING NAMESPACE STD; BİLDİRİMİ YAPILAMAZ.YA LOCAL DÜZEYDE YA DA NAMESPACE İÇİNDE YAPILIYOR.

---

**3 - ADL(ARGUMENT DEPENDENT LOOKUP)**

KURAL: EĞER BİR FONKSİYON ÇAĞRISINDA FONKSİYONA ARGÜMAN OLARAK GÖNDERİLEN İFADE, BİR NAMESPACE İÇİNDE TANIMLANANTÜRLERDEN BİRİNE İLİŞKİN İSE, O ZAMAN BU İSİM NORMAL ARANDIĞI YERİN DIŞINDA BU İSMİN AİT OLDUĞU TÜRÜNAİT OLDUĞU NAMESPACE İÇİNDE DE ARANIR.BU DURUMDA İSİM NEREDE DE ARANACAK? BU İSMİN AİT OLDUĞU SINIFIN TANIMLANDIĞI NAMESPACE İÇİNDE.

Amlamaman normal alt iki örnege bak.


```cpp
namespace nec{
	class Myclass{
		///
	};

	void foo();
	void func(int);
}

int main()
{
	foo(); // ismi arar bulamaz hata verir.
	nec::foo(); // ismi arar ve bulur hata yok.

	func(12); //sentaks hatası.Bulamadı yine
}
```


```cpp
namespace Nec{
	class Myclass{
		///
	};

	void foo(Myclass m);
	void func(int);
}

int main()
{
	Nec::Myclass m;
	
	foo(m); // SENTAKS HATASI DEĞİL. :D:D	Nec::foo() diye çağrılmadığı halde sentaks hatası değil.

	func(4); //SENTAKS HATASI.
}
```

func(a,b,c);
diyelimki a, a namespace içinde, b b namespacei içinde, c  c namespace i içinde tanımlanan türlerden olsun. bu durumda func ismi 3 namespace içinde de aranır.

---

```cpp
#include <vector>

namespace Nec{
	class Myclass{
		///
	};

	void foo(Myclass m);
	void func(std::vector<Myclass>);
}

int main()
{
	// Func ın parametresi Myclass türünden mi ? hayır Vector türünden
	std::vector<Nec::Myclass> myvec;
	//foo yu myvec ile çağırırsam ADL ile foo ismi bulunur mu bulunmaz mı?
}

```

NEDEN BULUNDU?
Tanıma dikkat!
Bir fonksiyona gönderilen argüman bir namespace içinde tanımlanan türdense demedik.
bir namespace içinde tanımlanan türe ilişkin ise dedik. Bu sebeple bulundu

```cpp
namespace Nec{
	class Myclass{
		///
	};

	enum color {Red,Green,White};
	void func(color);
}

int main()
{
	func(nec::color::black); //SENTAKS HATASI YOK.GEÇERLi.
}
```

Bir öncekinde de bunda da namespace içinde var olan bir tür kullanıldı parametrede.Adı geçti.
Dolayısı ile türe ilişkin oldu. Bu sebeple o türü argüman verince bulunduğu namespace de de arıyor yani ADL oluyor.

---

```cpp
namespace Nec{
	class Myclass{
		///
	};

	typedef int Word;
	void foo(Word);
}

int main()
{
	nec::Word myword{};
	foo(myword);		// SENTAKS HATASI
}

```

ADL typedef isimleri için geçerli değil.Burada yeni bir tür tanımlamıyoruz çünkü. buradaki int türü..

---

```cpp
namespace Nec{
	class Myclass{
		///
	};

	typedef Myclass Ctype;
	void foo(Myclass);
}

int main()
{
	nec::Ctype mx;
	foo(mx);		// ŞİMDİ GEÇERLİ.
}
```

typedef ismi eğer sınıf içinde belirlenen türe ilişkin ise ADL DEVREYE GİRER.
Eğer int veya double gibi bir türe ilişkin ise ADL devreye girmez bir öncekinde olduğu gibi.
typedef tanımlanan bir türe ilişkin olmalı.

---

```cpp
include iostream
include vector
include string
include algorithm

int main()
{
	std::vector<std::string> svec;
	// code
	auto iter = find(next(svec.begin()),prev(svec.end()),"ali"); 
	auto iter = std::find(std::next(svec.begin()),std::prev(svec.end()),"ali"); //Normalde böyle olmalıydı ama nasıl oldu da 
// yukarıdaki çalıştı.

}
```

Nedeni?
next i svec.begin() ile çağırdık, bu func ın return dğeeri türü vector "string:iterator tür olduğuna görebu türde std namespace i içinde tanımlanan bir türe ikişkin olduğu için std namespace i içinde de arayacak.aynısı prev içinde geçerli.

Peki next(svec.begin()) in geri dönüş değeri türü ne ?
bununda return değeri bir iterator türü. o zaman finda da gönderidğim argümanda std namespace i için tanımlanan bir  türe ilişkin olduğu için find isminide std namespace i içinde arar.

---

```cpp
namespace A
{
	class Myclass{	}
	void func(Myclass);
}

void func(A::Myclass);

int main()
{
	A::Myclass ax;
	func(ax);		//BURADA AMBIGIUTY VAR. FUNC İSMİ HEM GLOBALDA HEMDE NAMESPACE A İÇİNDE BULUNDU.
// ÖNCELİK YOK BURADA. İKİ TANE FUNC BULDU.
}
```

ADL NEDEN VAR?

operator overloading için var. cout<< "asd"; burada bile ADL VAR.

std::cout << "merhaba" << endl; // endl ismi adl ile bulunur mu bulunmaz mı? BULUNMAZ
endl bir func ismi ve bu bir func a argüman olarak gönderiliyor. 
operator<<(std::cout, "Merhaba Dunya").operator<<(std::endl)

endl(std::cout); // endl ismi bulunur. endl std namespace içinde tanımlanan function. ona gönderdiğimiz argüman std namespace içindeki bir türe ilişkin olduğundan, endl ismi std namespace içinde de arancak.

ENDL NEDEN SIK KULLANILMAMALI
endl std namespace i içinde bulunan bir fonksiyon. endl bir maniplator.
std::cout << "Merhab Dunya" << endl; // std::endl denmeyince hata olur neden?

operator<<(std::cout, "merhaba dunya").operator<<(std::endl); // açılmış hali bu.
endl yi fonksiyona gönderiyoruz bu yüzden std::endl olarak yazmamız gerekiyor.

fonksiyonu endl ye argüman olarak gönderelim
endl(std::cout); endl ismi bulunru mu bulunmaz mı? BULUNUR çünkü endl std namespace i içinde bildirilen bir function
Ona gönderdiğim argüman std namespace i içindeki türe ilişkin olduğu için endl ismi std namespaceinde de arancak.
ADL yani.
endl orijinalinde function template
``` cpp
std::ostream& Endl(std::ostream& os)
{
	os.put('\n');
	os.flush(); C deki gibi flush işlemi yapıyor.

	return os;
}
```

yukarısı <<"\n"; bununla aynı işlemi yapmıyor. endl her kullanıldığında buffer flush ediliyor.
hatta << '\n'; eb iyi yolu bu. "\n" bu bir string literali ve static ömürlü bir dizi. endl de verim kaybıda var.

Eğer cout << endl; dersek veya cout.operator<<(endl); //Derleyicinin burada inline expansion yapma şansıda yok. Ciddi verim kaybı.endl kullanma !! :D:D:D:D endl(cout); demiş oluyoruz.

---

```cpp
//.h
namespace A
{
	class Myclass
	{
	public:
		void func();
		//member func

	};

	void foo(Myclass);
}

//.cpp
int main()
{
	A::Myclass ax;
	ax.func(); // geçerli
	foo(ax);  //geçerli.
}
```

---


INLINE NAMESPACE C++17 DE GELDİ.

```cpp
namespace A
{
	namespace B
	{
		namespace C
		{
			int x;
		}
		using namespace C;
	}
	using namespace B;
}
using namespace A;

int main()
{
	x = 25; artık bu durumda direkt görür.
	
	// using namespace A; olmasaydı A::x = 40; olurdu
	// using namespace A ve B; olmasaydı A::B::x = 40; olurdu
	// using namespace A ve B ve C; olmasaydı A::B::C::x = 40; olurdu
}
```

---

```cpp
namespace A{
	namespace B
	{
		class Myclass {
		};
	}
	void func(B::Myclass);
}

int main()
{
	A::B::Myclass x;
	func(x); // SENTAKS HATASI.Çünkü x b namespace i içinde ama b functionu A namespace içinde tanımlanmış.Burası garip.
	
	//B den sonra using namespace B; yapsak bile yine hata devam ediyor.
}	

```

---

inline namespace C bildirimde adeta sanki biz bu namespace çıkışında using namespace c yazmışım gibi c namespace içindeki isimler doğrudan B namespace içinde visible hale geldiler.
B yide inline yazarsak öncekindeki gibi olur. b namespace içindekiler A içinde doğrudan görülür.
A da yapılabilir....

```cpp
namespace A
{
	int a;
	namespace B
	{
		inline namespace C
		{
			int x;
		}
	}
}

int main()
{
	A::B::x = 23; //geçerli
	A::x = 33; // geçersiz
}

```

inline ile çözüm:

```cpp
namespace A{
	int a,b;
	inline namespace B
	{
		int x,y;
		class Myclass {
		};
	}

	void func(B::Myclass);
}

int main()
{
	A::Myclass m;
	func(m); // inline yazmayınca ilk örneklerde bu hata idi.

}
```

Ornek inline namespaceler:

literals namespace ve string_literals namespace inline namespace

```cpp
#include <string>
#include <chrono>

int main()
{
	std::literals::string_literals::s; s bir nesne, diğerleri nested namespace
	std::literals::s; bunlarda nested namespace. hatta inline namespace kanıtı da s in kullanılabilmesi.
	std::s; burada bile görülüyor :D:D
	std::chrono::milliseconds
}


```

```cpp
namespace A
{
	inline namespace B{
	void func();
	}
	inline namespace C{
	void foo();
	}

}

int main()
{
	A::func();
	A::foo(); ikiside geçerli.
}
```

---

INLINE NAMESPACELERİN BİR AVANTAJIDA VERSION KONTROLUNDE KULLANILMASI

Biz belirli kodlarda  belirli kodsal varlıkları versiondan versiona değiştirmek istiyoruz.
Gerekirse bir versiondakini gerekirse diğer versiondakini kodları değiştirmeden kullanmak istiyruz.
Bunu sağlıyor.

```cpp


namespace project{
	
	namespace Version1
	{
		class Myclass{
		
		};
	}

	namespace Version2
	{
		class Myclass{
		
		};
	}

}

int main()
{
	Project::Version1::Myclass
	Project::Version2::Myclass
	// bu şekildede ikisinede erişilir.

}


```

Şimdi kullanmak istediğimiz versionun namespaceini inline olarak tanımlarsak
kapsayan namespacetede visible hale gelir artık bu.

```cpp




namespace project{

	inline namespace Version1
	{
		class Myclass{

		};
	}

	namespace Version2
	{
		class Myclass{

		};
	}

}

int main
{
	project::Myclass m; // inline tanımlandığı için namespace version1, içindeki tüm isimler onu kapsayan namespacede visibledır.
}						// tam terside yapılabilirdi. version2 inline olursa bu seferde version2 deki myclass ı kullanabiliriz.
						// ikiside aynı anda inline olsaydı, ambigiuty olurdu.
```

---


Conditional compiling ilede birleştirilip kullanılabilir.

```cpp
#define Version_1 // dersem 1. ifdef koşulu doğru version1 inline olacaktı.
#define Version_2 // dersem 2. ifdef koşulu doğru version2 inline olacaktı.


#define Version_1   // ben version1 i inline ederek onun myclass sınıfını kullandım

namespace project{
	

	#ifdef VERSION_1
		inline
	#endif
	namespace Version1
	{
		class Myclass{

		};
	}

	#ifdef VERSION_2
		inline
	#endif
	namespace Version2
	{
		class Myclass{

		};
	}

}

int main()
{
	Project::Myclass m;
}
```

---

**UNNAMED NAMESPACE**
Sadece ilgili kaynak dosyada geçerli olan ve bir using bildirimi olmadan doğrudan sanki inline keyword ile tanımlanmış gibi,
bu namespacedeki isimleri bunu kapsayan namespacede yani global namespacede kullanabileceğimiz bir özellik.

``` cpp
namespace{
	int x;
	double dval;
}

int main()
{
	x = 6; // derleyince hata vermedi.
}
```

Kural : ilgili kaynak dosyada global namespacede visible hale geliyor. Modern c++ öncesinde de kullanılan bir araç.
Ne işe yarıyor?
Bu namespace in ismi var sayalım. hemen çıkışında using namespace ismi; olduğunu varsayalım.
Ör:

```cpp


namespace name1
{
	int x;
	double dval;
}
using namespace std;

int main()
{
	x = 5;
}ait 

```


Bunları yapıyor aslında unnamed namespace
Neden kullanalım?
- UNNAMED NAMESPACE LER INTERNAL LINKAGE A AIT.
	- EXTERNAL LINKAGE = FARKLI KAYNAK DOSYALARDA BİR İSİM AYNI VARLIĞA İŞARET EDİYORSA BUNA EXTERNAL LİNKAGE DENİR.
	- INTERNAL LİNKAGE = O İSİM SADECE O KAYNALK DOSYADA KULLANILDIĞINDA AYNI VARLIĞI GÖSTERİYOR.AYNI İSİM BAŞKA KAYNAK DOSYADAmBAŞKA BİR VARLIK OLABİLİR.


External linkage = tek obje, farklı TUlardan aynı sembol.
Internal linkage = aynı isim farklı TUlarda farklı objeler.

C++’ta inline = header’a tanım koyabilmenin yolu (tek obje olacak şekilde).
Header’da static int val = 2324; → her TU kendi kopyasını üretir → bu yüzden “farklı değişkenler” olur.

Modern c++ öncesinde eklenildi.
static in kullanılıp internal linkage a ait demek deprecated oldu
Bunun yerine isimsiz namespace kullanıytoruz.


```cpp
namespace
{
	//artık namespacedeki tüm isimler iç bağlantı internal linkage a ait.
}
```

değişken function tür isimleri konulabiliyor.

---

Not: const nesnelerde bağlantı kuralı C den farklı
const int x = 10; bu global scopeta ise,C++ ta x internal linkage a ait.

```cpp
nutility.h
const int x = 10;
void fx();


nutility.cpp
#include "nutility.h"
#include <iostream>

void fx()
{
	std::cout << "&x = " << &x<<"\n"; //const nesnelerin adresi alındığında derleyici onlara yer ayırmak zorunda.
}					  // adresini almazsak, kod içinde sabit gibi kullanırsak compiler yer ayırmak zorunda değil.

main.cpp
#include "nutility.h"
#include <iostream>

int main()
{
	fx(); // buradaki x adres ile
	std::cout << "&x = " << x << "\n"; //buradaki x in adresi farklı çünkü bunlar ayrı nesneler.const ile tanımlanınca internal linkage
}
```


---

ÇOKOMELLİ


C ile C++ ın internal linkage olayı farklı.
C de kod file da static yapıyorduk. C++ ta header fileda bildirebiliyoruz .ama farklı nesneler oluyor bu değişkenler.
TEST : 
header fileda const veya static ile tanımlayıp tüm file lardan include edince adresler farklı.
Her bir code file için farklı bir nesne.

inline yapınca ise aynı nesne. inline a alternatif C style olarak yazmak. headerda extern bildirimi
onu headerı include eden code file da ise tanım.

---

**BIRDE BU DEĞIŞKENI INLINE OLARAK TANIMLAYALIM**

inline const int x = 10;
```cpp
nutility.h
inline const int x = 10;

nutility.cpp
#include "nutility.h"

main.cpp
#include "nutility.h"


nutility.h
void fx();

nutility.cpp
#include "nutility.h"
#include <iostream>

void fx()
{
	std::cout << "&x = " << &x<<"\n"; //const nesnelerin adresi alındığında derleyici onlara yer ayırmak zorunda.
}										// adresini almazsak, kod içinde sabit gibi kullanırsak compiler yer ayırmak zorunda değil.

main.cpp
include ları yap

int main()
{
	fx(); // buradaki x adres ile
	std::cout << "&x = " << x << "\n"; //değişken inline olunca bu değişkenden bir tane olması garantiydi.Bu sefer aynı adresi verdi
}

```

```cpp

nutility.h
int foo();
void fx();
const int x = foo();

nutility.cpp
void fx()
{
	std::cout <<"&x = " << &x << "\n";
} 

int foo()
{	
	std::cout << "foo()\n";
	return 1;
}

main.cpp
include nutility.h ve iostream
main()
{
	// bunu boş olarak çalıştırınca birkaç tane "foo()" yazısı göreceğiz.
	//çünkü internal linkage ve her include eden kendi x ini init ediyor.
	//inline olsaydı 1 adet foo() görecektim
}


```

Özetle = const değişkenler global olması durumunda internal linkage a ait.bir const değişekenin tanımını header file koyunca
ODR ihlali olmuyor ve bunu include eden her kod dosyasında ayrı bir değişken meydana geliyor.

---

hem main.cpp de hemde neco.cpp de aşağıdaki tanım var.

```cpp
namespace
{
	int x = 23;
}
```


Buradaki değişkenler bu durumda farklı oluyor. Internal linkage a konulmak istenen nesneleri isimsiz bir isim alanına koy !!!

---

Modern C++ öncesinden gelen bir araç
Biz biir header file ile dışarıya sunacağımız isimleri bir namespace içinde versek
Aşağıdaki isimlerin artık çakışması riskini kesin olarak ortadan kaldırmış olur muyuz

```cpp
namespace neco{
	//
}

```

%99 çözüyor.%1 çözemiyor :D:D

neco burada namespacein kendi ismi, bu isimde tek olmak zorunda. Kod dosyasında neco başka isimlerle çakışabilir.
Buna karşı önlem almakta mümkün. Bir eş isim alias bildirilebiliyoruz.

Türlere de eş isim bildirimi legal.Buradaki sentaksa namespace alias deniyor.

```cpp
namespace neco_project
{
	int x,y;
}
```

namespace nec = neco_project;
tabi bu bildirimin olması için nec visible olmalı.

```cpp
int main()
{
	neco_project::x = 10;
	nec::x = 20;  //aynı anlamdalar.
}
```

---

nested namesapceler içinde type allias verilebiliyor.

```cpp
int main()
{
	namespace rgc = std::regex_constants;

	std::regex_constants::egrep;
	rgc::egrep;
}
```

```cpp
namespace ali::veli::hasan::huseyin
{
	int x = 10;
}
```

```cpp
int main()
{
	ali::vel::hasan::huseyin::x;
	namespace nec = ali::vel::hasan::huseyin;
	nec::x;

}
```




## Nested Types / Types members

Sınıfların memberları 3 temel kategoriye ayrılır.
- Data Members
- Member Functions
- Type Members - Nested Type - Member Type

Bildirimi sınıfın içinde yapılan türlere o sınıfın memberı olan tür deniyor.
C++ ta std kütüphane olmak üzere çok sık kullanılıyor.

Sınıfın içinde bildirimi yapılan türler:

a - Başka bir sınıf olabilir.
b - Enum type olabilir. enum Color {red,blue};
c - Bir tür eş ismi olabilir. typedef veya using olabilir.
	typedef int word;
	using word = int;

NOT: Using bildirimlerinin dile eklenmesinini gerçek nedeni, bu şekilde yapılan bildirimerin	template hale getirilebilmesidir. Böyle template lere	Alias template deniyor.

---

İkinci classı namespace yerine class içinde bildirince fark oluyor mu? Evet.

```cpp
class Myclass{
	public:
	class Nested{
		
	};
};
```

Burada artık myclass türünü nitelememiz lazım.

```cpp
int main()
{
	Nested nx; // Burası sentaks hatası.
	Myclass::Nested nx;	// Burası Geçerli.
}
```

Access control Burada sözkonusu tabiki.

```cpp
class Myclass{
		
	class Nested{
		
	};
};

```

Myclass::Nested x: SENTAKS HATASI.Private eleman çünkü.Access controle takıldık.

---
**Bazı Karmaşık İsim arama  Kurallar**

Class definition için de isim ararsan kullandığın ismi kod alanın başından 
bildirime kadar olan kısma bakıyor.Bulamazsa namespace scopetan classa kadar bakıyor.

```cpp
class Myclass{
	word wx;		// hata.isim arama hatası.
	typedef int word;

};
```

```cpp
class Myclass{
	typedef int word;
	word wx;  //ARTIK HATA DEĞİL.
	
};

```

```cpp
struct Word{
};

class Myclass{
	
	Word wx;   // burası wordu yukarı doğru arar. struct olan Word türünden wx oldu. int değil.
	typedef int word; // burası yukarıda olsaydı eğer, word wx bildiriminde, word int olacaktı.

};
```


```cpp
struct Word{
};

class Myclass{

	typedef int word;
	::Word wx; // burada namespace scopetaki struct olan Word tür.

};
```

İnline olarak tanımlanan functionlar buna kurala dahil değil.

```cpp
class Myclass{
	void func()
	{
		Word w; //Burası geçerli. İnline funclar kurala dahil değil demiştik.
	}

	typedef int Word;
};
```


```cpp
typedef long Word;

class Myclass{
	
	Word wx;	// buradaki Word, long 
	
	void func()
	{
		Word w; //Ama buradaki w ise int türden.
	}

	typedef int Word;
};
```

---

Bir sınıfın bir başka sınıf türü elemanı olması, bu türden bir veri elemanına
sahip olduğu anlamına gelmiyor.

Yani A nın herhangibir data memberı yok.

```cpp
class A{
	class Nested{
	
	};
};
```

Ama A nın nested türden bir memberıda olabilirdi.

```cpp
class A{
	class Nested{

	};

	Nested nx; //burası artık veri elemanı.
};
```

---
NESTED TYPE A SAHIP SINIF, BU TYPE IN PRIVATE BÖLÜMÜNE ERIŞEMEZ
Enclosing class = Nestedin tanımına sahip olan sınıfa enclosing class deniyor.

```cpp
class A{
	class Nested{
	private:
		void func();
	};

	void foo()
	{
		Nested nx;
		nx.func(); // BURASI SENTAKS HATASI.NESTED OLSA BİLE PRIVATE BÖLÜMÜ KORUMA ALTINDA
	}
};
```

İÇERIDEKI CLASS TAN ENCLOSING CLASS IN PRIVATE KISMINA ERIŞMEYE ÇALIŞACAĞIZ. 
BURADA ACCESS CONTROL UYGULANMIYOR.

```cpp
class A{

	void foo();
	static void sf();
	static int sx();

	class Nested{
	private:
		void func()
		{
			A ax;
			
			ax.foo();
			sf();	
			sx = 5;
		}
	};

};
```

Enclosing type ın private memberlarına erişebliyorum ve burada acess
Control uygulanmıyor.Modern C++ öncesinde bu kodlar sentaks hatasıydı.

```cpp
class A{

	class Nested{
	private:
		void func()
		{
			A ax;

			ax.foo(); // Memberlar aşağı alındı ve isim arama halen daha geçerli.
			sf();
			sx = 5;
		}
	};

	void foo();
	static void sf();
	static int sx();
};
```

```cpp
class A{
	
	int mx;

	class Nested{
	private:
		void func()
		{
			auto n = sizeof(mx); // GEÇERLİ.sizeof unevaluated contex olduğu için geçerli.
		}							// mx normalde static olması lazımdı.sınıf nesnesine ihtiyaç vardı
	};
};
```

ÖZETLE:
NESTED CLASS, ENCLOSİNG CLASS IN PRİVATE BÖLÜMÜNE ERİŞEBİLİR.ORADAKİ İSİMLERİ KULLNABİLİR. DİLİN DİĞER SENTAKS KURALLARINI EZMEDİĞİ SÜRECE.

```cpp
class A{
	class Nested{
		
	};

public:
	static Nested foo();
};

int main()
{
	auto x = A::foo(); // GEÇERLİ.Nested private ama kullanmıyoruz. Sadece function return type 
						// olarak auto tarafından algılanıyor.İsmi kullanmadık.Kullansaydık bir access control uygulanacaktı.

	A::Nested y = A::foo(); // burası sentaks hatası mesela.
}
```

---

**NESTED CLASSLARDA FONKSİYON TANIMLARI**

İnline yapılabilir.

```cpp
class A{
	class Nested{
		void foo()
		{
		
		}
	};

public:
};
```

Bir cpp file de yapılabilir.

```cpp
class A{
	class Nested{
		void foo();		
	};

public:
};


//.cpp
void A::Nested::foo()
{
	Nested nx; // sınıfın içinde direkt nested türünü kullanabilirim.
}
```


```cpp
class A{
	class Nested{
		void foo(Nested); //parametreye nested geldi
	};

public:
};

//.cpp
void A::Nested::foo(Nested x)
{
	
}
```


```cpp
class A{
	class Nested{
		Nested foo(Nested); //Return value değeride geldi şimdi
	};

public:
};

A::Nested A::Nested::foo(Nested)
{
	Nested nx; // sınıfın içinde direkt nested türünü kullanabilirim.
}

//.cpp
Nested A::Nested::foo(Nested x) // Bu durumda burası SENTAKS HATASI.Çünkü buradaki return olan Nested func içinde kullanılmadığı için
{								// standart isim arama kurallarına göre kullanılacak.

}

A::Nested A::Nested::foo(Nested x) // BURASI GEÇERLİ.
{

}

A::Nested A::Nested::foo(A::Nested x) // BURASI DA GEÇERLİ.PARAMETREDE DE :: KULLANILABİLİR.ZORUNLU DEĞİL. RETURN VALUE DA GEÇERLİ.
{

}

```

Copy ctor için yazalım.

```cpp
class A{
	class Nested{
		Nested& operator=(const Nested& other)
		{
		
		}
	};

public:
};

A::Nested& A::Nested::operator=(const Nested& other)
{
//..
}
```

---
ENUM type.

```cpp
class A{
public:
	enum{size = 100};
};

int main()
{
	int x = A::size;// GEÇERLİ
}
```

INCPOPLETE type.

```cpp
class Myclass{
	class Nested;  // sınıfın dışında bildirmekle sınıfın içinde kullanmak aynı anlama gelmiyor.Erişimde faklılık oluyor.
	Nested *mp;
};
```

---
PIMP IDIOM

Handle body idiom veya cheshire cat idiyom opaq pointer idiom diye söyleyenler var

Adı pointer implementationdan geliyor.
Bir geleneksel birde smart pointer idiyomu var.
Sınıfın Private bölümünü gizliyor. Neden gizlemek isteyelim?

```cpp
#include "Mint.h"
#include "Date.h"
#include "Counter.h"

class nec
{
private:
	Mint mx;	// Eğer bu şekilde nesne oluşturacaksak bu sınıfı incomplete type olarak tanımlayamayız.
	Date dx;	// complete type olmalı. Pointer olsalardı, incomplete decleration ile çalışır.
	Counter cx; // static olsalardı, bu bir bildirim olacağından incomplete type olabilirdi.
};

```


```cpp
STATIC OLSUN

class Mint;
class Date;
class Counter;

class nec
{
private:
	static Mint mx;	    //	Mint &mx; 
	static Date dx;		//	Date &dx;
	static Counter cx; 	//	Counter &cx; bunlarda olabilirdi incomplete type ile.
};
```

Yani static değilse pointer veya referans değilse, tanımları tam olarak/Complete type olarak görmeli. Yoksa çok maliyet artırır

Pimple a geri dönelim. Hoca pimple ı her sınıf için önermiyor.

```cpp
//.h
class Nec{
	Nec();
	~Nec();
	void func();
	void foo();
private:
	struct Pimpl;
	Pimpl *mp;
};

//.cpp
#include "neco.h"
#include "mint.h"
#include "date.h"
#include "counter.h"	

struct Nec::Pimple{
	Mint mx;
	Date dx;
	Counter cx;
};

void Nec::Nec() : mp {new Pimpl}
{
	//..
}

void Nec::~Nec() : mp {new Pimpl}
{
	//..
}


void Nec::func()
{
	//... artık neler yapıacaksa
	mp->dx; //uyduruorum buralarda
	++mp->mx;
		
}
```

Dinamik ömürlü nesne yaratıldı. fiziksel olarakta struct nec içerisindeki veri elemanları ayrı yerde.
sizeof a girmiyor. destructor falanda buna göre tanımlanmalı. pimpl deletede edilmeli

SONUÇ : NESTED TYPE İLE İLİŞKİSİNİ GÖRMEK.  BUNUN DAHA MODERN HALİNİ GÖRECEĞİZ. ESKİ OLANDI BU. GÜNÜMÜZDE TERCİH EDİLEN SMART POINTER OLACAK.



## Composition

Nesne yönelimli programlamada, problem domainindeki varlıkları temsil eden sınıflar ile temsil etmeye deniyor. 
Prosedürel programlama paradigmasında(C) ayrıştırma functionlara yönelik, ama nesne yönelimlide arıştırma classlara/sınıflara yönelik

Bazı terimler var. Bunlar sınıflar arasındaki ilişkileri betimliyor.

UML Konusunu öğrenmekte fayda var.Modelleme.
Nesne yönelimli modellemeye bak. Modelleme dili ? UML?
Bunlar diagramatic diller, programlama dilleri değil.
Diagramlar var, sınıf diagramları, akış diagramları.
Aşağıdaki ilişki türleride UML de karşımıza çıkacak.

Dependancy

Association : Sistemdeki 2 sınıf birbiriyle işbirliği halinde kullanılıyorsa bu sınıflar arasında association vardır.
	Aggregation : Eğer bu ilişki içindeki sınıflardan biri, diğerinin sahibi olarak onu kulanıyorsa, buna aggregation deniyor. Her aggregation bir associatioBir futbolcu bugün fenerde yarın Gs de. gibi.
	Composition : Yine bir nesne diğerinini sahibi fakat sahip olan ile olunan nesne arasında ömürsel birliktelik var.Sahip hayata gelince, olunan da gelir.
				  Sahip ölürse, sahip olunanda ölüyor. Araba perte çıktı motoru da kullanılamaz kendide ise arada composition var.
				  ama eğer motorunu başka yerde kullanabileceksek aggregation var. Başka bir sınıfı veri elemanı olarak almak denebilir.


Containment : bir nesne diğerini eleman olarak alması durumuna deniyor.

Composition bir interface edinme ilişkisi değil. Bir sınıf başka sınıf türden bir ver ielemanına  sahip olunca o veri elemanının interface ini kendi interface ine katmıyor.

```cpp
class A{
private:
	void func();
	void foo();
	void f();
};

class B{
private:
	A ma;
};

int main()
{
	B bx;

	bx.func(); //BURASI HATA.İNTERFACE DEVRALINMAZ. KALITIMDA INTERFACE DEVRALINIR.
}	
```

En fazla B ye func yazıp. bu func ın diğer class nesnesi ile func çağırması olabilir. Aşağıdaki gibi.

```cpp

class B{
private:
	A ma;
public:
	void func()
	{
		ma.func
	}
};
```

B sınıfı A sınıfı türden bir elemana sahipse, B nin üye functionları içinde elemanı olan A nın private bölümüne erişebilir miyiz?


```cpp
class A{
private:
	void func();
	void foo();
	void f();
};

class B{
private:
	A ma;
public:
	void g()
	{
		ma.func(); //Burası hata. Private bölümüne erişim hakkı verilmedi
		ma.ival; // aynı şekilde hata.
	}
};
```

ELEMANIN PRİVATE BÖLÜMÜ KAPATILMIŞ DURUMDA.FRİENDLİK VEREBİLİR.

```cpp
class A{
	void func();
	void foo();
	void f();
	friend class B;	
};

class B{
private:
	A ma;
public:
	void g()
	{
		ma.func(); // HATA YOK
		ma.ival; // Legal. hata yok.
	}
};
```

---

Aşağıda owner sınıfının yazdığı default constructor elemanlar default init ettiğine göre, member türünden mx in default init edilmesi, default ctorunun çağrılması demek. Derleyicinin yazdığı destructor ise sınıf türden hayata gelenlerin nesnelerin hayata sırayla veda etmesi demek.
Mesela aşağıda
member ctor
destructor   yazdı 

```cpp
class Member{
public:
	Member()
	{
		std::cout << "Member default ctor\n";
	}
	~Member()
	{
		std::cout << "Member Destructor\n";
	}
};

class Owner
{

private:
	Member mx;
}


int main()
{
	Owner ox;
}

```

Sınıfın birden fazla elemanı olsaydı

```cpp
class Ownber{
	A ax;
	B bx;
	C cx;   //hayata gelme sırası buradaki bildirimdeki sıra

};
```

Default contructer programlayıcı tarafından yazılmıssa.

```cpp
// member class tanımlı say

class Owner
{
public:
	Owner()
	{
		std::cout << "Owner Ctor\n";
	}
private:
	Member mx;
}


int main()
{
	Owner ox;
}

/*
ÇIKTI
-----
Member default ctor
Owner Ctor
member Destructor
*/
```

Desstructer yazılırsa.

Aşağıda önce elemanlar mı destroy ediliyor yoksa önce destructor anabloğundaki kod çalışıyorda, bu kodun çalışmasından sonramı
elemanlar destroy ediliyor. 2. olan

Yani destructor anabloğundaki kodlar çağrılıyor. sonrasında hayata gelmesiyle ters sırada elemanlarında destructoru çağrılıyor.

```cpp
//member class tanımlı say

class Owner
{
public:
	Owner()
	{
		std::cout << "Owner Ctor\n";
	}
	~Owner()
	{
		std::cout << "Owner Destructor\n";
	}
private:
	Member mx;
}


int main()
{
	Owner ox;
}


/*
ÇIKTI
-----
Member default ctor
Owner Ctor
Owner Destructor
Member Destructor
*/
```

```cpp

```