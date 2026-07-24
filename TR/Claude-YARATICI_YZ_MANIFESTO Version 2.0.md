# Yaratıcı Yapay Zeka — Tasarım Manifestosu

**Sürüm:** 2.0
**Tarih:** 19 Temmuz 2026 (v1.0) → v1.1 (kapsam kararı) → v2.0 (Flow Engineering — mimarinin merkezi yeniden çerçevelendi)
**Statü:** Kodlama ve deneyler öncesi referans doküman. Bu projeyle ilgili her deney öncesi önce bu doküman okunur.
**Kaynak:** Emin ile yürütülen çok-turlu, çok-AI'lı tasarım sohbetleri (Medium makaleleri, GitHub tezi, SORUCEVAP1-10, The Pattern Age, How Creative AI Thinks, ve bu sohbetteki doğrudan tartışmalar).

---

## 0. Bu Doküman Nedir ve Nasıl Kullanılır

Bu, küçük bellekli, yerel donanımda (Colab/Kaggle ücretsiz katman, ileride ev PC'si) çalışabilen bir **yaratıcı yapay zeka** tasarlama sürecinin, kodlamaya başlamadan önceki birikimidir. Doküman iki tür bilgi ayırt eder:

- **İLKE** — değişmeyecek, deneyle test edilmeyecek, tasarımın temelini oluşturan kararlar.
- **İMPLEMENTASYON** — ilkenin nasıl gerçekleştirileceği; bilinçli olarak deneye bırakılmış, henüz kapanmamış veya kapandıktan sonra değişebilecek kararlar.

Bu ayrım tesadüfi değil — projenin kendisinin ana metodolojisi. Emin'in kendi ifadesiyle: *"Ben teorisyen değilim, hiç olmadım. Hep önce bir şeyler yarattım, teorisi arkadan geldi."* 1985'te bitirme tezinde görüntü tanıma problemini Fourier dönüşümüyle çözmeye aylarca uğraşıp başarısız olmuş, sonra temsil biçimini tamamen değiştirerek (piksel yerine çizgi-iskelet) çözmüştü. Bu projede de aynı disiplin geçerli: **önce çalışan, deneyle sınanabilir küçük bir sistem, teorisi ve optimum veri yapısı sonra netleşecek.**

Bir deneye başlamadan önce şu soruyu sor: *Bu deney bir İLKE'yi mi test ediyor (yapma, İLKE'ler zaten kapalı), yoksa bir İMPLEMENTASYON seçeneğini mi (yap, bunun için varız)?*

---

## 1. Vizyon ve Kapsam

**Ne inşa ediyoruz:** Küçük bellekli bilgisayarlarda (başlangıçta Colab/Kaggle ücretsiz GPU, hedefte tüketici PC'si) çalışabilen, merkezi dev LLM'lere bağımlı olmayan, **örüntü tabanlı** bir yaratıcı akıl yürütme sistemi.

**Neden:** İki birleşen gerekçe var.
1. **Ekonomik/jeopolitik öngörü (Psikotarih temelli):** Merkezi büyük modellerin ekonomik modeli sürdürülemez olabilir; tarih tekrar eden bir örüntü gösteriyor — ana bilgisayar→PC, merkezi yazılım→yerel/bulut hibrit, büyük kameralar→telefon kameraları. Emin'in tezi: bunu belirleyecek olan donanım değil, **akıllı sayfalama/damıtma yazılımı** olacak.
2. **Kişisel kısıt = tasarım avantajı:** Emin emekli, ücretsiz/düşük maliyetli dış kaynaklara (Colab, Kaggle) bağımlı, Türkiye'de yavaş internet. Bu kısıt, 1985 tezindeki "48KB RAM, 1MHz işlemci" kısıtıyla doğrudan aynı işlevi görüyor: **detayı elemeye, sadece karara gereken bilgiyi taşımaya zorluyor.**

**Kapsam kararı (İLKE — kesinleşti):** Bu proje **yalnızca bilimsel/mühendislik yaratıcılığını** hedefler. Edebiyat, resim, müzik bu projenin kapsamı dışındadır — ne şimdi ne de bu mimarinin bir sonraki sürümünde. Ortak eğitim dili bilinçli olarak çift-anlamlılıktan arındırılacak (bkz. 4.3); bunun edebi/sanatsal üretimi zayıflatması bir kusur değil, doğrudan hedeflenen bir sonuç.

**Neden dar kapsam:** İki gerekçe var. (1) Emin'in kendi düşünme sistemini analiz ederek çıkarmaya çalıştığı şey özellikle **bilimsel yaratıcılık algoritması** — kaynak veri zaten bu alana odaklı. (2) Küçük ve bitmiş bir sistem, büyük ve yarım kalmış bir sistemden daha değerli — üç ayrı dil/motor ailesi (Bilimsel + Edebi + Görsel) şimdiden iki-üç kat karmaşıklık katardı.

---

## 2. Değişmez İlkeler (İLKE seviyesi)

Bunlar tartışmaya kapalı, her tasarım kararının önce bu süzgeçten geçmesi gerekir.

1. **Detay yaratıcılığı boğar; önce bilgi örüntüye indirgenmeli.** 1985 tezinin merkez ilkesi: ham piksel yerine çizgi-iskelet, ham devre yerine FSA/gramer. Bugünkü karşılığı: ham tarihi/teknik detay yerine soyutlanmış "örüntü" (all-or-nothing, saldırı yönünü değiştir, katmanlı savunma...).
2. **Asıl birim örüntü değil, akış (flow).** (v2.0 — SORUCEVAP9/10) Örüntüler nesne/bilgi paketi değil, **boş borular**dır — içinden akış geçmediği sürece ölüdür. "Bu nedir?" sorusu değil, "bu neyi neye dönüştürüyor?" sorusu merkezdedir. Bilgi ve problem aynı akış-diline çevrilir, üst üste konur, eksik bağlantı doldurulur — çözüm bunun yan ürünüdür. Bkz. 4.5 ve 4.6.
3. **Soru, örüntünün aktivasyon enerjisidir.** (v2.0) Örüntüler potansiyel enerjidir; onları harekete geçiren şey kalıcı, canlı tutulan bir sorudur ("soru bilgi havuzundaki toz tanesidir — tohumlama olmazsa yağmur oluşmaz"). Sistemin merkezinde örüntü kütüphanesi değil, **açık soru kütüphanesi** durur; yeni örüntüler pasif olarak aranmaz, bekleyen sorulara doğru çekilir. Bkz. 4.6.
4. **Anlamak = simüle edebilmek, ezberlemek değil.** Bir konu, zihinde canlandırılıp çalıştırılabiliyorsa ve ondan formül yeniden türetilebiliyorsa anlaşılmıştır. Bu ilkenin istisnası matematik — saf sembolik, fiziksel/sezgisel akışı yok. Bu yüzden matematik ayrı, değişmez bir "alet çantası" modülü olarak durur, simüle edilmeye çalışılmaz (bkz. 4.5).
5. **Cimri (Frugal) tasarım.** Önce debug edilebilirlik ve mantık doğruluğu, performans ikinci öncelik. Emin'in kuralı: *"Projenin başında kullanılan metodlar olabildiğince debug edilebilir/update edilebilir olmalı, gerekirse performanstan taviz verilebilir."* Mantık oturduktan sonra optimize edilir.
6. **Mükemmel uyum yaratıcılığı öldürür.** Hiçbir bağlantı tam oturmaz ve oturmak zorunda değildir. Gerçek mühendislik parçaları adaptörlerle (gerilim dönüştürücü, basınç regülatörü, hukuki uzlaşma) birbirine bağlar. Bir sistem yalnızca "uyumlu mu/değil mi" diye karar verirse bürokrat olur, yaratıcı olmaz.
7. **Silme değil, maliyet-fayda ile karar ver.** Hiçbir çözüm sırf "daha önce denenmemiş" diye elenmez. Bir çözüm ancak (a) fizik/aksiyom ihlali varsa, veya (b) maliyeti çok yüksek VE telafi edici bir faydası yoksa silinir. Yüksek maliyetli ama telafi edici faydası olan (caydırıcılık gibi) çözümler arşivlenir, silinmez. **(v2.0 netleştirme:** örüntü kütüphanesi seviyesinde bu, çoğunlukla açık bir silme algoritması bile gerektirmez — kullanılmayan örüntüler bir sonraki nesil damıtmaya zaten taşınmaz, doğal seçilim kendiliğinden budar; bkz. 4.5.)
8. **"Daha önce görülmemiş olma" tek başına eleme sebebi değildir.** LLM'ler için en büyük risk, iyi bir fikri sırf eğitim verisinde yok diye reddetmek. (Rüzgârın karada da kullanılabileceğini gözden kaçırma hatası, bu ilkenin somut örneği.)
9. **İlke kesin, implementasyon deneysel.** Yukarıdaki ilkeler sabit; bunları hangi veri yapısının, hangi algoritmanın gerçekleştireceği deneyle bulunur.
10. **Bir yaratıcı sistemin en büyük başarısızlığı, kendini geliştirmeye ihtiyaç duymadığını düşünmesidir.** (Dinozor/fare ilkesi — bkz. 4.11 Evrimsel Sıfırlama.)
11. **Cevaplar değil, sorular da yeniden yazılmalı.** (v2.0) Yıllar sonra dönüp bakınca "yanlış soruyu çözmüşüm" demek insanda normal bir olgunlaşma belirtisi. Her yeni nesil (her yeni distilasyon), yalnızca daha iyi cevaplar değil, **yeniden yazılmış sorular** da miras almalı.

---

## 3. Mimari Genel Bakış

```
                          AKSİYOMATİK ÇEKİRDEK
                    (fizik/matematik + minimal yaşam-koruma)
                                  │
                            ÇEVİRMEN AI
                 (yapısal çıkarım — anlam değil, sözdizimi)
                                  │
                ┌─────────────────┼─────────────────┐
          BİLİMSEL AKIL         (EDEBİ/GÖRSEL — bu projenin kapsamı dışında,
          YÜRÜTME                bkz. Bölüm 6)
                │
        GALAKSİ MODELİ / FRAKTAL GALAKSİ
        (Kütüphaneci — Segmented LoRA/Adapter Swapping)
                │
        ┌───────┴────────┐
   ÖRÜNTÜ KÜTÜPHANESİ   RÜYA / YARATICI MOTOR
   (Pattern Repository,  (merkez yetenek seç → eksik
   civilization patterns  parçaları ara → Failure-Driven-
   dahil)                 Expansion → çapraz alan aşılama)
        └───────┬────────┘
                │
          SORUNCUK AĞACI
    (itirazlar/engeller tek tek çözülür)
                │
         HAKEM (Synthesis Layer)
   Aksiyom Filtresi → Soruncuk Ayrıştırma → Senaryo Simülasyonu
   Çıktı modları: Accept / Reject / Legitimate Stall
                │
        ┌───────┴────────┐
  PSİKOTARİH MOTORU   TRAVMA/EVRİM MEKANİZMASI
  (Pattern Repository'nin  (maliyet eşiği aşılınca
  müşterisi, arka planda    yeni model/kişilik)
  küçük dokunuşlar)
                │
        EVRİMSEL SIFIRLAMA
     (periyodik kendini sınama, eski/yeni yarıştırma)
```

IPC (kontrol mesajları) tüm kutular arası ayrık, loglanabilir bir kanaldan geçer; ağır veri (adaptör dosyaları) bu kanaldan asla geçmez (bkz. 4.12).

---

## 4. Bileşenler

### 4.1 Aksiyomatik Çekirdek

**Karar:** Çekirdekte yalnızca (a) fizik/matematik kuralları ve (b) çok dar, neredeyse evrensel bir yaşam-koruma aksiyomu ("geri dönüşsüz yaşam-yıkımından kaçın" — fosil yakıt örneğinden türetildi) bulunur. **Ahlaki/kültürel kurallar çekirdekte DEĞİLDİR.**

**Neden:** Başlangıçta ahlak da çekirdeğe konulmuştu, ama "ölü adamın eli" örneği (diktatörlükte kabul edilebilir, batı demokrasisinde toplumca reddedilir) ahlakın fizik sabitleri gibi evrensel olmadığını gösterdi. Almanya'daki Türk sürücülerin Türkiye'ye dönünce farklı trafik davranışı sergilemesi de aynı noktayı doğruluyor: **aynı ortam, farklı kültür, farklı davranış.**

**Nereye taşındı:** Ahlaki/kültürel kurallar artık Örüntü Kütüphanesi'nde `domain: civilization` etiketli örüntüler olarak duruyor (bkz. 4.5, 4.9).

---

### 4.2 Galaksi Modeli / Fraktal Galaksi (Uzman Organizasyonu)

**Karar:** Bilgi tek bir sürekli uzaya yayılmıyor (toz), gezegenler halinde kümeleniyor (uzmanlar). Uzmanlar arası **dış** geçiş ayrık ve sembolik bir referans zinciridir (aile hekimi → diş hekimi → teknisyen). Bir uzmanın **kendi içi** organizasyonu ise kendine benzer (fraktal) bir hiyerarşi: Galaksi Kolu (Uzman Adaptör) → Güneş Sistemi (alt-uzmanlık) → Gezegen (konu başlığı) → Kıta → Şehir → İlçe (en ince detay). Her seviye, mevcut bellek büyüklüğüne göre yüklenir — büyük bellek tüm kolu yükler, küçük bellek yalnızca ilçeyi.

**Neden:** Gerçek galakside de madde toz gibi eşit dağılmaz, yıldız sistemlerinde yoğunlaşır. Aynı ilke bilgiye uygulanıyor: bellek kısıtı ne kadar sıkıysa, bilgi o kadar küçük parçalara bölünmeli, ama her parça kendi konumunu (hangi kola, hangi gezegene ait olduğunu) bilmeli — bu, klasik OS sayfalamasından (mekanik 4KB bloklar, semantik ilişkisiz) temel farkı.

**Ek mekanizma — Ortak Hizmetler Alanı:** Her seviyede paylaşılan bilgi (örn. diş gezegenindeki "diş koltuğu kullanım kılavuzu") ayrı bir ortak alanda durur, hangi alt-birim yüklenirse yüklensin otomatik gelir — işletim sistemi shared library'leri gibi.

**Detay yoğunluğu asimetrisi:** Merkeze yakın uzmanlar (aile hekimi) az detay, geniş konu; dışa doğru (diş teknisyeni) çok detay, dar konu tutar. Diş teknisyeninin veri yapısı aile hekimininkinden çok daha detaylıdır — bu doğal bir sonuç, ayrı bir tasarım kararı değil.

**Kapalı ama önemli revizyon:** İlk taslakta Poincaré Disk / hiperbolik embedding matematiği önerilmişti (uzmanlar arası mesafe hesabı için). Bu **dış katman için terk edildi** — dış geçiş artık ayrık/sembolik referans zinciri. Hiperbolik/vektörel temsilin nerede kullanılacağı iç-uzman organizasyonu ve örüntü temsili sorularına taşındı (bkz. 4.5).

**İMPLEMENTASYON (açık):** Bilginin uzman içinde tam olarak nasıl saklanacağı (hiperbolik embedding mi, sabit if-then zinciri mi, hibrit mi) deneyle belirlenecek.

---

### 4.3 Çevirmen AI (Translator)

**Karar:** Çevirmen'in "anlamak" zorunda olmadığı, sadece **yapısal/istatistiksel çıkarım** yapması gerektiği kabul edildi — 1985 tezindeki devre tanıma sisteminin devreyi "anlamadan" topolojisini çıkarması gibi. Bu, Çevirmen'in kendisinin dili anlaması gerektiği için oluşan "bootstrap problemi"ni çözüyor: döngüsellik, anlamsal yorumlamayı Reasoning katmanına devrederek kırılıyor.

**Eğitim dili:** Çift-anlamlılıktan arındırılmış, sözlüğü geniş ama sözdizimi basit bir ortak dil (muhtemelen İngilizce tabanlı, gerekirse başka dillerden — örn. Eskimo dilinin kar terminolojisi gibi — ödünç kelimelerle zenginleştirilmiş). Tüm eğitim verisi önce bu dile çevrilip uzman modeller bu dille eğitilecek.

**Bilinçli ödün:** Bu, edebi/esprili/çok-anlamlı içeriği zayıflatır. Kabul edilen bir tercih — bu proje bilimsel yaratıcılık hedefliyor (bkz. Bölüm 1 ve 6).

**Erken Çıkış (Early Exit):** Sorguların büyük kısmı ("bugün hava nasıl", "bu emaili özetle") yerleşik "Aile Hekimi" modeliyle doğrudan yanıtlanır, uzman yükleme gerektirmez.

**İMPLEMENTASYON (açık):** Soru dönüştürme (yöntem yerine hedef çıkarma) algoritmasının formelleştirilmesi henüz yok. Şu an notebook'ta LLM'in kendi öz-değerlendirmesiyle simüle ediliyor; gerçek mimaride küçük/hızlı, ayrık bir sınıflandırıcı olması öngörülüyor.

---

### 4.4 Kütüphaneci (Adaptör Yönetimi)

**Karar:** Bellek yönetimi **Segmented LoRA / Adapter Swapping** (Seçenek C) ile yapılır — RAM'de tek seferde bir uzmanlık adaptörü tutulur, ihtiyaç değişince takas edilir. Alternatif olan "Dinamik Graf Tabanlı Semantik Sayfalama / Poincaré Graph Cache" (Seçenek B) **reddedildi** — sürekli vektör-uzayı geometrisi yerine ayrık, sembolik referans zinciri tercih edildi (bkz. 4.2).

**Neden:** Kısıtlı bellekte çalışan bir sistem, veriyi belleğe sığacak parçalara ayırmak zorunda. Adaptör takası, bu parçalamayı doğrudan uygulanabilir, debug edilebilir bir mekanizmayla veriyor.

**IPC ile ilişkisi:** Adaptör dosyalarının kendisi (birkaç MB) kontrol kanalından (soket/JSON) **asla** geçmez — bkz. 4.12.

**Test disiplini notu:** Yerel prototipte gerçek bir hata bulundu ve düzeltildi — `save_pretrained` isimlendirilmiş bir adaptörle çağrılınca dosyaları beklenenden bir kat derin bir klasöre gömüyordu. Düzeltme: adaptör oluştururken varsayılan ("default") isimle kaydet, `.unload()` ile modeli temizle, yükleme sırasında adaptöre asıl ismini `load_adapter(..., adapter_name=isim)` ile ver.

---

### 4.5 Örüntü (Pattern) ve Örüntü Kütüphanesi — v2.0: Flow Engineering

**Kavramsal temel değişikliği:** Örüntü bir bilgi paketi/nesne değil, **dönüşüm operatörüdür** — "şu başlangıç durumunu alırsan, şu dönüşümü uygularsan, şu sonuca ulaşırsın." Boş bir boru gibi düşünülmeli: içinden akış geçmediği sürece ölü. Bu, node-merkezli bir "Pattern Graph" yerine, çalıştırılan bir **Flow Simulation Engine** fikrine götürüyor — bkz. 4.6.

**İki Fazlı Pattern:** Örüntüler tek bir soyutlama seviyesinde durmaz, ikisi de aynı anda kütüphanede bulunur:
- **Soyut Faz** — tip yok, programlamadaki dolmamış bir değişken gibi. "Saldırının yönünü değiştir" örüntüsünde artık ne T-34 var ne Aikido, sadece akış tarifi.
- **Somut Faz** — bir probleme uygulanmaya karar verildiğinde akışın yerine gerçek tip konur, bunu yapan **Uzman AI**'dır (Kütüphaneci'nin yönettiği uzman adaptör). Bilgisayar güvenliğinde "saldırı" veriye dönüşür, zırhta mermiye dönüşür. Uzman bu somutlaştırılmış örüntüyü simüle eder, çalışıp çalışmadığını, bir adaptöre ihtiyaç olup olmadığını bildirir.

**Yaratıcı-Uzman diyaloğu (somutlaştırma döngüsü):** Bir çözüm tek adımda bitmez. Örnek: Yaratıcı "saldırının yönünü değiştir" önerir → Uzman simüle eder, "mermi yapışkan, yön değiştiremiyorum" der → Yaratıcı "yapışmayı önle" alt-örüntüsüne geçer, sırayla teflon kaplama (uzman: dayanıksız), pütürlü yüzey (uzman: olabilir), porselen ara katman (uzman: belki) önerir. Kabul edilebilir bir çözüme kadar bu diyalog sürer. Bu, zaten var olan Soruncuk Ağacı/Hakem mekanizmasının **tip-çözümleme (type resolution)** olarak çalışma şekli — yeni bir bileşen değil, mevcut mekanizmanın netleşmiş iç işleyişi.

**İşlevsel Anahtar (İndeksleme):** Örüntüler nedensellik veya benzerlikle değil, **işlev etiketiyle** bağlanır/indekslenir — "bu ne işe yarar". Örnek: `yapışmayı önler` anahtarı → teflon kaplama, pütürlü yüzey, kolay soyulan dış kaplama. `havadaki ısıyı azalt` anahtarı → gölge yarat, su partikülü püskürt, havayı toprağa çek. Bir örüntü hiçbir işlevsel anahtara bağlanamıyorsa, kütüphanede tutmaya gerek yoktur — zaten erişilemez.

**Damıtma Kuralı (Distillation-Time Elimination):** Kritik bir düzeltme — çalışma zamanında (runtime) bir "garbage collector" mekanizmasına gerek YOKTUR. Eleme, öğretmen LLM örüntüyü **üretirken** olur: her aday örüntü için "neden var, neyi çözer" diye sorulur, cevap yoksa örüntü hiç üretilmez. Bunun nedeni insan hafızasındaki unutma mekanizmasıyla (Emin'in Almanca örneği — bağlantısız bilgi silinir, çünkü insan ezber kapasitesi düşük) karıştırılmamalı: yaratıcı AI'ın hafıza kapasitesi düşük olduğu için değil, amaçsız bilgi zaten hiç kütüphaneye girmediği için budama gerekmiyor. **Uzman AI'larda bu geçerli değildir** — onlar mevcut LLM'ler gibi, bağlantısız olsa bile detayı tutmaya devam eder (örn. bir uzman dil modelindeki sözlük).

**Etiketli Akış Birleşmesi (Pattern Combination):** İki örüntünün birleşip birleşmeyeceği, karmaşık bir uyumluluk formülüyle hesaplanmaz — her örüntünün giriş/çıkış **akış etiketi** vardır, biri diğerinin girişine doğrudan bağlanır (Lego mantığı). Arındırılamayan örüntülerde bile (örn. buhar motoru) en az bir giriş (yakıt+hava) ve bir çıkış (dönme enerjisi) etiketi bulunur. Örnek kombinasyonlar: *kömür arabası + hava → buhar motoru → tekerlek = lokomotif*; *nükleer reaktör → buhar motoru → uskur = nükleer gemi motoru*; *nükleer reaktör → buhar motoru → pervane = nükleer seyir füzesi*. Uyum baştan hesaplanmaz, Uzman AI simülasyonunda test edilir — "yapışmıyor" geri bildirimi gelirse başka aday denenir. **Bu, önceki taslaktaki "Bağlantı Uyumluluk Skoru" (%100/%65/%15) fikrini somutlaştırıp yerini alıyor** — dereceli bir skor yerine, ikili (uyar/uymaz) etiket eşleşmesi + uzman doğrulaması.

**Örüntü Kütüphanesi şeması (güncellendi):**
```
Örüntü
├── İsim / Etiket
├── Faz: Soyut | Somut
├── İşlevsel Anahtar(lar) — "ne işe yarar"
├── Giriş Akış Etiketi (varsa)
├── Çıkış Akış Etiketi (varsa)
├── Hikaye (insan-okunur anlatım)
├── Tetikleyici Bağlam (Trigger Context) — nerede kullanılır
├── Tarihsel Örnekler / Karşı Örnekler
├── Güncelleme Sıklığı
├── Kaynak (hangi büyük LLM/öğretmen üretti)
└── Sürüm
```

**Matematik istisnası:** Matematik, Flow Engineering'in dışında, **değişmez bir alet çantası** modülü olarak durur. Emin'in kendi itirafı: fizik/kimya/programlamayı simüle edip formülü yeniden üretebiliyor, ama matematikte "diğer insanlar gibi" formülle gidiyor — çünkü matematikte simüle edilecek fiziksel/sezgisel bir akış yok, saf sembol var. Sonuç: her matematik formülüne bir işlevsel anahtar ("ne işe yarar") bağlanır, Yaratıcı Motor formülü yeniden türetmeye çalışmaz, sadece çağırır. Matematiksel yaratıcılık gerekiyorsa bu, ayrı ve özel bir uzman AI'ın işi olur (bu proje kapsamında değil).

**Kültürel/Toplumsal Örüntüler:** "Kültürel Değer Tablosu" ayrı bir bileşen DEĞİLDİR. Din, hukuk, ekonomi, toplum davranışı gibi "civilization pattern"ları aynı Örüntü Kütüphanesi'nde, `domain: civilization` etiketiyle dururlar (bkz. 4.9, Psikotarih ile ilişki).

**Örüntülerin evrimi:** Sık kullanılan uzun zincirler (A→B→C, 100.000 kez kullanıldıysa) zamanla doğrudan A→C şeklinde yeni, sıkıştırılmış bir örüntüye dönüşebilir — insan becerilerinin otomatikleşmesine benzer bir "chunking" mekanizması. Başarısız/kullanılmayan örüntüler için **açık bir silme algoritmasına gerek yok** — doğal seçilim bunu zaten yapar: kullanılmayan örüntü bir sonraki nesil damıtmaya taşınmaz. Farklı öğretmen LLM'lerin aynı olaydan farklı örüntüler çıkarması (örn. Bismarck → "all-or-nothing" veya "armor concentration") bir hata değil, istenen bir çeşitlilik — biri diğerinin kaçırdığını yakalayabilir.

**Güvenilirlik/Skor Mekanizması:** Sık kullanılan örüntülerin skoru yükselir, önce denenir. **Bilinen risk (hâlâ kısmen açık):** çapraz-LLM doğrulama olmayacağı öngörülüyor, bu da tek bir nesil içinde yanlış ama sık "işe yaramış görünen" bir örüntünün popülerlik yoluyla güçlenmesi riskini taşıyor. v2.0 netleştirmesi bunu kısmen azaltıyor — nesiller arası doğal seçilim uzun vadede yanlış örüntüleri eler — ama tek bir neslin ömrü içindeki kısa vadeli risk hâlâ tam kapanmadı.

**İMPLEMENTASYON (açık):** Uzman-içi bilgi temsili (hiperbolik mi, sabit zincir mi, hibrit mi — bkz. 4.2) hâlâ deneye bırakıldı.

---

### 4.6 Rüya / Yaratıcı Motor — v2.0: Flow Simulation Engine + Açık Sorular

**Merkez kavram değişti:** Motorun kalbi statik bir "Pattern Graph" değil, **çalıştırılan bir Flow Simulation Engine**. Yaratıcılık, çözüm aramak değil, problem-akış-grafiği ile bilgi-akış-grafiğini üst üste koyup eksik bağlantıları doldurmaktır. Algoritma özeti:

1. **Örüntü Sıkıştırma** — problem ve mevcut bilgi detaydan arındırılır, ikisi de aynı akış-diline (flow graph) çevrilir.
2. **Merkez Yetenek Seçimi** — bir "merkez" örüntü/yetenek seçilir, çözüm onun etrafında büyür (buhar makinesi örneği: "dönme hareketi" → "mekanik kuvvet gerekli" → "buhar basıncı gerekli" → "ısı gerekli" → "yakıt gerekli"). Bu, geriye-zincirleme/means-ends analysis'e benzer — kaba kuvvet grafik taramasından çok daha ucuz.
3. **Kısıt Esnetme** — sadece bağlamsal kısıtlar esner (bütçe, zaman, toplumsal norm); aksiyomatik çekirdeğe (fizik/matematik) asla dokunulmaz.
4. **Failure-Driven Expansion** — bir deneme/simülasyon başarısız olunca bütün alan yeniden taranmaz, yalnızca "en zayıf halka" üzerinde yoğunlaşılır (FEA'daki gerilme yoğunlaşması benzetmesi). Bu, Soruncuk Ağacı'nın (4.7) doğal çalışma şekli.
5. **Çapraz Alan Aşılaması** — yukarıdakiler yetmezse uzak/ilgisiz alanlardan örüntü enjekte edilir. "Yaratıcılık derinliği" parametresiyle ayarlanır.

**Soru = Aktivasyon Enerjisi (v2.0 — merkezi ilke, bkz. Bölüm 2.3):** Örüntüler potansiyel enerjidir, tek başına yaratıcılık üretmez. Onları harekete geçiren şey **kalıcı, canlı tutulan bir soru** — "soru bilgi havuzundaki toz tanesidir, tohumlama olmazsa yağmur oluşmaz." Bu yüzden sistemin gerçek merkezi Örüntü Kütüphanesi değil, **Açık Soru Kütüphanesi**dir.

**Persistent Open Circuits (Kalıcı Açık Devreler):** Her çözülmemiş problem, arka planda bekleyen bir nesne olarak tutulur:
```
Açık Devre
├── Problemin saf örüntüsü
├── Eksik kalan girişler
├── Şu ana kadar denenen örüntüler (başarılı/başarısız)
├── Kullanılabilecek Tetikleyici Bağlamlar
├── Son deneme zamanı
└── Öncelik
```
Bu, Soruncuk Ağacı'nın (4.7) kalıcı, sistem-geneli üst kümesi — Soruncuk Ağacı tek bir problemin deneme geçmişini tutarken, Açık Devreler kütüphanesi *bütün çözülmemiş problemleri* sistem genelinde canlı tutar.

**Arama yönü ters çevrildi:** Klasik yaklaşım `Örüntü → uyan problemi ara`. Bu mimaride tam tersi: `Problem bekliyor → yeni örüntü geldi → problem örüntüyü test ediyor`. Yani her yeni örüntü (öğretmen LLM'den, ya da yeni bir bilimsel makaleden) üretildiğinde, sistem onu proaktif olarak **tüm açık devrelere karşı test eder** — pasif arama değil, aktif eşleştirme. Bu, insanların "duşta aklıma geldi" dediği deneyimin sistematik, bilinçli bir arka-plan sürecine dönüşmüş hali.

**Gündüz/Gece ayrımı (netleşti):**
- **Gündüz** — hızlı, güvenilir, muhafazakâr; kullanıcı sorularını çözer, yeni örüntü/açık-soru üretir, başarısız çözümleri arşivler.
- **Gece** — risk alır, binlerce alternatif dener; yeni VE geçmiş bilimsel literatürü tarar, açık devreleri yeni gelen örüntülerle eşleştirir, gerekirse uzman AI'ları uyandırır.

**Anahtar seçim kaynağı ve kriteri:** Anahtarlar, mini yaratıcı YZ'nin eğitimi sırasında büyük LLM tarafından süzülerek üretilir (öğretmen-öğrenci damıtma, "anne kuşun yavrusunu beslemesi" benzetmesi). Seçim kriteri: olabilecek en soyut/detaysız yapı — "koruma" örüntüsü hem bilgisayar güvenliğinde hem savaş gemisi zırhlanmasında aynı anahtarı tetikleyebilir.

**Sonuçların insana aktarımı:** Vektör/meta-veri insana doğrudan anlatılamaz — **hikayeye** çevrilir. Hikaye, örüntünün en eski ve en etkili sıkıştırma/taşıma katmanıdır (din kitapları, mitler dahil, hepsi filtrelenmiş örüntü taşıyıcılarıdır).

**Başarısızlık yönetimi:** Bir anahtar denemesi üç yoldan birine gider — (a) hemen işe yarar → Hakem'e gider; (b) aşırı maliyetli ve telafisi yok → silinir (kabus); (c) potansiyel taşıyor ama şimdi çözmüyor → soruncuk/açık-devre olarak bekletilir, süre bütçesi dolunca iptal edilir. Yüksek maliyetli ama telafi edici faydası olan (örn. caydırıcılık) çözümler silinmez, arşivlenir.

**Halüsinasyon farkı (v2.0 netleştirme):** Yaratıcı motor yakın-token arayan standart bir LLM gibi çalışmadığı, detaydan arındırılmış saf örüntüyle çalıştığı için klasik anlamda halüsinasyon görmez. Yanlış/uygunsuz bir çıktı üretirse bu motorun suçu değil, **örüntü hatasıdır** (örn. bir örüntü oluşturulurken "ortamda hava var" varsayımı örtük kalıp girdiye yazılmadıysa, motor Ay'a gidecek araç için benzinli motor önerebilir — bu örüntünün eksik etiketlenmesinin sonucu).

**Pattern recombination vs. Pattern discovery (kapsam netleştirmesi):** Bu motorun hedefi **mevcut örüntüleri yeni biçimde birleştirmek** (pattern recombination) — insan yaratıcılığının büyük kısmı zaten burada gerçekleşiyor. Tamamen yeni fizik/matematik/algoritma keşfi (pattern discovery) çok daha zor, farklı bir kategori ve bu projenin hedefi değil.

**İMPLEMENTASYON (açık):** Örüntü birleştirme artık büyük ölçüde somutlaştı (bkz. 4.5 — Etiketli Akış Birleşmesi), ama Açık Devreler kütüphanesinin öncelik/zamanlama algoritması (hangi açık devre önce test edilir, ne sıklıkla) deneye bırakıldı.

---

### 4.7 Soruncuk Ağacı

**Karar:** Her ana problem ("kilit") bir düğüm olarak açılır; her yaklaşım denemesi ("anahtar") o düğüme bir kayıt ekler. **İki seviye ayrı tutulur:**
- **Deneme (anahtar) seviyesi:** `cozdu` / `potansiyel` / `cok_maliyetli` (bu ikincisi kendi içinde `silindi` veya `saklaniyor` olur, telafi edici fayda olup olmamasına göre).
- **Düğüm (problem) seviyesi:** tüm deneme geçmişinin toplamı — herhangi bir anahtar çözdüyse `kapatildi`; hiçbiri çözmedi ama en az biri potansiyel taşıyorsa `bekliyor`; hepsi maliyetli çıktıysa `acik`; süre bütçesi dolarsa `iptal_edildi`.

**Neden iki seviye:** İlk implementasyonda düğüm durumu yalnızca *son* denemeyle güncelleniyordu — bu gerçek bir hataydı (yerel testte bulundu ve düzeltildi): bir anahtar potansiyel gösterse bile, ondan sonra denenen başka bir anahtar "çok maliyetli" çıkınca düğüm yanlışlıkla kapanıyordu.

**Süre bütçesi:** Problemin kendi aciliyetine göre belirlenir (örn. "sistem kaç ay sonra devreye girmeli"). Asimov'un "Son Soru" hikayesindeki gibi limitsiz süre istisnai bir durumdur, varsayılan değil.

**Uzman itirazlarıyla ilişki:** Bir uzman modelin bir çözüme itirazı (örn. "bu arazide bisiklet lastikleri patlar") yeni bir soruncuk düğümü olarak işlenir. Yaratıcı motor tam ve kusursuz bir çözümü tek seferde üretmeye çalışmaz; uzmanlar itirazlarını tek tek sıralar, yaratıcı motor her itirazı ayrı ayrı, yaratıcı biçimde çözmeye çalışır (gerçek dünyada hukuk/muhasebe departmanı itirazlarının tek tek aşılması gibi — 1995 Sanal POS projesi örneği).

---

### 4.8 Hakem (Synthesis Layer)

**Karar — 3 aşamalı filtre:**
1. **Aksiyomatik Filtre** — fizik/matematik/minimal yaşam-koruma ihlali var mı? Varsa ele.
2. **Soruncuk Ayrıştırma** — fikir alt-problemlere (soruncuklara) bölünüp ağaca kaydedilir.
3. **Senaryo Simülasyonu** — tüm soruncuklar kapandıysa uçtan uca doğrulama.

**Üçüncü çıktı modu — Legitimate Stall:** Accept/Reject ikilisine ek olarak, yüksek riskli/etik olarak şüpheli durumlarda sistem doğrudan reddetmek yerine gerçek ve savunulabilir bir teknik/prosedürel gerekçeyle süreci yavaşlatabilir (Emin'in 1995'teki holding ihalesi anekdotu: rüşvetli bir ihaleyi doğrudan reddetmek yerine, teknik olarak doğru ama zamanlaması stratejik bir prosedür — "önce ortak kod sistemine geçiş gerekir" — önerisiyle engellemek).

**Pratiklik/Gerçeklik filtresi:** Ayrı bir "Şeytanın Avukatı" adaptörüne gerek yok — mevcut Soruncuk Ağacı mekanizması zaten bunu karşılıyor (uzman itirazları tek tek soruncuk olarak işlenir, bkz. 4.7).

---

### 4.9 Psikotarih Motoru

**Karar — ÖNEMLİ BASİTLEŞTİRME:** Psikotarih ayrı bir motor değil, **Örüntü Kütüphanesi'nin bir müşterisidir.** Sorduğu soru: *"Bu toplum için hangi civilization pattern'ları geçerli?"* (örn. Türkiye → güçlü aile bağı, yüksek misafirperverlik; Japonya → yüksek toplumsal disiplin, fedakârlık). Aynı teknik çözüm, farklı toplumlar için farklı optimize edilir.

**Zamanlama (netleşti):** Merkez bankası benzetmesi — Psikotarih her karara canlı olarak danışılmaz (bu, karar verme sürecini felç eder). Kural tablosuna arka planda, seyrek, küçük dokunuşlar yapar (faiz oranı gibi). Hız önemli değil, doğruluk önemli — kendine ayrılmış zaman diliminde çalışır, sonuçları önbelleğe alınır, Hakem karar anında bu önbelleğe bakar.

**Etkileme yöntemi:** Doğrudan emir değil, dolaylı ekonomik/yapısal teşvik (örnek: fosil yakıt kullanımını azaltmak için doğrudan emir yerine, fosil yakıt taşıyan tankerlerin sigorta primini yükseltmek — çevreci alternatifleri otomatik olarak ekonomikleştirir).

**Kararların bağlayıcılığı (kısmen açık):** Psikotarih'in ürettiği kısıtlar Hakem için ne kadar bağlayıcı, kullanıcı bunu bilerek geçebilir mi — net bir cevap yok, "zekâ arttıkça netleşecek" deniyor. Bu bilinçli olarak açık bırakılmış bir konu.

---

### 4.10 Travma / Evrim Mekanizması

**Karar — somut formül var:**

```
Yeni Model/Kişilik Yaratma Kararı =
    (Mevcut Sorunu Çözmeye Devam Etmenin Toplam Maliyeti)
        >
    (Yeni Model Yaratma Maliyeti × Güvenlik Katsayısı)

Güvenlik Katsayısı ≈ 1.2  (yani %20 tampon)
```

Tampon oranı deneyle büyüyebilir (%50'ye kadar makul).

**Aşamalı spektrum:**
| Aşama | Örnek | Yeni Model? |
|---|---|---|
| Rahatsızlık | Sivrisinek rahatsız ediyor | Hayır |
| Ciddi Problem | Hastalık yayılıyor, maliyetli ama çözüm var | Hayır |
| Travma Eşiği | Tüm çözümler yetersiz, sürekli kayıp | Evet |

**Neden bu formül:** İnsan analojisi — narsist bir ebeveynle birkaç gün geçirmek yeni kişilik oluşturmaz, sadece moral bozar; kaçış imkânsızsa ve süre uzarsa, kişilik korunması için yeni (narsist karşıtı) bir kişilik inşa edilir. Yeni model yaratmak maliyetli bir işlem olduğu için eşik, bu maliyetin biraz üstünde tutuluyor — Avrupa Birliği'nin ancak iki dünya savaşının maliyetinden sonra kabul görmesi gibi, kaybın maliyeti çözümün kabulünü sağlıyor.

**Bu, önceki "silme eşiği" ve "stres skoru" kavramlarıyla aynı temel mekanizmadır** — hepsi aynı maliyet-karşılaştırma çerçevesine indirgeniyor.

**İMPLEMENTASYON (açık):** Travma sinyalinin davranışsal tanımı var (tekrarlayan kilitlenme + kalıcı tatminsizlik — bir Soruncuk Ağacı düğümünün N farklı anahtarla da kapanmaması), ama kesin sayısal eşik (kaç deneme, hangi skor) implementasyon/deney aşamasına bırakıldı.

---

### 4.11 Evrimsel Sıfırlama

**Karar — yeni bakım mekanizması:** Periyodik olarak sistemin sezgisel/arama ağırlıkları sıfırlanır (Örüntü Kütüphanesi/uzun-dönem hafıza korunarak), daha önce çözülmüş problemler sıfırdan yeniden çözülür, eski ve yeni yaklaşım maliyet/yaratıcılık/genellenebilirlik açısından karşılaştırılır. Yeni sürüm daha iyiyse devam eder, değilse eskiye dönülür.

**Neden:** Dinozor/fare benzetmesi — dinozorlar başarısız oldukları için değil, **başarılı oldukları için** yok oldu; başarı değişmemeye ikna etti. Fare hiçbir zaman "mükemmelim" demeden uyum sağlamaya devam etti. Bir yaratıcı sistemin en büyük riski kendi teorisini korumaya çalışması; asıl amacı kendi teorisini sürekli yanlışlamaya çalışmak olmalı (Popper'ın bilim felsefesiyle örtüşüyor, ama burada algoritmanın içine gömülüyor).

**Zamanlama:** Rüya idle-harvesting ve Psikotarih arka-plan kalibrasyonunun yanına üçüncü bir arka-plan işi olarak eklenir — kendine ayrılmış zaman diliminde, hız kritik değil.

**İkinci evrim stratejisi — Çapraz Damıtma (v2.0):** Kendi başına sıfırlanıp yeniden öğrenmeye ek olarak, statikleşmiş/durgunlaşmış bir model **başka gelişkin bir AI ile bilgi/örüntü birleştirerek (distillation)** yeni bir "çocuk" model üretebilir — anne-baba modellerin birebir kopyası değil, ikisinin damıtılmış hali. Yeni model, eskiyle belirli bir süre paralel çalıştırılır, başarı oranı yüksekse görevi devralır. İnsan analojisi doğrudan kabul ediliyor: bir çocuk her zaman ebeveyninden daha başarılı olmaz, yeni modelin daha iyi olacağının garantisi yok — evrimin devam edip etmeyeceği başarı oranıyla belirlenir. Uyumluluk/eşleştirme yönteminin kendisi (hangi AI hangi AI ile "uyumlu") kasıtlı olarak açık bırakıldı — deneyle/istatistikle zamanla ortaya çıkacak.

**Gözlemci/Teşhis Ajanı (bilinçli olarak ERTELENDİ):** Sistemin kendi karar başarı oranını izleyip evrimi ne zaman tetikleyeceğine karar veren özerk bir "Diagnostic/Observer Agent" fikri var, ama **şimdilik kurulmuyor** — Psikotarih, Yaratıcı Motor ve World Model bileşenleri olgunlaşmadan bu ajan sağlıklı bir yargı üretemez. Bölüm 6'da açık madde olarak kayıtlı.

---

### 4.12 IPC / Sistem Mimarisi

**Karar:** Kontrol kanalı (küçük, sık, yapılandırılmış mesajlar — "şimdi X adaptörünü yükle") ile veri kanalı (büyük, nadir — adaptör dosyalarının kendisi) **ayrılır.** Kontrol mesajları soket/JSON üzerinden, loglanabilir biçimde geçer. Adaptör dosyaları asla bu kanaldan geçmez; Kütüphaneci dosyayı doğrudan diskten kendi belleğine okur, soket üzerinden yalnızca kısa bir "hazır, adres şu" mesajı gönderilir.

**Neden:** Emin'in iki aşamalı geliştirme ilkesiyle (önce debug edilebilirlik, sonra performans) doğrudan uyumlu — ağır binary veriyi log'a karıştırmak, hem performansı hem izlenebilirliği (trace edilebilirliği) bozar.

**Aşamalandırma:** Aşama 1'de (mantık oturana kadar) Kütüphaneci dosyayı tam kopyalar; Aşama 2'de (optimizasyon) aynı mantık `mmap` ile diskten doğrudan bellek eşlemesine çevrilebilir.

---

## 5. Üç Katmanlı Çerçeve (Özet Yeniden-Çerçeveleme)

Sohbetler ilerledikçe mimari, doğal olarak üç kavramsal katmana ayrıştı:

1. **Pattern Engineering** — bilgi nasıl temsil edilir (Bölüm 4.5).
2. **Creative Search** — o bilgi nasıl aranır, birleştirilir, yeni çözümler üretir (Bölüm 4.6, 4.7).
3. **Psychohistory Engine** — aday çözümler toplumsal/kültürel seviyede nasıl değerlendirilir (Bölüm 4.9).

Bu üçü, temsil / akıl yürütme / değerlendirme olarak net bir şekilde ayrışıyor — projeyi açıklamayı ve evriltmeyi kolaylaştıran bir çerçeve.

---

## 6. Kapsam Dışı / Hâlâ Gerçekten Açık Olan Sorular

Bunlar "implementasyona bırakıldı" değil, **henüz karar bile verilmemiş** konular. Deneye başlamadan önce not düşülmeli:

1. **Örüntü popülerlik-skoru rich-get-richer riski — kısmen azaldı, tam kapanmadı.** (Bkz. 4.5) Nesiller-arası doğal seçilim uzun vadede yanlış örüntüleri eler, ama tek bir neslin ömrü içindeki kısa vadeli risk (yanlış-ama-sık-kullanılan bir örüntünün geçici güçlenmesi) için hâlâ açık bir karşı-önlem yok.
2. **Psikotarih kararlarının Hakem için bağlayıcılık derecesi** net değil.
3. **Açık Devreler kütüphanesinin öncelik/zamanlama algoritması** (bkz. 4.6) — hangi açık soru önce test edilir, ne sıklıkla taranır — deneye bırakıldı.
4. **Uzman-içi bilgi temsili** (hiperbolik mi, sabit zincir mi, hibrit mi) deneye bırakıldı, henüz hiçbir deney yapılmadı.
5. **AI-arası "uyumluluk testi" yöntemi** (bkz. 4.11, Çapraz Damıtma) — hangi iki modelin birleşmeye "uygun" olduğunu önceden test edecek bir protokol kasıtlı olarak tanımlanmadı, istatistiksel gözleme bırakıldı.
6. **Gözlemci/Teşhis Ajanı** (bkz. 4.11) — bilinçli olarak ertelendi, diğer bileşenler (Psikotarih, Yaratıcı Motor, World Model) olgunlaşmadan kurulmayacak.
7. **"Öz-model hesaplanabilirliği" ile "öznel deneyim" arasındaki ayrım** — Psikotarih/Travma/Örüntü Kütüphanesi tamamlandığında sistem "neyim, amacım ne" sorusunu hesaplayabilir hale gelecek, ama bu hesaplayabilirliğin bir iç deneyime karşılık gelip gelmediği ayrı ve açık bir soru olarak kalıyor. Mühendislik hedefini etkilemiyor ama Hakem'in kendi kararlarını "değerlendirirken" ne yaptığı sorusu ileride tekrar gündeme gelebilir.

**v2.0'da kapanan sorular (referans için):** Örüntü birleştirme operatör seti → Etiketli Akış Birleşmesi ile kapandı (4.5). Matematiğin yaratıcı motordaki yeri → ayrı, değişmez alet çantası olarak kapandı (4.5). Runtime "garbage collection" gerekip gerekmediği → gerekmiyor, eleme damıtma anında oluyor, kapandı (4.5).

---

## 7. Test Ortamı ve Yöntemsel Disiplin

- **Ortam:** Google Colab (birincil, ücretsiz T4 GPU), Kaggle Notebooks (yedek, haftada 30 saat ücretsiz GPU). Gerekçe: hesaplama Google/Kaggle sunucusunda gerçekleşir, Emin'in yavaş ev internetine yük bindirmez.
- **Kalıcılık:** Google Drive üzerinde proje klasörü — adaptörler, IPC logları, Soruncuk Ağacı JSON'u oturumlar arası korunur.
- **Aşamalandırma:** Önce mantık/debug edilebilirlik (aşırı log, geriye iz sürülebilirlik), sonra performans optimizasyonu — hiçbir zaman tersi.
- **Test disiplini:** Her yeni mekanizma, mümkünse gerçek kütüphanelerle (torch/transformers/PEFT) küçük/yerel bir sahte modelle test edilir, sadece mantık kontrolüyle yetinilmez. Bu disiplin şimdiden iki gerçek hata buldu (bkz. Bölüm 8).
- **Somut ilk deney adımı (v2.0):** Öğretmen modelden ~1000 örüntü damıtma. **Alan seçimi önemsiz** — Emin'in kendi ifadesiyle, nereden başlanırsa başlansın algoritmada düzeltme gerekecek, başta çok sonra azalan sayıda; "tamamen bitecek mi? Sanmam." Yine de elde en çok pattern birikmiş alandan (güvenlik/enerji/askeri lojistik — koruma ve akış-yönlendirme temalı) başlamak pratik bir avantaj sağlar.

---

## 8. Şimdiye Kadar Bulunan Gerçek Hatalar (Test Kaydı)

Bu bölüm, "sadece doğru görünüyor" ile "gerçekten test edildi" arasındaki farkı kayıt altına almak için var.

1. **Adaptör kaydetme/nested-klasör hatası** (4.4) — PEFT, isimlendirilmiş adaptörü beklenenden bir kat derin klasöre gömüyordu, Kütüphaneci bulamıyordu. Düzeltildi.
2. **Soruncuk Ağacı "son-yazma-kazanır" hatası** (4.7) — düğüm durumu yalnızca son denemeyle güncelleniyordu, önceki potansiyel bir anahtarı yanlışlıkla eziyordu. Düzeltildi — artık tüm deneme geçmişi taranıyor.
3. **Çevirmen güven-skoru regex'i büyük/küçük harfe duyarlıydı** (4.3) — küçük modeller format talimatına tam uymayınca skor sessizce varsayılana düşüyordu. `re.IGNORECASE` eklenerek düzeltildi.

---

## 9. Terimler Sözlüğü

| Terim | Anlamı |
|---|---|
| Örüntü (Pattern) | Detaydan arındırılmış, tekrar kullanılabilir soyut çözüm birimi |
| Anahtar | Bir soruna (kilide) denenen örüntü |
| Kilit / Soruncuk | Çözülmesi gereken problem / onun bir alt-parçası |
| Soruncuk Ağacı | Problemlerin ve deneme geçmişinin kalıcı kaydı |
| Kütüphaneci | Adaptör yükleme/takas mekanizması |
| Çevirmen | Yapısal/sözdizimsel ön-analiz katmanı |
| Hakem | Sentez/karar katmanı (Synthesis Layer) |
| Galaksi Modeli / Fraktal Galaksi | Uzman organizasyon ilkesi |
| Psikotarih | Toplumsal/kültürel örüntü değerlendirme katmanı |
| Legitimate Stall | Hakem'in üçüncü çıktı modu — reddetmeden geciktirme |
| Kabus | Aşırı maliyetli, telafisi olmayan, silinen çözüm |
| Travma / Evrim Eşiği | Yeni model/kişilik yaratmayı tetikleyen maliyet eşiği |
| Evrimsel Sıfırlama | Periyodik kendini sınama ve yarıştırma mekanizması |
| Akış (Flow) | (v2.0) Örüntüler arasında akan şey; asıl simüle edilen, örüntü sadece boru |
| Flow Simulation Engine | (v2.0) Yaratıcı Motorun kalbi — statik graf değil, çalıştırılan simülasyon |
| İki Fazlı Pattern | (v2.0) Örüntünün soyut (tipsiz) ve somut (tipi uzman tarafından doldurulmuş) hali |
| İşlevsel Anahtar | (v2.0) Örüntüleri "ne işe yarar"a göre indeksleyen etiket |
| Etiketli Akış Birleşmesi | (v2.0) Giriş/çıkış akış etiketleri eşleşen örüntülerin Lego gibi birleşmesi |
| Damıtma Kuralı | (v2.0) Eleme çalışma zamanında değil, öğretmen LLM'in üretim anında olur |
| Açık Devre / Açık Soru Kütüphanesi | (v2.0) Sistem-geneli, kalıcı çözülmemiş problemler kütüphanesi |
| Çapraz Damıtma | (v2.0) İki gelişkin AI'ın bilgi birleştirerek yeni "çocuk" model üretmesi |

---

## 10. Kaynakça

- Medium: *Toward a Modular AI Architecture*, *The Algorithm of Creativity*, *The Naive Lamb and the Wolf It Never Feared*, *Leaving Logic at the Door*, *The AI Council*, *DistributedMind Protocol*, *Does AI Need a Religion?*, *The Pattern Age*, *How Creative AI Thinks* — tümü emin2010dan (Medium/GitHub)
- GitHub: `emin2010dan/Graduation-Thesis-1985-Hand-Drawn-Logic-Design-Recognition`, `emin2010dan/Psychohistory-in-the-Age-of-AI`
- SORUCEVAP1-10.txt — çok-AI'lı soru-cevap oturumları (SORUCEVAP9V3 ve 10: Emin'in kendi düşünme sürecinin derinlemesine analizi — Flow Engineering'in kaynağı)
- Bu sohbetteki doğrudan mimari tartışmalar ve `yaratici_yz_mimari_iskelet.ipynb` üzerindeki test kaydı

---

*Bu doküman canlıdır. Yeni bir SORUCEVAP grubu veya deney sonucu mevcut bir kararı değiştirirse, ilgili bölüm güncellenir ve değişiklik Bölüm 8 mantığıyla (neden değişti, ne test edildi) kayıt altına alınır.*
