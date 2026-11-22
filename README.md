# Değerin Korunumu web sitesi

Derleme adımı olmayan statik site. Cloudflare Pages bu klasörü olduğu gibi yayınlar.

```
index.html        Ana sayfa
stil.css          Bütün sayfaların ortak stili (renkler, başlık, kartlar, koyu tema)
araclar/dca.html  Düzenli alım (DCA) hesaplayıcı → /araclar/dca
veri/dca.json     Hesaplayıcının verisi: son 180 ayın aylık fiyatları
favicon.svg       Δ = 0 işareti
og.png            Bağlantı paylaşılınca görünen önizleme (1200×630, kanal/cikti/kapak_2560.png'den kırpıldı)
```

## Depo düzeni

Site, YouTube çalışma deposunda `site/` klasöründe yazılır. Yalnızca bu klasör
`github.com/MehmetTheConqueror/degerinkorunumu` deposuna gider (`site` uzak deposu, git subtree);
orada dosyalar kök dizindedir. Çalışma deposunun geri kalanı GitHub'a gitmez.

Değişiklikten sonra (çalışma deposunun kökünde):

```bash
git add site && git commit -m "Site: ..."
git subtree push --prefix=site site main
```

## Cloudflare Pages

Adres: https://degerinkorunumu.pages.dev/

Pages projesi `degerinkorunumu`, GitHub deposuna bağlı. Framework preset `None`, Build command boş,
Build output directory boş (kök). `main`'e her push siteyi günceller.

Adres değişirse (kendi alan adı bağlanırsa) `index.html`'deki `canonical`, `og:url` ve `og:image`
değerlerini yeni adrese çevir; `og:image` tam adres olmalı, göreli yolu çoğu uygulama okumaz.

## Verinin güncellenmesi

`veri/dca.json`, çalışma deposundaki `araclar/site_dca_veri.py` ile üretilir (Yahoo Finance, anahtar gerekmez):

```bash
.venv/bin/python araclar/site_dca_veri.py      # site/veri/dca.json (bu ay dahil son 180 ay)
```

Her ayın ilk işlem günü fiyatı; ETF'lerde temettü düzeltilmiş kapanış. Ayda bir çalıştırıp commit + subtree push
yeterli; 15 yıllık pencere kendiliğinden kayar. `veri/aylik/` dosyalarına dokunmaz.

Hesaplayıcı adresi parametre alır, hesap paylaşılabilir:
`/araclar/dca?tutar=100&bas=2016-12&bit=2026-11&varlik=voo,qqq&olcek=log`

## Yerel önizleme

Sayfalar `/stil.css`, `/veri/dca.json` gibi kökten yollar kullanır; dosyayı çift tıklayarak değil sunucuyla açın:
`python3 -m http.server 8765 --directory site` → http://127.0.0.1:8765/

## Yeni sayfa

Araç, veri ya da yazı sayfaları bu klasöre eklenir: `site/araclar/dca.html` → `/araclar/dca`.
