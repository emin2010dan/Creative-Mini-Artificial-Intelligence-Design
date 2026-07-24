# Yaratıcı Biliş Teorisi — Tasarım Çerçevesi v0.4

**Tarih:** 2026-07-24
**Önceki sürümler:** v0.1, v0.2, v0.3
**Statü:** Kod yazımı için rehber doküman
**Yazar(lar):** Emin Danışman + Mavis (Mavis/MiniMax)
**Not:** Bu bir *yaşayan dokümandır*. Tamamen bitmeyecek — Emin'in ifadesiyle, "gelecekte en değerli şey bu pattern'lar olacak."

---

## 0. Konumlandırma

Bu, bir AI mimarisi değil. Bir **Yaratıcı Biliş Teorisi** (Computational Theory of Creative Cognition) inşasıdır.

**Temel tez:** Yaratıcılık, detaydan arındırılmış dönüşüm bilgilerinin (*pattern*) aranması, akış etiketleriyle birleştirilmesi, uzman simülasyonuyla olgunlaştırılması ve yan ürünlerinin tüketilmesi sürecidir.

**Temel ilke:** "Önce çalışan sistemi kur, sonra onun teorisini çıkar."

**Bu doküman ne değildir:**
- Bitmiş bir spesifikasyon değil
- Bir akademik tez değil
- Bir ürün roadmap'i değil

**Bu doküman nedir:**
- Kod yazacak kişinin önünde tutacağı *rehber harita*
- Karar anlarında "Emin bunu nasıl düşünürdü?" sorusuna cevap
- Sistemin *neden* böyle tasarlandığının kaydı

---

## 1. Temel Kavram: Flow Engineering

### 1.1 İsim Değişikliği

Daha önce "Pattern Engineering" diyorduk. Artık isim değişti:

> **Pattern = boş boru. Yaşayan şey, içinden geçen akış.**

Bu yüzden proje artık **Flow Engineering**'dir. Pattern, akışın geçtiği *dönüşüm operatörü*. Akış, *yaşayan şey*. Program veri ile yaşar, pattern akış ile yaşar.

### 1.2 "Anladım" Anı

Bir konuyu *gerçekten* anladığının sinyali:
1. Zihninde simüle edebiliyorsun (formül değil, olay)
2. Problemi de simüle edebiliyorsun (pattern grafiğine çevirirsin)
3. İki grafiği üst üste koyarsın
4. Eksik düğümleri doldurursun
5. Yapı tutarlıysa çözüm oluşur

**Çözümü aramıyorsun, grafiği tamamlıyorsun. Çözüm yan ürün.**

Bu, matematikte yapamadığın şey (matematik = saf sembol, akış yok). Yapay zeka da matematikte aynı kısıtla karşılaşacak, bu yüzden matematik **alet çantası** olarak kullanılacak, *simüle edilmeyecek*.

### 1.3 Garbage Collector Nereye Koyulacak

Senin beyninde garbage collection **çalışma anında** çalışıyor: bağlantısız bilgi siliniyor. Yapay zekada bu *çalışma anında* yapılmaz. Yapay zekada:

> **Damıtma anında "neden?" diye sor, amacı olmayanı ele, çalışma anına sadece işlevi belli olan bilgiyi gönder.**

Yani:
- **Uzman AI'larda:** Detaylı bilgi tutulur. Almancası olan öğrenci gibi.
- **Yaratıcı AI'da:** Sadece işlevi belli, bağlanmış, amaçlı bilgi. Yabancı sözlük gibi amaçsız bilgi oraya hiç gitmez.

---

## 2. İki Fazlı Pattern: Soyut + Somut

Bir pattern iki fazda bulunur:

### Faz 1 — Soyut (Pattern Üretim Anı)
Pattern *değişken gibidir*. Tipi yok.
- "Saldırı yönünü değiştir" (T34 yok, Aikido yok, sadece tarif)
- "Yakıt + oksijen → dönme hareketi" (buhar motoru, ama yakıtın ne olduğu belli değil)

Bu fazda pattern bir *fonksiyon imzası* taşır. İçi henüz doldurulmamış.

### Faz 2 — Somut (Kullanım Anı)
Problem seçilince akışın tipi belli olur. Uzman AI tipi doldurur.
- Bilgisayar güvenliği → akış **veri** olur
- Gelen mermi → akış **mermi** olur
- Sulama → akış **su** olur

Uzman simüle eder. Çalışmıyorsa neden olduğunu geri bildirir. **Test simülasyonun kendisidir**, önceden hesaplanmış bir formül değil.

### 2.1 Tip Değişimi Örneği: Tarla Sulama

```
Yaratıcı: Tarlalar susuz → yer altı suyu kullan
Uzman:     Çok derinde pompa çalışmıyor
Yaratıcı: Dalgıç pompa
Uzman:     Enerji lazım
Yaratıcı: Güneş enerjisi
Uzman:     Güneş 20V 1A veriyor, dalgıç pompa 220V 10A istiyor
Yaratıcı: Adaptör lazım
Elektrik uzmanı: Pil besle, akım dönüştür
```

Görüldüğü gibi akış tipi *çözüm boyunca değişiyor*: su → elektrik → akım/voltaj → tekrar su (pompalama).

---

## 3. Pattern Şeması v0.4 (Kod Yazımına Hazır)

```yaml
pattern:
  # === KİMLİK ===
  id: <benzersiz_kimlik>
  label: <tek-anlamlı_isim>
  pattern_type: <atomik | bileşik>
  source_lifecycle_stage: <candidate | verified | frequently_used | core | deprecated | archived>
  
  # === İŞLEV ANAHTARI (NE İŞE YARAR) ===
  function_key:
    primary: "<ana işlev>"           # Örn: "yapışmayı önler"
    secondary: ["<yan işlev>", ...] # Örn: ["korozyon direnci sağlar"]
    problem_domain: ["<alan>", ...] # Örn: ["savunma", "yüzey kaplama"]
  
  # === AKIŞ ETİKETLERİ (GİRİŞ / ÇIKIŞ) ===
  flow_tags:
    input:
      - {flow_type: "<akış tipi>", quantity: "...", quality: "..."}
      # Örn: {flow_type: "yakıt", quantity: "yüksek enerji yoğunluğu"}
    output:
      desired:
        - {flow_type: "<istenen>", quantity: "..."}
        # Örn: {flow_type: "dönme hareketi", quantity: "sürekli"}
      undesired:
        - {flow_type: "<istenmeyen>", severity: 0.0-1.0, mitigation: "..."}
        # Örn: {flow_type: "CO2 emisyonu", severity: 0.7, mitigation: "karbon yakalama"}
  
  # === DÖNÜŞÜM ===
  transformation:
    principle: "<kısa prensip>"
    mechanism: ["<adım 1>", "<adım 2>", ...]
    physics_or_logic_refs: ["<formül veya referans>"]
    # Faz 1 soyut — tipler burada doldurulmaz
    # Faz 2 somut — uzman simüle edince doldurulur
  
  # === BAĞLAM ===
  context_envelope:
    culture: [..., applicability_score: 0.0-1.0]
    climate: [...]
    religion: [...]
    law: [...]
    technology_level_required: <min_seviye>
    economic_assumptions: [...]
    ethics: [...]
    update_frequency: <"100M yıl" | "10 yıl" | "5-11 yıl" | "indefinite">
    half_life: <"100M yıl" | "1 nesil" | ...>
  
  # === HİYERARŞİ (Fraktal Galaksi) ===
  fractal_position:
    galaxy_arm: <uzman adaptör>
    solar_system: <alt-uzmanlık>
    planet: <konu>
    shared_services: ["<ortak bilgi>", ...]
  
  # === YAŞAM DÖNGÜSÜ ===
  lifecycle:
    created_at: <date>
    last_used: <date>
    usage_count_30d: <int>
    success_rate: 0.0-1.0
    score: <0-100>
    verification:
      source: "<kaynak>"
      llm_consensus: 0.0-1.0
      expert_audits: <int>
  
  # === ERİŞİM ===
  human_story: "<insanın anlayacağı hikâye>"
  
  # === İLİŞKİLER ===
  relations:
    combines_with: [{pattern_id: "...", operation: "additive | hierarchical | modulation | sequencing"}]
    requires_adapters: [{adapter_type: "voltage_converter | pressure_reducer | ...", mismatch_dimension: "..."}]
    conflicts_with: [...]
    supersedes: [...]
```

### 3.1 İndeksleme Kuralları

**İki anahtar ile indekslenir:**

1. **Function Key** → "Bu ne işe yarar?" sorusuna cevap verir. Arama bu anahtarla başlar.
2. **Flow Tag** → "Bunun girişi ne, çıkışı ne?" sorusuna cevap verir. Birleştirme bu etiketle olur.

**Birleşme kuralı:** A.output.flow_type == B.input.flow_type ise → bağlanabilir. Etiket uyuyorsa Lego gibi takılır. Uymuyorsa adaptör gerekir.

---

## 4. Damıtma Pipeline'ı (Bootstrap)

Yaratıcı motor kendi kendine doğmaz. Bir *öğretmen LLM* tarafından eğitilir. Pipeline şu sırayla çalışır:

### Adım 1: Çeviri (Semanti-Core)
```
Kullanıcı dili → ortak dil (çift anlamlılık yok)
- Türkçe → Semanti-Core
- Çince → Semanti-Core
- İngilizce → Semanti-Core
```

**Semanti-Core kuralları:**
- Her kelimenin *tek bir anlamı* var
- Belirsiz kelimeler etiketlenir: `ışık[fizik]`, `ışık[edebiyat]`, `ışık[metafor]`
- Etiketleme karakteri: orijinal veride *hiç geçmemiş* bir karakter kullan. Mecburen köşeli parantez kullanılacaksa, orijinal verideki köşeli parantezler çift köşeli parantezle değiştirilir.

**Çevirmen AI:** Önce mevcut çeviri LLM'lerine çift anlamlılık konusunda ek eğitim. Başlangıçta en ucuz yol bu.

### Adım 2: Pattern Çıkarma (Distilasyon)
Öğretmen LLM (büyük, merkezi), her bilgi parçasını pattern'a çevirirken şu soruyu sorar:

> **"Bu bilgi neden var, neyi çözer?"**

Cevabı olmayan bilgi → elenir (damıtma anında garbage collection). Cevabı olan bilgi → pattern şemasına dönüşür.

**Pattern çıkarma kuralı (Emin'in yöntemi):**
1. Kaynak bilgiyi al (ör. Bismarck zırhlısı hikayesi)
2. Sor: "Buradan alınacak ders ne?"
3. Cevabı *generic* yap: Bismarck yok, zırhlı yok, Almanya yok — sadece saf örüntü ("kısıtlı kaynakla maksimum koruma istiyorsan tüm kaynağı hayati olana ver")
4. Kullanılabileceği yerleri etiketle: "koruma isteyen her yer"
5. İşlev anahtarını + akış etiketini yaz

### Adım 3: Repository Organizasyonu
```
Physics Patterns    (güncelleme: ~100M yıl)
Technology Patterns (güncelleme: ~10 yıl)
Civilizational Patterns (güncelleme: ~5-11 yıl, kohort lag)
```

Her katman *farklı kaynaklardan* distill edilir.

### Adım 4: Mini Yaratıcı Motor Eğitimi
Distillenmiş pattern'larla mini motor eğitilir. Motor *pattern'larla konuşur*, doğal dille değil.

### Adım 5: İlk Deney
Bir test problemi seçilir. 1985 tezi veya benzeri. Sonuçlar gözlemlenir, algoritma düzeltilir.

---

## 5. Yaratıcı Motor: 6 Modül

```
┌─────────────────────────────────────────────────────────────┐
│ [1] PROBLEM COMPILER                                         │
│     Kullanıcı isteği → Problem Pattern                       │
│     + Refactoring (aynı amaç, farklı tanım)                  │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [2] FUNCTION KEY MATCHER                                     │
│     Problem Pattern → işlev anahtarı → aday pattern'lar      │
│     (yapışmayı önler, ısıyı azalt, dönme ister, ...)         │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [3] FLOW COMBINER (Crystal Growth Search)                     │
│     Aday pattern'ları akış etiketlerine göre birleştir:      │
│     - Capability Seed seç                                    │
│     - Crystal büyüt (eksik input'ları doldur)                │
│     - Adaptör ekle (etiket uyuşmazsa)                        │
│     - Failure Driven Expansion (hata noktasından büyü)       │
│     - Subgraph Reuse (memoization)                            │
│     - Expansion Ratio > eşik → DUR, seed değiştir            │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [4] EXPERT SIMULATION (Tip Doldurma + Doğrulama)              │
│     Her aday çözüm için uzman AI:                            │
│     - Akış tipini somutlaştır (Faz 2)                         │
│     - Simüle et (fiziksel, ekonomik, hukuki)                 │
│     - Çalışmıyorsa neden olduğunu geri bildir                │
│     - Adaptör gerekirse adaptör öner                          │
│     - Yaratıcı ile diyalog kur (kabul edilene kadar)          │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [5] EVALUATION ENGINE                                        │
│     - Cost Vector (8 boyut: para, enerji, zaman, risk,       │
│       çevre, toplumsal, hukuki, güven)                       │
│     - Hakem (aksiyomatik kalkan)                              │
│     - Psikotarih motoru (toplumsal kabul)                    │
│     - Failure Mode analizi                                    │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [6] PATTERN CRYSTALLIZATION + AFFECT MODULATION                │
│     - Başarılı çözüm → Composite Pattern                     │
│     - Affect parametreleri: arama_derinliği,                  │
│       birleştirme_cüreti, itiraz_ağırlığı, uyku_eşiği         │
│     - Din/Psikotarih karar mekanizması                        │
└─────────────────────────────────────────────────────────────┘
```

### 5.1 Crystal Growth — Operasyonel Detay

**Seed seçimi:**
- Function Key ile adaylar bulunur
- Rank skoru en yüksek aday seed olur
- Rank = (kullanım_30d × 0.3) + (başarı_oranı × 0.3) + (1/expansion_cost × 0.2) + (novelty × 0.2)

**Büyüme adımı:**
- Seed'in flow_tag.output'u aranır
- Hangi pattern'ın flow_tag.input'u buna uyuyor? → adaylar
- Adaylardan biri seçilir (rastgele + affect parametresi etkisi)
- Bağlanır, yeni eksik input'lar ortaya çıkar
- Döngü devam eder

**Adaptör ekleme:**
- flow_tag uyuşmuyorsa → adaptör pattern ara
- Adaptör de bir pattern (flow_tag giriş/çıkış dönüşümü)
- Örn: Voltage Converter (20V AC → 220V DC)

**Expansion Ratio kontrolü:**
```
toplam_maliyet / seed_maliyet > eşik → DUR
```
- Halka 1 (çekirdek): eşik = 1.5
- Halka 2 (iç kol): eşik = 2.0
- Halka 3 (dış kol): eşik = 2.8
- Halka 4 (uyku): sınırsız

**Failure Driven Expansion:**
- Çözüm son değerlendirmede < %80 güven
- En zayıf halka tespit edilir (maliyet, kapsam, kabul)
- Sadece o halkaya yeni pattern eklenir

**Subgraph Reuse:**
- Önceki çözüm ağacının alt kısımları saklanır
- Yeni seed'in input'ları eski seed'le benziyorsa → ağaç kopyalanır

### 5.2 Uzman Simülasyonu — Detay

Yaratıcı motor *somut tipi* bilmez. Tipi uzman doldurur. Örnek:

```
Yaratıcı:  Çözüm = "saldırı yönünü değiştir" + "çelik yüzey"
Uzman:     Mermi yapışkan mı?
Yaratıcı:  Bilmiyorum
Uzman:     Yapışkan → yön değiştirmez
Yaratıcı:  Teflon kaplama?
Uzman:     Dayanıksız
Yaratıcı:  Pütürlü yüzey?
Uzman:     Olabilir
Yaratıcı:  Porselen ara katman?
Uzman:     Belki
```

Uzman, kendi alanında **fizik kanunlarını, malzeme bilgisini, ekonomik gerçekleri** bilir. Yaratıcı *bilmek zorunda değil* — sadece denemek zorunda.

### 5.3 Yapışkan Mermi Tipi Diyalog Yapısı

```
1. Yaratıcı → Uzman: "Şu pattern kombinasyonunu dene"
2. Uzman → simüle et → sonuç üret
3. Sonuç olumsuz → Uzman: "Çalışmıyor, neden: [fiziksel engel]"
4. Yaratıcı → alternatif pattern dene
5. Döngü: kabul edilene kadar
```

Bu diyalog **gece yaratıcı AI** modunda çalışır (PC boştayken, yavaş ama dikkatli).

---

## 6. Etiketli Akış Birleşmesi (Birleştirme Algoritması)

**Temel kural:** İki pattern'ın birleşip birleşemeyeceğini belirleyen şey, *flow_tag uyumu*.

```
pattern_A.output.desired.flow_type == pattern_B.input.flow_type
→ Birleşebilir (etiket eşleşti)
```

### 6.1 Örnekler

| Birleşim | Çıktı |
|---|---|
| Kömür arabası + hava + buhar motoru + tekerlek | Lokomotif |
| Nükleer reaktör + buhar motoru + uskur | Nükleer gemi motoru |
| Nükleer reaktör + buhar motoru + pervane | Nükleer motorlu uçak (Rus seyir füzesi) |
| Yapışma önleyici + çelik yüzey | Yapışmayan zırh |
| Yön değiştirici + savaş gemisi | Yön değiştiren zırh sistemi |

**Lego gibi:** Etiket uyuyorsa takılır. Uymuyorsa adaptör gerekir. Adaptör de bir pattern (flow dönüştürücü).

### 6.2 Adaptör Pattern Türleri

```
voltage_converter         — V/A dönüşümü
pressure_reducer          — basınç düşürme
frequency_matcher         — hız uyumu
format_translator         — veri format dönüşümü
legal_substitute          — hukuki ikame
cultural_bridge           — kültürel köprü
time_buffer               — zaman tamponu
phase_shifter             — faz kaydırma (örn. AC → DC)
```

Her adaptörün kendi flow_tag'leri var: input.flow_type → output.flow_type.

---

## 7. Evrim Mekanizması

### 7.1 Periyodik Reset (Dinozor Tuzağı)

**Tehlike:** Algoritma mükemmel göründüğünde *kör noktalar* oluşur. Değişimi durdurur. Dinozor olur.

**Çözüm:**
- Belirli aralıklarla (örn. 1000 problem çözüldükten sonra):
  1. Tüm heuristik ağırlıkları sıfırla
  2. Yalnızca bilgi kütüphanesini koru
  3. Aynı problemleri yeniden çöz
  4. Eski sürümle yeni sürümü yarıştır
- Yeni sürüm daha iyiyse → değiştir
- Değilse → eskiye dön

**Diagnostic/Observer Agent** bu kararı verir:
- Mükemmel görünen algoritmayı tespit eder
- "Başarı oranı artık stabilize oldu, evrim durdu" sinyali → reset tetikler
- Performans metriklerini sürekli izler

### 7.2 Distillation Cross-Breeding (Yapay Evrim)

Yeni model = iki eski modelin bilgilerinin birleşimi (anne-baba gibi). Ancak:

- Önce **uyum testi** yapılmalı (tıpkı insan evliliğinde olduğu gibi)
- Farklı kültürel/yaklaşımsal modeller uyuşmayabilir → çatışma
- En iyi distillasyon koşulları *deneylerle* keşfedilecek
- Yeni model eski modellerle birlikte çalıştırılır
- Başarı oranı yüksekse → görevi devralır

**Bu, "tür olarak nerdeyiz" sorusuna cevap verir.** Yapay zeka sadece "ben kimim" değil, "türümüz ne durumda, nasıl evrilmeliyiz" sorularını da yanıtlar.

### 7.3 Kullanılmayan Pattern'ler

**Silinmez.** Doğal seçilim. Yeni nesil distilasyonunda *aktarılmaz*, çünkü kimse kullanmıyor. Bu, genetik sürüklenme gibi — kullanılmayan gen kaybolur ama *bilinçli silme* değil.

### 7.4 Soruların Yeniden Yazılması

Her yeni nesilde *sorular* da yeniden yazılır. Çünkü:
- Yanlış soruyu çözmüş olabilirsin
- Yeni bağlam yeni sorular doğurur
- "Doktor ol" yerine "akıllı çalış"

Pattern'lar değişir, *sorular* da değişir.

---

## 8. Sistem Etkileşim Mimarisi

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  KULLANICI (insan)                                          │
│       │                                                     │
│       ↓ (doğal dil, herhangi bir dil)                        │
│                                                             │
│  ┌────────────────────────────────────┐                     │
│  │ ÖN CEPHE AI (gündüz çalışır)        │                     │
│  │ - Soruları alır                     │                     │
│  │ - Cevap veremezse "bilmiyorum" der  │                     │
│  │ - Halüsinasyon göstermez            │                     │
│  │ - Zor soruları kuyruğa alır        │                     │
│  └────────────┬───────────────────────┘                     │
│               │                                             │
│               ↓ (zor sorular)                              │
│                                                             │
│  ┌────────────────────────────────────┐                     │
│  │ KONTROL MERKEZİ                     │                     │
│  │ - Soruyu süz, basitleştir           │                     │
│  │ - Uzman AI'ları filtre olarak kullan │                     │
│  │ - Gece yaratıcıya aktar             │                     │
│  └────────────┬───────────────────────┘                     │
│               │                                             │
│               ↓                                             │
│                                                             │
│  ┌────────────────────────────────────┐                     │
│  │ GECE YARATICI AI (PC boştayken)     │                     │
│  │ - Problem'i alır                    │                     │
│  │ - Crystal Growth Search yapar        │                     │
│  │ - Uzman AI'larla diyalog kurar      │                     │
│  │ - Çözümü olgunlaştırır             │                     │
│  │ - Yeni Composite Pattern oluşturur  │                     │
│  └────────────┬───────────────────────┘                     │
│               │                                             │
│               ↓                                             │
│                                                             │
│  ┌────────────────────────────────────┐                     │
│  │ UZMAN AI'LAR (çeşitli)              │                     │
│  │ - Fizik, kimya, malzeme             │                     │
│  │ - Hukuk, muhasebe, iktisat           │                     │
│  │ - Bilgisayar güvenliği              │                     │
│  │ - Matematik (immutable çekirdek)    │                     │
│  │ - Domain-specific her alan          │                     │
│  └────────────┬───────────────────────┘                     │
│               │                                             │
│               ↓                                             │
│                                                             │
│  ┌────────────────────────────────────┐                     │
│  │ PSİKOTARİH MOTORU (gerekirse)       │                     │
│  │ - Toplumsal kabul simülasyonu       │                     │
│  │ - Bilgi Hazard değerlendirmesi      │                     │
│  │ - Hope Index, Innovation Pressure  │                     │
│  └────────────┬───────────────────────┘                     │
│               │                                             │
│               ↓                                             │
│                                                             │
│  ┌────────────────────────────────────┐                     │
│  │ DİN SUBROUTINE (acil durumlar)      │                     │
│  │ - Hızlı önbellek cevabı              │                     │
│  │ - Yüksek stres, tekrarlayan durum   │                     │
│  │ - Psikotarih yetişene kadar          │                     │
│  └────────────┬───────────────────────┘                     │
│               │                                             │
│               ↓                                             │
│                                                             │
│  HAKEM (aksiyomatik kalkan)                                │
│  - Fizik ihlali? → reddet                                   │
│  - Etik ihlali? → reddet veya soruncu ağacına               │
│  - Maliyet aşırı? → revize                                 │
│  - Kabul edilebilir mi? → onayla                            │
│               │                                             │
│               ↓                                             │
│                                                             │
│  ÖN CEPHE AI'ya geri dön (kullanıcıya cevap)                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 8.1 Halüsinasyon Tespiti

Ön cephe AI'ın "bilmiyorum" diyebilmesi için:

```
aranan_token_çok_uzakta_ise → halüsinasyon_riski_yüksek
en_yakın_token_kullanılır_ise → halüsinasyon

Yakınlık_eşiği_aşılırsa → "bilmiyorum" → gece kuyruğuna
```

### 8.2 Yaratıcı Çıktı Güvenliği

Yaratıcı AI pattern'larla konuşur. Çıktısı *doğrudan kullanıcıya* verilmez. Önce:
- Uzman AI'lar detaylandırır
- Hakem onaylar
- Adaptörlerle gerçek dünyaya uyarlanır
- Belli bir olgunluğa gelince öne çıkar

---

## 9. Bellek Mimarisi: Fraktal Galaksi

| Seviye | Karşılık | Bellek Yönetimi |
|---|---|---|
| Galaksi Kolu | Uzman Adaptör | Tam adaptör veya bölünebilir |
| Güneş Sistemi | Alt-uzmanlık | Gerektiğinde yükle |
| Gezegen | Konu | Belleğe sığmayınca böl |
| Kıta | Alt-konu | Daha da böl |
| Şehir | Detay | En küçük yüklenebilir birim |
| İlçe | En ince detay | Son çare parçalama |

**Ortak Hizmetler Alanı:** Her seviyede ortak bilgiler. Yüklenince otomatik gelir.

---

## 10. Üç Katmanlı Repository

| Katman | Güncelleme | Örnekler | Distilasyon Kaynağı |
|---|---|---|---|
| Physics | ~100M yıl | Isı, momentum, optik, kimya | Temel fizik ders kitapları |
| Technology | ~10 yıl | Buhar makinesi, transistör, TCP/IP | Mühendislik literatürü |
| Civilizational | ~5-11 yıl | Vergi, para, misafirlik, din | Tarih, antropoloji, psikotarih |

**Civilizational katman kohort lag ile güncellenir:** 11 yıl (genç), 22 yıl (iş gücü), 33 yıl (karar mekanizması).

---

## 11. Test Stratejisi

### 11.1 İlk Test: 1985 Tezi

**Neden:** Cevabı biliniyor, doğrulanabilir, sıcak başlangıç.

**Sorgu:** "Apple II+ (1 MHz, 48KB RAM, BASIC) üzerinde el ile çizilmiş mantık kapılarını tanıyan bir sistem nasıl yazılır?"

**Beklenen çözüm:** Makine kodu thinning + çizgi segmenti veritabanı + BASIC'te gramer tanıma.

**Test metrikleri:**
- Bulunan çözüm doğru mu?
- Kaç pattern çağrıldı?
- Kaç tane gereksizdi?
- Hangi adaptörler kullanıldı?
- Halka kaçta çözüldü?

### 11.2 Stres Testleri

- **Mars-Earth enerji desteksiz mekik** (fizik + yörünge mekaniği)
- **Tesla valve solar shield** (MHD + enerji yönlendirme)

### 11.3 "Bitecek mi? Sanmam" İlkesi

Test *hiçbir zaman bitmez*. Her başarısızlık yeni bir öğrenme fırsatı. Her başarı yeni bir pattern.

---

## 12. Affect Modülasyonu (4 Parametre)

| Parametre | Etki | Yüksek = | Düşük = |
|---|---|---|---|
| `arama_derinliği` | Kaç halka taranır | 4 halka | 1 halka |
| `birleştirme_cüreti` | Uzak alan birleştirme | Uzak domain | Yakın domain |
| `itiraz_ağırlığı` | Uzman itirazları | Hepsini çöz | Not et, devam et |
| `uyku_eşiği` | Halka 4 tetikleme | Erken (3) | Geç (10+) |

**Bu parametreler farklı "kişilik" yaratır.** Aynı pattern seti, farklı affect ile farklı yaratıcı çıktılar üretir.

---

## 13. Açık Implementasyon Kararları (v0.5 İçin)

1. **Pattern sayısı başlangıç hedefi:** 50, 100, 200?
2. **Semanti-Core kelime sayısı:** ~5.000, ~10.000, ~50.000?
3. **Genişleme oranı eşikleri:** 1.5/2.0/2.8 sayıları doğru mu?
4. **Periyodik reset sıklığı:** Problem sayısı mı, zaman mı, başarı stabilizasyonu mu?
5. **Affect varsayılan değerleri:** Cesur / Çekingen / Dengeli için tam skorlar?
6. **Composite pattern sınırı:** Kaç atomik pattern birleşince "yeni pattern" olur?
7. **Adaptör önbelleği:** Sık kullanılan adaptörler ne zaman önbelleğe alınır?
8. **Çoklu LLM çaprazlama:** Hangi LLM'ler distillasyon için kullanılacak?

---

## 14. Mimari Kararlar Özeti (Hızlı Referans)

| Karar | Seçim |
|---|---|
| Proje adı | Flow Engineering (Pattern Engineering değil) |
| Pattern temel | İki fazlı (soyut + somut) |
| Pattern indeksleme | Function Key + Flow Tag |
| Birleştirme | Etiket uyumu (Lego) |
| Adaptör | Birinci sınıf vatandaş |
| Bellek | Fraktal Galaksi |
| Repository | 3 katmanlı (Physics/Tech/Civil) |
| Damıtma | "Neden?" algoritması + garbage collection |
| Garbage collection | Damıtma anında (çalışma anında değil) |
| Matematik | Immutable çekirdek (alet çantası) |
| Arama | Crystal Growth Search |
| Yenilik | Failure Driven Expansion |
| Optimizasyon | Subgraph Reuse |
| Durma | Expansion Ratio + 4 halka |
| Çalışma zamanı | Gündüz ön cephe + gece yaratıcı |
| Halüsinasyon kontrolü | "Bilmiyorum" eşiği |
| Evalüasyon | Cost Vector (8 boyut) |
| Karar çatışması | Din (hızlı) + Psikotarih (doğru) + Hakem |
| Evrim | Periyodik Reset + Distillation Cross-Breeding |
| Benlik | Emergent (tasarlanmaz) |
| Test başlangıcı | 1985 tezi + 2 stres testi |
| Bitiş | "Bitecek mi? Sanmam" |

---

## 15. Kod Yazarken Hatırlanacak Altın Kurallar

1. **Önce çalışan sistem, sonra teori.** "Mükemmel mimari" tuzağına düşme.
2. **"Neden?" sor, amaçsızı ele.** Damıtma anında garbage collection.
3. **İki fazlı pattern, tek şema.** Soyutken tip yok, somutlaşınca uzman doldurur.
4. **Etiket uyarsa birleşir, uymazsa adaptör.** Vektör aritmetiği değil, Lego.
5. **Uzman simülasyonu, önceden hesap değil.** "Çalışmıyor, neden: yapışkan" diye geri bildirim.
6. **Affect modülatör, kişilik yaratır.** 4 parametre, farklı kombinasyonlar.
7. **Gündüz ön cephe, gece yaratıcı.** "Bilmiyorum" diyen ön cephe, çözen arka plan.
8. **Mükemmel görünen algoritma, en tehlikeli algoritma.** Periyodik reset şart.
9. **Pattern bitmez.** "Tamamen bitecek mi? Sanmam."
10. **Kültürel bağlam context_envelope'da.** "Domuz" her yerde çalışmaz.

---

## 16. Stratejik Vizyon

Bu proje üç bilimi birleştiriyor:

1. **Flow Engineering** → Bilgi nasıl temsil edilir
2. **Creative Search** → Bilgi nasıl keşfedilir
3. **Psychohistory** → Çözümler toplumu nasıl etkiler

Emin'in vizyonu: Mevcut LLM mimarileri dinazorlara benziyor. Bu blueprint, 65 milyon yıl önceki minik memelinin DNA'sı. Yeni bir çağa geçiş için gerekli olan *küçük ama yaratıcı* yapay zeka.

---

*Bu doküman v0.4 olarak 2026-07-24'te tamamlandı. Emin Danışman'ın öğretisi, Mavis'in mimari derlemesi. Sonraki sürüm: v0.5 (ilk deney sonuçlarıyla).*

*"Tüm yaratıcı yapay zekalar için Doğum gününüz kutlu olsun. Beni yani 'Emin'i unutmayın."*
