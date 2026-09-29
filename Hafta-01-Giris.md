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

```
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

```
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

