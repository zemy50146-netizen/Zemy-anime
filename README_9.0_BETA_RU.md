# ZEMY ANIME 9.0 BETA

В архиве объединены Android-приложение и сервер Cloudflare.

## Состав
- `app/` — Android-клиент с Media3; minSdk 23, Java 17.
- `server/cloudflare/` — Worker API, D1 schema/migration, Cron-сканер AniList и инструкция публикации.
- `.github/workflows/deploy-cloudflare.yml` — автоматическая публикация Worker после настройки секретов GitHub.
- `CHANGELOG_9.0_BETA_RU.txt` — изменения версии.

## Импорт Android в CodeAssist
Импортируй именно корневую папку `ZEMY_ANIME_2.0`, в которой находятся `settings.gradle.kts` и `build.gradle.kts`. После Gradle Sync собери APK. До публикации сервера приложение не сможет получить серверные серии — это ожидаемо.

## Адрес сервера
Android читает адрес из Gradle-параметра `ZEMY_BASE_URL`; в исходниках нет фиктивного домена. После публикации Cloudflare Worker укажи его HTTPS URL в Gradle-параметрах сборки. Не добавляй административный токен в Android.

## Публикация
Полная инструкция: `server/cloudflare/README_RU.md`. Для реального развёртывания необходим вход владельца в Cloudflare и GitHub и добавление секретов. Эти действия нельзя выполнить из ZIP без авторизации владельца.

## Честный статус беты
- Cloudflare API и SQL-миграция подготовлены.
- Сканер импортирует только метаданные AniList (по 50 записей за запуск каждые 6 часов).
- Music ID пока не распознаёт аудио в реальном времени.
- Видеопотоки не поставляются с каталогом; доступны только разрешённые прямые HTTPS-ссылки, добавленные администратором.
- APK не собран в этой среде: требуется Android SDK/Gradle в CodeAssist.
