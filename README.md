# Sesli Kitap

iPhone'da çalışan, sunucusuz (backend'siz) bir sesli kitap dinleyici. Tek statik
sayfa — GitHub Pages'e koyup "Ana Ekrana Ekle" ile uygulama gibi kullanılır.

## Özellikler

- 🎧 Sadece ses (video yok)
- ⏯️ Oynat / duraklat, ilerleme çubuğundan atlama
- ⏪ Ayarlanabilir geri / ileri sarma (varsayılan 15 sn / 30 sn)
- 💾 Kaldığın yeri otomatik kaydeder, tekrar açınca kaldığın yerden devam
- 🔁 Devam ederken otomatik birkaç saniye geri sarma (ayarlanabilir)
- 📚 Birden fazla kitap, her birinin ilerlemesi ayrı takip edilir
- 🔖 Kitap içinde işaret + not; dokununca o ana atlar
- ⏱️ Uyku sayacı (15/30/45/60 dk)
- 🐇 Oynatma hızı (0.75×–2×)
- 🔒 Kilit ekranı / kulaklık kontrolleri (oynat, duraklat, ileri, geri)
- 📴 Çevrimdışı çalışır — ses dosyaları telefonun içine kaydedilir

Ses dosyaları tarayıcının kalıcı deposunda (IndexedDB) tutulur; hiçbir yere
yüklenmez, internete gitmez.

## 1) YouTube videosunu ses dosyasına çevirme (Mac'te, kitap başına bir kez)

```bash
brew install yt-dlp
```

```bash
yt-dlp -x --audio-format mp3 -o "%(title)s.%(ext)s" "YOUTUBE_LINKI"
```

Çıkan `.mp3` dosyasını iPhone'a aktar (AirDrop, iCloud Drive veya Dosyalar
uygulaması). Dosya büyükse `--audio-quality 5` ekleyerek küçültebilirsin.

## 2) Uygulamayı GitHub Pages'e koyma (bir kez)

1. GitHub'da yeni bir repo oluştur (örn. `sesli-kitap`), **Public** seç.
2. Bu klasördeki **tüm dosyaları** repoya yükle:
   `index.html`, `sw.js`, `manifest.webmanifest`, `icon-192.png`,
   `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png`
   (Repo sayfasında **Add file → Upload files** ile sürükleyip bırak.)
3. Repo → **Settings → Pages**.
4. **Source:** `Deploy from a branch`, **Branch:** `main`, **Folder:** `/ (root)` → **Save**.
5. 1–2 dakika sonra adres hazır olur:
   `https://KULLANICIADIN.github.io/sesli-kitap/`

## 3) iPhone'a kurma

1. Safari'de yukarıdaki adresi aç.
2. Paylaş butonu → **Ana Ekrana Ekle**.
3. Ana ekrandaki "Sesli Kitap" simgesinden aç.

> Ana Ekrana eklemek önemli: iOS, ana ekrana eklenmemiş sitelerin verisini
> bir süre sonra silebilir. Eklenen uygulamada verin kalıcı olur.

## 4) Kullanım

- **＋ Kitap Ekle** → telefonundaki `.mp3` dosyasını seç, ad ver, kaydet.
- Kitaba dokun → oynatıcı açılır, oynat'a bas.
- Dinlerken **＋** (İşaretler) ile o ana not bırak.
- Kaldığın yer otomatik kaydolur; uygulamayı kapatıp açınca devam eder.
- Sağ üstteki ✎ ile kitabın adını/kapağını değiştir veya kitabı sil.
- ⚙️ (Kitaplık ekranı) → sarma süreleri ve otomatik geri sarma ayarları.

> **Kilit ekranı sınırı:** Telefon kilitliyken kilit ekranından duraklatıp yine
> kilit ekranından devam ettirmek çalışmayabilir ("oynatılamıyor" / widget
> kayboluyor) — bu iOS'un web sayfalarına koyduğu, kod tarafında aşılamayan bir
> kısıtlama (native uygulamalar özel arka plan izniyle bunu aşabiliyor, web
> sayfaları alamıyor). Duraklattıysan **kilidi aç, uygulamadan oynat'a bas** —
> bu her zaman çalışıyor ve kaldığın yerden devam ediyor.

## Güncelleme

`index.html` veya `sw.js` değişirse, dosyaları repoya tekrar yükle. Uygulama
internete bağlıyken açıldığında yeni sürüm otomatik gelir. Takılırsa `sw.js`
içindeki `sesli-kitap-v1` numarasını `v2` yapıp yeniden yükle.

## Sınırlar

- YouTube linkini uygulamaya doğrudan yapıştırıp ses çekmek mümkün değil
  (YouTube buna izin vermiyor); önce Adım 1 ile dosyaya çevirmek gerekiyor.
- Ses dosyalarının boyutu telefonun tarayıcı deposuyla sınırlıdır (genelde
  birkaç GB). ⚙️ ekranında kullanılan/boş alanı görebilirsin.
