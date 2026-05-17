# MFD — My Friendly Droid

Android için sıfırdan tasarlanmış sesli AI asistanı. Orijinal JARVIS macOS projesinden ilham alınarak Android'e tamamen yeniden inşa edildi.

## ✨ Özellikler

- 🎤 **Sesli komut** (Türkçe destekli SpeechRecognizer)
- 🗣️ **Sesli yanıt** (Türkçe TTS)
- 🧠 **Google Gemini 2.0 Flash** AI motoru
- 🎨 **Canlı orb animasyonu** — orijinal teal halka tasarımı Compose Canvas ile yeniden yaratıldı
- 💾 **Kalıcı hafıza** (SharedPreferences + JSON)
- 🔧 **9 yerleşik araç:**
  - `open_app` — WhatsApp, Spotify, YouTube, Telegram, Instagram, Chrome, Gmail, Maps vb. açar
  - `sys_info` — Pil, RAM, disk, saat, tarih, cihaz bilgisi
  - `get_weather` — Anlık hava durumu (wttr.in, API anahtarı gerektirmez)
  - `add_calendar_event` — Android takvimine etkinlik ekler
  - `add_reminder` — Alarm/anımsatıcı kurar
  - `browser_control` — URL açar veya web araması yapar
  - `play_media` — YouTube/Spotify'da içerik oynatır
  - `send_whatsapp_message` — WhatsApp üzerinden mesaj hazırlar (wa.me)
  - `save_memory` / `delete_memory` — Hafıza yönetimi

## 📋 Sistem Gereksinimleri

- **Min Android:** 7.0 (API 24)
- **Hedef Android:** 14 (API 34)
- **Gerekli:** Google Gemini API anahtarı (ücretsiz: https://aistudio.google.com/apikey)

## 🚀 APK Oluşturma

### Yöntem 1: GitHub Actions (Ücretsiz, En Kolay)
1. Bu projeyi GitHub'a yeni bir repo olarak yükleyin.
2. Otomatik olarak Actions çalışır ve APK üretir.
3. Actions > en son çalışma > Artifacts altından `MFD-debug-apk` indirin.

### Yöntem 2: Android Studio (Yerel)
1. Android Studio'yu açın.
2. `File > Open` ile bu klasörü seçin.
3. Sync tamamlandıktan sonra `Build > Build APK` tıklayın.
4. APK: `app/build/outputs/apk/debug/app-debug.apk`

### Yöntem 3: Komut Satırı
```bash
# Android SDK + JDK 17 gerekli
echo "sdk.dir=/path/to/Android/Sdk" > local.properties
./gradlew assembleDebug
```

## 📦 Kurulum

1. Oluşturulan `app-debug.apk` dosyasını Android cihaza aktarın.
2. "Bilinmeyen kaynaklardan yükle" iznini etkinleştirin.
3. APK'ya dokunarak yükleyin.
4. İlk açılışta ayarlara dokunup Gemini API anahtarınızı girin.
5. Konuşmaya başlayın!

## 🏗️ Mimari

```
app/src/main/java/com/mfd/assistant/
├── MainActivity.kt              # Compose host activity
├── MFDViewModel.kt              # State management + AI orchestration
├── ai/
│   └── GeminiClient.kt          # Gemini REST API client + tool declarations
├── voice/
│   └── VoiceManager.kt          # SpeechRecognizer + TextToSpeech
├── actions/
│   └── ActionExecutor.kt        # Tüm araç implementasyonları
├── data/
│   ├── AppConfig.kt             # SharedPreferences (API key)
│   └── MemoryStore.kt           # JSON-backed memory
└── ui/
    ├── MFDApp.kt                # Ana Compose UI
    ├── OrbCanvas.kt             # Animasyonlu orb (teal ring)
    └── Theme.kt                 # JARVIS renk paleti
```

## 🔒 Gizlilik

- Gemini API anahtarı sadece cihazınızda SharedPreferences içinde saklanır.
- Sesli komutlar Google SpeechRecognizer üzerinden işlenir.
- AI istekleri doğrudan Google Gemini sunucularına gider — üçüncü taraf yok.
- Hafıza tamamen yerel.

## 📝 Orijinal JARVIS'ten Farklılıklar

Bu proje, orijinal Python/macOS tabanlı JARVIS'in Android'e **uyarlanmış yeniden yazımıdır**:

| Özellik | JARVIS (macOS) | MFD (Android) |
|---|---|---|
| Dil | Python | Kotlin |
| UI | Tkinter | Jetpack Compose |
| Ses tanıma | PyAudio + Gemini Live | Android SpeechRecognizer |
| TTS | Gemini native audio | Android TextToSpeech |
| Uygulama açma | macOS `open` | Android Intent + PackageManager |
| Takvim | Apple Calendar (AppleScript) | Android CalendarContract Intent |
| Anımsatıcı | Apple Reminders | Android AlarmClock Intent |
| WhatsApp | Desktop otomasyonu | wa.me Intent |
| Ekran analizi | macOS screencapture | (kaldırıldı — Android'de root gerektirir) |
| YouTube istatistikleri | YouTube Data API | (kaldırıldı — API anahtarı gerektirir) |

## ⚖️ Lisans

Eğitim ve kişisel kullanım amaçlıdır. Orijinal JARVIS macOS projesinin yazarı: Alp Ünlü (@alppunlu).
