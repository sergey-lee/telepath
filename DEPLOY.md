# Как выложить

## Один раз

1. Создать публичный репозиторий и залить содержимое этой папки:

   ```bash
   cd publish
   git init && git add . && git commit -m "Сайт и лента обновлений"
   gh repo create sergey-lee/telepath --public --source . --remote origin --push
   ```

2. Включить Pages: Settings → Pages → Source: **Deploy from a branch**,
   branch `main`, папка `/ (root)`. Через минуту сайт открывается по адресу
   `https://sergey-lee.github.io/telepath/`.

3. Домен настроен: `telepath.alienminds.net`. В GoDaddy заведена запись
   CNAME `telepath` → `sergey-lee.github.io`, адрес лежит в файле `CNAME`.
   В Settings → Pages его надо указать в поле Custom domain и, когда GitHub
   выпустит сертификат, включить Enforce HTTPS.

## При каждом выпуске

```bash
cd ../TeleFinder && ./package.sh          # собрать, подписать, нотаризовать
./package.sh release                       # выложить образ в Releases
cd ../publish && git add . && git commit -m "Выпуск 1.1" && git push
```

`package.sh` кладёт свежий `appcast.xml` прямо сюда, поэтому второй командой
уезжает и лента обновлений.

## Почему адрес ленты нельзя менять после первого выпуска

Адрес `SUFeedURL` зашит в каждую разошедшуюся копию приложения. Установленные
копии будут ходить по старому адресу вечно — сменить его можно только выпуском,
который они получат по старому адресу. То есть **домен надо выбрать до первой
продажи**: если сначала выложить на `sergey-lee.github.io`, а потом переехать
на свой домен, старый адрес придётся держать живым всегда.
