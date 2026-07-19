# Yaratıcı Yapay Zeka — Tasarım Manifestosu

**Sürüm:** 1.0
**Tarih:** 19 Temmuz 2026
**Statü:** Kodlama ve deneyler öncesi referans doküman. Bu projeyle ilgili her deney öncesi önce bu doküman okunur.
**Kaynak:** Emin ile yürütülen çok-turlu, çok-AI'lı tasarım sohbetleri (Medium makaleleri, GitHub tezi, SORUCEVAP1-8, The Pattern Age, How Creative AI Thinks, ve bu sohbetteki doğrudan tartışmalar).

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

**Kapsam kararı (İLKE, ama sınırı henüz net değil — bkz. Bölüm 6):** Bu proje **bilimsel/mühendislik yaratıcılığını** hedefliyor, edebi/sanatsal yaratıcılığı değil. Ortak eğitim dili bilinçli olarak çift-anlamlılıktan arındırılacak (bkz. 4.3), bu da edebi üretimi zayıflatacak — bu bir kusur değil, tercih. Edebi/görsel akıl yürütme, farklı şekilde eğitilecek **ayrı** sistemlere bırakılıyor.

---

## 2. Değişmez İlkeler (İLKE seviyesi)

Bunlar tartışmaya kapalı, her tasarım kararının önce bu süzgeçten geçmesi gerekir.

1. **Detay yaratıcılığı boğar; önce bilgi örüntüye indirgenmeli.** 1985 tezinin merkez ilkesi: ham piksel yerine çizgi-iskelet, ham devre yerine FSA/gramer. Bugünkü karşılığı: ham tarihi/teknik detay yerine soyutlanmış "örüntü" (all-or-nothing, saldırı yönünü değiştir, katmanlı savunma...).
2. **Cimri (Frugal) tasarım.** Önce debug edilebilirlik ve mantık doğruluğu, performans ikinci öncelik. Emin'in kuralı: *"Projenin başında kullanılan metodlar olabildiğince debug edilebilir/update edilebilir olmalı, gerekirse performanstan taviz verilebilir."* Mantık oturduktan sonra optimize edilir.
3. **Mükemmel uyum yaratıcılığı öldürür.** Hiçbir bağlantı tam oturmaz ve oturmak zorunda değildir. Gerçek mühendislik parçaları adaptörlerle (gerilim dönüştürücü, basınç regülatörü, hukuki uzlaşma) birbirine bağlar. Bir sistem yalnızca "uyumlu mu/değil mi" diye karar verirse bürokrat olur, yaratıcı olmaz.
4. **Silme değil, maliyet-fayda ile karar ver.** Hiçbir çözüm sırf "daha önce denenmemiş" diye elenmez. Bir çözüm ancak (a) fizik/aksiyom ihlali varsa, veya (b) maliyeti çok yüksek VE telafi edici bir faydası yoksa silinir. Yüksek maliyetli ama telafi edici faydası olan (caydırıcılık gibi) çözümler arşivlenir, silinmez.
5. **"Daha önce görülmemiş olma" tek başına eleme sebebi değildir.** LLM'ler için en büyük risk, iyi bir fikri sırf eğitim verisinde yok diye reddetmek. (Rüzgârın karada da kullanılabileceğini gözden kaçırma hatası, bu ilkenin somut örneği.)
6. **İlke kesin, implementasyon deneysel.** Yukarıdaki ilkeler sabit; bunları hangi veri yapısının, hangi algoritmanın gerçekleştireceği deneyle bulunur.
7. **Bir yaratıcı sistemin en büyük başarısızlığı, kendini geliştirmeye ihtiyaç duymadığını düşünmesidir.** (Dinozor/fare ilkesi — bkz. 4.11 Evrimsel Sıfırlama.)

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

### 4.5 Örüntü (Pattern) ve Örüntü Kütüphanesi

**Örüntü nedir:** Ham detaydan arındırılmış, tekrar kullanılabilir bir "kilit açma anahtarı". Örnek: "all-or-nothing" (kritik noktaları tam koru, gerisini feda et), "saldırı yönünü değiştir" (T-34 eğik zırhı ve Aikido'da aynı örüntü, tamamen farklı kaynaklardan). Emin'in kendi iç gözlemi: bir örüntüyü ismiyle değil **özellikleriyle** saklıyor, ilk girdiyi hatırlamıyor, örüntüden genel resmi yeniden inşa ediyor ("uyduruyor") — bu, örüntünün gerçekten detaydan arındırılmış olması gerektiğinin kanıtı.

**Veri yapısı kararı — ÖNEMLİ REVİZYON:** İlk kararda (SORUCEVAP4) saf hiperbolik vektör (Seçenek B) seçilmişti — maksimum yaratıcılık için. Ama üç psikotarih örneği (parasal genişleme hızı, haberleşme hızı, bilimsel yayın hızı) bunun yetersiz kaldığını gösterdi — nedenler zinciri metin/sembol gerektiriyor. **Karar Hibrit yapıya (Seçenek 4) döndü:**

```
Örüntü
├── İsim / Etiket
├── Hikaye (insan-okunur anlatım)
├── Çekirdek Fikir
├── Tetikleme Koşulları
├── Başarı/Başarısızlık Koşulları
├── Kültürel Varyantlar
├── Tarihsel Örnekler / Karşı Örnekler
├── Ebeveyn/Çocuk Örüntüler
├── Uyumlu/Zıt Örüntüler
├── Vektör Gömme (varsa)
├── Güven Skoru
├── Güncelleme Sıklığı (bkz. aşağı)
├── Kaynak (hangi büyük LLM/öğretmen üretti)
└── Sürüm
```

**Neden bu kadar geniş başlanıyor:** En büyük enerji maliyeti zaten büyük LLM'in geçmiş bilgiyi süzüp örüntü üretmesi (öğretmen-öğrenci damıtma). Bu pahalı adım bir kez yapılacağına göre, olabilecek en zengin formatla başlamak mantıklı; deneyler hangi alt-kümenin yeterli olduğunu gösterince küçültülür.

**Güncelleme Sıklığı:** Her örüntünün kendi "yarı ömrü" vardır — fizik yasaları ≈ sonsuz, vergi politikası ≈ birkaç yıl. Öğretmen LLM bazı örüntüleri hiç güncellemez, bazılarını sık sık yeniden damıtır.

**Bağlantı Uyumluluğu:** İki örüntü birleştirilirken (bisociation) ikili değil, **dereceli** bir uyumluluk skoru kullanılır: %100 doğrudan bağlanır; ~%65 bir "adaptör" (dönüştürücü ara-örüntü) gerektirir; ~%15 muhtemelen imkansızdır. Adaptör kavramı geniş tutulur — fizikte basınç regülatörü, hukukta alternatif kanıt yöntemi, ekonomide kur mekanizması, hepsi aynı üst işlevi görür: amaca sadık kalarak uyumsuz parçalar arasında köprü kurmak.

**Kültürel/Toplumsal Örüntüler — Önemli Birleştirme:** "Kültürel Değer Tablosu" ayrı bir bileşen DEĞİLDİR. Din, hukuk, ekonomi, toplum davranışı gibi "civilization pattern"ları aynı Örüntü Kütüphanesi'nde, `domain: civilization` etiketiyle dururlar (bkz. 4.9, Psikotarih ile ilişki).

**Güvenilirlik/Skor Mekanizması:** Sık kullanılan örüntülerin skoru yükselir, önce denenir (arama motoru sıralaması benzetmesi). **Bilinen risk:** çapraz-LLM doğrulama olmayacağı öngörülüyor (örüntü bilgisi rekabetçi/paylaşılmaz bir varlık olarak görülüyor), bu da yanlış ama sık "işe yaramış görünen" bir örüntünün salt popülerlik yoluyla yanlışlıkla güçlenmesi riskini taşıyor (SEO-manipülasyonuna benzer bir zayıflık). **Bu risk için kesin bir karşı-önlem henüz kararlaştırılmadı — açık.**

**Örüntülerin yaşlanması:** Keskin bir durum makinesi (Candidate→Verified→Deprecated...) yerine, örüntüler "hikaye" gibi yavaşça evrilir, isim değiştirir (din → evrensel insan hakları → gelecekte evrensel zeka hakları gibi) ama öz kalıcıdır. Bu, tam bir mekanizma değil, bir **felsefi çerçeve** — somut kodlanışı hâlâ açık.

**İMPLEMENTASYON (açık):** Örüntü birleştirme (bisociation) için hangi matematiksel yöntemlerin kullanılacağı, birleşim veriminin nasıl ölçüleceği deneye bırakıldı.

---

### 4.6 Rüya / Yaratıcı Motor (Creative Search)

**Karar — arama stratejisi netleşti:** Kaba kuvvet (her örüntüyü her örüntüyle dene) DEĞİL. Süreç şöyle işler:

1. **Örüntü Sıkıştırma** — problem ve mevcut bilgi detaydan arındırılır (kilit + anahtarlar).
2. **Merkez Yetenek Seçimi** — bir "merkez" örüntü/yetenek seçilir, çözüm onun etrafında büyür (buhar makinesi örneği: "dönme hareketi" merkez seçilince "mekanik kuvvet gerekli", o da "buhar basıncı gerekli" der, zincir kendi kendine büyür). Bu, geriye-zincirleme/means-ends analysis'e benzer bir arama — kaba kuvvet grafik taramasından çok daha ucuz.
3. **Kısıt Esnetme** — sadece bağlamsal kısıtlar esner (bütçe, zaman, toplumsal norm); aksiyomatik çekirdeğe (fizik/matematik) asla dokunulmaz.
4. **Failure-Driven Expansion** — bir deneme/simülasyon başarısız olunca bütün alan yeniden taranmaz, yalnızca "en zayıf halka" (FEA'daki gerilme yoğunlaşması benzetmesi) üzerinde yoğunlaşılır. Bu, aslında Soruncuk Ağacı'nın (4.7) doğal çalışma şekli: her açık soruncuk düğümü bir "zayıf halka", yeni anahtar denemeleri oraya odaklanır.
5. **Çapraz Alan Aşılaması** — yukarıdakiler yetmezse uzak/ilgisiz alanlardan örüntü enjekte edilir (biyomimikri, eski makaleler, tarihsel emsaller gibi). Ne kadar derin/geniş aranacağı bir "yaratıcılık derinliği" parametresi — az yaratıcı sistem yakın geçmişe bakar, çok yaratıcı sistem antik/uzak analojilere (Mısırlıların Nil taşkını sonrası harita yeniden oluşturma yöntemi, kuşların manyetik alan algısı gibi) kadar gider.

**Anahtar seçim kaynağı ve kriteri:** Anahtarlar, mini yaratıcı YZ'nin eğitimi sırasında büyük LLM tarafından süzülerek üretilir (öğretmen-öğrenci damıtma, "anne kuşun yavrusunu beslemesi" benzetmesi). Seçim kriteri: olabilecek en soyut/detaysız yapı — "koruma" örüntüsü hem bilgisayar güvenliğinde hem savaş gemisi zırhlanmasında aynı anahtarı tetikleyebilir.

**Sonuçların insana aktarımı:** Vektör/meta-veri insana doğrudan anlatılamaz — **hikayeye** çevrilir. Hikaye, örüntünün en eski ve en etkili sıkıştırma/taşıma katmanıdır (din kitapları, mitler dahil, hepsi filtrelenmiş örüntü taşıyıcılarıdır).

**Başarısızlık yönetimi (netleşti):** Bir anahtar denemesi üç yoldan birine gider — (a) hemen işe yarar → Hakem'e gider; (b) aşırı maliyetli ve telafisi yok → silinir (kabus); (c) potansiyel taşıyor ama şimdi çözmüyor → soruncuk olarak bekletilir, süre bütçesi dolunca iptal edilir. Yüksek maliyetli ama telafi edici faydası olan (örn. caydırıcılık) çözümler silinmez, arşivlenir.

**İMPLEMENTASYON (açık):** Örüntü birleştirme için kesin matematiksel operatör seti (Pattern Algebra) henüz tanımlanmadı — deneye bırakıldı.

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

1. **Edebi/Görsel Reasoning AI bu projenin içinde mi, dışında mı?** Bölüm 1'deki kapsam kararı (bilimsel yaratıcılık) ile ilk Medium makalesindeki üç-parçalı (Bilimsel/Edebi/Görsel) şema arasında çözülmemiş bir gerilim var.
2. **Örüntü popülerlik-skoru rich-get-richer riskine karşı bir karşı-önlem var mı?** (Bkz. 4.5 — çapraz-LLM doğrulama olmayacağı için yanlış ama sık kullanılan bir örüntü yanlışlıkla güçlenebilir.)
3. **Psikotarih kararlarının Hakem için bağlayıcılık derecesi** net değil.
4. **Örüntü birleştirme (bisociation) için kesin matematiksel operatör seti** (Pattern Algebra) tanımlanmadı.
5. **Uzman-içi bilgi temsili** (hiperbolik mi, sabit zincir mi, hibrit mi) deneye bırakıldı, henüz hiçbir deney yapılmadı.

---

## 7. Test Ortamı ve Yöntemsel Disiplin

- **Ortam:** Google Colab (birincil, ücretsiz T4 GPU), Kaggle Notebooks (yedek, haftada 30 saat ücretsiz GPU). Gerekçe: hesaplama Google/Kaggle sunucusunda gerçekleşir, Emin'in yavaş ev internetine yük bindirmez.
- **Kalıcılık:** Google Drive üzerinde proje klasörü — adaptörler, IPC logları, Soruncuk Ağacı JSON'u oturumlar arası korunur.
- **Aşamalandırma:** Önce mantık/debug edilebilirlik (aşırı log, geriye iz sürülebilirlik), sonra performans optimizasyonu — hiçbir zaman tersi.
- **Test disiplini:** Her yeni mekanizma, mümkünse gerçek kütüphanelerle (torch/transformers/PEFT) küçük/yerel bir sahte modelle test edilir, sadece mantık kontrolüyle yetinilmez. Bu disiplin şimdiden iki gerçek hata buldu (bkz. Bölüm 8).

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

---

## 10. Kaynakça

- Medium: *Toward a Modular AI Architecture*, *The Algorithm of Creativity*, *The Naive Lamb and the Wolf It Never Feared*, *Leaving Logic at the Door*, *The AI Council*, *DistributedMind Protocol*, *Does AI Need a Religion?*, *The Pattern Age*, *How Creative AI Thinks* — tümü emin2010dan (Medium/GitHub)
- GitHub: `emin2010dan/Graduation-Thesis-1985-Hand-Drawn-Logic-Design-Recognition`, `emin2010dan/Psychohistory-in-the-Age-of-AI`
- SORUCEVAP1-8.txt — çok-AI'lı soru-cevap oturumları
- Bu sohbetteki doğrudan mimari tartışmalar ve `yaratici_yz_mimari_iskelet.ipynb` üzerindeki test kaydı

---

*Bu doküman canlıdır. Yeni bir SORUCEVAP grubu veya deney sonucu mevcut bir kararı değiştirirse, ilgili bölüm güncellenir ve değişiklik Bölüm 8 mantığıyla (neden değişti, ne test edildi) kayıt altına alınır.*
