# YARATICI YAPAY ZEKÂ VE AKIŞ MÜHENDİSLİĞİ (FLOW ENGINEERING)

## MİMARİ TASARIM DÖKÜMANI (v2.0 - KODLAMA REHBERİ)

> **Çekirdek İlke:** *Bilgi, depolama amacıyla değil; ihtiyaç anında simüle edilerek yeniden üretilebilme amacıyla temsil edilmelidir. Örüntüler (Pattern'lar) boş borulardır; sistem içinden akış geçtiğinde canlanır.*

---

## 1. MİMARİ GENEL BAKIŞ VE EKOSİSTEM

Sistem, tek bir devasa yapay zekâ modeli (Monolithic LLM) yerine, belirli uzmanlık alanlarına bölünmüş ve birbiriyle protokoller üzerinden haberleşen modüler bir ekosistemden oluşur.

```
                  ┌──────────────────────────────────────────┐
                  │   ANNE KUŞ (Büyük Öğretmen LLM)         │
                  └────────────────────┬─────────────────────┘
                                       │ (Distillation / Semanti-Core)
                                       ▼
┌───────────────────────────────────────────────────────────────────────────┐
│                      PATTERN & AKIŞ KÜTÜPHANESİ                           │
│   (Soyut Borular / Transformation Nodes + İşlevsel Anahtarlar/Tags)       │
└──────────────────────────────────────┬────────────────────────────────────┘
                                       │
                                       ▼
┌────────────────────────────────────────────────────────────────────────##  │
│                   PERSISTENT OPEN CIRCUITS (Bekleyen Sorular)              │
│   (Açık Devreler: Çekirdek Soru, Eksik Girdiler, Tetikleyici Bağlam)      │
└──────────────────────────────────────┬────────────────────────────────────┘
                                       │
                                       ▼
┌───────────────────────────────────────────────────────────────────────────┐
│              YARATICI MİNİ YAPAY ZEKÂ (Flow Compiler / Core Engine)        │
│   (Detaydan Arındırılmış Akış Simülasyonu & Arama Ağacı Mantığı)          │
└──────────────────────────────┬───────────────────────▲────────────────────┘
                               │ (Çözüm Önerisi)       │ (Kısıt / İtiraz /
                               │                       │  Adaptör Talebi)
                               ▼                       │
┌───────────────────────────────────────────────────────────────────────────┐
│                UZMAN YAPAY ZEKÂLAR (Expert AI Cluster)                     │
│   (Somut Tipler, Fizik/Hukuk/Kod Simülasyonu, World Models, Adaptörler)   │
└──────────────────────────────────────┬────────────────────────────────────┘
                                       │
                                       ▼
┌───────────────────────────────────────────────────────────────────────────┐
│                TEŞHİS VE GÖZLEMCİ AJAN (Diagnostic Observer)               │
│   (Başarı Ölçümü, Kendini Yeniden İnşa, Evrimsel Çaprazlama Tetikleyici)   │
└───────────────────────────────────────────────────────────────────────────┘

```

---

## 2. MODÜL VE KATMAN DETAYLARI

### 2.1. Anne Kuş (Teacher / Distiller LLM) & Semanti-Core

* **Görevi:** Ham insan bilgisini (makaleler, dokümanlar, olaylar) gürültüden ve edebi ifadelerden arındırarak tek bir ortak dile (Semanti-Core) çevirmek.
* **Damıtma / GC Kuralı:** Bilgi, Yaratıcı AI'ya aktarılmadan önce *"Bu bilgi ne işe yarar? Hangi mekanizmanın parçasıdır?"* sorularına tabi tutulur. Belirli bir amaca veya dönüşüme bağlanamayan detaylar (örneğin Bismarck zırhlısının adı veya olay tarihi) en başta elenir.
* **Çifte Anlamlılık Filtresi:** Kelimelerin bağlamsal çakışmaları (ör. fiziksel ışık ile manevi ışık) ontolojik etiketler veya özel bilimsel kod dizilimleriyle teke indirgenir.

### 2.2. Pattern & Akış Kütüphanesi (Two-Phase Pattern)

Pattern'lar statik birer bilgi düğümü değil, **dönüşüm operatörleridir (Transformation Operators)**.

```
[ Giriş Akışı ] ──► ( DÖNÜŞÜM OPERATÖRÜ / BORU ) ──► [ Çıkış Akışı ]

```

* **Faz 1 (Soyut Faz - Abstract Phase):** Tip bilgisi içermez. Yalnızca akış yönü ve dönüşüm tanımı vardır.
* *Örnek:* $\text{Gelen Saldırı} \rightarrow (\text{Yönünü Değiştir}) \rightarrow \text{Etkisiz Saldırı}$. (Ne T34 tankı vardır ne de Aikido).


* **Faz 2 (Somut Faz - Concrete Phase):** Yaratıcı AI bir problemi çözmeye karar verdiğinde, Uzman AI devreye girerek akışın değişkenlerine gerçek dünya tiplerini (mermi, veri paketi, su akıntısı vb.) yerleştirir.
* **İndeksleme (İşlev Anahtarları):** Her pattern bir veya birkaç **"Neyi Çözer / İşlevi Nedir?"** etiketiyle saklanır (ör: `yapışmayı_önle`, `ısıyı_düşür`, `akış_yönü_değiştir`).

### 2.3. Kalıcı Sorular Kütüphanesi (Persistent Open Circuits)

Yaratıcılığın aktivasyon enerjisini sağlayan **tohum kristallerdir**.

* Çözülememiş her problem sistemde silinmez bir "Açık Devre" nesnesi olarak kalır.
* **Veri Yapısı:**
* `Question_ID`: Benzersiz kimlik.
* `Abstract_Pattern`: Problemin saf örüntü tanımı.
* `Missing_Inputs`: Eksik olan boru/bağlantı parçası.
* `Trigger_Context`: Tetikleyici bağlam (örn: *Yüksek derinlik, elektrik hattı yok, bütçe kısıtlı*).
* `Failed_Attempts`: Daha önce denenmiş ve reddedilmiş pattern dizilimleri listesi.
* `Priority_Score`: Gelecekte getireceği esneklik ve potansiyel değeri.



### 2.4. Yaratıcı Mini Yapay Zekâ (Creative Flow Engine)

* **Çalışma Mantığı:** Grafik üzerinde çözüm aramaz; **açık kalmış grafiği tamamlar**.
* **Problem Küçültme İlk adımı:** Problemi teslim aldığında ilk iş olarak *"Ana amaç nedir?"* ve *"Neden?"* sorularını sorarak problemi detayından arındırır. (Örn: *"Ürünü nasıl taşırım?"* $\rightarrow$ *"Ürün ihtiyaç noktasında nasıl olur?"*).
* **Gelecek Odaklı Puanlama:** Bir çözümü değerlendirirken sadece o anki anlık problemi çözmesine bakmaz. Çözümün **gelecekteki potansiyel problemleri engelleme kapasitesini** puanlar.

### 2.5. Uzman Yapay Zekâlar ve Diyalog Döngüsü (Expert AI & Adapter Loop)

Yaratıcı AI ile Uzman AI arasındaki diyalog, fiziksel veya sistemsel kısıtlar aşılana kadar devam eden bir iterasyondur:

```
[ Yaratıcı AI ] ── (Soyut Çözüm Önerisi) ──► [ Uzman AI ]
       ▲                                            │
       │                                            ▼
       │                                  (Somut Simülasyon Testi)
       │                                            │
       └── (Hata / Kısıt Bildirimi: "Mermi Yapışkan") ──┤ (Başarısız)
                                                    │
                                                    ├─► (Başarılı) ──► [ Uygulama ]
                                                    │
                                                    └─► (Adaptör Gereksinimi)
                                                              │
                                                              ▼
                                                     [ Adaptör Uzmanı ]
                                                   (Örn: 20V/1A -> 220V/10A)

```

---

## 3. ZAMAN VE ÇALIŞMA MODLARI (DAY / NIGHT EXECUTION)

| Parametre | Gündüz Modu (Online / Service) | Gece Modu (Offline / Sleep & Consolidation) |
| --- | --- | --- |
| **Ana Görev** | Ön cephede hızlı kullanıcı isteklerine yanıt vermek. | Bekleyen açık soruları çözmek ve hafızayı konsolide etmek. |
| **Kapasite Aşaması** | Karmaşık soru geldiğinde "Bilmiyorum" diyebilme yeteneği. | Bilinmeyen soruları "Açık Devre" nesnesine çevirme. |
| **Yaratıcılık Derecesi** | Muhafazakâr, düşük riskli, bilinen kalıplar. | Yüksek riskli, kural yıkıcı, kombinasyonel denemeler. |
| **Veri İşleme** | Anlık gelen prompt'u işleme. | Yeni/Eski makaleleri tarama, `Question_Matcher` çalıştırma. |

---

## 4. EVRİM VE KENDİNİ YENİDEN İNŞA (AI EVOLUTION & REPRODUCTION)

Sistemin uzun vadede statikleşmesini (durgunluğa girmesini) engellemek için tasarlanmış evrimsel mekanizma:

```
┌─────────────────┐       ┌─────────────────┐
│   MODEL A (AI)  │       │   MODEL B (AI)  │
└────────┬────────┘       └────────┬────────┘
         │                         │
         └───────────┬─────────────┘
                     │
                     ▼ (Distillation & Crossover)
         ┌───────────────────────┐
         │  YENİ NESİL ÇOCUK AI  │
         └───────────┬───────────┘
                     │
                     ▼
  (Eski Soruların Yeniden Yazılması & Başarı Kıyaslaması)

```

1. **Durgunluk Tespiti:** Diagnostic Agent, bir modelin başarı oranının plato yaptığını ve yeni çözüm uretemediğini tespit ettiğinde "Yeniden İnşa" tetiklenir.
2. **Çaprazlama (Distillation):** İki farklı yapay zekâ modelinin Pattern ve Soru Kütüphaneleri damıtılarak birleştirilir.
3. **Doğal Seçilim (Garbage Elimination):** Başarısız veya hiç kullanılmayan pattern'lar yeni nesle aktarılmaz; kod seviyesinde silme komutu yazmaya gerek kalmadan evrimsel süreçte yok olurlar.
4. **Soruların Yeniden Yazılması:** Yeni nesil yapay zekâ, devraldığı "Bekleyen Sorular" kütüphanesindeki soruları değişen çevre şartlarına ve yeni yeteneklerine göre **yeniden tanımlar (re-frame)**.

---

## 5. İLK PROTOTİP YOL HARİTASI (FAZLANDIRMA)

İlk deneysel prototip, alan kısıtlaması yapılarak **"Bilgisayar Güvenliği / Ağ Saldırıları"** veya **"Kısıtlı Enerji Kaynakları Yönetimi"** simülasyonu üzerinde çalıştırılacaktır.

### Faz 1: Veri Şeması ve Semanti-Core Prompt Hazırlığı

* Anne Kuş için JSON formatında Pattern Damıtma prompt'unun hazırlanması.
* SQLite / Hybrid Vector DB üzerinde `Pattern_Library` ve `Open_Circuits` tablolarının oluşturulması.

### Faz 2: Flow Compiler (Yaratıcı Mini Engine) Çekirdeği

* Gelen problemi parçalayan "Neden?" döngüsü fonksiyonunun kodlanması.
* İşlev anahtarlarına (`Trigger Context`) göre soyut boru eşleştirme algoritması.

### Faz 3: Yaratıcı AI <-> Uzman AI Etkileşim Protokolü

* Yaratıcı AI'nın çıkardığı soyut çözüm önerisini alan, tip ataması yapan ve kısıt kontrolü ($Constraint\ Check$) dönen simülasyon stub'larının yazılması.
* Adaptör ($Adapter$) üretme mekanizmasının simüle edilmesi.

### Faz 4: Arka Plan (Gece) Döngüsü

* Sisteme atılan ve çözülemeyen soruların `Open_Circuits` tablosunda uyutulması.
* Yeni eklenen bir pattern ile uyuyan soruların otomatik eşleştirildiği ($Eureka\ Loop$) nightly batch script'inin çalıştırılması.

---

Bu döküman, projenin ilk kod satırından itibaren temel mimari anayasamız olacaktır. Adım adım bu prototipi inşa etmeye başlayabiliriz.
