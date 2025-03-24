# Twitch

## 1. Тема и целевая аудитория

Twitch -  видеостриминговый сервис.

### MVP

1. Регистрация/авторизация
2. Создать стрим
3. Смотреть стрим
4. Подписка на стримера
5. Писать в чат
6. Ставить реакции стриму, лайк/дизлайк 
7. Поиск стримеров по категориям, тегам, ключевым словам
8. Хранение записи стрима после завершения
9. Просмотр записи

### Ключевые продуктовые решения

- рекомендации стримов на основе интересов
- бесконечная лента прямых трансляций
- 7 дней хранения записи прямых трансляций для обычных пользователей и 60 дней для партнеров, на количество самих записей в этот период ограничений нет [^5] 
- буферизация прямых трансляций и записей 

### Целевая аудитория

#### Метрики вовлеченности:

- MAU 240M[^1]
- DAU 30M[^1]
- общее количество посещений за январь 2025 - 1.2B [^3]
- В месяц 7M человек запускает стрим хотя бы раз, активных стримеров в день 1.2M [^3]
- одновременно просматривает в среднем 2.5M пользователей, пик 7M [^3]
- одновременное количество прямых трансляций 100K  [^3]
- среднее количество стримов в месяц более 7M  [^3]
- среднее время общей длительности стримов за месяц - 65.7M, за день - 2.5M [^3]
- было отправлено более 28B ообщений в чате за год,
   т.е ~80M в день, ~2.33B в месяц (2023 год) [^4]
- на мобильные устройства приходится 35% всех просмотров [^1]
- средняя продолжительность прямой трансляции на Twitch 3 часа[^2]
- смотрят в среднем 1,7B часов контента в месяц  [^3]
- среднее время сессии 36 минут [^7]

#### Рекорды:

- одновременное количество зрителей - 3.44M
- максимальное количество подписчкиков - 19M

#### Распределение аудитории по полу и возрасту:

- 52% пользователей в возрасте 25-34 лет [^2]
- 22% пользователей в возрасте 35-44 лет [^2]
- 72% пользователей - мужчины

#### Распределение аудитории по странам

Десктоп трафик в 2024 [^2] 

| №   | Страна   | Количество пользователей | % от общего числа |
| --- | -------- | ------------------------ | ----------------- |
| 1   | США      | 49.5M                    | 20.6%             |
| 2   | Германия | 16.9M                    | 7.17%             |
| 3   | Россия   | 11.6M                    | 4.85%             |
| 4   | Франция  | 11.44M                   | 4.61%             |
| 5   | Япония   | 10.5M                    | 4.39%             |

## 2. Расчет нагрузки

### Продуктовые метрики
#### Аудитория [^1]

| Тип | Количество |
| --- | ---------- |
| MAU | 240M       |
| DAU | 30M        |

#### Действия пользователя

| Тип                     | Среднее в месяц<br>от 1 юзера | В месяц <br>от всех юзеров   |
| ----------------------- | ----------------------------- | ---------------------------- |
| Регистрация/авторизация | 0.05                          | 2M (регистраций) + 12M = 14M |
| Проведение<br>стрима    | 3ч                            | 75M часов                    |
| Просмотр<br>стрима      | 14мин*                        | 1.7B часов [^3]              |
| Подписки                | 3                             | 720M                         |
| Сообщения<br>в чате     | 9.7                           | 2.33B  [^4]                  |
| Реакций на<br>стрим     | 1.5                           | 360M                         |
| Поиск                   | 20                            | 4.8B                         |
| Посещения <br>профиля   | 4                             | 960M                         |
| Сохранение записи стрима | 1.5**                        | 10.5M                         |
| Просмотр записи         | 5                             | 1.2B                         |

- ( \* ) Из расчета, что MAU 240M[^1]
- ( \** ) Из расчета, что активных стримеров 7M, в среднем в месяц проходит 3 стрима, половина стримов сохраняется
#### Хранилища

##### Пользователя:

| Тип               | Размер |
| ----------------- | ------ |
| Аватарка          | 200КБ  |
| Фото баннер       | 200КБ  |
| Общая информация* | ~2КБ   |
| Итого             | 402КБ  |

- ( \* ) Имя пользователя и отображаемое имя пользователя до 25 символов, информация  о себе до 300 символов, кодировка utf8 - 4б, итого 350 * 4б / 1024 ~ 2КБ
- Максимальный размер загружаемых аватарки/банеров 10МБ, но сжимается до 200КБ

##### Стримера

| Тип                 | Размер    |
| ------------------- | --------- |
| Стримы*             | 75ГБ      |
| Чат**              | 126Мб     |
| Итого               | 75,16Гб   |


У Twitch нет возможности вести прямую трансляцию в 2к и 4к, это находится на этапе тестирования [^6]. Twitch рекомендует делать трансляцию в 1080р с битрейтом 6000кбит/с [^6] . Средний размер файла на 1минуту с таким разрешением 40МБ. Но так как при просмотре записи Twitch предлагает выбор из качеств видео: 720р60 - в среднем 30МБ/мин, 480 - 11МБ/мин, 360 - 7МБ/мин, 240 - 5МБ/мин, 144 - 3МБ/мин.

Без потери качества можно сжать на 30%

- ( \* ) [Отсюда](#метрики-вовлеченности), информация, что общая длительность прямых трансляций 65.6M, и средняя продолжительность стрима - 3ч, и 7M активных стримеров в месяц (т.е проводят хотя бы 1 трансляцию в месяц) => 65.7M/7M = 9.4ч на стримера в месяц или ~3 стрима в месяц. Запись хранится 60 дней, т.е 2 месяца Посчитаем размер хранилища за 2 месяца: 2 * 9.4  * 60мин * (40 + 30 + 11 + 7 + 5 + 4) = 109416МБ. Итого после сжатия 109 416МБ* 0.7 = 76591.2МБ ~ 75ГБ.
- ( \** ) Из расчетов действий пользователя получим, что среднее количество сообщений в чате 1100, максимальный размер сообщения 500 символов [^9]  , при кодировке utf8 1100 * 500 * 4Б * 60= 126МБ

### Технические метрики
#### Хранилища

Точных данных по количеству зарезарегистрированных аккаунтов на Twitch нет, при MAU 240M[^1] пусть общее количество будет 2.4B (1 к 10). Стримеров в месяц 7M[^3]

| Тип          | Размер  |
| ------------ | ------- |
| Пользователи | 49.1ТБ  |
| Стримеры     | 501.75ПБ |
| Итого        | 501.8ПБ |

#### Трафик и запросы
Twitch работает по протоколу RTMP [^10] ,  который работает поверх TCP. Раз в секунду делается запрос на получение фрагмента стрима.

| Тип                         | Средний RPS | Сетевой трафик<br>(средний) | Пиковый RPS | Сетевой трафик<br>(пиковый) |
| --------------------------- | ----------- | --------------------------- | ----------- | --------------------------- |
| регистрация<br>/авторизация | 6           | 12Мбит/с                  | 12          | 24Мбит/с                  |
| Проведение<br>стрима        | 100К        | 0.6Тбит/с                   | 250K        | 1.2Тбит/с                   |
| Просмотр<br>стрима          | 2.5M        | 15Тбит/с                    | 5M          | 30Тбит/с                    |
| Подписки                    | 300         | 240Мбит/с                   | 600         | 480Мбит/с                   |
| Чат                         | 1000        | 20Мбит/с                    | 2000        | 40Мбит/с                    |
| Реакции                     | 250K        | 120Мбит/с                   | 500K        | 240Мбит/с                   |
| Поиск                       | 2K          | 1000Мбит/с                  | 4К          | 2000Мбит/c                  |
| Переход <br>в профиль       | 370         | 1200Мбит/с                  | 740         | 2400Мбит/с                  |
| Хранение записи             | 300         | 1.72Гбит/с                  | 600         | 3.44Гбит/с                  |
| Просмотр записи стрима      | 5           | 0.05Гбит/с                  | 10          | 0.1Гбит/с                   |
| Итого                       | 2.9M        | 15.6Тбит/с                  | 5.8M        | 32.7Тбит/с                  |

## 3. Глобальная балансировка нагрузки

### Функциональное разбиение по доменам (при наличии, нужно для следующего пункта)

Основной тип нагрузки приходиться на сервис стриминга и просмотра стрима, логично вывести их в отдельный домен.

### Обоснования расположения ДЦ (влияние на продуктовые метрики)

Twitch не предоставляет гарантии единой задержки для всех пользователей и может меняться в зависимости от скорости интернета, к примеру на картинке снизу, настройка слева - "4g - быстрый", справа - "4g - медленный", и задержка может замедлиться динамически при замедлении интернета и исчерпании буфера.

![MyCollages](https://github.com/user-attachments/assets/e17e32ac-505a-4455-89df-c4aa0acb9720)

При отсутствии гарантии по длительности задержки ДЦ Twitch можно расположить исходя из плотности населения и популярности сервиса в регионе.

В [части 1](#распределение-аудитории-по-странам), привел информацию по десктоп трафику, но нужно расширить и на мобильный трафик. 

Так как точные данные по трафику не раскрыты, можно сделать некоторые выводы из локальности языков [^11], нужно чтобы расширить список стран, где Twitch популярен:

| Язык          | Среднее количество<br>одновременных зрителей | Среднее количество<br>одновременных стримов |
| ------------- | -------------------------------------------- | ------------------------------------------- |
| Английский    | 1134.2K                                      | 56.1K                                       |
| Русский       | 253.7K                                       | 7.1K                                        |
| Испанский     | 185.5K                                       | 8.1K                                        |
| Немецкий      | 161K                                         | 4.6K                                        |
| Французкий    | 159.6K                                       | 4.9K                                        |
| Португальский | 156.1K                                       | 4.5K                                        |
| Японский      | 142.2K                                       | 4.5K                                        |

- На **испанском** языке говорят в следующих странах: Испания, страны Латинской Америки
- На **немецком** языке говорят в следующих странах: Германия, Австрия, Лихтенштейн, а также одним из официальных языков Швейцарии, Люксембурга и Бельгии.
- На русском языке говорят в следующих странах: Россия и Беларусь
- На французком языке говорят: 
	- в странах Европы: Франция, Бельгия, Люксембург и др
	- в странах Америки: Канада, США
	- в странах Африки
- На португальском говорят в следующих странах: Бразилия, в странах Африки

Исходя из этой информации, общий трафик Twitch будет из этих стран:

| №   | Страна / Регионы                                                              | Основной язык | Десктоп (пользователей, млн / доля) | (сред. зрители / стримы) |
| --- | ----------------------------------------------------------------------------- | ------------- | ----------------------------------- | ------------------------ |
| 1   | США                                                                           | Английский    | 49.5M / 20.6%                       | 1134.2K / 56.1K          |
| 2   | Германия и сопутств. страны (Австрия, Швейцария, Лихтенштейн)                 | Немецкий      | 16.9M / 7.17%                       | 161K / 4.6K              |
| 3   | Россия, Беларусь, Казахстан                                                   | Русский       | 11.6M / 4.85%                       | 253.7K / 7.1K            |
| 4   | Франция и франкофонные регионы (Бельгия, Люксембург, Канада, часть США и др.) | Французский   | 11.44M / 4.61%                      | 159.6K / 4.9K            |
| 5   | Япония                                                                        | Японский      | 10.5M / 4.39%                       | 142.2K / 4.5K            |
| 6   | Испания и Латинская Америка                                                   | Испанский     | –                                   | 185.5K / 8.1K            |
| 7   | Бразилия и африканские страны                                                 | Португальский | –                                   | 156.1K / 4.5K            |


![mir-плотность](https://github.com/user-attachments/assets/4d2d929e-1fdc-493d-80b7-eae9393d4c8a)

![mir](https://github.com/user-attachments/assets/340f9db7-75f5-4a17-89a2-b69c9d3e0062)

![asia-net](https://github.com/user-attachments/assets/278f28de-e7a7-48cc-85b7-e3bee58b6e17)

![asia](https://github.com/user-attachments/assets/5699d5d5-ce9f-4fe0-8e80-a3f8d080ad25)

![europe-net](https://github.com/user-attachments/assets/3b5c2afb-f97f-46c3-bbfb-b1a4dac06441)

![europe](https://github.com/user-attachments/assets/ab6b952b-3b15-40d7-b027-a635ab6facea)

![america-net](https://github.com/user-attachments/assets/92449627-5508-4acc-90d5-6817d0f94577)

![amer](https://github.com/user-attachments/assets/46257a16-6c1e-4c75-ade7-718e1e0f63cb)

![s-amer](https://github.com/user-attachments/assets/15fdd0ed-fb09-488c-af6a-f3a40b982149)

Расположение ЦОД:
- Америка:
	- Северная Америка: 
		- В США, часть серверов, при резком увеличении трафика, могут облуживать Мексику и Канаду (10шт):
		  	1. Нью-Йорк, может брать на себя часть трафика из Канады
		  	2. Вашингтон
		  	3. Майами, может брать на себя часть трафика из Мексики
		  	4. Атланта
		  	5. Колумбус, может брать на себя часть трафика из Канады
		  	6. Канзас-Сити
		  	7. Хьюстон, может брать на себя часть трафика из Мексики
		  	8. Сан-Франциско, может брать на себя часть трафика из Канады
		  	9. Денвер, может брать на себя часть трафика из Канады
		  	10. Лос-Анджелес, может брать на себя часть трафика из Мексики
    			11. Эль-Пасо
    	  		12. Ноксвилл
    	    		13. Чикаго
    	      		14. Мемфис
    	        	15. Даллас
    	         	16. Миннеаполис , может брать на себя часть трафика из Канады
    	          	17. Хомер
		- Канада:
			1. Эдмонтон
   			2. Монреаль, может брать на себя часть трафика из США
      			3. Ванкувер, может брать на себя часть трафика из США
		- Мексика
			1. Мехико
   			2. Масалтан 
	- Южная Америка (3шт):
 		1. Лима
   		2. Буэнос-Айрес
     		3. Форталеза
       		4. Рио-де-Жанейро 
- Европа      
	- Великобритания:
 		1.  Лондон, может брать трафик на себя из Ирландии
  	- Ирландия:
  		1. Дублин
	- Франция:
 		1. Париж, трафик Франции
   		2. Лион, трафик Франции и Италии
        	3. Марсель
        - Италия:
          	1. Милан 
     	- Испания
      		1. Бальбао, может брать трафик на себя из Франции и Испании
        	2. Лиссабон, может брать трафик на себя из Северной Африки
      	- Германия:
      	  	1. Франкфурт
      	  	2. Мюнхен, может брать трафик на себя из Италии
      	- Австрия:
      	  	1. Вена, может брать трафик на себя из Германии и восточной Европы
	- Польша:
      	  	1. Варшава, Трафик из Восточной Европы
   	- Греция:
   	  	1. Афины, может брать трафик на себя из Турции, Юго-Восточной Европы
  	- Швеция:
  		1. Стокгольм
   	- Западная часть России:
   	  	1. Санкт-Петербург, , может брать на себя часть трафика из Финляндии
   	  	2. Москва
   	  	3. Воронеж
   	- Сербия:
   	  	1. Белград
- Южная Африка
	- Яунде
- Азия:
	- Восточная частть России:
 		1. Новосибирск
	- Сингапур
   	- Япония:
   	  	1. Токио
   	  	2. Осака
   	- Австралия:
   	  	1. Сидней

### Расчет распределение запросов из секции "Расчет нагрузки" по типам запросов по датацентрам


| №   | ЦОД                 | Доля | средний RPS | Средние сетевые <br> нагркузки в Гбит/с |
| --- | ------------------- | ---- | ----------- | --------------------------------------- |
| 1   | **Нью-Йорк**        | 3%   | 87K         | 480                                     |
| 2   | **Вашингтон**       | 2%   | 58K         | 320                                     |
| 3   | **Майами**          | 2%   | 58K         | 320                                     |
| 4   | **Атланта**         | 2%   | 58K         | 320                                     |
| 5   | **Колумбус**        | 2%   | 58K         | 320                                     |
| 6   | **Канзас-Сити**     | 1%   | 29K         | 160                                     |
| 7   | **Хьюстон**         | 3%   | 87K         | 480                                     |
| 8   | **Сан-Франциско**   | 2%   | 58K         | 320                                     |
| 9   | **Денвер**          | 2%   | 58K         | 320                                     |
| 10  | **Лос-Анджелес**    | 3%   | 87K         | 480                                     |
| 11  | **Эль-Пасо**        | 2%   | 58K         | 320                                     |
| 12  | **Ноксвилл**        | 2%   | 58K         | 320                                     |
| 13  | **Чикаго**          | 3%   | 87K         | 480                                     |
| 14  | **Мемфис**          | 3%   | 87K         | 480                                     |
| 15  | **Даллас**          | 2%   | 58K         | 320                                     |
| 16  | **Миннеаполис**     | 3%   | 87K         | 480                                     |
| 17  | **Хомер**           | 1%   | 29K         | 160                                     |
| 18  | **Эдмонтон**        | 2%   | 58K         | 320                                     |
| 19  | **Монреаль**        | 2%   | 58K         | 320                                     |
| 20  | **Ванкувер**        | 2%   | 58K         | 320                                     |
| 21  | **Мехико**          | 2%   | 58K         | 320                                     |
| 22  | **Масалтан**        | 2%   | 58K         | 320                                     |
| 23  | **Лима**            | 1%   | 29K         | 160                                     |
| 24  | **Буэнос-Айрес**    | 2%   | 58K         | 320                                     |
| 25  | **Форталеза**       | 2%   | 58K         | 320                                     |
| 26  | **Рио-де-Жанейро**  | 3%   | 87K         | 480                                     |
| 27  | **Лондон**          | 2%   | 58K         | 320                                     |
| 28  | **Дублин**          | 1%   | 29K         | 160                                     |
| 29  | **Париж**           | 2.5% | 72.5K       | 400                                     |
| 30  | **Лион**            | 2.5% | 72.5K       | 400                                     |
| 31  | **Марсель**         | 2.5% | 72.5K       | 400                                     |
| 32  | **Милан**           | 2%   | 58K         | 320                                     |
| 33  | **Бальбао**         | 2%   | 58K         | 320                                     |
| 34  | **Лиссабон**        | 2%   | 58K         | 320                                     |
| 35  | **Франкфурт**       | 2.5% | 72.5K       | 400                                     |
| 36  | **Мюнхен**          | 2.5% | 72.5K       | 400                                     |
| 37  | **Вена**            | 2.5% | 72.5K       | 400                                     |
| 37  | **Варшава**         | 1%   | 29K         | 160                                     |
| 37  | **Стокгольм**       | 1%   | 29K         | 160                                     |
| 37  | **Москва**          | 3%   | 87K         | 320                                     |
| 37  | **Санкт-Петербург** | 3%   | 87K         | 480                                     |
| 37  | **Воронеж**         | 2%   | 58K         | 320                                     |
| 37  | **Новосибирск**     | 2%   | 58K         | 320                                     |
| 37  | **Белград**         | 1%   | 29K         | 160                                     |
| 38  | **Токио**           | 3%   | 95.7K       | 480                                     |
| 39  | **Осака**           | 3%   | 95.7K       | 480                                     |
| 40  | **Сингапур**        | 1%   | 29K         | 160                                     |
| 41  | **Сидней**          | 2%   | 58K         | 320                                     |


###  Схема DNS балансировки 

Поскольку дата-центры Twitch расположены по всему миру, целесообразно использовать GeoDNS. Пользователь, отправляя DNS-запрос, получает ответ от глобальной системы, которая основывается на географическом положении пользователя. Она направляет запросы на ближайший ДЦ к пользователю

### Схема Anycast балансировки 

| Area                       | Основные ДЦ                                              | 
| -------------------------- | -------------------------------------------------------- |
| Северо-восток США и Канада | Нью-Йорк, Вашингтон, Монреаль, Колумбус, Чикаго, Торонто, Миннеаполис            | 
| Юго-восток США и Мексика   | Майами, Атланта, Ноксвилл, Хьюстон, Эль-Пасо, Мехико    Даллас, Мемфис         |
| Запад США и Канады         | Сан-Франциско, Лос-Анджелес, Ванкувер, Денвер, Эдмонтон  Хомер                  |
| Южная Америка              | Рио-де-Жанейро, Форталеза, Лима, Буэнос-Айрес              |
| Западная Европа            | Лондон, Дублин, Париж, Лион, Марсель, Франкфурт, Мюнхен  |
| Южная Европа и Африка      | Бальбао, Лиссабон, Милан, Афины, Яунде                        |
| Восточная Европа и Россия  | Варшава, Белград, Вена, Санкт-Петербург, Москва, Воронеж, Стокгольм           |
| Восточная Азия             | Токио, Осака, Новосибирск                                               |
| Юго-Восточная Азия         | Сингапур, Сидней                                                  |

Для обеспечения быстрого отклика и отказоустойчивости Twitch объединяет несколько географически распределённых серверов под одним Anycast IP-адресом. Запросы пользователей направляются через глобальную BGP-сеть к ближайшему узлу,  на основе маршрутов сети провайдера т.е по hop'ам

## 4. Локальная балансировка

### Схема балансировки для входящих запросов

Для выбора NGINX балансировщика используем L3 балансировщик

![image](https://github.com/user-attachments/assets/35191e79-0965-4a61-a031-5f5edc51211e)

стоят несколько балансировщиков, используется схема active-passive, один работает, другие следят за его работой, при падении ввыбирается следующий по приоритету

При помощи NGINX
- Для доставки видеопотоков и сообщений чата используется алгоритм Least Connections, который направляет запросы на серверы с минимальной текущей нагрузкой.
- Некритичные к задержкам запросы балансируются по Weighted Round Robin

### Схема балансировки для межсервисных запросов

Для взаимодействия между внутренними сервисами используется отдельный внутренний балансировщик Nginx, настроенный на Weighted Round Robin.

### Схема отказоустойчивости

- Регулярная проверка состояния серверов (Healthcheck) с помощью встроенных механизмов Kubernetes
- Если сервер перестает отвечать, балансировщик исключает его из маршрутизации
- Регулярная проверка софта, с помощью специальных запросов
- Таймаут на основе квантилей, если сервер начинает отвечать медленнее, чем 95% других серверов, его соединения закрываются, а новые запросы перенаправляются на более производительные серверы.
- Выполняется асинхронная репликация данных между дата-центрами (например, чат-сообщения и метаданные о стримах), чтобы минимизировать потери информации в случае аварий.
- В случае сбоя одного сервера или кластера нагрузка автоматически перераспределяется на резервные серверы с минимальной задержкой переключения.


### Нагрузка по терминации SSL
- SSL-терминация выполняется на уровне балансировщика Nginx, после чего внутри дата-центра обмен между сервисами осуществляется по протоколу HTTP, снижая нагрузку на софт.
- В каждом ДЦ несколько балансировщиков 5-15 (в зависимости от нагрузки), для того чтобы при падении одного балансировщика, остальные перенимали нагрузку
- Использование отдельного auth сервиса, для того чтобы не нагружать тяжелые бекенды.
- Использование кеширования SSL-сессий,

Расчет для среднего RPS
- Полный handshake (PFS)	2 мс
- Возобновление сессии из кэша 	0.5 мс

| Тип запроса      | Доля | RPS       | Время CPU | Итого CPU   |
| ---------------- | ---- | --------- | --------- | ----------- |
| Полный handshake | 30%  | 870,000   | 2мс       | 1,740,000мс |
| Session cache    | 70%  | 2,030,000 | 0.5мс     | 1,015,000мс |
| **Итого:**       | 100% | 2,900,000 | –         | 1,885,000мс |

1,885,000мс=1,885c CPU

В пиковое 3.77c CPU

## 5. Логическая схема БД

### Схема

![image](https://github.com/user-attachments/assets/5e9bd840-959f-47a0-880e-3c8522d4a30f)

## 6. Физическая схема БД

![image](https://github.com/user-attachments/assets/d756ff06-394f-47ca-8662-9f4a22242973)

- синий: Tarantool
- голубой: Hadoop
- фиолетовый: ElasticSeatrch
- оранжевый: YDB
- желтый: ClickHouse

### Схема шардирования

Консистентная хэш функция для распределения по шардам пользователей по user_id. Популярных пользователей по map, распределять вручную.

Остальные сущности распределять только по хэш функции

### Резервное копирование 

Для catecory_avatar, user_avatar, user_banner дублирующий master-slave Hadoop

Для viewers, users_reactions, message, sessions полусинхронная репликация master-slave Tarantool

Для user, stream, follow синхронная репликация master-slave YDB

### Индексы

- username для User
- title для stream


## Источники
[^1]:  https://www.demandsage.com/twitch-users
[^2]: https://analyzify.com/statsup/twitch
[^3]: https://twitchtracker.com/statistics
[^4]: https://leftronic.com/blog/twitch-statistics
[^5]: https://help.twitch.tv/s/article/video-on-demand?language=ru
[^6]: https://help.twitch.tv/s/article/multiple-encodes?language=ru
[^7]: https://www.sostav.ru/publication/twitch-49828.html
[^8]: https://au.finance.yahoo.com/news/twitch-caps-streamers-storage-100-150858673.html
[^9]:  https://discuss.dev.twitch.com/t/message-character-limit/7793
[^10]: https://help.twitch.tv/s/article/guide-to-using-twitch-inspector?language=ru
[^11]: https://twitchtracker.com/languages
[^12]: https://worldpopulationreview.com/country-rankings/twitch-users-by-country
