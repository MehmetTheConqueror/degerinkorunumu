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

Workers & Pages → Create → Pages → Connect to Git → `degerinkorunumu`.
Framework preset `None`, Build command boş, Build output directory boş (kök).
`main`'e her push siteyi günceller.

Alan adı belli olunca `index.html`'deki `og:image` değerini tam adrese çevir
(ör. `https://degerinkorunumu.pages.dev/og.png`); bazı uygulamalar göreli yolu okumaz.

## Yeni sayfa

Araç, veri ya da yazı sayfaları bu klasöre eklenir: `site/araclar/dca.html` → `/araclar/dca`.
