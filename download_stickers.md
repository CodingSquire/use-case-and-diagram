# Загрузка нового набора стикеров

**Акторы:** авторизованные пользователи, приложение.

**Цель:** авторизированный пользователь загружает новый набор стикеров, чтобы в дальнейшем отправлять их другому авторизированному пользователю или в групповой чат.

**Предусловия:** у авторизованного пользователя открыт чат с конкретным авторизованным пользователем или групповой чат.

**Сценарий:**
1. Пользователь открывает меню для выбора конкретного стикера.
2. Приложение предлагает [выбрать стикер из конкретного набора и отправить его ](https://github.com/polinanov/use-case-and-diagram/blob/master/send_stickers.md "Выбрать стикер из конкретного набора") или загрузить новый набор стикеров.
3. Пользователь выбирает загрузить новый набор стикеров.
4. Приложение открывает меню загруки: создать набор своих стикеров или загрузить набор существующих стикеров.
5. Пользователь выбирает загрузить (создать) набор своих стикеров.  

Пользователь может [загрузить набор существующих стикеров](#Загрузить_набор_существующих_стикеров).  

6. Приложение открывает соединение (канал связи) для предачи данных, используя протокол TCP/IP.
7. Приложение открывает форму загрузки файлов на сервер.
8. Пользователь выбирает изображения в формате png.
9. Приложение загружает файлы на сервер, используя протокол HTTP.
10. Приложение присваивает набору и каждому стикеру уникальный код.  

{Успешная загрузка стикеров}  

11. Приложение возвращает ответ успешной загрузки набора стикеров.
12. Приложение сохраняет данные в БД (никнейм пользователя (загрузившего набор), код набора стикеров и код каждого из стикеров).
13. Приложение отображает стикер в меню пользователя.

**Результат:**
* Пользователь успешно отправил стикер в выбранный груповой чат или диалог с конкретным пользователем.
* В выбранном груповом чате или диалоге с конкретным пользователем отображается отправленный стикер.
* В базу данных успешно записаны данные об отправке стикера.

**Исключения:**
1. Отсутствует интернет-соединение.  

**Альтернативный сценарий:**  

5а. <a name="Загрузить_набор_существующих_стикеров"></a> *Загрузить набор существующих стикеров*.  

5а1. Приложение отправляет запрос на сервер для получения всех существующих наборов.  
5а2. Приложение возвращает пользователю все существующие наборы.  
5а3. Пользователь выбирает конкретный набор(-ы), который(-ые) он хочет довавить.  

Возврат на шаг 11 {Успешная загрузка стикеров}.


# Диаграмма activity
![activity_for_personal_call](http://www.plantuml.com/plantuml/svg/RLF1aXGX3Btp5JdE7DJxzc7NqeEUtDBn0o8TPYXfG19ctRytKCtOEzLzWf3tylAIVcB18dK9nlIJUVZ9L21bYWm82yKABXLW2cJ5nxC6EPFrpbjWyVOtbSbu1uSV56VGp9f3mdcyFO9SAC9XZHuDj4_pH-GrrJAIkU7fh-TUQ0GVZol7crHb6j_3jrMjJJ4sbKcJRLgM6ht5VhKNrATmxBtCA0XICBAZ0fMrMAi0fq_Fy06-FaCkIP9DOTgfeGGBk5kV3Ujy80P9dOIfNAbiaB0XwTxEwINsrls2PmNw2EzpF7Tcb6dQvlSQl5TXe_lBwRIl-IEpFtVLwiIVIchGJFzf1517HcWlmzKLJ8493cCGkvQtQJVYGihBSgTDRuMaUBeIO0YRcPBmLk5tabhYhRMg-7t0hfTZBRc1Dsj9SdZ7RMjGG1zUC4elaIjVkltJIgHDU6Vkf2YY4ESKcI2vjk_LMc9sDTncjpwGjCFmPpAhDtWbxbis-chdNyWqCZvxpW5V6N20mSUR0_slcmprAR1gF0xYDRV5kZcs-2oQsTje7qlAvadlTGd_0000 "Диаграмма activity")

# Диаграмма sequence
![sequence_for_personal_call](http://www.plantuml.com/plantuml/png/ZP8nRy8m48Lt_ueJNSZ07s2eYCJU2jJPEkm3MN7EgUzCoxylGQMDHGQoHNxVy_FTsuXYrj978rtW0JFs8FHPY1szOzRWme2iKDXJZe7967IQCdm8PND8XJtc2opQOOZ1eOR42q21rfXH0QjNQDVmDX3RdhWicn4FPrGQ9IsiheARS0qxqf9vgRbGOpnDTHEhRVhYcD1RqU0wodP0rrMsyBB5tEqnzecDCHWLX1JI4IwfPFZb11mA6RX-xJIbf8vqsS3jP69w-wzIFQ37bFjhaXgSvoOFsbCafpRqUA8dwVQEufbgyDcyhKWuiNN9Ft4d68f2zo7ITn0DV7eOPFMgtTWXKNjNr-kQlVA_37zT6CNDJ1v3xAkAL3j_DBAPP4X2S-MgXydMe-81XUfErSo6s9S-_W00 "Диаграмма sequence")

