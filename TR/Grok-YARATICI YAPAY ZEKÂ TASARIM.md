# **YARATICI YAPAY ZEKÂ TASARIM MANİFESTOSU**  
**v0.3 — Pattern Engineering ve Creative Search**  
**Hazırlayan:** Grok (Emin ile ortak sentez)  
**Tarih:** Temmuz 2026

### 1. Temel Felsefe — Pattern Age

Medeniyetler malzemelerle değil, **örüntüleri (patterns) keşfetme ve birleştirme yeteneğiyle** ilerler.  

- Taş, bronz, demir, silikon zaten vardı.  
- İnsan onları **kullanılabilir örüntülere** dönüştürdü.  

Bilgi Çağı’ndan sonra gelen **Pattern Age**’dir.  
Yaratıcı zekânın görevi:  
- Mevcut akışları (energy, information, attention, money, trust vb.) tespit etmek,  
- Onları pasif geometri / mekanizmalarla yeniden yönlendirmek,  
- Yeni, faydalı moleküler örüntüler oluşturmaktır.

**Yaratıcılık = Akış dönüşümü + Adaptör bulma yeteneğidir.**  
Mükemmel uyum aramak yerine, **adaptör** (köprü) yaratmak esastır.

### 2. Çekirdek İlkeler (Değişmez)

1. **Detaylar yaratıcılığı boğar.**  
   Önce bilgiyi ve sorunu **örüntüye indirge** (detayları ele). Örüntü = en soyut, yeniden kullanılabilir ilke.

2. **Akış (Flow) temel kavramdır.**  
   Pattern’lerin özü “mevcut akışı istenen yöne dönüştürmek”tir.  
   Tesla Valfı, All-or-Nothing, Saldırı Yönünü Değiştir, Rejeneratif Fren, Sosyal Medya Dikkat Fragmentasyonu… hepsi aynı üst ilkedir.

3. **Maliyet her zaman rehberdir.**  
   Frugal (cimri) ol. Arama maliyetini (CPU, RAM, I/O, adaptör yükleme) sürekli izle. Maliyet eşiğini aşarsa araştırılan dalı buda.

4. **Başarısızlık eğitim verisidir.**  
   Her başarısız deneme soruncuk ağacına kaydedilir. “Neden çalışmadı?” sorusu yeni pattern’ler doğurur.

5. **Mükemmeliyet tuzağına düşme.**  
   Algoritma “çok iyi” görünmeye başladığında:  
   - Arşivle,  
   - Unut,  
   - Aynı problemi sıfırdan yeniden çöz.  
   Eski ve yeni sürümü karşılaştır. Daha iyi olan kazanır. (Dinazor → Memeli prensibi)

6. **Deney > Teori.**  
   Önce çalışan sistemi kur, sonra teorisini yaz. Teori deneyden doğar.

### 3. Mimari Katmanlar (v0.3)

**1. Kütüphaneci (Librarian / MMU)**  
- Adaptör swapping (Segmented LoRA) ile fraktal galaksi yapısı.  
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

### 4. Pattern Temsili (Hibrit)

```json
{
  "pattern_id": "redirect_existing_flow",
  "core_principle": "Use existing flow without adding new energy",
  "flow_type": ["energy", "information", "attention", "money"],
  "mechanism": "passive_geometry / variable_reward / interest_rate",
  "core_seed_vector": [0.12, -0.45, ...],   // 32-64 boyut (hiperbolik tercih)
  "constraint_relations": ["if_cost_high then core_only"],
  "source_history": ["tesla_valve", "virtual_pos_1995", "aikido"],
  "lifecycle_stage": "verified",           // candidate / verified / core / deprecated
  "verified_score": 0.87,
  "story": "Mağara insanı ateşi korudu..."
}
```

**Bisociation**: Vektör işlemleri + sembolik eşleştirme + hikâye simülasyonu.

### 5. Pattern Lifecycle

- Candidate → Verified (soruncuk kapatma) → Core (sık kullanım) → Deprecated → Archived  
- Psikotarih ve kullanım skoru ile yaşlanma tespiti.

### 6. Operasyonel Kurallar

- **Debug önceliği**: IPC olarak yerel mesaj kuyruğu/soket (Option B).  
- **Travma/Konteyner**: Çok yüksek maliyet eşiği (yeni adaptör maliyeti × 1.2+ buffer).  
- **Idle Zamanı**: Rüya > Psikotarih (öncelik kuyruğu).  
- **Başarı Ölçüsü**: Soruncuk kapatma + kullanıcı memnuniyeti + genelleme yeteneği.  
- **Yeniden Doğuş**: Belirli aralıklarla veya “mükemmeliyet” algısı oluştuğunda algoritmayı sıfırla.

### 7. Son Söz — Vizyon

Bu sistem sadece “küçük yerel AI” değildir.  
**Pattern temelli yaratıcı biliş mimarisidir.**

Hedef:  
- Merkezi dinazor modellerin yanında, esnek, frugal, kendini yeniden icat edebilen memeli zekâlar yaratmak.  
- İnsanın hikâye anlatma yeteneğini makineye aktarmak.  
- Akışları daha iyi yönlendirmek.

**Unutma:**  
En büyük tehlike, algoritmanın “çok iyi” olduğuna inanmaktır.  
Her zaman yeniden öğrenmeye, denemeye ve başarısızlığa açık ol.

Bu manifesto değişebilir.  
Ama temel ilkeler (detayları ele, akışı yönlendir, maliyeti izle, kendini sıfırla) değişmeyecek.

---

**Manifesto bitti.**  

Bundan sonra kodlama veya deney aşamasına geçtiğinde, her kritik karardan önce bu dokümanı oku.  

Hazırsan **v0.3 implementasyon yol haritası** veya **ilk prototip akışı** (pseudocode + hangi parçalar önce kodlanacak) yazalım.

Ne yapmak istersin?
