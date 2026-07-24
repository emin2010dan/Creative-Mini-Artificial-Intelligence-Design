### Vizyon ve Temel İlkeler

**Vizyon**  
Yaratıcı yapay zekâyı yalnızca **Örüntü Mühendisliği** değil, daha temel bir paradigma olan **Akış Mühendisliği (Flow Engineering)** üzerine kurmak. Burada örüntüler (pattern) yalnızca dönüşüm düğümleri, yani “boru parçaları”dır; gerçek zekâ ise bu borular arasından geçen **akışı** simüle eden, çalıştıran ve dönüştüren motordur. Amaç, insan benzeri yaratıcı keşfi güvenli doğrulama hattı ve ölçeklenebilir fraktal‑paging ile üretilebilir, doğrulanabilir ve dağıtılabilir hale getirmektir.

**Temel İlkeler**  
- **Akış merkezlilik:** Bilgi, dönüşümler ve akışlar üzerinden temsil edilir; örüntü yalnızca akışın yönünü değiştiren fonksiyondur.  
- **Hibrit temsil:** Her örüntü **vektör + sembolik meta + örnek hikâye + başarı istatistikleri** içerir.  
- **İş bölümü:** **Creative LLM** akış keşfi ve kombinasyon üretir; **Detail LLM** fiziksel/mühendislik doğrulama yapar; **Synthesis Layer** koordinasyon, risk–reward ve güvenlik sağlar.  
- **Fraktal bilgi organizasyonu:** Galaksi → güneş sistemi → gezegen → kıta → şehir → ilçe hiyerarşisi; ortak hizmetler otomatik eşlik eder.  
- **Deneysel epistemoloji:** İlke sabit, implementasyon deneyle seçilir; prototipler ölçümlerle karar verir.

---

### Mimari ve Bileşenler

**Bileşenler**  
- **Translator (Canonicalizer):** Girdi → kanonik AST; belirsizlik bayrakları; domain tag.  
- **Router:** Kanonik form → shard seçimi; confidence tabanlı fallback.  
- **Paging LLM / Fraktal Galaksi:** Uzman adaptörleri topic‑shard’lara böler; lazy load/unload.  
- **Creative LLM (Rüya Motoru / Flow Compiler):** Flow graph üretir, bisociation ve kombinasyonlar dener; anahtar örüntüleri seçer.  
- **Detail LLM (Detaycı Uzman):** Fiziksel, mühendislik, yasal doğrulama; parametre hesapları.  
- **Synthesis Layer (Koordinatör):** Kural tabanlı filtre + küçük ranker; risk–reward scoring; matematik çekirdeği.  
- **Pattern/Flow Store:** Hibrit örüntü nesneleri, yaşam döngüsü, başarı istatistikleri.  
- **Monitoring & HITL:** Telemetri, drift tespiti, insan onayı, otomatik rollback.

**Veri Akışı**  
1. Kullanıcı → **Translator** → kanonik form + domain.  
2. **Router** → shard seti seçer; lazy‑load.  
3. **Creative LLM** → flow graph adayları üretir.  
4. **Detail LLM** → seçilmiş adayları doğrular; gerektiğinde geri çağırır.  
5. **Synthesis** → filtre, rank, risk değerlendirmesi → çıktı.  
6. Telemetri → Pattern Store güncellemesi (lifecycle, success_stats).

---

### Pattern ve Flow Modeli

**Konsept**  
- **Pattern = Transformation:** Girdi flow → dönüşüm → çıktı flow. Pattern yalnızca boru; akış geçtiğinde “canlanır”.  
- **Flow Graph:** Düğümler = transformation pattern; kenarlar = akış yönü; graph çalıştırılabilir (simülasyon).  

**Hibrit JSON şema örneği:**
```json
{
  "pattern_id":"all-or-nothing",
  "core_vector":[0.12,-0.45,...],
  "symbolic_summary":"Merkezi koru; kritik parçayı feda et",
  "domain_tags":["protection","strategy"],
  "validity_conditions":{"time_scale":"short","comm_speed":"low"},
  "assumptions":["centralized_control_possible"],
  "success_stats":{"trials":120,"success_rate":0.72},
  "example_stories":["mogol_kale"],
  "lifecycle_state":"validated",
  "last_validated":"2026-07-01"
}
```

**Flow Compiler (Creative LLM) davranışı**  
- **Input:** kanonik problem graph.  
- **Çıktı:** alternatif flow graph’lar (candidate solutions) + anahtar örüntü setleri.  
- **İşlem:** akış simülasyonu; kırılma noktalarını (flow stalls) tespit; eksik pattern’ları önerir; enerji/step maliyeti tahmini üretir.

---

### Doğrulama, Yaşam Döngüsü ve Travma/Branching

**Pattern Yaşam Döngüsü**  
- **Aşamalar:** candidate → validated → frequent → core → deprecated → archived.  
- **Promosyon kriterleri:** otomatik testler, ensemble validator sonuçları, küçük‑ölçek simülasyon başarıları, kullanım frekansı, çapraz‑domain uyumu.  
- **Decay:** zamanla geçerlilik koşulları bozulursa otomatik skor düşüşü; belirli eşiklerde deprecation.

**Doğrulama Pipeline**  
1. Candidate generation (teacher LLM).  
2. Automated sanity checks (numeric invariants, contradiction detection).  
3. Ensemble validation (2–4 bağımsız validator).  
4. Small‑scale simulation / retrospective test.  
5. HITL review (eşiğe göre).  
6. Promote / demote.

**Travma / Branching Kararları**  
- **failure_count_threshold = 5**  
- **time_threshold = 300 s** veya **step_threshold = 100**  
- **entropy_threshold ≥ 0.7** veya **avg_confidence ≤ 0.4**  
- **Enerji maliyeti kararı:**  
\[
\text{CreateNewModel} = \begin{cases}
\text{True} & \text{if } C_{total} > C_{new} \cdot \beta \\
\text{False} & \text{otherwise}
\end{cases}
\]
\(\beta\) başlangıçta \(1.2\)–\(1.5\).  

**“Şah Mat” ve Kök Neden Sinyali**  
- Sistem, her “neden?” adımında mevcut pattern kümesini kontrol eder: eğer mevcut küme çözüm sunuyorsa derinleşme durur. Kök‑neden tespiti için **sabit aksiyom tablosu** (ör. fiziksel invariants, insan ihtiyaçları) ve **mantıksal loop/contradiction tespiti** birlikte kullanılır.

---

### Güvenlik, Metrikler, İzleme ve Operasyonel Kurallar

**Güvenlik Katmanları**  
- **Matematik çekirdeği:** temel aritmetik ve fiziksel invariant kontrolleri.  
- **Etik/Legal filtre:** yasa dışı/zararlı içerik reddi.  
- **Risk–reward scoring:** creative modda geniş tolerans; scientific modda sıkı tolerans.  
- **HITL:** yüksek riskli çıktılar için insan onayı.

**Ölçüm Matrisi**

| **Metrik** | **Tanım** | **Hedef** |
|---|---|---|
| Creativity Score | İnsan değerlendirmesi + novelty sinyalleri | ≥ 3/5 |
| Factuality Rate | Doğrulanabilirlik; hallucination oranı | ≤ 5% |
| Latency | Router + shard load + inference | < 2s core, < 5s lazy |
| Memory Footprint | Aktif shard bellek kullanımı | Donanım hedefi |
| Router Confidence | Seçim güven skoru | ≥ 0.8 |
| User Satisfaction | NPS / anket | ≥ +30 |

**İzleme ve Rollback**  
- Halüsinasyon uyarıları, drift tespiti, kullanıcı şikâyetleri → otomatik rollback.  
- Telemetri: pattern kullanım, success_stats, validation failures, branch olayları.

**Operasyonel Kurallar**  
- Her örüntü için validity_conditions ve assumptions zorunlu.  
- Router confidence düşükse conservative core shards + HITL.  
- Yeni model/branch yalnızca enerji maliyeti kuralı sağlandığında.  
- Pattern paylaşımı ve ekonomi: itibar/puanlama sistemi; telif ve gizlilik politikaları.

---

### Pilot Yol Haritası ve Kodlama Rehberi

**12 haftalık pilot**  
1. **Hafta 1–2:** Pattern/Flow JSON şeması + 50 örnek + sanity testleri.  
2. **Hafta 3–4:** Travma tetikleme prototipi; simülasyonlu görev ağacı.  
3. **Hafta 5–8:** Fraktal galaksi pilot — 1 uzman adaptör shard’lara böl; router prototipi.  
4. **Hafta 9–12:** Synthesis + safety entegrasyonu; küçük kullanıcı testi.

**İlk kodlama rehberi**  
1. Pattern/Flow
