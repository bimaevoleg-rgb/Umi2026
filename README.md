# Числята: Волшебные острова — Android (Flutter)

Обучающая игра про цифры 1–10 для детей 4 лет. Вся игра — один офлайн-HTML
(`assets/index.html`), приложение — Flutter-обёртка на WebView. Работает без интернета.

## Сборка APK

Нужны: Flutter 3.32+ и Android SDK (platform android-34, build-tools 34.0.0).

```bash
git clone https://github.com/bimaevoleg-rgb/Umi2026.git
cd Umi2026

# 1. Дособрать платформенные файлы (gradle wrapper, иконки, стили).
#    Существующие файлы проекта команда НЕ перезаписывает.
flutter create --org ru.chislyata --project-name chislyata .

flutter pub get
```

### Отладочная сборка (подпись debug, для проверки)

```bash
flutter build apk --debug
# готово: build/app/outputs/flutter-apk/app-debug.apk
```

### Релизная сборка (подпись ключом публикации)

1. Положите `umi-upload-keystore.jks` в корень репозитория (файл уже в `.gitignore`).
2. Скопируйте `android/key.properties.example` в `android/key.properties`
   и впишите пароль ключа (хранится отдельно, вне репозитория!).
3. Соберите:

```bash
flutter build apk --release
# готово: build/app/outputs/flutter-apk/app-release.apk
```

Если `key.properties` нет — release соберётся с debug-подписью (для Google Play не подойдёт).

## Публикация в Google Play (кратко)

1. В Play Console создайте приложение, включите подпись Google Play (Play App Signing).
2. Загрузите release-APK (или соберите `flutter build appbundle` — для консоли лучше AAB).
3. Ключ `umi-upload-keystore.jks` — ваш upload-ключ. Берегите его: потеряете —
   обновления приложения выпускать будет нельзя.

## Структура

- `assets/index.html` — вся игра (офлайн, со встроенными фото-ассетами и озвучкой TTS)
- `lib/main.dart` — WebView-обёртка, полноэкранный режим
- `android/` — конфигурация Android, подпись релиза
