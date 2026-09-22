# Doğra Bakalım!

Tarayıcıda çalışan, bilgisayardan ve telefondan oynanabilen kısa bir 3B casual oyun.
Şenlik meydanında sabit duran kılıçlı bir aşçıyı yönetirsin: yukarıdan yağan meyveleri
tek tıkla doğrarsın, ama kılıç ağır olduğu için gelişigüzel savuramazsın — **doğru anı beklemelisin.**

👉 **[Oyna](https://calkanli5.github.io/dogra-bakalim/)** — kurulum yok, linke tıklayan herkes oynayabilir.

## Fruit Ninja'dan farkı ne?

Fruit Ninja'da parmağını sürüklediğin her çizgi keser, bu yüzden hızlı ve sürekli savurmak
ödüllendirilir. Burada karakter sabittir, kılıcın taradığı **kavis her zaman aynı yerdedir**
ve savurma tek tıktır. Boşa savurmak puan kaybettirip kılıcı 0,4 saniye kilitler.
Yani oyun hızı değil, **zamanlamayı** ölçer.

Patlayıcılar da meyvelerle aynı kavisten geçtiği için şöyle anlar doğar:
*"Üç meyveyi birden kesebilirim ama yanlarında C4 var — savursam mı, beklesem mi?"*

## Nasıl oynanır

| Platform | Savurma | Duraklatma |
|---|---|---|
| Bilgisayar | Sol Tık veya `Boşluk` | `Esc` |
| Telefon / Tablet | Ekrana dokun | İki parmakla dokun |

Ekran yönelimi: **dikey**.

### Kurallar

- Tur 90 saniye, 100 dayanıklılık ile başlarsın.
- Bir savuruş, kavisin içindeki **her şeyi** aynı anda keser — kombo buradan doğar.
- 90 saniye sonunda dayanıklılığın varsa ve skorun **500+** ise Altın Kepçe senindir.

### Meyveler

| Meyve | Puan | Not |
|---|---|---|
| Elma, portakal, limon | +10 | en sık gelenler |
| Muz | +12 | |
| Çilek, karpuz | +15 | çilek küçük ve hızlı |
| Üzüm | +20 | en küçük hedef |
| Ananas | +25 | en değerlisi, seyrek |
| Altın meyve | +50 | turda en fazla 4 tane |
| Çürük meyve | −15 | kesme, bırak düşsün |

Dokunmadan yere düşen meyve, değerinin yarısı kadar (en çok −15) puan kaybettirir ve
üst üste 3 kaçırma 20 dayanıklılık götürür.

### Patlayıcılar

| Patlayıcı | Hasar | Görünüş |
|---|---|---|
| Dinamit | −10 | kırmızı çubuk demeti, turuncu uyarı halkası |
| Bomba | −30 | fitili yanan siyah küre |
| C4 | −100 | yeşil kalıp, yanıp sönen kırmızı LED — **tek dokunuşta tur biter** |

Kesilen her patlayıcı ekranı kaplayan bir ışık patlaması, genişleyen şok dalgaları ve
kamera sarsıntısı başlatır. Hasar arttıkça patlama da büyür.

### Diğer puanlar

| Olay | Puan |
|---|---|
| Boşa savurma | −5 |
| 2 nesnelik kombo | ×2 |
| 3+ nesnelik kombo | ×3 |
| Tur sonu kalan dayanıklılık | ×0,75 puan |

### Zorluk artışı

| Ne değişir | Ne zaman |
|---|---|
| Düşme hızı %10 artar | her 15 saniyede |
| Aynı anda 2 → 5 nesne | 15 / 45 / 75. saniyelerde |
| Patlayıcı oranı %10 → %35 | 15. saniyeden sonra |
| Bomba devreye girer | 15. saniyeden sonra |
| C4 devreye girer | 40. saniyeden sonra |
| Çürük meyveler girer | 40. saniyede |
| Patlayıcılar meyvenin yanına konumlanır | 50. saniyeden sonra |

Düşen nesnelerin patlayıcı olma oranı tur boyunca **%10'dan %35'e** çıkar; üstelik
patlayıcının kendisi de ağırlaşır — turun sonunda her dört patlayıcıdan biri C4'tür.

### Kostümler

3 şapka ve 3 kılıç, en yüksek skorunla açılır (300 / 500 / 700 / 1000 puan).
Oynanışa hiçbir etkileri yoktur, sadece görünüş. İlerleme tarayıcının `localStorage`'ında tutulur.

## Çalıştırma

Kurulum yok, derleme adımı yok. `index.html` dosyasını tarayıcıda aç, yeter.
(Three.js CDN'den çekildiği için ilk açılışta internet gerekir.)

Gereksinim: **WebGL destekleyen güncel bir tarayıcı** — Chrome, Edge, Firefox veya Safari'nin
son sürümleri ve güncel telefon tarayıcıları çalıştırır.

```bash
git clone https://github.com/calkanli5/dogra-bakalim.git
```

### Yayın

Oyun **`gh-pages`** dalından yayınlanıyor: https://calkanli5.github.io/dogra-bakalim/

Değişiklik yaptıktan sonra yayını güncellemek için `main`'e gönderip aynı içeriği
`gh-pages` dalına da itmek yeterli:

```bash
git push origin main
git push origin main:gh-pages
```

İkinci komuttan 1-2 dakika sonra site güncellenir.

## Teknik

- Tek dosya: `index.html` (HTML + CSS + JS)
- Three.js r128 (CDN) ile WebGL; başka bağımlılık yok
- 3B model veya doku dosyası yok — karakter, meyveler ve patlayıcılar kod içinde
  temel geometrilerden (küre, silindir, koni, torus) kuruluyor
- Ses efektleri WebAudio ile üretiliyor, ses dosyası yok
- Bütün oynanış hesabı 2B oyun düzleminde (z = 0) yapılıyor; 3B olan sunum —
  böylece görünen kavis ile gerçek vuruş alanı birebir örtüşüyor
- Gölgeli aydınlatma, `devicePixelRatio` desteği, sabit 9:16 dikey oran

Uygulama notu: skor 0'ın altına düşmez (cezalar skoru eksiye götürmez).

## Tasarım dosyası

Oyun, ders ödevi olarak hazırlanan tasarım dosyasındaki A–U bölümlerine göre yapıldı.
Ödev teslimi tasarım dosyasının kendisidir; bu depo, o tasarımın çalışan hâlidir.

Ödev kuralı oyunun "küçük ve yapılabilir" olmasını istiyor ve uygun türler arasında
refleks, tek dokunuşlu ve mini arcade oyunlarını sayıyor — bu oyun üçüne birden giriyor:
tek ekran, tek girdi, 90 saniyelik tek tur, bölüm yok, çok oyunculu yok.
