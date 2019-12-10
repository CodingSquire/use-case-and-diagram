# Отправка стикеров

**Акторы:** авторизованные пользователи, приложение.

**Цель:** авторизированный пользователь отправляет выбранный стикер другому авторизированному пользователю или в групповой чат, чтобы довавить характерных визуальных эффектов в диалог с конкретном пользователем.

**Предусловия:** у авторизованного пользователя открыт чат с конкретным авторизованным пользователем или групповой чат в который он хочет отправить стикер.

**Сценарий:**
1. Пользователь открывает меню для выбора конкретного стикера.
2. Приложение предлагает выбрать стикер из конкретного набора или загрузить новый набор стикеров.
3. Пользователь выбирает стикер из конкретного набора и нажимает на него.

Пользователь может загрузить новый набор стикеров [загрузить новый набор стикеров](https://github.com/polinanov/use-case-and-diagram/blob/master/download_stickers.md "Загрузить новый набор стикеров").

4. Приложение открывает соединение (канал связи) для предачи данных, используя протокол TCP/IP.
5. Приложение возвращает ответ успешной отправки стикера.
6. Приложение сохраняет данные в БД (никнеймы пользователей, код стикера, дата и время отправки стикера).
7. Приложение отображает стикер в диалоговом окне всем пользователям, открытого чата.  

**Результат:**
* Пользователь успешно отправил стикер в выбранный груповой чат или диалог с конкретным пользователем.
* В выбранном груповом чате или диалоге с конкретным пользователем отображается отправленный стикер.
* В базу данных успешно записаны данные об отправке стикера.

**Исключения:**
1. Отсутствует интернет-соединение.

# Диаграмма activity
![activity_for_personal_call](http://www.plantuml.com/plantuml/png/pLHDYzj03BtFhn3qua2XXTxYomPwsKFRi1_iMHdBcw6svCveDYtanzVou6QzTIdqqZqb5i_lGq_uAYb6pNtdplU9ujbDpsxxYJY32YJgo2leaK1_30JIWiUkgztvpOurVClqS0nAvzqmTC6Z1k6p2orKj-ilRcp2K65kWfI90zW-OD30Zz1A18H8QH1E16sKVgB8YI9K7zv38h-f7O19t2nW1fdPlJ2JLwE6aVs6Hfz9BK-FNmcGuQ9V_mxI71c49-K--2Z3KPXcu9U1E0524R74K5tlOHz5nKitsQCk4LIJQnQ54gWP4ywMFek6Db02QSrEvfIzfvJQt06gKZ_ynUujFjd26bG4F4ZM1OT15qGMfJdKBzNdtHOAUrotOYv_oTEOf7MkP7mA3QqNMOZdBl-jlVNwu29Qpw2xFzK6oCq8xIcYWVzRXURvrLLOVhPtHxeKfG88BtpK4wPOEWLkv0HYEnpdzn_txwxt9GLzzqVaHteB6f5J7zIEeLnlGLJ8JLd5ffu_EOLQ-g4ZgyASMegYwzpos_Bi6Yp5C-Hsn-b4qIOB-ol4gu5y9ud6H7ClCxGO3-MkxFy14usmqe37cTfAIAM5XV-aChWhuYRttKy00 "Диаграмма activity")

# Диаграмма sequence
![sequence_for_personal_call](http://www.plantuml.com/plantuml/png/lP6nQiD038RtUmgHAO7c1JAKcBv0IUXirBC2HsNvUf82UVlU9KFSug6bfJTea3x-JvRtQbZCHmxwbYHZmH6KtfqaqdETf9WoYe7BG8MJK0WORIhmebJ2wrJxM2wmwdBc5D7I92j0XIw4Hi3s4ReT78afMc-NJ7r4vlMcfQGp6ZMoWstbhlmE3cHUPDtOJHXepiqZ3sr9jQMuW6oW7YEfdfmXebA0-XOznQkdJJ-vMcDcUsgM6tQ7lcJ-D78QCvDH7_y--uXdwkyNk2a4Hte0IwqENgx_wfTQOYLm-UwjJyYw40EBwxlymmT0Uu5a2FjQVEGF "Диаграмма sequence")
