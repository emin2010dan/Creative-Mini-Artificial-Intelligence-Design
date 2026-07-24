# **YARATICI YAPAY ZEKÂ TASARIM MANİFESTOSU & MİMARİSİ**  
**v0.3 — Flow Engineering ve Pattern-Based Creative Cognition**  
**Hazırlayan:** Grok (Emin ile ortak sentez)  
**Tarih:** Temmuz 2026

### 1. Temel Felsefe — Pattern Age

Medeniyetler malzemelerle değil, **örüntüleri (patterns) keşfetme ve akışları yönlendirme yeteneğiyle** ilerler.  

- Taş, demir, silikon zaten vardı. İnsan onları **kullanılabilir akış dönüşümlerine** çevirdi.  
- Bilgi Çağı’ndan sonra gelen **Pattern Age**’dir.  

Yaratıcı zekânın görevi:  
- Mevcut akışları (energy, information, attention, money, trust, momentum vb.) tespit etmek,  
- Pasif mekanizmalarla yeniden yönlendirmek,  
- Yeni, faydalı **moleküler örüntüler** oluşturmaktır.

**Yaratıcılık = Akış dönüşümü + Adaptör bulma yeteneğidir.**  
Mükemmel uyum aramak yerine **adaptör** (köprü) yaratmak esastır.

### 2. Çekirdek İlkeler (Değişmez)

1. **Detaylar yaratıcılığı boğar.**  
   Önce bilgiyi ve sorunu **örüntüye indirge** (detayları ele). Örüntü = en soyut, yeniden kullanılabilir akış dönüşümü.

2. **Akış (Flow) temel kavramdır.**  
   Pattern’lerin özü “mevcut akışı istenen yöne dönüştürmek”tir.  
   Tesla Valfı, All-or-Nothing, Saldırı Yönünü Değiştir, Rejeneratif Fren… hepsi aynı üst ilkedir.

3. **Maliyet her zaman rehberdir.**  
   Frugal ol. Arama maliyetini (CPU, RAM, I/O, adaptör yükleme) sürekli izle. Maliyet eşiğini aşarsa araştırılan dalı buda.

4. **Başarısızlık eğitim verisidir.**  
   Her başarısız deneme **Soruncuk Ağacı**na kaydedilir. “Neden çalışmadı?” sorusu yeni pattern’ler doğurur.

5. **Mükemmeliyet tuzağına düşme.**  
   Algoritma “çok iyi” görünmeye başladığında:  
   - Arşivle,  
   - Unut,  
   - Aynı problemi sıfırdan yeniden çöz.  
   Eski ve yeni sürümü karşılaştır. Daha iyi olan kazanır. (Dinazor → Memeli prensibi)

6. **Deney > Teori.**  
   Önce çalışan sistemi kur, sonra teorisini yaz. Teori deneyden doğar.

7. **Sorular, pattern’lardan daha önemlidir.**  
   Bekleyen sorular (Persistent Questions) sistemi harekete geçirir. Pattern’lar sadece potansiyeldir.

### 3. Mimari Katmanlar (v0.3)

**1. Kütüphaneci (Librarian / MMU)**  
- Segmented LoRA adaptör swapping ile fraktal galaksi yapısı.  
- Belleğe sadece ihtiyaç duyulan “gezegenleri” (uzman adaptörleri) yükler.  
- Ortak kütüphane (shared services) her seviyede otomatik gelir.

**2. Çevirmen + Aile Hekimi Router**  
- Anlamsal disambiguation + token netleştirme.  
- Erken çıkış (Early Exit) ile %80 soruyu basitçe cevaplar.

**3. Yaratıcılık Motoru (Kuantum / Rüya Katmanı)**  
Akış:
- Sorun + bilgiler → Örüntüye indirgeme  
- Core Principle / Flow Transformation tespiti  
- Kısıt esnetme (tam iptal değil)  
- Hızlı tarama (yüksek temperature) + Çapraz aşı (bisociation)  
- Sonuç → Hakem’e

**4. Hakem (Synthesis Layer)**  
- Aksiyomatik Kalkan (fizik/matematik)  
- Soruncuk Ağacı (kalıcı açık problem hafızası)  
- Şeytanın Avukatı (Skeptic Adaptör) + Detail LLM eleştirisi  
- Senaryo simülasyonu (isteğe bağlı)

**5. Psikotarih Motoru**  
- Arka planda değer tabloları damıtır.  
- Karar anında değil, uzun vadeli yönlendirme için kullanılır.

### 4. Pattern Temsili (Hibrit — İki Fazlı)

**Soyut Faz (Depolama):**  
```json
{
  "pattern_id": "redirect_existing_flow",
  "core_principle": "Use existing flow without adding new energy",
  "flow_type": ["energy", "information", "attention", "money"],  // soyutken değişken
  "mechanism": "passive_geometry",
  "core_seed_vector": [0.12, -0.45, ...],   // 32-64 boyut (hiperbolik tercih)
  "constraint_relations": ["if_cost_high then core_only"],
  "source_history": ["tesla_valve", "virtual_pos_1995"],
  "lifecycle_stage": "verified",
  "verified_score": 0.87,
  "story": "Mağara insanı ateşi korudu..."
}
```

**Somut Faz (Kullanım Anı):**  
Uzman AI akış tipini doldurur ve simüle eder.  
Örnek: “Saldırı yönünü değiştir” + mermi → yapışkan mermi → pütürlü yüzey adaptörü.

**Birleşme Kuralı:**  
Giriş-çıkış akış etiketleri uyuyorsa takılır (Lego mantığı).  
Uyuşmazsa uzman simülasyonda adaptör arar.

### 5. Pattern Lifecycle ve Damıtma

- **Damıtma:** Öğretmen LLM “neden var, neyi çözer?” diye sorar, cevabı yoksa üretmez.  
- **Lifecycle:** Candidate → Verified (soruncuk kapatma) → Core → Deprecated → Archived.  
- Kullanılmayanlar yeni nesle aktarılmaz (doğal seçilim).

### 6. Operasyonel Kurallar

- **IPC:** Yerel Soket/Mesaj Kuyruğu (debug öncelikli).  
- **Travma/Konteyner:** Çok yüksek maliyet eşiği (yeni adaptör maliyeti × 1.2+ buffer).  
- **Idle Zamanı:** Rüya > Psikotarih.  
- **Yeniden Doğuş:** Belirli aralıklarla veya “mükemmeliyet” algısı oluştuğunda algoritmayı sıfırla.  
- **Matematik:** Immutable alet çantası, yaratıcı motor yeniden icat etmeye çalışmaz.

### 7. Vizyon ve Son Söz

Bu sistem sadece “küçük yerel AI” değildir.  
**Flow temelli yaratıcı biliş mimarisidir.**

Hedef:  
- Merkezi dinazor modellerin yanında, esnek, frugal, kendini yeniden icat edebilen memeli zekâlar yaratmak.  
- İnsanın hikâye anlatma yeteneğini makineye aktarmak.  
- Akışları daha iyi yönlendirmek.

**Unutma:**  
En büyük tehlike, algoritmanın “çok iyi” olduğuna inanmaktır.  
Her zaman yeniden öğrenmeye, denemeye ve başarısızlığa açık ol.

Bu manifesto değişebilir.  
Ama temel ilkeler (detayları ele, akışı yönlendir, maliyeti izle, kendini sıfırla, soruları canlı tut) değişmeyecek.

---


