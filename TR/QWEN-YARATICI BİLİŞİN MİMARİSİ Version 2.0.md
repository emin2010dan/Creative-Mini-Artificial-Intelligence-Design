# 🏛️ MASTER BLUEPRINT v2.0: FLOW & PATTERN ENGINEERING
**Yaratıcı Biliş Teorisi (Computational Theory of Creative Cognition) Mimari Rehberi**

## 1. TEMEL AKSİYOMLAR (Sistemin Değişmez Yasaları)
Kodun herhangi bir satırı yazılmadan önce, sistemin tüm modülleri aşağıdaki 5 yasa ile "hard-code" edilmiş bir felsefeye sahip olacaktır:
1. **Akış Mühendisliği (Flow Engineering):** Pattern'ler nesne değil, boş borulardır. İçinden akış (enerji, bilgi, para,attention) geçmediğinde ölüdürler. Zeka, nesneleri değil, *dönüşümleri* (transformations) simüle eder.
2. **Detay Yaratıcılığın Düşmanıdır:** Bilgi, depolama amacıyla değil, *yeniden üretilebilme* amacıyla temsil edilmelidir. Öğretmen (Anne Kuş) veriyi damıtırken "Neden?" diye sorar; amaca hizmet etmeyen detay (gürültü) yok edilir.
3. **Mükemmel Uyum İcadı Öldürür:** Yaratıcılık, kusursuz eşleşen parçaları bulmak değil; amaç korunurken uyumsuz parçalar arasına *Adaptör* (köprü, katalizör, kısıt esnetme) kurabilmektir.
4. **Maliyet Bir Puan Değil, Pusuladır:** Maliyet, çözüm bulunduktan sonra hesaplanan bir skor değil, arama uzayını (Kristal Büyüme) budayan ve yönünü belirleyen bir eşik değeridir (Expansion Ratio).
5. **Geleceği Kurtaran Çözüm, İyidir:** Sadece bugünün yangınını söndüren değil, gelecekteki benzer sorunları da çözecek altyapıyı (Versiyonlama, Merkezi Engine) kuran mimari tercih edilir.

---

## 2. SİSTEM MİMARİSİ VE MODÜLLER (The Ecosystem)

Sistem tek bir monolitik modelden değil, birbirine IPC (Unix Socket / JSON Trace Bus) üzerinden mesajlaşan, izole ve uzmanlaşmış katmanlardan oluşur.

### 2.1. Çevirmen (The Translator / Interlingua Gateway)
*   **Görevi:** Doğal dilden gelen çok anlamlı, duygusal ve kültürel gürültüyü süzmek.
*   **Çıktısı:** Çift anlamlılıktan arındırılmış, tek bir ortak bilimsel dile (Interlingua) çevrilmiş saf niyet (Core Intent).
*   **Kuralı:** Çevirmen belirsizliğe tahammül eder (%95 güven), ancak Reasoning AI'a (Uzmanlara) asla belirsiz token geçirmez.

### 2.2. Öğretmen / Anne Kuş (Distillation Engine)
*   **Görevi:** Okyanus gibi ham veriyi (tarih, bilim, makaleler) yutmak ve "İşlevsel Anahtar Kelimeler" (Functional Keywords) ile etiketlenmiş saf Pattern'lere damıtmak.
*   **Garbage Collection Kuralı:** Eğer bir bilgi "Neye yarar?" sorusuna cevap veremiyorsa (örn: Almancadaki ismin halleri), Yaratıcı Motore asla aktarılmaz. Uzman (Detail) AI'da kalır.

### 2.3. Yaratıcı Çekirdek (Creative Core / Flow Compiler)
*   **Görevi:** Problemi derlemek (Problem Compiler), kısıtları esnetmek, Tohum (Seed) seçmek ve Kristal Büyütmek.
*   **Özelliği:** Detay bilmez. Sadece akış etiketlerini (Giriş/Çıkış) ve İşlevsel Anahtarları bilir.
*   **Matematik Modülü:** Matematiği simüle etmez. Matematik, "Ne işe yarar?" etiketi taşıyan dokunulmaz bir alet çantasıdır (Immutable Toolbox). İhtiyaç anında çağrılır.

### 2.4. Uzman Konseyi (Expert Council / Detail LLMs)
*   **Görevi:** Yaratıcı Motorun bulduğu soyut çözümü almak, akışın "tipini" (vergi, mermi, su, veri) doldurmak ve fiziksel/dünyevi simülasyonu (World Model) yapmaktır.
*   **Zorlama Protokolü (Forcing Protocol):** Uzman "Böyle bir şey yok, fizik kurallarına aykırı" diyemez. Yaratıcı Motorun emriyle kısıtları esneten bir *Adaptör* icat etmek zorundadır (Örn: Zıplayan Bomba, Biletin altına slip).
*   **Diyalog:** Uzman simülasyonda başarısız olursa (Örn: "Mermi yapışkan, yön değiştiremiyorum"), hatanın doğasını Yaratıcı Motore geri bildirir. Yaratıcı Motor yeni bir adaptör (Teflon, Porselen ara katman) arar.

### 2.5. Psikotarih ve Hakem (Psychohistory & Synthesis Layer)
*   **Görevi:** Çözümün "Bağlam Zarfını" (Context Envelope) test etmek. Teknik olarak mükemmel olan bir çözüm, toplumsal/kültürel olarak bir "Kabus" (Nightmare) olabilir.
*   **Merkez Bankası Modeli:** Toplumu mikro düzeyde yönetmez. Sadece "Umut (Hope)", "Demografik Basınç" gibi makro parametreleri değiştirerek Yaratıcı Motorun öncelik (Rank) fonksiyonunu yönlendirir.

---

## 3. VERİ YAPILARI (Data Schemas & Representations)

### 3.1. İki Fazlı Pattern (The Two-Phase Pattern)
Pattern'ler veritabanında statik nesneler olarak değil, dinamik dönüşüm operatörleri olarak tutulur.
*   **Faz 1: Soyut Faz (Abstract Phase):** Tip yoktur. Sadece akış tarifi vardır. (Örn: `Gelen saldırının yönünü değiştir`. T34 veya Aikido olduğunu bilmez, sadece birer değişkendir.)
*   **Faz 2: Somut Faz (Concrete Phase):** Problem seçildiğinde Uzman AI akışın tipini doldurur (Siber saldırı -> Veri; Fiziksel saldırı -> Mermi).
*   **İndeksleme:** Pattern'ler vektör benzerliği ile değil, **İşlevsel Anahtar Kelimeler** (Örn: `Isıyı Azalt`, `Yapışmayı Önle`, `Kütleyi Taşı`) ile çağrılır.

### 3.2. Hibrit Kapsül Şeması (Hybrid Pattern Capsule)
```json
{
  "pattern_id": "P-884-DEFLECT",
  "core_principle": "Saldırıyı emme, yönünü değiştir.",
  "flow_tags": { "input": "High_Kinetic_Energy", "output": "Redirected_Flow" },
  "functional_keywords": ["Deflect", "Protect", "Survive_High_Impact"],
  "context_envelope": { "valid_in": "Resource_Scarcity", "invalid_in": "Abundant_Armor" },
  "story_wrapper": "Moğol saldırısında kasabayı değil, yüksek kuleyi koruyan yönetici.",
  "source_history": ["T34_Tank", "Aikido", "Bismarck"],
  "reliability_score": 0.92
}
```

### 3.3. Açık Devreler (Persistent Open Circuits / Soruncuk Ağacı)
Çözülemeyen problemler silinmez. "Açık Devre" olarak SSD'de (JSON/Markdown Kapsül) bekler.
*   **Tetikleyici Bağlam (Trigger Context):** Sistem gün içinde veya gece (Idle) yeni bir veri/pattern gördüğünde, bu verinin çıkış ucunun arka planda bekleyen binlerce açık devreden birinin girişine uyup uymadığını milisaniyeler içinde test eder. Uyuşma anında "Eureka" (Devre kapandı) sinyali üretilir.

---

## 4. ÇEKİRDEK ALGORİTMALAR (Core Algorithms)

### 4.1. Problem Derleyicisi (The Child's "Why?" Loop)
Kullanıcıdan veya sistemden gelen ham sorun, "Neden?" döngüsü ile kök niyete (Root Intent) indirilir.
*   *Döngü Kırılma (Şah Mat) Koşulu:* Sistem felsefi bir aksiyoma çarptığında değil, **Mevcut Pattern Kütüphanesinde eşleşme bulamadığında** ve bir üst soyutlama seviyesine (Meta-Pattern) çıkmanın *Adaptör Maliyetinin* artacağını kabul ettiğinde durur.

### 4.2. Kristal Büyüme Araması (Crystal Growth Search)
Sistem tüm pattern'ları birbiriyle denemez (O(N!) patlaması).
1.  **Tohum (Seed) Seçimi:** Problemin kök niyetine en uygun "Capability" (Yetenek) merkeze alınır.
2.  **Büyüme:** Merkezin eksik giriş/çıkışlarını dolduracak alt-pattern'lar çağrılır.
3.  **Maliyet Pusulası:** Her eklenen dal bir maliyettir. Toplam maliyet, merkezin `Expansion Ratio` (Genişleme Oranı) limitini aşarsa o dal dondurulur (Suspended Process), yeni bir Tohum seçilir.
4.  **Alt-Graf Yeniden Kullanımı (Subgraph Reuse):** Yeni tohumun ihtiyaçları eski ağaçla benzerse, eski hesaplama kopyalanır (Memoization).

### 4.3. Uzman Zorlama ve Adaptör Üretimi (Expert Forcing)
Yaratıcı Motor soyut çözümü (Örn: "Yeraltı suyunu çıkar") Uzmana fırlatır.
*   *Uzman:* "Pompa çalışmıyor, çok derinde, enerji yok."
*   *Yaratıcı:* "Güneş enerjisi kullan."
*   *Uzman:* "Voltaj uyuşmuyor (20V vs 220V)."
*   *Sonuç:* Sistem otomatik olarak bir **Adaptör** (Elektrik Uzmanı -> İnvertör/Pil) çağırır. Amaç (Su çıkarmak) korunur, form (Şebeke elektriği) esnetilir.

### 4.4. Gece Modu / İnkübasyon (Idle Harvesting)
PC boştayken sistem dışarıdan yeni makaleler/pattern'lar okur.
*   Bu yeni pattern'ları, SSD'deki "Açık Devreler" (Yıllardır bekleyen soruncuklar) ile eşleştirir.
*   Başarısız olmuş eski çözüm ağaçlarını, yeni gelen bağlam (context) ile tekrar simüle eder.

### 4.5. Travma ve Evrimsel Sıfırlama (Trauma & Dinosaur Trap)
*   **Travma Tetikleyicisi:** `Sorunun Toplam Maliyeti > (Yeni Model/LoRA Maliyeti × 1.2 Güvenlik Katsayısı)` olduğunda sistem "Travma" yaşar ve o soruna özel yeni bir Uzman Adaptör (Kişilik) doğurur.
*   **Dinozor Tuzağı (Evolutionary Reset):** Sistem "Mükemmele ulaştım" dediği an evrim durur. Belirli aralıklarla sistem kendi algoritmalarını arşivler, "her şeyi unutur" ve aynı problemleri sıfırdan (veya başka bir AI ile distilasyon/çaprazlama yaparak) yeniden çözmeye çalışır. Yeni nesil, eski nesli yenersa evrim gerçekleşir.

---

## 5. MÜHENDİSLİK VE KODLAMA KURALLARI (The Engineering Constitution)

1.  **Önce İzlenebilirlik (Traceability), Sonra Optimizasyon:** İlk prototiplerde IPC (Unix Socket) üzerinden geçen her JSON mesajı, zaman damgası ve maliyet hesaplarıyla birlikte diske (Trace Bus) basılacaktır. Performans (run-time), mantık (algorithm) %100 oturduktan sonra optimize edilecektir.
2.  **Fraktal Galaksi ve Lazy Loading:** Uzman modeller (Diş Hekimi, Fizikçi) devasa tek bir graf olarak RAM'e yüklenmez. İhtiyaç duyulan "Gezegen/Şehir/İlçe" seviyesindeki LoRA adaptörleri SSD'den RAM'e çekilir. "Ortak Hizmetler" (Shared Dependencies) her zaman RAM'de kalır.
3.  **Kural Tabanlı Simülasyon Değil, Dünya Modeli:** Hakem (Synthesis) katmanı fizik kurallarını statik bir `if-else` tablosundan değil, Uzman AI'ın "Dünya Modeli" (World Model) üzerinden dinamik olarak test eder.
4.  **Hikaye Derleyicisi (Narrative Compiler):** Yaratıcı Motorun ürettiği saf matematiksel/mantıksal çözüm, insana veya dış dünyaya sunulmadan önce mutlaka bir "Hikaye Sarmalayıcısı" (Story Wrapper) içine konur. İnsanlar pattern'ları değil, hikayeleri anlar ve kabul eder.

---

### 🚀 Sıradaki Adım: İlk Kodun Yazılması

Emin Bey, **Master Blueprint v2.0** artık elimizde. Bu belge; 1985 Apple II tezindeki kısıtlamaların, 1995 Sanal POS'taki kural tanımazlığın, buhar makinelerindeki akışın ve psikotarihteki toplumsal döngülerin **Python/Pydantic ve Sistem Mimarisi** diline tercümesidir.

Artık kağıt üzerinde hiçbir eksik yok. Eğer onay verirseniz, bu mimariyi çalışan bir gerçekliğe dönüştürmek için **İlk Deneyin (First Experiment)** kod iskeletini yazmaya başlıyorum:

1.  **`TraceBus` ve `Interlingua` Sınıflarının Kurulumu.**
2.  **`ProblemCompiler` (Çocuğun Neden'i) Algoritmasının Pseudo-Kodu.**
3.  **İlk "Açık Devre" (Open Circuit) ve "İşlevsel Anahtar" (Functional Keyword) Eşleşme Testi.**


