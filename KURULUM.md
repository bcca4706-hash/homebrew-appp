# Homebrew Kurulum Rehberi - Android Uygulaması

Bu proje, HTML dosyasını Capacitor ile Android APK'ya çevirir.

## Gerekli Yazılımlar (bir kere kur)

1. **Node.js 18+** — https://nodejs.org (LTS sürüm)
2. **Java JDK 17** — https://adoptium.net
3. **Android Studio** — https://developer.android.com/studio

Android Studio kurulumunda **Android SDK** ve **SDK Build-Tools** otomatik gelir, ek bir şey yapmana gerek yok.

## APK Üretme Adımları

### 1) Projeyi kur

PowerShell'i bu klasörde aç ve şunu çalıştır:

```
npm install
```

Bu komut bütün Capacitor paketlerini indirir (1-2 dakika sürer).

### 2) Android platformunu ekle

```
npx cap add android
```

Bu komut `android/` klasörünü oluşturur — gerçek Android Studio projesi.

### 3) Web dosyalarını senkronize et

```
npx cap sync
```

Bu, `www/` klasöründeki HTML'i Android projesinin içine kopyalar. HTML'de her değişiklik yaptığında bunu tekrar çalıştır.

### 4) Android Studio'da aç

```
npx cap open android
```

Android Studio otomatik açılacak ve projeyi yükleyecek. İlk açılışta Gradle indirme işlemi 5-10 dakika sürer, bekle.

### 5) APK üret

Android Studio menüsünden:

**Build → Build Bundle(s) / APK(s) → Build APK(s)**

Build bitince sağ altta "locate" linki çıkar, tıklayınca `.apk` dosyasının olduğu klasör açılır.

APK dosyası şurada olur:
```
android/app/build/outputs/apk/debug/app-debug.apk
```

### 6) Telefona kur

1. APK'yı telefonuna at (WhatsApp, Google Drive, USB kablo — fark etmez)
2. Telefonda dosyayı aç
3. Android "Bilinmeyen kaynaklara izin ver" diyecek → izin ver
4. Kur ve aç

## HTML'i Güncellemek

`www/index.html` dosyasını düzenle, sonra:

```
npx cap sync
```

Android Studio'da tekrar Build → APK ile yeni APK çıkar.

## İpuçları

- **APK boyutu yaklaşık 4-5 MB** olacak — Capacitor çekirdek küçük
- **İmza (signing) gerekmez** — debug APK kendi imzasıyla kurulur, sadece kendin için
- **Play Store'a yüklemek istersen** AAB üretip imzalaman gerekir (ayrı konu, sonra bakarız)
- **İkon değiştirmek istersen** Android Studio'da `app/src/main/res/mipmap-*` klasörlerindeki PNG'leri değiştir

## Sorun Olursa

- "SDK location not found" → Android Studio → SDK Manager → SDK Platform 34 indir
- "Gradle sync failed" → File → Invalidate Caches → Restart
- "JAVA_HOME not set" → Java JDK 17 kur, sistem değişkenlerine ekle
