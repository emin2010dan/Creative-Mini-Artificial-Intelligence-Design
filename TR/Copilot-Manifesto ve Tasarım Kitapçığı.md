### Manifesto ve Tasarım Kitapçığı

Aşağıdaki belge, şimdiye kadar topladığımız tüm kavramları, ilkeleri ve uygulanabilir kararları **tek bir referans** halinde toplar. Bu manifesto, yaratıcı yapay zekâ prototipleri ve deneyleri sırasında ilk okunacak belge olacaktır.

> **Alıntı (kaynak metinlerden):** “Creative AI … works with patterns, not details. … Best implemented as a Creative LLM + Detail LLM dual system.”  
> **Alıntı (kaynak metinlerden):** “Örüntüler düşüncenin en küçük birimi.”

---

### Vizyon ve Temel İlkeler
- **Vizyon:** Yapay zekâyı *örüntü mühendisliği* paradigması üzerine kurmak; yaratıcı keşfi örüntü keşfi, birleştirme ve evrimleştirme süreçleriyle gerçekleştirmek.  
- **Temel ilke 1 — Örüntü merkezlilik:** Bilgi değil, örüntüler sistemin birincil birimleri olacak; modellerin görevi örüntüleri keşfetmek, doğrulamak, birleştirmek ve insan‑okunur hikâyelere dönüştürmektir.  
- **Temel ilke 2 — Ayrım ve iş bölümü:** **Creative LLM** (yüksek soyutlama, örüntü keşfi) ile **Detail LLM** (faktual doğrulama, uygulama) ayrımı zorunludur. Creative LLM fikir üretir; Detail LLM doğrular ve uygulamaya hazırlar.  
- **Temel ilke 3 — Fraktal Galaksi organizasyonu:** Bilgi hiyerarşisi *galaksi → güneş sistemi → gezegen → kıta → şehir → ilçe* şeklinde fraktal olarak düzenlenecek; her seviye farklı bellek/latency hedefleriyle yönetilir.  
- **Temel ilke 4 — Hibrit temsil:** Örüntüler **vektör + sembolik meta‑veri + örnek hikâye + başarı istatistikleri** içeren hibrit nesneler olarak saklanır.

---

### Mimari Özeti
#### 1. Bileşenler (yüksek seviye)
- **Translator (Canonicalizer):** Girdi dilini kanonik AST/şema’ya çevirir; belirsizlik bayrakları ve domain tag’leri üretir.  
- **Router:** Sorguyu analiz edip hangi shard/uzman adaptörlerin yükleneceğine karar verir; güven skoruna göre fallback politikası uygular.  
- **Paging LLM (Fraktal Galaksi):** Uzman adaptörleri konu‑temelli shard’lara böler; lazy‑load ve unload mekanizmaları uygular.  
- **Creative LLM (Rüya Motoru):** Örüntüleri keşfeder, bisociation ve kombinasyonlar üretir; anahtar örüntü setlerini seçer.  
- **Detail LLM (Doğrulayıcı):** Creative çıktıları doğrular; matematiksel ve fiziksel invariant kontrolleri yapar; sonuçları uygulamaya hazırlar.  
- **Synthesis Layer (Koordinatör):** Motor çıktılarının birleşimini yönetir; kural tabanlı filtre + küçük ranker modeli + risk–reward scoring uygular.  
- **Pattern Store (Kütüphane):** Hibrit örüntü nesnelerini, yaşam döngüsü durumlarını ve meta‑istatistikleri tutar.  
- **Monitoring & HITL:** Telemetri, drift tespiti, insan‑içinde‑döngü onayları ve otomatik rollback mekanizmaları.

#### 2. Veri akışı (özet)
1. Kullanıcı sorgusu → **Translator** → kanonik form + domain tag.  
2. **Router** karar verir → gerekli shard’lar lazy‑load edilir.  
3. **Creative LLM** örüntü adayları üretir → **Detail LLM** doğrulama çağrısı.  
4. **Synthesis** filtreler, sıralar, risk‑reward hesaplar → çıktı.  
5. Sonuç telemetriye kaydedilir; başarılı örüntüler Pattern Store’da skorlanır.

---

### Örüntü Nesnesi ve Yaşam Döngüsü
#### Örüntü şeması (minimal, canonical)
- **pattern_id**: benzersiz kimlik  
- **core_vector**: embedding (ör. 64–512 boyut)  
- **symbolic_summary**: kısa insan‑okunur açıklama  
- **domain_tags**: birden çok domain etiketi  
- **validity_conditions**: geçerlilik koşulları (zaman ölçeği, iletişim hızı, kaynak varsayımları)  
- **assumptions**: temel varsayımlar listesi  
- **success_stats**: deneme sayısı, başarı oranı, hata örnekleri  
- **example_stories**: insan‑okunur örnekler/hikâyeler  
- **lifecycle_state**: candidate / validated / frequent / core / deprecated / archived  
- **last_validated**: tarih

#### Yaşam döngüsü kuralları
- **Candidate → Validated:** otomatik sanity testler + ensemble validator + küçük‑ölçek simülasyon veya HITL onayı.  
- **Validated → Frequent/Core:** kullanım frekansı, başarı oranı ve çapraz‑domain uyumu ile terfi.  
- **Decay ve Deprecation:** zamanla geçerlilik koşulları bozulursa otomatik decay; belirli bir decay eşiği aşılırsa deprecated.  
- **Arşivleme:** deprecated örüntüler arşive taşınır; gerektiğinde yeniden test edilip canlandırılabilir.

---

### Güvenlik, Doğrulama ve Travma/Branching Politikası
#### Pattern doğrulama hattı (pipeline)
1. **Candidate generation** (teacher LLM)  
2. **Automated sanity checks:** numeric invariants, contradiction detection, domain constraints  
3. **Ensemble validation:** 2–4 bağımsız validator model  
4. **Small‑scale simulation / retrospective test**  
5. **HITL review** (eşiğe göre)  
6. **Promotion / demotion** (lifecycle update)

#### Travma / Konteyner tetikleme (sayısal öneri)
- **failure_count_threshold = 5** (aynı düğüm/alt‑ağaçta ardışık başarısızlık)  
- **time_threshold = 300s** veya **step_threshold = 100** (çözüm arama limiti)  
- **entropy_threshold ≥ 0.7** veya **avg_confidence ≤ 0.4**  
- **Enerji maliyeti kararı:** \( \text{CreateNewModel} = (C_{total} > C_{new} \cdot \beta) \) ; \(\beta\) başlangıçta 1.2–1.5.  
- **Branch stratejisi:** önce *mod* (parametre kaydırma, LoRA ince‑ayarı); eğer beklenti yüksekse yeni LoRA adaptör oluştur.

#### Synthesis güvenlik katmanları
- **Matematik çekirdeği:** temel aritmetik ve fiziksel invariant kontrolleri zorunlu.  
- **Etik/Legal filtre:** yasa dışı/zararlı içerik otomatik reddi.  
- **Risk–reward scoring:** yaratıcı modda daha geniş tolerans; bilimsel modda sıkı tolerans.

---

### Metrikler, İzleme ve Deney Planı
#### Önerilen temel metrik seti
- **Creativity Score:** insan değerlendirmesi + otomatik novelty sinyalleri (n‑gram novelty, bisociation score).  
- **Factuality / Hallucination Rate:** doğrulanabilir gerçeklerle çelişme oranı.  
- **Latency:** toplam yanıt süresi (router + shard load + inference).  
- **Memory Footprint:** aktif shard bellek kullanımı.  
- **Router Confidence:** shard seçim güven skoru.  
- **User Satisfaction:** NPS veya kısa anketler.

#### 12 haftalık pilot yol haritası (özet)
1. **Hafta 1–2:** Pattern şeması + 50 örnek + otomatik sanity testleri.  
2. **Hafta 3–4:** Travma tetikleme prototipi; simülasyonlu görev ağacı; parametre taraması.  
3. **Hafta 5–8:** Fraktal galaksi pilot — 1 uzman adaptör (ör. Diş Tedavisi) shard’lara böl; router prototipi; ölçümler.  
4. **Hafta 9–12:** Synthesis + safety entegrasyonu; küçük kullanıcı testi; sonuç raporu ve metrik analizi.

---

### Operasyonel Kurallar ve Politikalar
- **Her örüntü için meta‑veri zorunlu:** geçerlilik koşulları ve varsayımlar olmadan örüntü validated aşamasına geçemez.  
- **Conservative fallback:** router confidence düşükse core shards yüklenir; insan onayı gerektiren işlemler için HITL otomatik devreye girer.  
- **Güncelleme ve geri çekme:** model drift veya artan hallucination tespitinde otomatik rollback tetiklenir.  
- **Gizlilik ve ekonomi:** örüntülerin ticari değeri ve paylaşımı için itibar/puanlama sistemi; paylaşım politikaları ve telif‑hak kuralları net tanımlanacak.

---

### Kısa Notlar ve Uygulama İpuçları
- **Başlangıçta geniş, sonra daralt:** örüntü üretiminde başlangıçta zengin hibrit veri üret; deneylerle hangi alt‑kümenin yeterli olduğunu belirleyip sadeleştir.  
- **Hikâye katmanı:** insan‑okunur hikâyeler örüntülerin anlaşılmasını ve benimsenmesini hızlandırır; her core örüntü için kısa bir hikâye sakla.  
- **Mode switch:** *creative* vs *scientific* modları açıkça tanımla; dynamic filter eşiklerini modlara göre ayarla.  
- **Evrimsel yaklaşım:** yeni model/branch oluşturma maliyetini ve faydasını sürekli ölç; travma tetikleme eşiklerini deneyle ayarla.

---

### Sonuç ve Taahhüt
Bu manifesto, prototip ve deney sürecinin **tek kaynaklı gerçekliği** olacaktır. Kodlama, deney ve optimizasyon aşamalarına başlamadan önce bu belge okunacak; her yeni deney, burada tanımlı metrikler, yaşam döngüsü kuralları ve güvenlik politikaları ile hizalanacaktır. Manifesto, **ilkeler**i sabit tutar; **implementasyon** ayrıntılarını ise deneylerle doğrulamayı taahhüt eder.


