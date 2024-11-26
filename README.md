# Урок № 102
## 1. Подготовка
Убедитесь, что установлено:
1) JDK (версия 8 или выше).
2) Maven (если используется Maven).
3) IDE (например, IntelliJ IDEA или Eclipse) или текстовый редактор.
### Подключение к интернету для скачивания зависимостей.
Скачайте или склонируйте проект:
Если вы используете Spring Initializer, убедитесь, что структура проекта создана корректно. Поместите проект в удобную директорию на вашем компьютере.

## 2. Настройка профилей
Настройте файл application.yml:
```yaml
spring:
  profiles:
    active: dev # Укажите "dev" для разработки или "prom" для промышленного режима

http:
  endpoint:
    url: https://httpbin.org/get # URL для реального вызова (используется в профиле "prom")
```
Вы можете переключать профиль на prom или dev в зависимости от режима работы.

## 3. Сборка проекта
Откройте терминал (или встроенную консоль вашей IDE).
Перейдите в директорию проекта:
```bash
cd /путь/к/вашему/проекту
```
Соберите проект с помощью Maven:
```bash
mvn clean install
```
## 4. Запуск приложения
Через Maven:
Запустите проект с профилем dev:
```bash
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```
Запустите проект с профилем prom:
```bash
mvn spring-boot:run -Dspring-boot.run.profiles=prom
```
Через JAR-файл:
Если сборка прошла успешно, в директории target появится файл с расширением .jar, например, spring-profile-1.0-SNAPSHOT.jar.
Запустите приложение, указав нужный профиль:
```bash
java -jar -Dspring.profiles.active=dev target/spring-profile-1.0-SNAPSHOT.jar
```
## 5. Тестирование
Откройте в браузере или Postman:
Если приложение запущено, перейдите по адресу:
```bash
http://localhost:8080/call
```
В зависимости от профиля (dev или prom) вы увидите JSON-ответ:
Для dev (заглушка):
```json
{
  "url": "https://stub-url",
  "origin": "stub-origin"
}
```
Для prom (реальный вызов):
```json
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "Java/17"
  },
  "origin": "127.0.0.1",
  "url": "https://httpbin.org/get"
}
```
## 6. Логи
Консоль:
Логи приложения будут выводиться в консоль.
Файл:
Если настроено логирование в файл, логи сохраняются в директории logs:
```bash
logs/application.log
```
## 7. Переключение профилей
Профиль можно переключить, изменив параметр:
В application.yml:
```yaml
spring:
  profiles:
    active: prom
```
Или указав параметр при запуске:
```bash
java -jar -Dspring.profiles.active=prom target/spring-profile-1.0-SNAPSHOT.jar
```
## 8. Устранение возможных ошибок
### Если приложение не запускается:

1) Проверьте, установлен ли JDK и добавлен ли он в PATH.
2) Убедитесь, что все зависимости загружены (mvn clean install).
### Если не работает профилирование:

1) Убедитесь, что профиль указан правильно (например, dev или prom).
2) Проверьте синтаксис файлов application.yml или application.properties.
###Пример запуска в реальном времени
Сначала запускаем в режиме dev:

```bash
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```
Ожидаемый результат: Заглушечный ответ в браузере или Postman.
Затем переключаемся на prom:

```bash
mvn spring-boot:run -Dspring-boot.run.profiles=prom
```
Ожидаемый результат: Ответ от реального HTTP-сервиса https://httpbin.org/get.
