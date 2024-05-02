# C# Notları - Microsoft Learn
- .NET Runtime'ın en son sürümü, tür adını tekrarlamak zorunda kalmadan bir nesneyi örneklemenize olanak tanır (target-typed constructor invocation). Amaç, kodun okunabilirliğini basitleştirmektir. Hedef tipli `new` ifadesi yazarken her zaman parantez kullanırsınız.  Örneğin, aşağıdaki kod `Random` sınıfının yeni bir örneğini oluşturacaktır:
```C#
Random dice = new();

// Önceden böyleydi, hâlâ kullanılıyor.
Random dice = new Random();
```

---

- C# veya .NET Sınıf Kitaplığının nasıl çalıştığını açıklayan kod açıklamalarını kullanmayın. Kodlara yorum eklerken her kodu açıklayan yorum satırı eklenmemelidir. Bunlar low-quality comments (düşük kaliletili yorumlar) olarak isimlendirilir. Bunların yerine programın asıl amacını açıklayan kod satırları en üste eklenebilir.
- Yorumlara asla güvenmeyin. Birçok değişiklik ve güncellemeden sonra kodun mevcut durumunu yansıtmayabilirler.

- Tek bir kod satırı uzarsa onu bölebilirsiniz. Ancak, bunu yapmak için iyi bir nedeniniz olmadıkça, tek bir ifadeyi keyfi olarak birden fazla satıra bölmekten kaçınmalısınız.
- Genel olarak konuşursak, okunabilirliği artırmak için benzer veya ilgili şeyler yapan iki, üç veya dört kod satırı arasına boş bir satır eklersiniz.
- Benzer göründüklerinde veya küçük bir görevi gerçekleştirmek için birbirleriyle çalıştıklarında kod satırlarını bir arada tutun.

---

- Koşullu ifadeniz tek satırdan oluşuyorsa {} kaldırabilirsiniz.
```C#
bool flag = true; 
if (flag) 
	Console.WriteLine(flag);
```
- Koşullu ifade tek satır içeriyorsa tüm kodu tek satırda da yazabilirsiniz.
```C#
string name = "steve"; 
if (name == "bob") Console.WriteLine("Found Bob"); 
else if (name == "steve") Console.WriteLine("Found Steve"); 
else Console.WriteLine("Found Chuck");
```
- Microsoft kodları böyle kullanmamanızı tavsiye eder.

---

- Value type değişkenler, değerlerini doğrudan stack (yığın) adı verilen bir depolama alanında saklar.
	- Stack, şu anda CPU üzerinde çalışan koda ayrılan bellektir.
- Reference type değişkenler, değerlerini heap adı verilen ayrı bir bellek bölgesinde saklar. 
	- Heap, işletim sistemi üzerinde aynı anda çalışan birçok uygulama arasında paylaşılan bir bellek alanıdır.

---

- `out` keyword'ü, bir metodun değer döndürmek yerine bir veya daha fazla değeri metodun dışındaki bir değişkene aktarmasına olanak tanır. Yani, `out` parametreleri, metottan dışarıya veri aktarmanın bir yolu olarak kullanılır. Bu sayede, bir metot birden fazla değer döndürebilir.
```C#
using System;

class Program
{
    static void Main()
    {
        int sayi1 = 10;
        int sayi2 = 3;
        int bolum, kalan;

        BolmeIslemi(sayi1, sayi2, out bolum, out kalan);

        Console.WriteLine("Bölüm: " + bolum);
        Console.WriteLine("Kalan: " + kalan);
    }

    static void BolmeIslemi(int bolunen, int bolen, out int bolum, out int kalan)
    {
        bolum = bolunen / bolen;
        kalan = bolunen % bolen;
    }
}
```

---

- `TryParse()` metodu:
	- Bir string'i istenilen sayısal veri türüne dönüştürmeye çalışır.
	- Başarılı olursa dönüştürülen değeri bir çıkış parametresinde saklar.
	- Dönüştürme işleminin başarılı mı yoksa başarısız mı olduğunu belirten bir `bool` ifade döndürür.
```C#
string value = "102";
int result = 0;
if (int.TryParse(value, out result))
{
   Console.WriteLine($"Measurement: {result}");
}
else
{
   Console.WriteLine("Unable to report the measurement.");
}
```

---

- Composite Formatting
```C#
string first = "Hello";
string second = "World";
string result = string.Format("{0} {1}!", first, second);
Console.WriteLine(result);

// Hello World!
```

```C#
string first = "Hello";
string second = "World";
Console.WriteLine("{1} {0}!", first, second);
Console.WriteLine("{0} {0} {0}!", first, second);

// World Hello!
// Hello Hello Hello!
```

---

- Para birimi biçimlendirme:
```C#
decimal price = 123.45m;
int discount = 50;
Console.WriteLine($"Price: {price:C} (Save {discount:C})");

// Price: $123.45 (Save $50.00)
```

- Bu para biçimlendirme programın çalıştığı bilgisayarın yerel konumuna ve kullandığı dile bağlıdır. Buna **culture code** denir.
	- the culture code of an English speaker in the USA is `en-US`.
	- the culture code of a French speaker in France is `fr-FR`.
	- the culture code of a French speaker in Canada is `fr-CA`.

---

- Sayıları biçimlendirmede `N` sayıları daha okunabilir hale getirir. 
```C#
decimal measurement = 123456.78912m;
Console.WriteLine($"Measurement: {measurement:N} units");

// Measurement: 123,456.79 units
```

- Varsayılan olarak ondalık noktadan sonra yalnızca iki rakamı görüntüler. Bunu `N` belirtecinden sonra rakam belirterek değiştirebilirsiniz.
```C#
decimal measurement = 123456.78912m;
Console.WriteLine($"Measurement: {measurement:N4} units");

// Measurement: 123,456.7891 units
```

---

- Yüzdeleri (%) biçimlendirmek için `P` belirteci kullanılır.
- Ondalık noktadan sonraki görüntülemek istenilen basamak sayısını belirtmek için `P` belirtecinin yanına rakam koyun.
```C#
decimal tax = .36785m;
Console.WriteLine($"Tax rate: {tax:P2}");

// Tax rate: 36.79 %
```

---

- Biçimlendirme amacıyla boşluk ekleyen yöntemler: `PadLeft()`, `PadRight()`
```C#
string input = "Pad this";
Console.WriteLine(input.PadLeft(12));

// 	Pad this
```

```C#
Console.WriteLine(input.PadRight(12, '-'));

// Pad this---
```

- `+=` operatörü, `formattedLine` değişkeninin önceki değerini alıp yeni değeri ona ekleyerek bir dize birleştirme işlemi gerçekleştirir.
```C#
string paymentId = "769C";
string payeeName = "Mr. Stephen Ortega";

var formattedLine = paymentId.PadRight(6);
formattedLine += payeeName.PadRight(24);

Console.WriteLine(formattedLine);

// 769C  Mr. Stephen Ortega
```

---

- İki string'i karşılaştıran veya karşılaştırmayı kolaylaştıran yöntemler: `Trim()`, `TrimStart()`, `TrimEnd()`, `GetHashcode()` ve `Length` özelliği
- Bir string'in içinde ne olduğunu belirlemenize hatta dizenin yalnızca bir kısmını almanıza yardımcı olan yöntemler: `Contains()`, `StartsWith()`, `EndsWith()`, `Substring()`
- Parçaları değiştirerek, ekleyerek veya çıkararak string'in içeriğini değiştiren yöntemler: `Replace()`, `Insert()`, `Remove()`
- Bir string'i dize veya karakter dizisine dönüştüren yöntemler: `Split()`, `ToCharArray()`
- `LastIndexOf()` bir karakterin veya string'in başka bir dize içindeki son konumunu döndürür.
- `IndexOfAny()` başka bir string'in içinde oluşan bir karakter dizisinin ilk konumunu döndürür.

---

- Metodun çağrılması için çağrılmadan önce tanımlanmış olmasına gerek yoktur.
```C#
SayHello();

void SayHello() 
{
    Console.WriteLine("Hello World!");
}
```

---
