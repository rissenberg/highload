# Highload VK

## Содержание
  #### [1. Тема и целевая аудитория](#topic)
  #### [2. Диверсификация](#diversification)
  #### [3. Расчет нагрузки](#load)
  #### [4. Глобальная балансировка нагрузки](#balance)
  #### [5. Локальная балансировка нагрузки](#balance-local)
  #### [6. Источники](#source)

<a name="topic"></a>
## 1. Тема и целевая аудитория 

### Тема
VK - Развлекательная социальная сеть, позволяющая создавать, 

### MVP
- Публикация записей на стене пользователя
- Лайки и комментарии к постам
- Создание сообществ
- Лента новостей пользователя
- Просмотр страниц пользователей и лент

### Целевая аудитория  
- Страны СНГ.
- Пользователи:
	-  MAU 100 млн \[[1](https://vk.com/about)]
	-  DAU 76 млн \[[2](https://vk.company/ru/investors/info/11642/)]
- Распределение аудитории по странам \[[3](https://inclient.ru/vk-stats/#lwptoc2)]
  - Россия - 84,4%
  - Беларусь - 3%
  - Казахстан - 2,1%
  - Украина - 1,1%
  - Другие - 9,4%

<a name="diversification"></a>
## 2. Диверсификация 

Сервис ВК по своему функционалу схож с сервисами Твиттер, но за обоими сервисами стоят разные цели - первый, ВК, является популярным развлекательным сервисом с широким спектром контента, в то время как Твиттер ориентирован на быстрый и краткий обмен новостями, мнениями и информацией. Именно различие в целях задает различия и в функционале, предоставляемому пользователям, и в аудитории, для которой сервис был создан.

### Формирование функциональных различий

#### Посты

Функционал, что разделяют ВК и Твиттер - лента, в которой пользователь может просматривать новые посты/твиты из источников, на которые он подписан. Чтобы сформировать различия сервисов, нужно начать с самих постов - в Твиттере они представляют из себя небольшие сообщения ограниченные 280 символами, с возможностью прикрепить к записи фото (до 4 шт) или видео (1 шт с доп ограничением по длительности). В свою очередь ВК имеет ограничения намного большие: 4096 символов на пост, 10 медиафайлов - фотографий, видео- и аудиозаписей.

#### Источники

Теперь мы разберем то, откуда контент попадает в новостную ленту - источники. Для Твиттера единственным источником являются профили пользователей - их блоги. На кого подписан пользователь - их же посты он и будет видеть в своей ленте. В ВК помимо записей на стене пользователей существуют сообщества - блоги, не связанные с профилем автора и предоставляющие новый функционал, не встречающийся в профилях ВК и Твиттера - например, разделение права администрирования сообщества между несколькими людьми, добавление новых ролей - модератора и редактора, закрытые сообщества дают возможность приглашать в них только определенный круг людей, и, в конечном итоге, сообщества позволяют одному человеку создавать и вести несколько блогов, оставаясь при этом в одном аккаунте.

#### Подписка на источники

Источники, публикуя новые записи/посты/твиты, формируют новостную ленту своих подписчиков, таким образом, чтобы пользователь начал получать новости из источника, необходима подписка на него. В Твиттере пользователь может начать "читать" другого - тем самым оформив подписку на новости. По тому же принципу работают остальные микроблогинговые сервисы, например, Инстаграм и Тамблер. В ВК действует система друзей - пользователь может подать заявку в друзья, и, если второй пользователь ее примет, оба начнут получать новые записи друг друга в своих лентах (в то время как в Твитере подписка "односторонняя"). Подписки на сообщества ВК ничем принципиально не отличаются от подписок в Твиттере - пользователь при вступлении в сообщества "подписывается" на его обновления - и новые записи начинают появляться в ленте подписчика.

#### Файлохранилище

Также стоит добавить об одной функциональной особенности ВК - у каждого пользователя (или сообщества) есть "свои" фотографии, видео, музыка и файлы - в отличие от Твиттера, у этого сервиса есть функционал файлохранилища с доступом к любому загруженному файлу из общей страницы того или иного типа документа, в то время как доступ к файлу в Твиттере возможен лишь через пост, к которому он был прикреплен.

<a name="load"></a>
## 3. Расчёт нагрузки

Ежемесячная аудитория VK: 100 млн. пользователей.

Ежедневная аудитория VK: 76 млн. пользователей.

Согласно исследованию [[3]](https://inclient.ru/vk-stats/):

 - Во ВКонтакте 48 млн активных авторов

 - Во ВКонтакте создано более 2 млн авторских пабликов

 - В среднем пользователь проводит во ВКонтакте 18 минут в день

 - Каждый день пользователи ВКонтакте оставляют 1 млрд отметок «Нравится»

 - Контент во ВКонтакте набирает 10.3 млрд просмотров каждый день

 - Пользователи ВКонтакте просматривают короткие видео 1 млрд раз в день (~ 10% от общего кол-ва просмотров)

### Средняя статистика для пользователя
Посчитаем количество просмотров и лайков в день на одного пользователя : 

	10.3 млрд. / 76 млн. ~ 135 [просм/чел]

	1 млрд. / 76 млн. ~ 13 [лайков/чел]
 

### Анализ новостной ленты

В прикрепленном файле VK_feed_data.ods содержится выборка 100 постов из ленты рекомендованных новостей, в которой произведена оценка процентного отношения типов постов (было выделенно 3, с фото, с видео и текстовый), и регрессионный анализ отношения комментариев к лайкам. Результаты так же видны на следующем скриншоте:

![image](https://github.com/rissenberg/highload/assets/114286666/d643caad-3930-4bb3-9bbb-e68ae82f814e)

Откуда следует, что:
* Посты с фото составляют 87% от общего числа, с видео - 8%, текстовые посты - 5%
* Соотношение постов с видео в 8% почти совпадает со статистикой[[3]](https://inclient.ru/vk-stats/) в 10% от общего количества просмотров. Из чего можно судить, что ~80% видео пользователи прсматривают из ленты новостей
* Среднее количество фото в постах этого типа равно ~2
* Лайки с комментариями коррелируют с коэфициентом ~0,5, что свидетельствует об умеренной положительной корреляции - для нашего эксперимента приемлемое значение для построения зависимости
* Коэффициент наклона у этой зависимости = 42,4646 а сдвига = 600

Дополнительно, оценим объем медиафайлов постов:
* Средняя длина одного поста равна 300 символам в кодировки UTF-16, где 1 символ равен 2 байту
* Средний размер одной фотографии равен 200 кБ
* Средний размер аватарки сообщества составляет 4 кб
* Лента отдает лишь ссылку на видео и картинку превью, которая будет весить 30 кб

Кроме того, был произведен анализ запросов на составление ленты новостей - лента и страницы пользователя/сообщества прогружается в виде чанков по 8 постов - соответственно, на каждые 8 просмотров пользователя приходится по 1 запросу на формирование ленты / просмотр страницы

  ![Снимок экрана от 2024-03-04 11-37-37](https://github.com/rissenberg/highload/assets/114286666/471b21b2-82ab-43e6-b13a-396478413e91)
  ![image](https://github.com/rissenberg/highload/assets/114286666/69b084a4-566c-45a3-8ac3-8e96d613b930)

Дополним этой информацией статистику для одного пользователя:
	
	135 просм / 8 ~ 16,9 [запросов/чел]
	13 лайков / 42,4646 ~ 0,3 [комментариев/чел]
 

### Средняя статистика для автора
Посчитаем количество опубликованного контента в день на одного автора : 

В 2022 году во ВКонтакте было опубликовано более 6.3 млрд постов[[3]](https://inclient.ru/vk-stats/). Следовательно, на один день приходится 6.3 млрд. / 365 дней ~ 17,2 млн. [постов/день]

	17,2 млн. / (48 + 2) млн. ~ 0,344 [пост/автор]


### Предварительные расчеты:
Посчитаем объем трафика для просмотра ленты на одного человек за сутки:

	Размер одного поста: 4 кб (размер аватарки сообщества) + 600 б (текст поста) = 4 кб
	
	Размер одного поста с фото: 4 кб (размер аватарки сообщества) + 600 б (текст поста) + 2 * 200 кб (фотографии в посте) = 404 кб
	
	Размер одного поста с видео: 4 кб (размер аватарки сообщества) + 600 б (текст поста) + 30 кб (превью видео) = 34 кб
	
	Трафик для одного пользователя в среднем: ( 4 кб * 5% + 404 кб * 87% + 34 кб * 8% ) * 135 просм = 47844 кб = 46,7 мб


Рассмотрим трафик на сервере по видам постов:


Тип          | Отправка (дневная аудитория 76 млн)   | Отправка Гб/сек |
-------------| -------------| ---------|
Текстовый     | 135 * 5% * 76 млн. * 4 кБ / 18*60 сек            		| 1,812           |
   Фотографии     | 135 * 87% * 76 млн. * 404 кБ / 18*60 сек                 | 3 184             | 
   Видео    	| 135 * 8% * 76 млн. * 47 кб / 18*60 сек               	 | 34             |
   Итого  |                                            			 | 3 220          |

### RPS
 
* Запрос формирование ленты / просмотра страницы : 10,3 млрд / 8 / 86400 = 14 900 RPS
* Лайк поста: 1 млрд / 86400 = 11 575 RPS
* Комментарий: 1 млрд / 42,4646 / 86400 = 272 RPS
* Публикация: 17,2 млн. / 86400 = 200 RPS

Действие                            | RPS
------------------------------------| ---
Просмотр страницы / ленты           | 14 900
Лайк поста                          | 11 575
Комментирование поста               | 275
Публикация                          | 200
**Итого**                           | 26 950

Статистики, отражающей пиковое значение активности пользователей сервиса ВКонтаке в интернете нет. Возьмем коэффициент запаса равный 2
Соответственно:

   Тип          | Пиковое значение   | Пиковое значение с коэффициентом запаса 2  |
-------------| -------------| ---------|
RPS                         | 26 950                | 53 900            |
   Сетевой трафик(Гб/c)     | 3 220                 | 6 440             | 

<a name="balance"></a>
## 4. Глобальная балансировка нагрузки

Общемировая география пользователей на момент октября 2023г [[3](https://inclient.ru/vk-stats/#lwptoc2)]:  
Страна           | Процентное соотношение
---------------- | -------------
Россия           | 84.4%
Беларусь         | 2.95% 
Казахстан        | 2.12% 
Украина          | 1.12%
Другие           | 9.41% 

Так как основная аудитория ВКонтакте находится в России, распологать датацентры будем в России.  

Если мы посмотрим на карту плотности населения России, то мы можем увидеть, что основная нагрузка будет приходиться на европейскую часть страны. Поэтому основную часть ЦОД-ов будем размещать там.  

![image](https://github.com/rissenberg/highload/assets/114286666/359ea70a-f685-43b6-99f4-e50e564bf461)

В связи с этим для размещения датацентров были выбраны следующие города:
- Москва
- Санкт-Петербург
- Екатеринбург
- Новосибирск
  
Для балансировки клиентов будем использовать GeoDNS. ЦОД-ы будут отвечать за следующие районы:
- Москва -> Москва, Центральная часть России
- Санкт-Петербург -> Санкт-Петербург, Центральная часть России
- Екатеринбург -> Средняя часть России
- Новосибирск -> Сибирь и Дальний Восток

<a name="balance-local"></a>
## 5. Локальная балансировка нагрузки

Балансировка будет осуществляться на L3 и L7 уровнях

#### L3 Балансировка
Балансировка на этом уровне будет производится по схеме Virtual Server via IP Tunneling

![image](https://github.com/rissenberg/highload/assets/114286666/968bff91-96b0-4797-abde-e3b016c899cf)

Для обеспечаения отказоустойчивости системы стоит использовать фреймфорк **Keepalived**, реализующий балансировку нагрузки, мониторинг работы серверов.

Кроме того Keepalived подерживает Virtual Router Redundancy Protocol (VRRP), который и предоставляет возможность отслеживать состояние узлов системы, а при отказе одного из них перенаправить трафик на другой узел.

#### L7 балансировка 
Будем использовать сервер Nginx. Использовать его будем для следующих процессов:

- Отдача статики
- Кеширование популярных запросов
- Сжатие контента (gzip)
- Обеспечение перезапуска сервиса без остановки обслуживания
- Отслеживание обработки медленных клиентов (с помощью использования асинхронной обработки)

Шифрования будет производиться с помощью Let`s Encrypt

Для улучшения производительности и ускорения подключения будем использовать Session Cache. 

<a name="source"></a>
## 6. Источники 
  1. https://vk.com/about
  2. https://vk.company/ru/investors/info/11642/
  3. https://inclient.ru/vk-stats/
   
