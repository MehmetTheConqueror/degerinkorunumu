# Değerin Korunumu web sitesi

Derleme adımı olmayan statik site. Cloudflare Pages bu klasörü olduğu gibi yayınlar.

```
index.html   Ana sayfa (stiller içinde)
favicon.svg  Δ = 0 işareti
og.png       Bağlantı paylaşılınca görünen önizleme (1200×630, kanal/cikti/kapak_2560.png'den kırpıldı)
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

## Yeni sayfa

Araç, veri ya da yazı sayfaları bu klasöre eklenir: `site/araclar/dca.html` → `/araclar/dca`.
