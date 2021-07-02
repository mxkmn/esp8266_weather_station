# Погодная станция на ESP8266 от mxkmn

### [English](README.md) | Русский

Погодная станция создана с нуля и использует дисплей LCD1602 для отображения следующей информации:
* Температура с двух датчиков DS18B20: за окном и в помещении
* Дата и время
* Текущая погода: температура настоящая и ощущаемая, скорость ветра, влажность, давление (над уровнем моря)
* Прогноз почасовой (до 48 часов): температура настоящая и ощущаемая, статус\*
* Прогноз дневной (до 8 часов): минимальная и максимальная температура за день, статус\*

\* Под статусом подразумевается подпись, в которой пишется об осадках, ситуации на небе или экстремальных погодных условиях (Дождь со снегом, Ясно, Пасмурно, Торнадо...)


Для навигации по вкладкам используется две кнопки. Имеющиеся вкладки:
* Основная вкладка: температура за окном/в городе\*\*, ощущаемая температура, дата и время (сменяется раз в 5 секунд), иконка осадков и получения данных\*\*\*\*
* Дополнительная вкладка: скорость ветра, влажность, давление (над уровнем моря), температура в помещении/в городе\*\*\*
* Дебаг-вкладка: температура в городе, время с последней перезагрузки станции
* Вкладки с прогнозом на час: температура настоящая и ощущаемая, статус
* Вкладки с прогнозом на день: минимальная и максимальная температура за день, статус

\*\* Температура в городе пишется, если внешний датчик не подключён
\*\*\* Температура в городе пишется, если внутренний датчик не подключён и внешний датчик подключён (то есть если на главном экране пишется температура с внешнего датчика и для полной картины нужно написать температуру от OWM)
\*\*\*\* Иконка в углу экрана видна не всегда: показывается капля, если в скором времени будет дождь, снежинка если будет снег, часы во время синхронизации погоды/времени

Схема вкладок:
```
--- MainPage ⇄ AdditionalPage ?⇄? DebugPage
|   ↑
|   DayPage0 ⇄ DayPage1 ⇄ DayPage2 ⇄ ... ⇄ DayPage7
|   ↑
--> HourPage0 ⇄ HourPage1 ⇄ HourPage2 ⇄ ... ⇄ HourPage47
```

Фото вкладок:
| ![MainPage](/ReadmeFiles/Ru/MainPage.jpg "MainPage") | ![AdditionalPage](/ReadmeFiles/Ru/AdditionalPage.jpg "AdditionalPage") | ![DebugPage](/ReadmeFiles/Ru/DebugPage.jpg "DebugPage") |
| ![DayPage0](/ReadmeFiles/Ru/DayPage0.jpg "DayPage0") | ![DayPage1](/ReadmeFiles/Ru/DayPage1.jpg "DayPage1") | ![DayPage2](/ReadmeFiles/Ru/DayPage2.jpg "DayPage2") |
| ![HourPage0](/ReadmeFiles/Ru/HourPage0.jpg "HourPage0") | ![HourPage5](/ReadmeFiles/Ru/HourPage5.jpg "HourPage5") | ![HourPage6](/ReadmeFiles/Ru/HourPage6.jpg "HourPage6") |

Настройка станции происходит с помощью веб-интерфейса, в который можно войти при включении станции. Для этого необходимо подключиться к точке доступа и перейти по адресу 192.168.4.1:
![Настройки](/ReadmeFiles/Ru/Settings.png "Настройки по адресу 192.168.4.1")
Остальные настройки (их немного, при этом достаточно настроить лишь один раз) доступны в начале скетча.
---
Станция использует несколько сторонних библиотек. Их необходимо установить перед использованием:
* [OWM_for_ESP](https://github.com/mxkmn/OWM_for_ESP) - получение погоды от OWM
* [JSON_Decoder](https://github.com/Bodmer/JSON_Decoder) - необходима для OWM_for_ESP
* [TimeLib](https://github.com/PaulStoffregen/Time) - работа с временем
* [DallasTemperature](https://github.com/milesburton/Arduino-Temperature-Control-Library) - получение температуры с датчиков DS18B20
* [OneWire](https://github.com/PaulStoffregen/OneWire) - необходима для DallasTemperature
* [LiquidCrystalRus](https://github.com/mxkmn/LiquidCrystalRus) - библиотека для печати русских символов на ЖК-дисплеях

Я очень рекомендую установить увеличенную скорость CPU 160MHz. Это важно для ускорения получения данных из интернета, при этом не увеличивает энергопотребление и не ухудшает стабильность чипа. 
---
Схема подключения пока что отсутствует :(.
---
Корпуса для 3D-принтера пока что нет, он в разработке.
---
Я попытался сделать код простым для изменения, поэтому я надеюсь, что Вы сможете переделать его под другие типы дисплеев/навигации/датчики/языки. Если ваша реализация полностью закончена, Вы можете отправить мне в Issues ссылку на неё и я добавлю её ниже.
* Пока что тут пусто