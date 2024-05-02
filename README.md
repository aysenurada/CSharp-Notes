# CSharp-Notes

#### ==Değişkenler==

**`var` ==keyword==**
Bir değişkenin veri türünü açıkça belirtmeden, derleyicinin değişkenin tipini otomatik olarak çıkarmasını sağlayan bir özelliktir.
Bu, genellikle değişkenin tipini belirlemenin açık bir şekilde belirtilmesi gerekmeyen durumlarda kodun daha kısa ve okunabilir olmasını sağlar.
```C#
var isim = "Zeynep";  // isim değişkenin tipi otomatik olarak string olarak belirlenir
var yas = 25;         // yas değişkeninin tipi otomatik olarak int olarak belirlenir
```

`var` kullanırken dikkat edilmesi gereken birkaç önemli nokta vardır:
- Değişkenin ilk değeri, belirtilen değerden türetilir. Bu nedenle, değişkenin tipi, ilk değere bağlı olarak derleme zamanında belirlenir ve daha sonra değiştirilemez.
- `var` keyword'ü, metot parametreleri, dönen değerler veya üye değişkenleri belirlemek için kullanılamaz. Yalnızca yerel değişkenlerde kullanılabilir.
- Kodun anlaşılırlığı için, değişkenin tipi açıkça belirtmek genellikle iyi bir uygulama olabilir, özellikle değişkenin adı üzerinden türü anlamak zor veya mümkün değilse.

Bu özellik, özellikle LINQ sorguları gibi durumlarda, değişken türlerini kısa ve okunabilir tutmak için sıkça kullanılır.

---
#### ==Data Types==
**Value Types:**
- Tam sayı:                 byte, short, int, long
- Ondalıklı sayı:         float, double, decimal
- Diğer veri tipleri:     char, boolean, struct

**Reference Types:**
- string
- class
- array
- interface

```C#
byte sayi = 56;
int maas = 30000;
float fiyat = 78.90f;    // float tanımlandığında değerin sonuna f harfi koyulmalı
double sicaklik = 25.5;
decimal pi = 3.14m;      // decimal tanımlandığında değerin sonuna m harfi koyulmalı
char kod = 'A';
bool acikKapali = true;
string cinsiyet = "Erkek";
```

![[Pasted image 20240220110110.png]]


==**Data Type Conversion**==
*Veri tipi dönüşümüne neden ihtiyaç duyulur?*
```C#
// Console.Write() ekrana yazdırır ve aynı satırda kalır
// Console.WriteLine() ekrana yazdırır ve alt satıra geçer
Console.Write("1.Sayı: ");
string? sayi1 = Console.Readline();
// Console.ReadLine() kullanıcıdan veri alır
// Console.ReadLine() değer girildiğinde string olarak döndürür değeri
// string? Console.ReadLine() şeklinde tanımlanır
// ? işareti, bir değer girilmezse null değer de döndürebilir demektir
// var sayi1 = Console.ReadLine() şeklinde tanımlama yapıldığında var keyword'ü null olabileceğini de otomatik olarak içermektedir
sayi1 = Convert.ToInt32(sayi1);  // yaparak int tipine dönüştürülür
sayi1 = int.Parse(sayi1);   // Convert.ToInt32() ile aynıdır
// tekrar string'e dönüştürmek istersek ToString() metodu kullanılır
sayi1 = sayi1.ToString();
```

Veri tipi dönüşümü iki türde ele alınabilir:
- **implicit casting** - bilinçsiz tür dönüşümü
- **explicit casting** - bilinçli tür dönüşümü

```C#
// implicit casting
// küçük veriden büyük veriye dönüşüm
int a = 10;
long b = a;

// explicit casting
// büyük veriden küçük veriye dönüşüm
long d = 20;
int e = (int)d;

double f = 20.5;
float g = (float)f;
```

Boyut olarak büyük veri tipindeki bir değeri küçük veri tipine dönüştürmeye kalkışıldığında hata alınır. Çünkü veri kaybı olacaktır. Tam tersi olduğunda dönüştürme işlemi yapılabilir.


==**Nullable Types**==
- Value type'larda mutlaka bir değer ataması yapılmalıdır. Reference type'lar için böyle bir zorunluluk yoktur.

```C#
// reference type için null ataması
string isim = null;
```

- Value type'lara null değeri verebilmek için ? işareti kullanılır.
```C#
// value type için null ataması
int? maas = null;
```

- `HasValue` metodu ile değişkene değer ataması yapılıp yapılmadığını kontrol edilebilir.
```C#
int? maas = null;
Console.WriteLine(maas.HasValue);
// false döner
```

- `GetValueOrDefault` metodu değer atanmış ise değeri döndürür, değer atanmamışsa null olarak default olarak atanmış olan değeri döndürür.
```C#
int? maas = null;
Console.WriteLine(maas.GetValueOrDefault);
// 0 döndürür -> default değer int için 0 dır

int? yas = default;
Console.WriteLine(yas.GetValueOrDefault);
// 0 dondürür
```

Referance type'ların default değeri `null`,
int (short, long vs. dahil) ve float'ın (double, decimal dahil) default değeri `0`,
bool veri tipinin `false`,
char veri tipinin default değeri `\0` yani boşluk karakteri
struct veri tipinin default değeri `null`


==**string**==
- String değişkenleri tek bir string değişkende birleştirmeye **string concat** denir.
```C#
string ad = "Ahmet";
string soyad = "Yılmaz";
string yas = "20";
//string concat
string mesaj = ad + " " + soyad + " isimli kişi " + yas + " yaşındadır."
```

- String birleştirme işlemi $ işareti ile daha kolay şekilde yapılabilir.
```C#
string mesaj = $"{ad} {soyad} isimli kişi {yas} yaşındadır.";
// python'daki f string gibi.
```

- `@` işareti ile string'ler içerdikleri karakterler ve boşluklar ile olduğu gibi korunabilir.
```C#

```

**string Metotları**
```C#
string mesaj = "Ahmet Turan isimli kişi 20 yaşındadır."

// string değişkenin kaç karakterden oluştuğunu verir
var sonuc = mesaj.Lenght;
// string değişkenin tüm karakterlerini küçük harf yapar
var sonuc = mesaj.ToLower();
// string değişkenin tüm karakterlerini büyük harf yapar
var sonuc = mesaj.ToUpper();
// string değişkenin başındaki ve sonundaki boşlukları siler ve yazdırır
var sonuc = mesaj.Trim();
var sonuc = mesaj.TrimStart();  // baştaki boşlukları siler
var sonuc = mesaj.TrimEnd();  // sondaki boşlukları siler
// string değişkeni verilen parametreye göre diziye çevirir.
var sonuc = mesaj.Split(" ");  // boşluklardan ayırarak dizi oluşturur
// string değişkenin verilen parametre ile başlayıp başlamadığına göre bool değer döner
var sonuc = mesaj.StartsWith("Ahmet");  // Ahmet ile mi başlıyor?
// string değişkenin verilen parametre ile bitip bitmediğine göre bool değer döner
var sonuc = mesaj.EndsWith(".");  // . ile mi bitiyor?
// string değişkenin içerisinde verilen parametrenin olup olmadığını kontrol eder ve bool değer döndürür.
var sonuc = mesaj.Contains("Ali");
// string değişkenin içerisinde verilen parametrenin olup olmadığını bool değer olarak görmek yerine varsa konumunu öğrenmeyi sağlar
var sonuc = mesaj.IndexOf("Ahmet");  // yoksa -1, varsa ilk karakterin index'ini verir
// string değişkenin verilen başlangıç parametresinden başlayarak sonuna kadar yazdırır
var sonuc = mesaj.Substring(6);  // 6.indexten başlayıp son karaktere kadar yazdırır.
var sonuc = mesaj.Substring(6, 5);  // 6.indexten başlayıp 5 karakter alır ve yazdırır
// String değişkende yer alan bir karakterin yerine yeni karakter yazılmasını sağlar.
var sonuc = mesaj.Replace("Ahmet", "Ayşe");  // Ahmet yerine Ayşe yazar
```

#### ==DateTime==
```C#
// DateTime türünde bir değişken
DateTime simdi = Datatime.Now;
Console.WriteLine(simdi.Year);
Console.WriteLine(simdi.Month);
Console.WriteLine(simdi.Day);
Console.WriteLine(simdi.DayOfWeek);
Console.WriteLine(simdi.Hour);
Console.WriteLine(simdi.Minute);
Console.WriteLine(simdi.Second);

DateTime dt = new DateTime(2022, 6, 10, 14, 30, 45);
```

---

#### ==Diziler==
Diziler ikiye ayrılabilir:
- Tek Boyutlu Diziler
- Çok Boyutlu Diziler

```C#
// Tek Boyutlu Dizi
string[] adlar = new string[3];
adlar[0] = "Ayşe";
adlar[1] = "Ali";
adlar[2] = "Mehmet";
// veya boyut belirtmeden de oluşturulabilir
int[] adlar = {"Ayşe", "Ali", "Mehmet"};
```

```C#
// Çok Boyutlu Dizi
int[,] sayilar = new int[2, 3];    // [sütun, satır]
sayilar[0,0] = 1;
sayilar[0,1] = 2;
sayilar[0,2] = 3;
sayilar[1,0] = 4;
sayilar[1,1] = 5;
sayilar[1,2] = 6;
// veya boyut belirtmeden de oluşturulabilir
int[,] sayilar = {{1, 2, 3}, {4, 5, 6}};
```

**Dizi Metotları**
```C#
string[] sehirler = {"İstanbul", "Rize", "Kocaeli"};

// İstenilen index'teki nesneyi günceller
sehirler.setValue("Sakarya", 0);   // (yeni veri, index numarası)
// İstenilen index'teki nesneyi getirir
Console.WriteLine(sehirler.GetValue(0));
// Dizinin kaç elemanlı olduğunu verir
ConsoleWriteLine(sehirler.Lenght);
// Dizinin içerisinde belirtilen elemanı arar ve varsa index'ini, yoksa -1 döner
// Array sınıfı üzerinden erişilir
Console.WriteLine(Array.IndexOf(sehirler, "Rize"));  // (dizi, aranan eleman)
// Diziyi alfabetik olarak sıralar
// Dizi sayısal değerlerden oluşuyorsa küçükten büyüğe sıralar
Array.Sort(sehirler);
// Diziyi ters çevirir
Array.Reverse(sehirler);
// Dizinin elemanlarının hepsini siler ve dizi null değer alır, value type diziler 0 değerini alır
Array.Clear(sehirler);
// Belirtilen index aralığındaki elemanları siler
Array.Clear(sehirler, 0, 1);   // 0.index'ten 1.index'e kadar siler
```

**Array Slicing**
```C#
string[] sehirler = {"Zonguldak", "Sivas", "Samsun", "Ankara"};

var sonuc = sehirler[0..3];  // 0, 1 ve 2.index'i alır
var sonuc = sehirler[1..];   // 1.index'ten başlayıp son index'e kadar alır, son index dahil
var sonuc = sehirler[..2];   // başlangıçtan 2.index'e kadar alır, 2.index dahil değil
```


**?? Operatörü**
```C#
string ad = new string[2];
Console.WriteLine("İsim: ");
ad[0] = Console.ReadLine() ?? "";
// gelen veri boş ise boş karakter koy
```
Kullanıcıdan alınan verinin null değer olup olmadığını kontrol eder `??` operatörü. Null ise boş karakter koyar.

---

#### ==Operatörler==

**++ Operatörü**
```C#
int a = 2;
int b = a++;
// sonraki satırda a = 3 ve b = 2 olur çünkü 
int b = ++a;
// b = 3 ve a = 3;
```

**Math Sınıfı**
```C#
double sonuc;

// Üs alma
sonuc = Math.Pow(2,3);   // (taban,üs)  8
// Karekök alma
sonuc = Math.Sqrt(25);   // 5
// Mutlak değerden çıkarma
sonuc = Math.Abs(-10);  // 10
// Yuvarlama
sonuc = Math.Round(4.5);  // aşağı yuvarlar
sonuc = Math.Round(4.6);  // yukarı yuvarlar
// Her koşulda yukarı yuvarlama
sonuc = Math.Ceiling(4.4);  // 5
// Her koşulda aşağı yuvarlama
sonuc = Math.Floor(4.6);   // 4
// Büyük olanı döndürme
sonuc = Math.Max(10,20);   // 20
// Küçük olanı döndürme
sonuc = Math.Min(10,20);   // 10
```

**Random Sınıfı**
```C#
// Random sınıfı instance class'tır. Nesne oluşturulmadan kullanılamaz.
Random rnd = new Random();
// Negatif olmayan tam sayı üretir
rnd.Next();
// Aralık verilebilir
rnd.Next(100);   // 100'e kadar sayı üretir, 100 dahil değil
rnd.Next(60, 100);  // 60 ve 100 arasında sayı üretir, 60 dahil, 100 dahil değil
```

---

#### ==Koşullu Bloklar==

**Kod Blokları**
- Her blok kendi kapsamını tanımlar.
- Her bloktan çıkıldığında veriler bellekten silinir.

Global scope aralığında tanımlanan bir değişken, yerel scope'da tanımlanamaz.
Global scope'da tanımlanan bir değişken, global scope dışında tekrar tanımlanabilir.

**?: Ternary Operatörü**
```C#
int a = 10, b = 20;

var sonuc = (a > b) ? "a büyük" : (a == b) ? "a ve b eşit" : "b büyük";
```

---

#### ==Döngüler==

**foreach Döngüsü**
- Diziler için kullanılır.
```C#
string ad = "Burcu";

foreach(var i in ad) {
	Console.WriteLine(i);
}
```

---

#### ==Dosya Yönetimi==

**Dosya Okuma**
- Bir .txt uzantılı dosya olsun.
```C#
// File sınıfı static bir sınıftır. Metotlara direkt nesne oluşturmadan sınıf üzerinde ulaşılabilir.
File.OpenText("dosya_yolu");     // StreamReader nesnesi döner
// Aşağıdaki gibi oluşan nesneye erişilebilir
StreamReader sr = File.OpenText("dosya_yolu");
// Dosya içerisindeki veriyi okumak için
var s = "";
while(s = sr.ReadLine() != null) {
	Console.WriteLine(s);
}
```

- Bir başka yöntem olarak dosyanın içeriğinin okunması için `ReadAllText()` metotu kullanılabilir.
```C#
string sonuc = File.ReadAllText("dosya_yolu");
```

- Dosya satır satır okutulup satırlar bir dizi içine atanabilir. `ReadAllLines()` verileri dizi şeklinde gönderir.
```C#
string[] sonuc = File.ReadAllLines("dosya_yolu");
Console.WriteLine(sonuc[0]);
Console.WriteLine(sonuc[1]);
```


**Dosyaya Yazma ve Ekleme**
- `CreateText()` metodu dosyayı yazma modunda açar. İçerisinde veri var ise yeni yazılan veriler, var olan verilerin üzerine yazılır, yani eski veriler kaybedilir.
```C#
// StreamWriter nesnesi döner
StreamWriter sw = File.CreateText("dosya_yolu");

// Eski veriler silinir ve yeniler dosyaya yazılır
sw.WriteLine("merhaba");
sw.WriteLine("dünya");

// Dosyayı kapatır
sw.Close();
```

- `Close()` metodu yerine `using` kullanarak nesneyi kullandıktan sonra scope dışına çıkıldığında silinmesi sağlanır.
```C#
using(StreamWriter sw = File.CreateText("dosya_yolu")) {
	sw.WriteLine("merhaba");
	sw.WriteLine("dünya");
}
```

- `AppendText()` metodu dosyayı yazma modunda açar ve var olan verileri silmeden yeni verileri dosyaya ekler.
```C#
using(StreamWriter sw = File.AppendText("dosya_yolu")) {
	sw.WriteLine("merhaba");
	sw.WriteLine("dünya");
}
```

- `WriteAllText()` metodu ilk parametre olarak verilen dosya yolu veya dosya ismi zaten var ise dosyayı açar, yoksa dosyayı oluşturur. İkinci parametre olarak dosyaya yazılacak veriler girilir. Dosya içerisinde veri varsa veriler silinir ve yeni veriler yazılır. Yazma işlemi bittikten sonra dosya otomatik kapatılır.
```C#
File.WriteAllText("dosya_yolu", "selam");
```

- `AppendAllText()` metodu ilk parametre olarak verilen dosya yolu veya dosya ismi zaten var ise dosyayı açar, yoksa dosyayı oluşturur. İkinci parametre olarak dosyaya yazılacak veriler girilir. Dosya içerisinde veri var ise verileri silmez, yeni verileri dosyaya ekler.
```C#
File.AppendAllText("dosya_yolu", "merhaba");
```


**Klasörlerle Çalışma**
- `CreateDirectory()` metodunda parametre olarak yol belirtmeyip direkt oluşturulacak klasörün adı yazılırsa proje klasörünün altında belirtilen klasörü oluşturur.
```C#
// Directory sınıfı static bir sınıftır, nesne oluşturmadan metotlara erişilebilir
Directory.CreateDirectory("klasor_yolu");
// Başka bir klasörün altında klasör oluşturur
Directory.CreateDirectory("klasor_adi/diger_klasor");
```

- `Delete()` parametre olarak verilen yoldaki klasörü siler. Olmayan klasör silinmeye çalışıldığında hata verir.
```C#
Directory.Delete("klasor_yolu");
```

- `Exists()` belirtilen yolda klasörün olup olmadığını döndürür.
```C#
Directory.Exists("klasor_yolu");
```

- Path oluşturma
```C#
string path = @"C:\temp";
// verilen yolda temp klasörünü oluşturur
Directory.CreateDirectory(path);
```

- `GetCurrentDirectory()` projenin çalışmakta olduğu klasörün dizinini verir.
```C#
string path = Directory.GetCurrentDirectory();
```


**Belirli Bir Yoldaki Dosya ve Klasörlerle Çalışma**
- `GetDirectories()` metodu parametre olarak verilen dizindeki tüm klasörleri getirir ve bunları dizi şeklinde döndürür.
- `"*"` parametresi arama kriteridir ve tüm klasörleri getirmesini söyler.
- `SearchOption.TopDirectoryOnly` sadece ana klasörleri getirir.
- `SearchOption.AllDirectories` ana ve alt klasörlerin hepsini getirir.
```C#
// Projenin çalışmış olduğu kök dizin
string rootPath = Directory.GetCurrentDirectory();

string[] dirs = Directory.GetDirectories(rootPath, "*", SearchOption.TopDirectoryOnly);

// Dizinin elemanlarına erişmek için
foreach(var dir in dirs) {
	Console.WriteLine(dir);
}
```

- `GetFiles()` metodu parametre olarak verilen dizindeki tüm dosyaları getirir ve bunları dizi şeklinde döndürür.
- `"*"` parametresi arama kriteridir ve tüm dosyaları getirmesini söyler.
- `"*.txt"` parametresi arama kriteridir ve .txt uzantılı tüm dosyaları getirir.
- `SearchOption.AllDirectories` tüm klasörlerde aramayı yapar.
```C#
string[] files = Directory.GetFiles(rootPath, "*", SearchOption.AllDirectories);

foreach(var file in files) {
	Console.WriteLine(file);
}
```

- Ulaşılan dosyalar üzerinde işlemlar yapılabilir.
- `Path` sınıfı static bir sınıftır ve nesne oluşturulmadan metotlara erişilebilir.
- `GetExtension()` metodu dosyanın uzantısını döndürür.
- `GetFileName()` metodu dosyanın ismini ve uzantısını döndürür.
- `GetFileNameWithoutExtension()` metodu sadece dosyanın ismini döndürür.
```C#
string[] files = Directory.GetFiles(rootPath, "*", SearchOption.AllDirectories);

foreach(var file in files) {
	Console.WriteLine(file);
	Console.WriteLine(Path.GetExtension(file));
	Console.WriteLine(Path.GetFileName(file));
	Console.WriteLine(Path.GetFileNameWithoutExtension);
}
```

---

#### ==Object Orianted Programming==

**Program Class**
.Net 6 versiyonundan önce Consol şablonu aşağıdaki gibiydi.
```C#
using System;

namespace MyApp 
{ 
	internal class Program 
	{ 
		static void Main(string[] args) 
		{ 
			Console.WriteLine("Hello World!"); 
		} 
	} 
}
```

.Net 6 versiyonundan sonra aşağıdaki gibi oldu.
```C#
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```
Artık program class'ı arka tarafta ekleniyor ve yazılan kodlar o şekilde derleniyor.
`using` keyword'ünü kullanarak namespace'leri eklemeye gerek yok. Programa dahil edilmiş olarak geliyor.

- `namespace` sınıfları gruplamaya yarar.

**Class Oluşturmak**
```C#
namespace ConsoleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Ogrenci ogr1 = new Ogrenci() {OgrenciNo = "100", AdSoyad = "Ada Bilgi", Sube = "6/A"};
            // Aynı atamadır
            Ogrenci ogr2 = new Ogrenci();
            ogr2.OgrenciNo = "100";
            ogr2.AdSoyad = "Ada Bilgi";
            ogr2.Sube = "6/A";
            
			Console.WriteLine($"{ogr1.OgrenciNo} numaralı öğrencinin adı {ogr1.AdSoyad} ve şubesi {ogr1.Sube}");

            Console.WriteLine($"{ogr2.OgrenciNo} numaralı öğrencinin adı {ogr2.AdSoyad} ve şubesi {ogr2.Sube}");
        }
    }

    class Ogrenci
    {
        // property
        public string OgrenciNo { get; set; }
        public string AdSoyad { get; set; }
        public string Sube { get; set; }

		// method
		public string BilgileriYazdir()
        {
            return $"{this.OgrenciNo} numaralı öğrencinin adı {this.AdSoyad} ve şubesi {this.Sube}";
        }
    }
}
```

**Constructors**
- Class ismi ile aynı olur.
- Her nesne için otomatik olarak çalıştırılır.
```C#
class Ogrenci 
{
	public Ogrenci()
	{
		// codes
	}
	// properties
	// methods
}
```

---

#### ==Collections==

- Dizileri kullanma amacıyla aynıdır.
- non-generic collections -> tip tanımlamasına bağlı değildir.
- generic -> tipe bağımlıdır.


**Array List**
- Herhangi bir tipe bağımlı değildir. Her eleman bir object'tir.
- Dinamik bir hafızayla kullanılabilir.
```C#
ArrayList liste = new ArrayList();

liste.Add(10);
liste.Add("armut");
liste.Add(true);

// Verilen parametreleri listenin sonuna ekler
liste.AddRange(20, 30);
// İstenilen index'e veri ekler
liste.Insert(1, "aynur");
// Verilen parametreyi siler
liste.Remove("armut");
// Belirtilen index'teki veriyi siler
liste.RemoveAt(2);
```


**Generic List**
- Tip bağımlıdır.
```C#
List<int> sayilar = new List<int>();

sayilar.Add(10);
sayilar.Add(20);
```

```C#
List<string> isimler = new List<string>() {"Ahmet", "Aynur"};
```


**Dictionary**
```C#
Dictionary<int, string> plakalar = new Dictionary<int, string>();

plakalar.Add(41, "Kocaeli");
plakalar.Add(6, "Ankara");

Console.WriteLine(plakalar[41]);

// tüm verileri yazdırmak için
foreach(KeyValuePair<int, string> plaka in plakalar)
{
	Console.WriteLine(plaka.Key + " " + plaka.Value);
}
```

```C#
Dictionary<int, string> sayilar = new Dictionary<int, string>() 
{
	{1, "bir"},
	{2, "iki"},
	{3, "üç"}
};
```

---

#### ==Exception Handling - Hata Yönetimi==

```C#
try {
	// hatalar
}
catch(Exception) {
	// çözüm kodları
	// uyarı mesajları
}
```


**Hata Fırlatma**
```C#
throw new Exception("mesaj_yazilabilir");
```

