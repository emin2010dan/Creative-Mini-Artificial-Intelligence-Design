

---

# Psikotarih ve Modüler Yaratıcı AI - Çalışma Özeti

**Hazırlayan:** Meta AI (Muse Spark)  
**İçin:** Emin - Emekli Mühendis  
**Tarih:** 30 Haziran 2026  
**Amaç:** Yeni sohbette kaldığımız yerden devam etmek için bilgi aktarımı

---

## 1. Temel Felsefe - 1985 Tezinden Gelen İlkeler

Emin'in 1985 Apple II+ (48KB, 1MHz) bitirme tezi, bugünkü mimarinin kökü:

1. **Detayları ele, sadece karar için gerekli bilgiyi koru**
2. **Sadece gereken veriyi en kolay işlenecek şekilde belleğe yükle**
3. **En optimum metod ile sonuca ulaş**

Tezde iki katman vardı:
- **Katman 1 (Makine Kodu):** Piksel seviyesi işlemler - gürültü temizleme, iskeletleştirme
- **Katman 2 (BASIC):** Anlamsal işlemler - ilkel çıkarma, FSA ile tanıma

Bu, bugünkü "sayfalama" fikrinin atasıdır.

---

## 2. Psikotarih Çerçevesi

### Temel Formül
```
ΔS = [ ∫ (TDD × MBB × KAVM × Vf) dt + BKB ] × I
```

**Değişkenler:**
- **ΔS:** Sistemik Değişim
- **TDD:** Toplumsal Duygu Durumu (Kahraman/Fedakarlık, Kuralcı/Güven, Hırs/Çürüme)
- **MBB:** Motivasyonel Buhar Basıncı = Toplumsal Eksiklik × Kültürel Akışkanlık (içinde Umut Vektörü barındırır)
- **KAVM:** Kültürel Akışkanlık ve Viskozite Matrisi
- **Vf:** Hız Çarpanı
- **BKB:** Boyanmış Beyaz Kuğu (yapay krizler)
- **I:** Müdahale Değişkeni (11-22-33 kuşak matrisi)

**Ana İlke:** Umut olmadan motivasyon yıkıma gider. Umut varsa inovasyona.

---

## 3. Modüler AI Mimarisi (Makale 1)

### Üç Ana Bileşen

**1. Translator AI (Çevirmen)**
- Görev: Doğal dildeki belirsizliği çöz, tek anlamlı iç temsile çevir
- Örnek: "light" → LIGHT_PHYSICS_PHOTON veya LIGHT_LITERARY_METAPHOR
- İşlevler: Anlam ayrıştırma, sözdizimsel normalizasyon, alan etiketleme, niyet sınıflandırma
- Özellik: %95 güven yeterli, kalan belirsizliği aşağıya geçirmez

**2. Alan-Uzman Akıl Yürütme AI'ları**
- **Bilimsel AI:** Sıfır belirsizlik, deterministik, halüsinasyon yasak
- **Edebi AI:** Üretken belirsizlik, çağrışımsal, metafor serbest
- **Görsel AI:** Dilsel olmayan, uzamsal-desen tabanlı

**3. Dinamik Vektör Uzayları (Galaksi Modeli)**
- **Merkez:** Temel kavramlar (matematik, mantık) - düşük boyut
- **İç yörüngeler:** Alan-genel kavramlar - orta boyut
- **Dış kollar:** Uzman kavramlar - yüksek boyut
- **İlke:** Lexical density (sözcüksel yoğunluk) boyut belirler

### Synthesis Layer (Sentez Katmanı)
Dört modülün çıktısını birleştiren hakem. Monolitik LLM değil, seçici:
1. Kanuni filtre (yasal olmayanı at)
2. Amaç filtresi (kullanıcı hedefine uygun mu)
3. Maliyet filtresi (optimumdan pahalıya sırala)

---

## 4. Yaratıcılık Algoritması (Makale 2)

### Temel Sorun: Katastrofik Unutma
İnsan beyni detay saklamaz, desen saklar. AI için çözüm: **semantik konsolidasyon**

### Uyku Mekanizması
- Her N adımda modeli durdur, özet çıkar
- "Ana fikir ne? Mevcut bilgiyle çelişiyor mu?"
- Özeti sakla, ham veriyi at

### Rüyalar = Kuluçka Makinesi
- Desenler puzzle parçaları gibi
- Uzak parçaların kenarları birleşmeye çalışır
- Başarılı → yeni büyük desen (buluş)
- Başarısız → atılır (kabus)

### Sorunun Gücü
- Yöntem yüklü soru sorma: "Nasıl yürürüz?" → yürüme
- Amaç odaklı soru: "Nasıl hızlı taşınırız?" → bisiklet
- En iyi soru: "Bu binadan ne değer çıkar?" → reklam panosu

### İki Bellek Sistemi
- **Yaratıcı LLM:** Optimize desenler, az yer, hızlı tarama, detay yok
- **Detay LLM:** Ham bilgi, spesifik veri, boşlukları doldurur

### Çok Seviyeli Zoom
- Level 1: Araba = taşıyıcı
- Level 2: Araba = tekerlekli motorlu taşıyıcı
- Level 3: Araba = dört tekerlekli kapalı
- Level 4: BMW 3.20d
- İlke: Lazy evaluation - gerekenden derine inme

---

## 5. Küçük Bilgisayarda Çalışan Sayfalama LLM

### Problem
70B modeli 48KB gibi küçük belleğe sığdırmak değil, akıllı yüklemek.

### Naive Lamb Mimarisi (3 Katman)

**Katman 1 - Gürültü Temizleyici (Yönlendirici)**
- 1-3B parametre, hep resident
- Görev: Prompt'u iskelete indir, niyeti çıkar
- Çıktı: "konu=tarih+ekonomi, derinlik=orta"

**Katman 2 - Sayfalama Yöneticisi**
- Model önceden konu bazlı sayfalara bölünmüş (LoRA, MoE uzmanları)
- Sadece gereken sayfalar VRAM'e yüklenir
- Diğerleri diskte bekler

**Katman 3 - Optimum Çözücü**
- Yüklenen sayfaları birleştirir
- En küçük yeterli modeli kullanır

### Avantajlar
- Enerji maliyeti kullanıcıya geçer
- Mahremiyet artar
- Abonelik modeli mümkün (5-10$/ay)

---

## 6. Kritik Sorular ve Cevaplar

### Soru 1: False Positive'ler - Yaratıcı kıvılcım mı, halüsinasyon mu?
**Cevap:** Üç kapılı dinamik filtre
1. Kanuni kapı - yasa dışı ise at
2. Amaç kapısı - kullanıcı hedefine hizmet ediyor mu?
3. Maliyet kapısı - risk/fayda analizi

Örnekler:
- Piyade + bisiklet = başlangıçta false positive, amaç "hızlı hareket" ise buluş
- Tekerlekli sandalye + yük taşıma = başlangıçta hata, amaç "ucuz kısa mesafe" ise market arabası

Edebiyat modunda kapılar gevşek, bilim modunda sıkı.

### Soru 2: Evrim nasıl olacak?
**Cevap:** Stres tetiklemeli doğum
- Sistem çözemediği sorunla karşılaşınca stres $S$ artar
- $S$ > eşik ise "yeni uzman yaratayım mı?" sorar
- Kanuni sınırlar içindeyse galaksiye yeni kol eklenir
- İnsan örneği: iş için sert kişilik geliştirme, naif kişiliği koruma

### Soru 3: Hangi matematik?
**Cevap:** Yorumlanamaz çekirdek
- Aritmetik: 2+2=4
- Mantık: A ve değil-A olamaz
- Küme teorisi, bilgi teorisi
- Fizik formülleri: E=mc²

Milyon tane "2+2=5" verisi gelse bile çekirdek reddeder. Bu, halüsinasyonu mimari olarak engeller.

---

## 7. Yaratıcılığın Sınırı

Bugünkü LLM'ler düşük olasılıklı fikri reddeder çünkü loss fonksiyonu cezalandırır. Çözüm:

1. **Cesaret bütçesi:** Her 100 cevapta 5 tanesi düşük olasılıklı olabilir
2. **Ayrı modlar:** Yaratıcı LLM üretir, Bilimsel AI test eder
3. **Uyku döngüsü:** Uzak bağlantılar arka planda denenir

"Mantığı kapıda bırak" makalesindeki LLM dede, robot anne-baba, quantum torun metaforu: Her nesil öncekinin anlayamadığı kapıyı açar. Yaratıcılık, bu kapıların birleşiminden doğar.

---

## 8. Bir Sonraki Adım İçin Açık Sorular

1. Translator AI'ın iç temsil dili nasıl olmalı? (JSON, mantık formülleri, vektör?)
2. Sayfalama için model hangi kriterle bölünecek? (konu, lexical density, kullanım sıklığı?)
3. Uyku/konsolidasyon ne sıklıkta tetiklenecek? (her N token, her hata, her gün?)
4. Synthesis Layer hangi teknolojiyle? (kural motoru, küçük LLM, hibrit?)
5. İki bellek (yaratıcı+detay) arası senkronizasyon nasıl?
6. Matematik çekirdeği nasıl korunacak? (immutable layer, cryptographic hash?)

---

## 9. Test Edilebilir Hipotezler

1. **Uyku hipotezi:** Her 10.000 adımda özetleme yapan model, temel bilgiyi daha az unutur
2. **Rüya hipotezi:** Arka planda rastgele desen birleştiren model daha fazla bisociation üretir
3. **İki bellek hipotezi:** Ayrılmış sistem, tekil modele göre %90 daha az bellekle aynı doğrulukta çalışır

---

**Not:** Bu özet, 12 yapay zeka ile yapılan bağımsız çalışmalar, üç Medium makalesi, 1985 bitirme tezi ve çok gecelik sohbetlerin damıtılmış halidir. Bir sonraki sohbette bu iskelet üzerine et koyacağız.
