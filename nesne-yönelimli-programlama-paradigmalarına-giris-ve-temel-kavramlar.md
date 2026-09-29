# 1. Nesne Yönelimli Programlama (OOP) Nedir?

**Nesne Yönelimli Programlama (Object-Oriented Programming - OOP)**, karmaşık sistemleri modellemek ve yönetmek için veriyi (durum/state) ve bu veriler üzerinde çalışan davranışları (fonksiyonlar/metotlar) tek bir mantıksal birimde (class / sınıf) birleştiren bir yazılım geliştirme yaklaşımıdır. OOP mantığında yazılım, birbiriyle etkileşen nesnelerin bir koleksiyonu olarak ele alınır.

### Tarihsel Gelişim
### Simula (1960'lar)

İlk nesne yönelimli programlama özellikleri (sınıf ve nesne kavramları), 1960'ların ortalarında Ole-Johan Dahl ve Kristen Nygaard tarafından Norveç Bilgisayar Merkezi'nde geliştirilen **Simula I** ve **Simula 67** dillerinde ortaya çıkmıştır. Simula, özellikle simülasyon sistemleri yazmak için tasarlanmış ve nesne kavramını ilk kez bilgisayar bilimine kazandırmıştır.

### Smalltalk ve Terimin Doğuşu (1970'ler)

1970'lerde Alan Kay öncülüğünde Xerox PARC'ta geliştirilen **Smalltalk** dili, tam anlamıyla dinamik ve saf bir OOP dili olarak tasarlanmıştır. "Object-oriented" (nesne yönelimli) terimi ilk kez Alan Kay ve Smalltalk ekibi tarafından popülerleştirilmiştir.

### Endüstriye Yayılım (1980'ler ve 1990'lar)

OOP'nin ana akım yazılım dünyasına girmesi ve endüstri standardı haline gelmesi, 1980'lerde Bjarne Stroustrup tarafından geliştirilen **C++** dilinin çıkışı ve ardından 1990'larda Java gibi dillerin popülerleşmesiyle hız kazanmıştır.

### OOP'nin Temel Mantığı

Nesne Yönelimli Programlama (OOP), yazılımı gerçek dünyadaki nesneler gibi modelleyerek geliştirme yaklaşımıdır. Kod, **sınıflar (class)** ve bunlardan üretilen **nesneler (object)** etrafında organize edilir.

Bu yaklaşımın temel avantajları:

- Daha düzenli kod yapısı
- Yeniden kullanılabilirlik
- Kolay bakım
- Genişletilebilir mimari

Nesne Yönelimli Programlama (OOP - Object-Oriented Programming), yazılımı gerçek dünyadaki nesneler gibi modelleyerek geliştirme yaklaşımıdır. Kod, “sınıflar” (class) ve bunlardan üretilen “nesneler” (object) etrafında organize edilir. Bu yaklaşım, kodun daha düzenli, yeniden kullanılabilir, bakımı kolay ve genişletilebilir olmasını sağlar.

Prosedürel programlamada (C, klasik Pascal, erken BASIC gibi) her şey fonksiyonlar ve global/yerel değişkenler etrafında döner. Veri ve işlemler ayrı tutulur. Aşağıdaki kodda OOP olmayan (Prosedürel) programlamaya C dilinde bir örnek verilmektedir.

```c
#include <stdio.h>
#include <string.h>

struct Araba {
    char marka[50];
    char model[50];
    int yil;
    int hiz;	// Herkes erişebilir
};

void hizlan(struct Araba *a, int miktar) {
    a->hiz += miktar;
    printf("%s %s hızlandı. Yeni hız: %d\n", a->marka, a->model, a->hiz);
}

void yavasla(struct Araba *a, int miktar) {
    a->hiz = (a->hiz - miktar > 0) ? a->hiz - miktar : 0;
    printf("Yeni hız: %d\n", a->hiz);
}

int main() {
    struct Araba araba1 = {"Toyota", "Corolla", 2020, 0};
    struct Araba araba2 = {"Honda", "Civic", 2022, 0};

    hizlan(&araba1, 50);
    hizlan(&araba2, 30);
    return 0;
}
```

C’de veri (struct) ve fonksiyonlar ayrıdır. Fonksiyonlara her seferinde yapıyı (pointer ile) geçmek zorunluluğu vardır. struct (structure / yapı), farklı türdeki değişkenleri tek bir çatı altında toplamaya yarayan özel bir veri tipidir. C dilinde int, float, char gibi temel veri tipleri vardır. Ancak gerçek dünyadaki bir nesneyi (örneğin bir Araba veya bir Öğrenci) temsil etmek için tek bir değişken yetmez. Bu durumda struct kendi karmaşık veri tipimizi oluşturmaya yarar.

Kodda kapsülleme yani koda dışarıdan herkes tarafından erişim vardır. Kapsülleme, bir nesnenin iç verisini (değişkenlerini) dışarıdan gizleyip, sadece kontrollü metodlar (getter/setter veya davranış metodları) üzerinden erişime izin verilmesidir. Burada amaç veri tutarlılığını korumak, istenmeyen değişiklikleri engellemek ve iç implementasyonu değiştirebilme özgürlüğü sağlamaktır. Aşağıda ise nesne yönelimli bir dil olan C++’den örnek verilmektedir.

```java
class Araba {
private:
    std::string marka;
    std::string model;
    int yil;
    int hiz;                 // Dışarıdan erişilemez

public:
    void hizlan(int miktar) {
        if (miktar > 0)
            hiz += miktar;
    }

    void yavasla(int miktar) {
        hiz = (hiz - miktar > 0) ? hiz - miktar : 0;
    }

    int getHiz() const { return hiz; }   // Sadece okuma
};
```

C’de gerçek anlamda private üye yoktur (sadece pointer + incomplete type ile taklit edilebilir). Bu yüzden C’de yazılan “nesne yönelimli” kodlar genelde zayıf kapsüllemeye sahip olur. C++ veya modern dillerde private / public ile bu kontrol çok daha net sağlanır. Sadece kapsülleme değil daha birçok konuda OOP avantaj sağlamaktadır. Fakat bu prosedürel dillerin işlevsiz olduğunu göstermemektedir. Sistem programlama (işletim sistemi çekirdeği), yüksek performans gerektiren düşük seviye kod, matematiksel hesaplamalar, veri işleme boru hatları (data processing pipelines) gibi alanlarda hala tercih edilmektedir.

### 1.1. Nesne Yönelimli Programlamanın Avantajları

Nesne yönelimli programlama; kapsülleme, kalıtım, çok biçimlilik ve soyutlama prensipleri sayesinde daha güvenli, yeniden kullanılabilir, bakımı kolay ve genişletilebilir yazılımlar üretmeyi sağlar. Özellikle büyük ölçekli projelerde bu avantajlar belirgin şekilde ortaya çıkar.

**Kapsülleme (Encapsulation)**

Veri ve bu veriyi işleyen metotlar bir sınıf (class) içinde bir araya getirilir. Dışarıdan erişim kontrollü hale getirilir (genellikle private, protected, public erişim belirleyicileriyle).

**Avantajı:** Veri güvenliği artar, hatalı dış müdahaleler önlenir ve kodun iç yapısı gizlenerek karmaşıklık azaltılır (information hiding).

**Kalıtım (Inheritance)**
Bir sınıf, başka bir sınıfın özelliklerini ve davranışlarını miras alabilir. Temel sınıf (base class / parent class) ile türetilmiş sınıf (derived class / child class) arasında “is-a” ilişkisi kurulur.

**Avantajı:** Kod tekrarı azalır, yeniden kullanılabilirlik (reusability) artar ve ortak özellikler tek bir yerde toplanarak bakım kolaylaşır.

**Çok Biçimlilik (Polymorphism)**

Aynı arayüz (interface) veya metot adı, farklı sınıflarda farklı davranışlar sergileyebilir. Derleme zamanı (compile-time) veya çalışma zamanı (runtime) polimorfizmi mümkündür.

**Avantajı:** Kod daha esnek ve genişletilebilir olur. Yeni sınıflar eklemek mevcut kodu bozmadan mümkündür (open-closed principle).

**Soyutlama (Abstraction)**
Karmaşık sistemlerin sadece gerekli detayları gösterilir, gereksiz uygulamaya özel ayrıntılar gizlenir. Soyut sınıflar (abstract classes) ve arayüzler (interfaces) bu amaçla kullanılır.

**Avantajı:** Geliştirici, sistemin “ne yaptığına” odaklanır, “nasıl yaptığı” detaylarından uzaklaşır. Bu da anlama ve tasarım sürecini basitleştirir.

**Diğer Önemli Avantajlar**

- **Modülerlik (Modularity):** Program küçük, bağımsız parçalara (modüllere / sınıflara) bölünür. Her parça ayrı geliştirilebilir, test edilebilir ve değiştirilebilir.
- **Yeniden Kullanılabilirlik (Reusability):** Sınıflar ve nesneler farklı projelerde tekrar kullanılabilir. Bu da geliştirme süresini ve maliyeti düşürür.
- **Bakım Kolaylığı (Maintainability):** Kodun yapısı düzenli olduğu için hata bulma, düzeltme ve güncelleme işlemleri daha kolaydır.
- **Ölçeklenebilirlik (Scalability):** Büyük ve karmaşık sistemler daha rahat yönetilebilir. Yeni özellikler eklemek mevcut yapıyı bozmadan mümkündür.
- **Gerçek Dünya Modellemesi:** OOP, gerçek hayattaki nesneleri ve ilişkileri doğrudan kodda yansıtmaya uygundur. Bu sayede problem analizi ve tasarım daha doğal hale gelir.
- **Takım Çalışmasına Uygunluk:** Farklı geliştiriciler farklı sınıflar üzerinde paralel çalışabilir; arayüzler sayesinde entegrasyon kolaylaşır.

### 1.2. OOP'nin Ortaya Çıkışı

Programlama dilleri ve yazılım geliştirme yöntemleri, yazılım sistemlerinin giderek büyümesiyle birlikte önemli bir dönüşüm geçirmiştir. İlk dönemlerde geliştirilen programlar genellikle sınırlı sayıda işlem gerçekleştiren, küçük boyutlu ve tek bir geliştirici tarafından yönetilebilen uygulamalardan oluşmaktaydı. Bu tür uygulamalarda değişkenlerin ve fonksiyonların doğrudan kullanılması çoğu zaman yeterliydi.
OOP’nin ortaya çıkış ihtiyacı, yazılım dünyasının büyüyen karmaşıklığıyla başa çıkabilmek ve eski programlama yaklaşımlarının getirdiği tıkanıklıkları aşmak için doğmuştur.

Yazılım tarihi boyunca programcılar, gerçek dünyadaki problemleri bilgisayara aktarırken komutlar dizisi **(prosedürel yaklaşım)** kullandılar. Ancak projeler büyüdükçe şu temel sorunlar ortaya çıktı. Prosedürel dillerde (örneğin C dilinde) veriler genellikle daha önce de belirtildiği üzere **struct** gibi yapılarda tutulur, bu verileri işleyen fonksiyonlar ise kodun başka yerlerinde bağımsız olarak bulunurdu. Bu durum, hangi fonksiyonun hangi veriyi değiştirdiğinin takip edilmesini zorlaştırıyordu. OOP, veriyi **(state/durum)** ve o veriyi işleyen davranışları **(metotları)** tek bir çatı altında **(Class / Sınıf içinde)** birleştirerek bu dağınıklığı ortadan kaldırdı.

Prosedürel kodlarda programın her yerinden erişilebilen global değişkenler, büyük projelerde kontrol edilemez hatalara yol açıyordu. OOP; verileri sınıf içerisine hapsederek *(kapsülleme - encapsulation)* dışarıdan rastgele ve tutarsız müdahaleleri engelledi.

Binlerce satırlık prosedürel kodlarda küçük bir değişiklik yapmak, domino taşı etkisi yaratarak kodun başka yerlerini bozuyordu. OOP ise sistemi modüler nesnelere bölerek her nesnenin kendi sorumluluğunu almasını sağladı.

Bunun yanı sıra, geleneksel programlama dilleri bilgisayarın adım adım nasıl çalışacağına odaklanırken, gerçek dünyadaki karmaşık problemleri ifade etmekte anlamsal (semantik) olarak yetersiz kalıyordu. İnsan zihni çevresini nesneler, bu nesnelerin özellikleri ve birbirleriyle olan etkileşimleri üzerinden algılar. OOP'nin ortaya çıkışındaki en büyük motivasyonlardan biri de yazılım mimarisini insan zihninin problem çözme mantığına yaklaştırmaktır. Bu sayede gerçek dünya varlıkları (örneğin bir bankacılık sistemindeki müşteri, hesap veya fatura) kod ortamında doğrudan "nesneler" olarak modellenebilmiş, kodun okunabilirliği ve anlaşılabilirliği büyük ölçüde artmıştır.

Projelerin çapı büyüdükçe ortaya çıkan bir diğer kriz ise "spagetti kod" problemi ve kod tekrarıydı. Prosedürel yaklaşımda benzer işlevler gerektiğinde kodun kopyalanıp yapıştırılması veya aynı işlemlerin ufak farklarla yeniden yazılması sıklıkla karşılaşılan bir durumdu. OOP, *kalıtım (inheritance)* mekanizmasını sunarak önceden yazılmış, test edilmiş ve hatasız çalışan kod yapılamalarının yeni alt sistemler tarafından miras alınmasını sağladı. Bu durum **"Kendini Tekrar Etme" (DRY - Don't Repeat Yourself)** prensibinin temelini atarak geliştirme süreçlerini inanılmaz derecede hızlandırdı.

Yazılım endüstrisinin büyümesiyle tek bir geliştiricinin yerini çok kalabalık yazılım ekiplerinin alması da yapısal bir değişimi zorunlu kıldı. Geleneksel yöntemlerde onlarca geliştiricinin aynı kod tabanı üzerinde çalışması, kod parçalarını birleştirirken ciddi **"çakışma" (conflict)** sorunlarına yol açıyordu. OOP'nin nesne tabanlı modülerliği sayesinde geliştiriciler, diğer nesnelerin iç işleyişini bilmek zorunda kalmadan sadece nesnelerin dışa açılan yüzüyle (arayüzler/interfaces) ilgilenebildi. Bu sayede devasa projelerde iş bölümü yapmak ve eşzamanlı kod geliştirmek çok daha güvenli hale geldi.
Son olarak, değişen müşteri gereksinimlerine veya yeni iş kurallarına uyum sağlamak, eski prosedürel sistemlerde kodun merkezine inip köklü değişiklikler yapmayı gerektiriyordu. OOP, sunduğu çok biçimlilik (polymorphism) özelliği ile yazılımlara adeta bir "tak-çalıştır" esnekliği kazandırdı. Mevcut sistemi hiç bozmadan yeni nesne türlerinin ve davranışların sisteme dışarıdan eklenebilmesi, yazılımın yaşam döngüsü boyunca ortaya çıkan bakım (maintenance) maliyetlerini ve hata riskini dramatik ölçüde düşürmüştür.

### 1.3. OOP’NİN FARKLI PROGRAMLAMA DİLLERİNDE UYGULAMALARI
Günümüz yazılım dünyasında programlama dillerinin ezici bir çoğunluğu *çok paradigmalı (multi-paradigm)* bir yapıya bürünmüştür. Yani bir dil hem nesne yönelimli (OOP) hem *fonksiyonel* hem de *prosedürel* yaklaşımları aynı anda destekleyebilir. Programlama dilleri diğer pek çok şey gibi eksiklikleri giderilerek, fonksiyonellikleri artırılarak geliştirilmektedir. OOP desteği olan diller 3 farklı kategoriye ayrılabilir. Bunlar **klasik (sınıf tabanlı)**, **prototip tabanlı** ve **modern OOP** diller olarak isimlendirilebilir.

#### 1.3.1. KLASİK (SINIF TABANLI) OOP DİLLERİ
Sınıf (class), nesne (object), kalıtım (inheritance), kapsülleme (encapsulation) ve çok biçimlilik (polymorphism) kavramlarını doğrudan dilin sözdiziminde barındıran en yaygın dillerdir.

**Java & C#:** Kodun neredeyse tamamının bir sınıf içerisinde yazılmasını zorunlu kılan, kurumsal yazılımlarda OOP standardı kabul edilen diller.

Aşağıda Java dilinde yazılmış kod verilmektedir. Java’da erişim belirleyiciler (access modifiers) her değişkenin ve metodun başında tek tek belirtilir. Java'da erişim belirleyiciler, sınıfların, değişkenlerin (niteliklerin) ve metotların (davranışların) programın diğer kısımları tarafından nereden ve nasıl erişilebileceğini kontrol eden anahtar kelimelerdir. Bunlar private, default, protected ve public’dir.

```java
public class BankaHesabi {
    public String hesapSahibi;
    private double bakiye; // Private anahtar kelimesi ile veri gizleme

    // Kurucu Metot
    public BankaHesabi(String hesapSahibi, double baslangicBakiyesi) {
        this.hesapSahibi = hesapSahibi;
        this.bakiye = baslangicBakiyesi;
    }

    public void paraYatir(double miktar) {
        if (miktar > 0) {
            this.bakiye += miktar;
            System.out.println(miktar + " TL yatırıldı. Yeni bakiye: " + this.bakiye + " TL");
        }
    }

    public void paraCek(double miktar) {
        if (miktar > 0 && miktar <= this.bakiye) {
            this.bakiye -= miktar;
            System.out.println(miktar + " TL çekildi. Kalan bakiye: " + this.bakiye + " TL");
        } else {
            System.out.println("Yetersiz bakiye veya geçersiz işlem!");
        }
    }

    public double bakiyeGoster() {
        return this.bakiye;
    }
    
    // Kullanım
    public static void main(String[] args) {
        BankaHesabi hesap = new BankaHesabi("Ahmet Yılmaz", 1000);
        hesap.paraYatir(500);
        hesap.paraCek(200);
        // System.out.println(hesap.bakiye); // HATA VERİR: Kapsülleme
    }
}
```

Python'da isimlendirme geleneği **(_ veya __)** ile sağlanan veri gizleme mantığı, Java'da doğrudan dilin yapısına entegre edilmiş private, default, protected, public kelimeler ile yapılır.  Bu yapı derleyici (compiler) tarafından kesin kurallarla denetlenir. 

**C++:** C dilinin hızını OOP yetenekleriyle birleştiren, çoklu kalıtımı (multiple inheritance) destekleyen güçlü bir sistem programlama dilidir. C++, sınıfları tanımlarken private ve public bloklarını açıkça belirtmenizi ister. Hafıza yönetimi ve tip güvenliği (type safety) konusunda çok daha katıdır.

```cpp
#include <iostream>
#include <string>
using namespace std;

class BankaHesabi {
private: // Bu bloğun altındakilere sadece sınıf içinden erişilebilir
    double bakiye; 

public:  // Bu bloğun altındakilere her yerden erişilebilir
    string hesap_sahibi;

    // Kurucu Metot (Constructor)
    BankaHesabi(string isim, double baslangic_bakiyesi) {
        hesap_sahibi = isim;
        bakiye = baslangic_bakiyesi;
    }

    void para_yatir(double miktar) {
        if (miktar > 0) {
            bakiye += miktar;
            cout << miktar << " TL yatirildi. Yeni bakiye: " << bakiye << " TL\n";
        }
    }

    void para_cek(double miktar) {
        if (miktar > 0 && miktar <= bakiye) {
            bakiye -= miktar;
            cout << miktar << " TL cekildi. Kalan bakiye: " << bakiye << " TL\n";
        } else {
            cout << "Yetersiz bakiye veya gecersiz islem!\n";
        }
    }

    double bakiye_goster() {
        return bakiye;
    }
};

// Kullanım
int main() {
    BankaHesabi hesap("Ahmet Yilmaz", 1000);
    hesap.para_yatir(500);
    hesap.para_cek(200);
    // cout << hesap.bakiye; // HATA VERİR: Kapsülleme
    return 0;
}

```

Python: "Her şey bir nesnedir" felsefesini benimseyen, ancak zorunlu kılmayıp prosedürel veya fonksiyonel kod yazılmasına da izin veren çok paradigmalı bir dildir. Python'da erişim belirleyiciler (access modifiers) public, private gibi anahtar kelimeler yerine isimlendirme kuralıyla yapılır. Değişkenin başına iki alt tire (__) konulduğunda dışarıdan doğrudan erişim engellenir.

```python
class BankaHesabi:
    def __init__(self, hesap_sahibi, baslangic_bakiyesi):
        self.hesap_sahibi = hesap_sahibi
        self.__bakiye = baslangic_bakiyesi  # '__' ile private (gizli) değişken

    def para_yatir(self, miktar):
        if miktar > 0:
            self.__bakiye += miktar
            print(f"{miktar} TL yatırıldı. Yeni bakiye: {self.__bakiye} TL")

    def para_cek(self, miktar):
        if 0 < miktar <= self.__bakiye:
            self.__bakiye -= miktar
            print(f"{miktar} TL çekildi. Kalan bakiye: {self.__bakiye} TL")
        else:
            print("Yetersiz bakiye veya geçersiz işlem!")

    def bakiye_goster(self):
        return self.__bakiye

# Kullanım
hesap = BankaHesabi("Ahmet Yılmaz", 1000)
hesap.para_yatir(500)
hesap.para_cek(200)
# print(hesap.__bakiye) # HATA VERİR: Kapsülleme nedeniyle dışarıdan erişilemez.

```

**Ruby:** Tamamen nesne merkezli bir dil; sayılar ve basit veri türleri dahil her eleman birer nesnedir. Ruby, 1995 yılında Japon bilgisayar bilimci *Yukihiro "Matz" Matsumoto* tarafından geliştirilmiş, dinamik, açık kaynaklı ve tamamen nesne yönelimli bir programlama dilidir.

OOP kavramları anlatılırken Ruby'nin yeri çok ayrıdır çünkü dilin temelinde yatan felsefe diğer birçok dilden daha *radikaldir.*

Java veya C++ gibi dillerde int, char, double gibi nesne olmayan, bellekte doğrudan değer olarak tutulan ilkel (primitive) veri tipleri vardır. Ruby bu ayrımı tamamen reddeder. 

Ruby'de her şey bir nesnedir. Bir tam sayı, bir metin, hatta bir *"boşluk" (nil)* bile kendi metotlarına ve sınıflarına sahip birer nesnedir. Örneğin, bir işlemi 5 kere tekrar etmek için for veya while döngüsü kurmak yerine, doğrudan 5 nesnesinin times (kere) metodunu çağırırsınız.

```ruby
# 5 bir Integer nesnesidir ve 'times' adında bir metodu vardır
5.times do
  puts "Yönetim Bilişim Sistemleri"
end
```

Ruby'de @ ile başlayan örnek değişkenlerine (instance variables) dışarıdan erişmek mimari olarak tamamen kapalıdır. Onları dışarı açmak için ya bir metot yazmanız ya da attr_reader gibi okuma izinleri tanımlamanız gerekir. Aşağıda aynı örnek Ruby dilinde verilmektedir.

```ruby
class BankaHesabi
  # Sadece hesap sahibinin isminin dışarıdan "okunabilmesi" için izin veriyoruz.
  # Bakiye için böyle bir izin vermediğimiz için tamamen gizli (private) kalıyor.
  attr_reader :hesap_sahibi

  def initialize(hesap_sahibi, baslangic_bakiyesi)
    @hesap_sahibi = hesap_sahibi
    @bakiye = baslangic_bakiyesi # Kapsüllenmiş değişken
  end

  def para_yatir(miktar)
    if miktar > 0
      @bakiye += miktar
      puts "#{miktar} TL yatırıldı. Yeni bakiye: #{@bakiye} TL"
    end
  end

  def para_cek(miktar)
    if miktar > 0 && miktar <= @bakiye
      @bakiye -= miktar
      puts "#{miktar} TL çekildi. Kalan bakiye: #{@bakiye} TL"
    else
      puts "Yetersiz bakiye veya geçersiz işlem!"
    end
  end

  def bakiye_goster
    # Ruby'de son satır otomatik olarak return edilir, 'return' yazmaya gerek yoktur.
    @bakiye 
  end
end

# Kullanım
hesap = BankaHesabi.new("Ahmet Yılmaz", 1000)
hesap.para_yatir(500)
hesap.para_cek(200)

# puts hesap.bakiye # HATA VERİR (NoMethodError): Kapsülleme nedeniyle dışarıdan erişilemez.
# puts hesap.@bakiye # HATA VERİR (SyntaxError): Sözdizimi olarak bile dışarıdan çağrılamaz.

```

*__init__* yerine initialize: Ruby, kurucu metot (constructor) olarak initialize ismini kullanır ve nesne oluşturulurken BankaHesabi.new() şeklinde çağrılır.

*self Karmaşası Yok:* Python'da sınıfa ait bir değişkene ulaşırken sürekli self.__bakiye yazmak zorundayız. Ruby'de değişkenin başındaki @ sembolü, onun bu nesneye ait olduğunu belirtmek için yeterlidir (@bakiye).

*Kapsülleme Mantığı:* Python'da __bakiye yazdığımızda Python arka planda ismini değiştirerek (name mangling) bunu gizlemeye çalışır. Ancak özel bir yöntemle (hesap._BankaHesabi__bakiye) dışarıdan yine de erişebilirsiniz. Ruby'de ise @bakiye değişkenine sınıf dışından erişmenin hiçbir yolu yoktur. Dışarıdan sadece sınıfa "mesaj gönderebilirsiniz" (yani metot çağırabilirsiniz). Bu yüzden Ruby'nin kapsüllemesi çok daha saf ve katıdır.

**PHP:** Web geliştirmede modern sürümleriyle (PHP 7 ve 8) birlikte katı OOP standartlarını (arayüzler, soyut sınıflar, tip belirleme) eksiksiz sunan dildir.

**Kotlin & Swift:** Sırasıyla Android ve iOS dünyasında modern yazılım geliştirmenin temeli olan, modern OOP ile fonksiyonel programlamayı harmanlayan diller.

#### 1.3.2. PROTOTİP TABANLI OOP DİLLERİ

**JavaScript & TypeScript:** Klasik sınıf hiyerarşisi yerine prototip zinciri (prototype-based) mantığını kullanır. Modern JavaScript **(ES6)** ile birlikte gelen class anahtar kelimesi, arka plandaki bu prototip yapısının üzerine inşa edilmiş sözdizimsel bir kolaylıktır *(syntactic sugar).*

Java, C++ veya C# gibi dillerde sınıf (class) bir mimari plandır, nesne (object) ise o plana bakılarak inşa edilen binadır. Sınıfın kendisi bellekte canlı bir nesne değildir; sadece kuralları tanımlar. Bir alt sınıf oluşturduğunuzda, kurallar bu soyut şablonlar üzerinden yukarıdan aşağıya miras (inheritance) yoluyla aktarılır.

JavaScript'in orijinal tasarımında **"sınıf"** veya **"şablon"** diye bir kavram yoktur; sadece bellekteki canlı nesneler vardır. JavaScript'te miras alma işlemi kalıplardan değil, doğrudan mevcut nesnelerden klonlama veya referans gösterme yoluyla yapılır. 

Yeni bir nesne oluşturduğunuzda, mimari yapı bu nesneye şunu söyler: "Senin özelliklerin şurada duran başka bir canlı nesneye benziyor. Eğer sende olmayan bir metot çağrılırsa, git ona sor. "Referans alınan bu orijinal nesneye Prototip (Prototype) denir.

Eğer aranan özellik o prototipte de yoksa, o prototipin kendi prototipine bakılır. Bu birbirine bağlı referanslar dizisine Prototip Zinciri (Prototype Chain) adı verilir.

JavaScript'in prototip mantığı ve yazım biçimi, Java ve C++ gibi dillerden gelen yazılımcılara karmaşık ve yabancı geliyordu. Dilin popülaritesi arttıkça, kurumsal projelerde işleri kolaylaştırmak ve yazılımcılara tanıdık bir sözdizimi sunmak amacıyla 2015 yılında **(ES6 sürümüyle)** dile *class* anahtar kelimesi eklenmiştir.

Ancak bu bir illüzyondur. Dilin temel çekirdek mimarisi değişmemiştir. class kelimesiyle oluşturulan yapı, arka planda JavaScript motoru tarafından yine eski usul prototip zincirine dönüştürülerek çalıştırılır.

*"Syntactic sugar" (sözdizimsel şeker/kolaylık)* terimi yazılım mühendisliğinde tam olarak bunu ifade eder: Arka plandaki asıl mekanizmayı değiştirmeden, sadece programcının yazdığı kodu daha okunabilir, daha kısa veya aşina olunan bir formata sokmaktır. Aşağıda ES6 öncesi bir JavaScript kodu verilmektedir. 

```javascript
// Kurucu fonksiyon (Class yerine)
function Araba(marka) {
    this.marka = marka;
}

// Metodu prototipe ekleme (Her nesne bellekte kopyalamasın diye)
Araba.prototype.calistir = function() {
    console.log(this.marka + " çalıştı.");
};

let bmw = new Araba("BMW");
Aşağıda ise ES6 sonrası kod verilmektedir.
class Araba {
    constructor(marka) {
        this.marka = marka;
    }

    calistir() {
        console.log(this.marka + " çalıştı.");
    }
}

let bmw = new Araba("BMW");
```

Klasik dillerde kalıtım hiyerarşik ve katıdır. Örneğin Otomobil sınıfı Arac sınıfından türer. Alt sınıf üst sınıfın bütün özelliklerini hiyerarşik bir ağaç yapısıyla (inheritance tree) devralır. 

JavaScript’de kalıtım yerine delegasyon (Yetki Devri / Delegation) prensibi vardır. JavaScript'teki bir nesnenin, kendine ait olmayan bir özelliğe veya metoda ihtiyacı olduğunda yukarıdaki bir sınıfa ait kuralları ezberlemez; doğrudan referans aldığı prototip nesnesine gidip bakar. Eğer o nesnede de yoksa zincir yukarı doğru taranır (Prototype Chain). 

Bu, nesnelerin çalışma zamanında (runtime) bile prototiplerini değiştirip başka nesnelere bağlanabilmesine (dinamik yetki devri) olanak tanır.

```typescript
class BankaHesabi {
  // JavaScript'te gerçek private değişkenler '#' işareti ile tanımlanır (ES2022+)
  #bakiye;
  
  constructor(hesapSahibi, baslangicBakiyesi) {
    this.hesapSahibi = hesapSahibi; // Dışarıdan okunabilir public özellik
    this.#bakiye = baslangicBakiyesi; // Tamamen gizli (private) bakiye
  }

  paraYatir(miktar) {
    if (miktar > 0) {
      this.#bakiye += miktar;
      console.log(`${miktar} TL yatırıldı. Yeni bakiye: ${this.#bakiye} TL`);
    }
  }

  paraCek(miktar) {
    if (miktar > 0 && miktar <= this.#bakiye) {
      this.#bakiye -= miktar;
      console.log(`${miktar} TL çekildi. Kalan bakiye: ${this.#bakiye} TL`);
    } else {
      console.log("Yetersiz bakiye veya geçersiz işlem!");
    }
  }

  bakiyeGoster() {
    return this.#bakiye;
  }
}

// Kullanım
const hesap = new BankaHesabi("Ahmet Yılmaz", 1000);
hesap.paraYatir(500);
hesap.paraCek(200);

// console.log(hesap.hesapSahibi); // ÇALIŞIR: Public bir özelliktir.
// console.log(hesap.#bakiye);     // HATA VERİR (SyntaxError): Private alanlara sınıf dışından erişilemez.
```

### 1.3.3. GELENEKSEL KALITIMI REDDEDEN "MODERN OOP" YAKLAŞIMLARI

Bu dillerde klasik class veya kalıtım (inheritance) yapısı yoktur; ancak veri modelleri üzerinde metot tanımlama ve arayüzler (interfaces/traits) sayesinde OOP'nin temel hedeflerini sağlarlar:

**Go (Golang):** class veya extends yoktur. Bunun yerine struct yapılarına metotlar bağlanır ve nesneler arası ilişki kalıtımla değil, kompozisyon (composition) ve dinamik arayüzler (interface) ile kurulur.

**Rust:** Nesne yönelimli kalıtımı tamamen devre dışı bırakmıştır. Veriyi struct veya enum ile tutar, davranışları impl bloklarıyla ekler, arayüz ve çok biçimliliği ise trait mekanizması ile çözer. Yüzeysel olarak (verileri class yerine struct ile tutması ve geleneksel kalıtımı reddetmesi bakımından), Rust dili C diline benzer bir ham veri felsefesinden beslenir; ancak mimari, güvenlik ve yetenekler açısından C’den uzaklaşır ve bambaşka bir boyuta evrilir. 

C ve Rust ortak olarak, nesneleri veya sınıfları şişkin yapılarla (class hiyerarşisiyle) belleğe yüklemez. Her ikisinde de veriler ham ve hafif yapılar olan **struct** içinde saklanır. Arka planda ağır bir **çöp toplayıcı (Garbage Collector)** yoktur, donanıma yakın ve yüksek performanslı çalışırlar. Aşağıda daha önce verilen örnek Rust dilinde verilmektedir.

```rust
// Rust dilinde yapıları tutmak için 'struct' kullanılır
struct BankaHesabi {
    pub hesap_sahibi: String, // Dışarıdan okunabilir public alan
    bakiye: f64,              // Varsayılan olarak private (gizli) bakiye
}

// Davranışları ve metotları struct yapısına bağlamak için 'impl' bloğu kullanılır
impl BankaHesabi {
    // Kurucu metot (Constructor - Genellikle 'new' adlandırılır)
    pub fn yeni(hesap_sahibi: &str, baslangic_bakiyesi: f64) -> BankaHesabi {
        BankaHesabi {
            hesap_sahibi: hesap_sahibi.to_string(),
            bakiye: baslangic_bakiyesi,
        }
    }

    pub fn para_yatir(&mut self, miktar: f64) {
        if miktar > 0.0 {
            self.bakiye += miktar;
            println!("{} TL yatırıldı. Yeni bakiye: {} TL", miktar, self.bakiye);
        }
    }

    pub fn para_cek(&mut self, miktar: f64) {
        if miktar > 0.0 && miktar <= self.bakiye {
            self.bakiye -= miktar;
            println!("{} TL çekildi. Kalan bakiye: {} TL", miktar, self.bakiye);
        } else {
            println!("Yetersiz bakiye veya geçersiz işlem!");
        }
    }

    pub fn bakiye_goster(&self) -> f64 {
        self.bakiye
    }
}

fn main() {
    // Nesne oluşturma (Mutabil / Değiştirilebilir olmalı ki bakiye güncellenebilsin)
    let mut hesap = BankaHesabi::yeni("Ahmet Yılmaz", 1000.0);
    
    hesap.para_yatir(500.0);
    hesap.para_cek(200.0);

    // println!("{}", hesap.bakiye); // HATA VERİR: bakiye alanı private olduğu için dışarıdan erişilemez.
}
```

