
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



#### Ozel Metodların Kalıtımda kullanımı

