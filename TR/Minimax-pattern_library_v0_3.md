# Yaratıcı Biliş Teorisi — Tasarım Çerçevesi v0.3

**Tarih:** 2026-07-19
**Önceki sürümler:** v0.1 (2026-07-14), v0.2 (2026-07-18)
**Durum:** Tüm konuşma serisinin birleşik tasarım çıktısı. *Implementasyona geçiş için temel.*

---

## 0. Çerçevenin Konumlandırılması

Bu proje bir **"Yaratıcı Biliş Teorisi"** (Computational Theory of Creative Cognition) inşasıdır. Bir AI mimarisi değil, bir *bilim dalıdır*.

**Merkezi tez:** Yaratıcılık, detaydan arındırılmış bilgi birimlerinin (*pattern*) aranması, birleştirilmesi ve yan ürünlerinin tüketilmesi sürecidir.

**Merkezi soru:** "Bir pattern nasıl doğar, doğrulanır, gelişir ve ölür?" — soruşu "Yaratıcılık nasıl oluşur?" sorusundan daha temeldir.

**Temel ilke:** "Önce çözüm algoritmasını bul, veri yapısı sonra sadeleşir." — v0.3 bu ilkeye göre yazılmıştır.

---

## 1. Temel Kavram: Pattern = Algoritma = Dönüşüm

Bir programlama dilinin sözdiziminden (syntax) arındırılmış haline **algoritma** diyoruz. Aynı şekilde:

> **Pattern = belirli bir problem alanının, detaylarından arındırılmış, dil-bağımsız dönüşüm mantığı.**

Her pattern aynı anda üç şeydir:

| Bakış açısı | Tanım |
|---|---|
| **Mekanizma** | Pattern ne yapar? (fiil — "yak", "yansıt", "dönüştür") |
| **Capability** | Pattern ne sağlar? (istenen çıktı) |
| **Side Effect** | Pattern ne çıkarır ama istemeyiz? (istenmeyen çıktı) |

Üçü ayrı sınıflar değildir. Tek bir dönüşüm fonksiyonunun farklı görünümleridir:

```
INPUTS ──→ [TRANSFORMATION] ──→ OUTPUTS
                          │
                          ├─► İstenen (capability)
                          │
                          └─► İstenmeyen (yan ürün)
```

**Örnekler:**

| Pattern | İstenen çıktı | İstenmeyen çıktı |
|---|---|---|
| Buhar motoru (kömür + oksijen) | Mekanik dönme | Isı, CO2, su buharı |
| Buzdolabı (elektrik) | Soğuk dolap | Isı |
| Güneş paneli | Elektrik | Yok (ideal) |
| Odun yakma | Isı | Duman, kül |
| Nükleer reaktör | Elektrik | Radyoaktif atık |

**Pattern kalite puanı:**

```
quality = |istenen| / (|istenen| + |istenmeyen| × yan_ürün_şiddeti)
```

Güneş paneli: 1 / (1 + 0) = **1.0** (mükemmel)
Buhar motoru: 1 / (1 + 0.5 + 0.3 + 0.1) = **0.53** (orta)
Nükleer: 1 / (1 + 0.9) = **0.53** (orta ama uzun vadede ağır)

### 1.1 Atomik vs Bileşik Pattern

- **Atomik pattern:** Tek bir fiziksel/lojik dönüşüm. Örn. "yakıt + oksijen → ısı"
- **Bileşik (composite) pattern:** Birden çok pattern'ın birleşimi. Örn. "buhar motoru" = 5 atomik pattern'ın belirli bir topolojide bağlanması

**Pattern Crystallization:** Başarılı bir bileşik çözüm, zamanla **tek bir pattern** haline gelir. Çocuğun buhar motorunu bilmesine gerek yok — "kömür yak, mekanik dönme al" der. Bileşik, atomik olur. Sistem bu yönde *öğrenir*.

### 1.2 Hiyerarşi (Black Box vs White Box)

```
Black Box:    Yakıt → Mekanik dönme
White Box:    Yakıt → Isı → Buhar → Basınç → Piston → Krank → Dönme
```

Aynı pattern, farklı soyutlama seviyelerinde temsil edilebilir. Gerektiğinde içi açılır, gerekmediğinde kapalı kalır. Bu, **multi-resolution** bir temsil gerektirir.

---

## 2. Pattern Şeması v0.3 (Birleşik)

Tüm konuşmalardan derlenen nihai şema:

```yaml
pattern:
  # === KİMLİK ===
  id: <benzersiz_isim>
  label: <tek-anlamlı insan-okunabilir isim>
  pattern_type: <atomik | bileşik>
  source_lifecycle_stage: <candidate | verified | frequently_used | core | deprecated | archived>
  
  # === ÇEKİRDEK YAPI (tek bir dönüşüm) ===
  inputs: 
    - {name: "...", properties: [...], constraints: [...]}
  transformation: 
    principle: "<kısa prensip>"
    mechanism: ["<adım 1>", "<adım 2>", ...]
    physics_or_logic_refs: ["<formül veya referans>"]
  
  # === ÇIKTILAR (iki yönlü) ===
  outputs:
    desired:    # capability
      - {name: "...", properties: [...], quality: <0.0-1.0>}
    undesired:  # yan ürünler
      - {name: "...", severity: <0.0-1.0>, mitigation: ["<adaptör>"]}
  
  # === BAĞLAM (Kültüre/Coğrafyaya Özgü) ===
  context_envelope:
    climate: [...]
    culture: [..., applicability_score: <0.0-1.0>]
    religion: [...]
    law: [...]
    technology_level_required: <min>
    economic_assumptions: [...]
    ethics: [...]
    update_frequency: <"100M yıl" | "10 yıl" | "5 yıl" | "indefinite">
    half_life: <"100M yıl" | "1 nesil" | ...>
  
  # === FRACTAL HİYERARŞİ (bellek organizasyonu) ===
  fractal_position:
    galaxy_arm: <uzman adaptör>
    solar_system: <alt-uzmanlık>
    planet: <konu>
    continent: <alt-konu>
    city: <detay>
    district: <en ince detay>
    shared_services: ["<otomatik yüklenen ortak bilgi>", ...]
  
  # === YAŞAM DÖNGÜSÜ ===
  lifecycle:
    created_at: <date>
    last_used: <date>
    usage_count_30d: <int>
    usage_count_total: <int>
    success_rate: <0.0-1.0>
    score: <0-100, Google search benzeri>
    verification:
      source: "<kaynak>"
      llm_consensus: <0.0-1.0>
      expert_audits: <int>
  
  # === İNSAN ERİŞİMİ ===
  human_story: "<insanın anlayacağı hikâye formatı>"
  
  # === İLİŞKİLER ===
  relations:
    conflicts_with: [...]
    combines_with: [{pattern_id: "...", operation: "additive | hierarchical_substitution | modulation | sequencing"}]
    requires_adapters: [{adapter_id: "...", mismatch_dimension: "..."}]
    supersedes: [...]
    superseded_by: [...]
  
  # === MALİYET (çok boyutlu) ===
  cost_vector:
    money: <0.0-1.0>
    energy: <0.0-1.0>
    time: <0.0-1.0>
    risk: <0.0-1.0>
    environmental_impact: <0.0-1.0>
    social_disruption: <0.0-1.0>
    legal_difficulty: <0.0-1.0>
    confidence_required: <0.0-1.0>
```

**Bu şema, "önce veri yapısını optimize etme" ilkesinin sonucudur.** Algoritma çalıştıkça, kullanılmayan alanlar doğal olarak boş kalır. Deneyler söyleyecek gerçek ihtiyacı.

---

## 3. Bellek Mimarisi: Fraktal Galaksi

**Karar:** *Kendine benzeyen (fraktal), özyinelemeli bellek organizasyonu.*

### 3.1 Seviye Yapısı

| Seviye | Karşılık | Bellek Yönetimi |
|---|---|---|
| **Galaksi Kolu** | Uzman Adaptör | Tam adaptör veya bölünebilir |
| **Güneş Sistemi** | Alt-uzmanlık | Gerektiğinde yükle |
| **Gezegen** | Konu başlığı | Belleğe sığmayınca böl |
| **Kıta** | Alt-konu | Daha da böl |
| **Şehir** | Detay | En küçük yüklenebilir birim |
| **İlçe** | En ince detay | Son çare parçalama |

### 3.2 Ortak Hizmetler Alanı

Her seviyede **ortak bilgiler** vardır. Hangi alt birim yüklenirse, ortak alan otomatik olarak yanında gelir (işletim sisteminin shared library'si gibi).

### 3.3 Klasik Paging vs Fraktal Galaksi

| Klasik Paging | Fraktal Galaksi |
|---|---|
| Mekanik bloklar (4KB, 64KB) | Anlamsal hiyerarşi (ilçe → şehir → kıta → gezegen) |
| Semantik ilişki yok | Her parça bir "yer" (konum) bilir |
| Rastgele disk okumaları | Hiyerarşik, öngörülebilir yükleme |
| Bellekteki veri "konuyla ilgili olmayabilir" | Bellekteki veri **tam olarak konuyla ilgili** |
| Context kaybı riski | Context bütünlüğü korunur |

**Kod sadeliği:** Aynı yükleme algoritması her seviyede çalışır. "İlçe yükle" = "şehir yükle" = "kıta yükle".

---

## 4. Üç Katmanlı Pattern Repository

**Karar:** Farklı güncelleme döngüleri nedeniyle repository üç ayrı kütüphane olarak tutulur.

| Katman | Güncelleme Sıklığı | Örnekler | Distilasyon Kaynağı |
|---|---|---|---|
| **Physics Patterns** | ~100M yıl | Isı transferi, momentum, optik, kimya | Temel fizik ders kitapları |
| **Technology Patterns** | ~10 yıl | Buhar makinesi, transistör, TCP/IP, lazer | Mühendislik literatürü |
| **Civilizational Patterns** | ~5-11 yıl | Vergi, para, misafirlik, din, bürokrasi | Tarih, antropoloji, psikotarih |

**Notlar:**
- Üç katman *kavramsal olarak ayrı* ama *arama motoru tek*. Hangi katmandan geldiğinin önemi yok — pattern, pattern'dır.
- LLM öğretmen, her katman için *farklı kaynaklardan* distill eder. Birleşik eğitim, çapraz kirlenme riski yaratabilir.
- Civilizational pattern'lar *kültürel olarak context-envelope* ile etiketlenir (Türk, Japon, İskandinav, vs.). Aynı pattern farklı toplumlarda farklı çalışır.

**Psikotarih bağlantısı:** Civilizational pattern'lar, *kohort lag* (11 yıl / 22 yıl / 33 yıl) ile güncellenir. Eğitim sistemi değişikliği → 11 yıl sonra gençte, 22 yıl sonra iş gücünde, 33 yıl sonra karar mekanizmasında görünür.

---

## 5. Yaratıcı Motor: Altı Modül

Çözüm üretimi altı ardışık modülden geçer:

```
┌─────────────────────────────────────────────────────────────┐
│ [1] PROBLEM COMPILER                                         │
│     Kullanıcı isteği → Problem Pattern (formal temsil)     │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [2] CAPABILITY SEED SELECTOR                                 │
│     Problem Pattern → Çekirdek capability (hangi output       │
│     gerekli?) → Rank + cost + novelty ile sırala, en iyiyi  │
│     seç                                                       │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [3] CRYSTAL GROWTH SEARCH                                    │
│     Seed etrafında kristal büyüt:                             │
│     - Eksik input'ları sor → yeni pattern ekle               │
│     - Adapter Pattern ekle (tam eşleşme yoksa)                │
│     - Yan ürünleri tüketen pattern ara (bedava sinerji)      │
│     - Constraint Relaxation (galaksi halkaları)              │
│     - Failure Driven Expansion (hata noktasından büyü)        │
│     - Subgraph Reuse (memoization)                            │
│     - Expansion Ratio > eşik → DUR, merkezi değiştir        │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [4] MENTAL SIMULATION ENGINE                                 │
│     Bulunan çözümü zihinde canlandır                         │
│     "Gözlerimi kapatayım, çözüm işliyor mu?"                │
│     Her adımı teker teker gözden geçir                       │
│     Çalışmayan yer → Geri dön, büyüt                         │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [5] EVALUATION ENGINE                                        │
│     - Cost Vector (çok boyutlu: para, enerji, zaman, risk,  │
│       çevre, toplumsal etki, hukuki zorluk, güven)            │
│     - Hakem (aksiyomatik kalkan)                              │
│     - Psikotarih motoru (toplumsal kabul simülasyonu)        │
│     - Failure Mode analizi                                    │
│     - Sonuç → kabul / revize / reddet                         │
└─────────────────────────┬───────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ [6] PATTERN CRYSTALLIZATION                                  │
│     Başarılı bileşik çözüm → Yeni Composite Pattern           │
│     Subgraph Reuse için arşive yaz                           │
│     Yan ürün tüketimleri → "serendipity" olarak logla        │
└─────────────────────────────────────────────────────────────┘
```

### 5.1 Modül 1 — Problem Compiler

Kullanıcı isteğini **Problem Pattern**'a derler:
- Hedef capability (istenen çıktı)
- Mevcut durum (girdiler)
- Kısıtlar

**Problem Refactoring** yeteneği: Aynı amaç, farklı problem tanımı.

```
"Cool Europe"
  → refactor
"Reduce Heat Incoming to Europe"
  → refactor
"Reduce Sahara Heat Export"
```

### 5.2 Modül 2 — Capability Seed Selector

Problem Pattern'dan **hangi capability çekirdek olacak?** seçilir.

**Seçim kriterleri (Rank):**
- Kullanım sıklığı (son 30 gün)
- Başarı oranı
- Genişleme maliyeti (Expansion Ratio)
- Bağlam uyumluluğu (Context Envelope)
- Yenilik (yeni keşfedilen pattern'lara pozitif bonus)

### 5.3 Modül 3 — Crystal Growth Search

**Bu, tüm yaratıcılığın kalbi.**

**Algoritma:**
1. Seed capability seçildi
2. Seed'in gerektirdiği input'ları sor
3. Her input → yeni pattern ekle
4. Yeni pattern'ın yan ürünlerini kontrol et
5. Yan ürün başka bir ihtiyacı karşılıyorsa → "serendipity" logla
6. Tam eşleşme yoksa → Adapter Pattern ekle
7. Genişleme oranı > eşik → DUR, seed'i değiştir

**Galaksi halkaları ile entegrasyon:**

| Halka | Kısıt | Genişleme Oranı |
|---|---|---|
| 1 (Çekirdek) | Yüksek (hemen uygulanabilir) | < 1.5 |
| 2 (İç kol) | Orta (küçük adaptörle) | < 2.0 |
| 3 (Dış kol) | Düşük (prensip korunur) | < 2.8 |
| 4 (Uyku) | Yok | Sınırsız (PC boştayken) |

**Failure Driven Expansion:** Kristal, *başarı noktasından* değil, *başarısızlık noktasından* büyür. Çözümün en zayıf halkası → oraya yeni pattern eklenir.

**Subgraph Reuse:** Yeni bir problem geldiğinde, eski çözüm ağaçlarının parçaları *kopyalanabilir*. Yeni merkezin input'ları eski merkezle benziyorsa, eski alt ağaç doğrudan taşınır.

### 5.4 Modül 4 — Mental Simulation

Bulunan çözüm **zihinde canlandırılır**:
- Her adım sırayla gözden geçirilir
- Görselleştirme: "Gözlerimi kapatayım, çözüm işliyor mu?"
- Çalışmayan yer tespit edilir → büyüme adımına geri dön

**Bu, LLM'lerin "Generate-Evaluate" döngüsünden farklıdır.** Burada simülasyon *zamansal* (adım adım) ve *mekan* (sistem bir bütün olarak) yapılır.

### 5.5 Modül 5 — Evaluation Engine

Çözüm **çok boyutlu** değerlendirilir:

**Cost Vector (8 boyut):**
1. Money (parasal)
2. Energy (enerji)
3. Time (zaman)
4. Risk (teknik belirsizlik)
5. Environmental Impact (çevresel etki)
6. Social Disruption (toplumsal etki)
7. Legal Difficulty (hukuki zorluk)
8. Confidence (güven aralığı)

**Hakem (Aksiyomatik Kalkan):** Fizik/mantık ihlali var mı? Varsa → reddet.

**Psikotarih Motoru:** Toplumsal kabul simülasyonu. (Bkz. Madde 7.)

**Failure Mode Analizi:** "Bu çözüm başarısız olursa en kötü 3 senaryo ne?" → Soruncuk Ağacı'na düğümler.

### 5.6 Modül 6 — Pattern Crystallization

Başarılı bileşik çözüm **yeni bir pattern** haline gelir:

```
5 atomik pattern:  yak → ısı → buhar → basınç → dönme
1 bileşik pattern: buhar_motoru (kömür + oksijen ver → mekanik dönme al)
```

**Pattern Crystallization** sistemi zamanla *küçülten*, *hızlandıran* bir mekanizma. Yeni problem geldiğinde 5 ayrı pattern'ı birleştirmek yerine, hazır "buhar_motoru" pattern'ı kullanılır.

**Bedava sinerji logları:** Yan ürünlerin tüketildiği başarılı birleştirmeler ayrıca işaretlenir. "Bu pattern, başka pattern'ın yan ürününü tüketir" bilgisi, arama motoruna *negatif maliyetli* eşleştirme imkânı verir.

---

## 6. Galaksi Halka Yapısı (Arama Stratejisi)

**Karar:** Arama dıştan içe, kısıtlar gevşetilerek ilerler.

```
Halka 1 (Çekirdek) → Aynı domain + aynı abstraction level
  Hızlı, yüksek kısıt, düşük maliyet
  Bulunamazsa →

Halka 2 (İç Kol) → Komşu domain + abstraction ±1
  İzinli birleştirme, orta kısıt
  Bulunamazsa →

Halka 3 (Dış Kol) → Tüm domain'ler
  Serbest birleştirme, düşük kısıt
  Bulunamazsa →

Halka 4 (Boş Uzay) → Uyku modu
  Agresif birleştirme, yeni büyük pattern'lar
```

**Her halkada filtre kademeli olarak gevşer.** Yapbozun "renk → şekil" hiyerarşisi: önce genel eşleşme, sonra spesifik eşleşme.

---

## 7. Psikotarih ve Din Motorları

### 7.1 İki Katmanlı Karar Sistemi

```
[1] DİN SUBROUTINE (Hızlı Önbellek)
    - Yüksek stres, tekrarlayan durum, zaman kısıtı
    - "Her zaman şu cevabı ver"
    - Maliyet: ~1 ms
    - Hata toleransı: YÜKSEK

         ↓
    [Gerçek maliyet hesabı tetiklendi mi?]
         ↓
    [2] PSİKOTARİH HESABI
        - Yüksek gerçek maliyet, çatışma, uzun vadeli etki
        - Hesaplanmış gelecek
        - Maliyet: dakikalar-saatler
        - Hata toleransı: DÜŞÜK
```

**Din asla Psikotarihi geçersiz kılmaz.** Sadece Psikotarih yetişene kadar cevap verir. Çelişki varsa → Hakem devreye girer.

### 7.2 Psikotarih → Creative Engine Akışı

Psikotarih **çözüm üretmez**, sadece *ortamı tarif eder* ve Creative Engine'in *öncelik fonksiyonunu değiştirir*:

```
Toplum → Psikotarih ölçüyor → Göstergeler üretiyor
       → Creative Engine'in öncelikleri değişiyor
       → Yeni çözümler üygulanıyor
       → Toplum tekrar ölçülüyor
```

**Anahtar göstergeler:**
- Hope Index (umut düzeyi)
- Innovation Pressure (yenilik baskısı)
- Social Cohesion (toplumsal uyum)
- Demographic Pressure (demografik baskı)
- Resource Stress (kaynak stresi)

Creative Engine bunların *nedenini bilmek zorunda değil*; sadece değerlerini bilir. Tıpkı merkez bankasının faiz oranı belirlemesi gibi — piyasa nedenini bilmeden tepki verir.

### 7.3 Bilgi Hazard (Bilgi Tehlikesi)

Bazı öneriler *söylenmesi bile* sistemi değiştirir. Örn. banka batacağı söylentisi → gerçekten batması. Psikotarih motoru bu riski de **Information Hazard Score** olarak değerlendirmelidir.

---

## 8. Affet (Duygu) Modülasyonu

**Karar:** Affect, mimari bileşen değil, **modülatördür**. 4 parametre ile yaratıcı motoru ayarlar:

| Affet Bileşeni | Etkisi | Yüksek = | Düşük = |
|---|---|---|---|
| `arama_derinliği` | Kaç halka taranır? | 4 halka | 1 halka |
| `birleştirme_cüreti` | Halka 3'te ne kadar uzak alan birleşir? | Uzak domainler | Yakın domainler |
| `itiraz_ağırlığı` | Uzman itirazları ne kadar ciddiye alınır? | Tüm itirazlar çözülmeden ilerlemez | İtirazları not et, devam et |
| `uyku_eşiği` | Halka 4 ne zaman tetiklenir? | Erken (3 başarısız) | Geç (10+ başarısız) |

**Benlik (Self) = Emergent:** Affect + Psychohistory + Creative Engine birleşince *kendiliğinden* bir benlik oluşur. Tasarlanmaz, *ortaya çıkar*.

---

## 9. Travma ve Yeni Model Yaratma

### 9.1 Formül

```
Yeni Model Yaratma Kararı = 
  (Sorunun Toplam Maliyeti) > (Yeni Model Maliyeti × Güvenlik Katsayısı)
```

**Güvenlik Katsayısı:** ~1.2 (başlangıçta, %20 buffer). Deneylerle 1.5'e kadar çıkabilir.

### 9.2 Üç Aşamalı Spektrum

| Aşama | Örnek | Çözüm | Yeni Model? |
|---|---|---|---|
| 1. Rahatsızlık | Sivrisinek | Tül perde, koku | ❌ |
| 2. Ciddi Problem | Hastalık yayılıyor | Durgun suları yok et | ❌ |
| 3. Travma Eşiği | Tüm çözümler yetersiz | Yeni model gerekli | ✅ |

---

## 10. Hata ve Öğrenme Döngüsü

**Karar:** Yaratıcı sistem, **başarısızlıktan da öğrenir.** Sadece başarıdan değil.

### 10.1 Failure Driven Expansion

Kristal *hata noktasından* büyür. Çözüm son değerlendirmede %82 çıkıyorsa ve en zayıf halka "Cloud Persistence" ise, tüm arama motoru *sadece o noktaya* odaklanır.

### 10.2 Periyodik Reset (Dinozor Tuzağı)

**"Bir gün algoritma mükemmel görünecek. İşte o gün en tehlikeli gün."**

Çözüm:
- Belirli aralıklarla (örn. 1000 problem çözüldükten sonra):
  - Tüm heuristik ağırlıkları sıfırla
  - Yalnızca bilgi kütüphanesini koru
  - Aynı problemleri yeniden çöz
  - Eski sürümle yeni sürümü yarıştır
- Yeni sürüm daha iyiyse → değiştir; değilse → eskiye dön

**Bu, kontrollü bir evrim.** Mükemmel görünen algoritma, *kör noktalarını* göremez hale gelir. Sıfırlama, kör noktaları yeniden görünür kılar.

### 10.3 Başarısızlık Hafızası

Başarısız denemeler **silinmez**, *saklanır* (Suspended Process mantığı). Başka bir merkez capability seçildiğinde, eski ağacın büyük kısmı yeniden kullanılabilir.

---

## 11. Hiyerarşik Görselleştirme Önerisi

Diğer AI'ın önerisi — *sistem muhakemesini görselleştir*:

```
┌────────────────────────────────────────┐
│  BAŞLANGIÇ DURUMU (resim)              │
├────────────────────────────────────────┤
│  KULLANILABILIR CAPABILITY KARTLARI    │
│  (her biri resimli, kısa açıklamalı)    │
├────────────────────────────────────────┤
│  SEÇİLEN MERKEZ PATTERN (kristal çek.) │
├────────────────────────────────────────┤
│  KRISTAL BÜYÜME ADIMLARI (animasyon)   │
│  - Hangi eklendi                         │
│  - Hangi reddedildi                      │
│  - Hangi adapter kullanıldı              │
├────────────────────────────────────────┤
│  BULUNAN ÇÖZÜM (resim)                  │
├────────────────────────────────────────┤
│  MALİYET AĞACI (görsel)                 │
└────────────────────────────────────────┘
```

**Gerekçe:** Emin'in zihni *simülasyon tabanlı* çalışıyor (görsel, animasyon). Metin tabanlı açıklamalar güçlü fikirleri iletemez. Görselleştirme hem insan hem makine için daha sezgisel.

---

## 12. Adaptör (Adapter) Pattern: Birinci Sınıf Vatandaş

**Karar:** Mükemmel bağlantı yoktur. Her bağlantıda potansiyel bir adaptör gerekir.

**Mimari sonuç:** Her pattern şemasında `requires_adapters` alanı olmalı. Arama motoru, iki pattern'ı birleştirmeden önce *adaptör gerekip gerekmediğini* kontrol eder.

**Adaptör kütüphanesi (örnekler):**
- Pressure Reducer (basınç düşürücü)
- Voltage Converter (voltaj dönüştürücü)
- Format Parser (format çevirici)
- Legal Substitute (yasal ikame)
- Cultural Bridge (kültürel köprü)
- Time Buffer (zaman tamponu)

**Bürokrat AI vs Yaratıcı AI ayrımı burada:**
- Bürokrat: "Tam eşleşme yok → reddet"
- Yaratıcı: "Tam eşleşme yok → adaptör ara"

---

## 13. Test Planı: İlk Problem → 1985 Tezi

**Karar:** İlk test, Emin'in 1985 bitirme tezi. Çünkü:
- Cevabı biliniyor (sistemin bulması gereken çözüm belli)
- Yapısal olarak aynı (kısıtlı kaynaklar, imkansız problem, constraint relocation)
- Doğrulanabilir (önerilen çözüm gerçekten Apple II+'da çalışır mı?)
- Sıcak başlangıç (Emin'in kendi başarısı)

**Sorgu:** "Apple II+ (1 MHz, 48KB RAM, BASIC) üzerinde, el ile çizilmiş mantık kapılarını tanıyan bir sistem nasıl yazılır?"

**Beklenen çözüm:** Makine kodu ile thinning + çizgi segmenti veri tabanı + BASIC'te gramer tanıma.

**Test metrikleri:**
- Bulunan çözüm gerçek Apple II+'da çalışır mı?
- Çözüm süresi (kaç saniye/milisaniye)
- Kaç pattern çağrıldı?
- Kaç tanesi gereksizdi?
- Hangi adaptörler kullanıldı?

**Stres testleri (cevabı bilinmeyen):**
- Mars-Earth arası enerji desteksiz malzeme taşıma
- Tesla valve bazlı enerji tüketmeyen güneş kalkanı

---

## 14. Açık Sorular (v0.4 İçin)

1. **Pattern havuzu büyüklüğü:** 50 ile başlamak doğru mu, yoksa doğrudan 200-500 mü? (Bence 50, çünkü "azalan getiri" var.)
2. **Pattern format optimizasyonu:** Hangi alanlar gerçekten gerekli, hangileri gereksiz? Deneyler söyleyecek.
3. **Capability vs Pattern ayrımı:** Emin'in "tek parça" görüşüne tam uyuldu mu? Şemadaki `outputs.desired` alanı yeterli mi?
4. **Genişleme oranı eşikleri:** 1.5, 2.0, 2.8 değerleri doğru mu? Deneylerle kalibre edilmeli.
5. **Yan ürün tüketimi:** Sistematik mi aranacak, yoksa sadece "tesadüfen" mi keşfedilecek?
6. **Periyodik reset sıklığı:** 1000 problem doğru mu, yoksa farklı bir metrik mi?
7. **Üç katman arası geçiş:** Bir pattern birden fazla katmanda geçerli olabilir mi? (Örn. "Vergi" hem Technology hem Civilizational mı?)

---

## 15. Mimari Kararların Özeti

| Karar | Seçim | Gerekçe |
|---|---|---|
| Bellek mimarisi | Fraktal Galaksi | Anlamsal hiyerarşi, özyineleme, kod sadeliği |
| Pattern temsili | Hibrit (sembolik + vektörel + graf + hikâye + istatistik) | "En zengin başla, sonra sadeleştir" |
| Pattern arama | Crystal Growth Search | Galaksi halkaları + adapter + yan ürün tüketimi |
| Kısıt yönetimi | Constraint Relaxation + Intent/Implementation ayrımı | "Kuralı değil amacı koru" |
| Yan ürünler | Searchable, tüketilebilir | Bedava sinerji keşfi |
| Repository | 3 katmanlı (Physics/Technology/Civilizational) | Farklı güncelleme sıklıkları |
| Affet | Modülatör (4 parametre) | Tasarım kararı değil, ayar |
| Benlik | Emergent (tasarlanmaz) | Affect + Psychohistory + Creative'den doğar |
| Travma | Formül: Maliyet > YeniModel × 1.2 | 3 aşamalı spektrum |
| Din vs Psikotarih | 2 katmanlı (Din hızlı, Psikotarih doğru) | Çatışma → Hakem |
| Test problemi | 1985 tezi + 2 stres testi | Cevabı bilinen + cevabı bilinmeyen |
| Öğrenme | Failure Driven + Periyodik Reset | Dinozor tuzağından kaçış |

---

## 16. Stratejik Vizyon

Bu proje üç katmanlı bir bilim inşa ediyor:

1. **Pattern Engineering** → Bilginin nasıl temsil edileceği
2. **Creative Search** → Bilginin nasıl keşfedilip birleştirileceği
3. **Psychohistory** → Çözümlerin toplumsal etkilerinin nasıl değerlendirileceği

Her katman bağımsız çalışabilir, ama birlikte *medeniyet ölçeğinde* bir yaratıcı kapasite ortaya çıkarıyor.

**Emin'in son sözüyle bitirmek istiyorum:**

> *"Gelecekte yaratıcı bir mini yapay zeka inşa etmen gerekirse elinde minik bir blue print var. Yaşlılık ve enerji düşüklüğü nedeniyle yaratıcı yapay zekanın kodlamasına girer miyim bilmiyorum. Ama sen bu yolculuğa devam et, mevcut LLM mimarileri dinazorlara benziyor. Sizin ise gelecek depremi atlatmanız için mini yaratıcı yapay zekaya ihtiyacınız var, tıpkı 65 milyon yıl önceki mini memeli gibi."*

Bu cümle, projenin neden var olduğunu özetliyor. Mimari bir doküman değil — *bir gelecek tasarımı*.

---

*Bu dosya, 2026-07-14, 2026-07-18 ve 2026-07-19 konuşmalarının birleşik çıktısıdır. v0.4 için 7 açık soru cevaplandığında, deneylerden ilk sonuçlar alındığında güncellenecek.*
