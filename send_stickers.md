# Отправка стикеров

**Акторы:** авторизованные пользователи, приложение.

**Цель:** авторизированный пользователь отправляет выбранный стикер другому авторизированному пользователю или в групповой чат, чтобы довавить характерных визуальных эффектов в диалог с конкретном пользователем.

**Предусловия:** у авторизованного пользователя открыт чат с конкретным авторизованным пользователем или групповой чат в который он хочет отправить стикер.

**Сценарий:**
1. Пользователь открывает меню для выбора конкретного стикера.
2. Приложение предлагает выбрать стикер из конкретного набора (или [загрузить новый набор стикеров](https://github.com/polinanov/use-case-and-diagram/blob/master/download_stickers.md "Загрузить новый набор стикеров")).
3. Пользователь выбирает стикер из конкретного набора и нажимает на него.

Пользователь может [загрузить новый набор стикеров](https://github.com/polinanov/use-case-and-diagram/blob/master/download_stickers.md "Загрузить новый набор стикеров").

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
![activity_for_personal_call](http://www.plantuml.com/plantuml/png/XP11JyCm38Nl-HMMk6mI4lVsicbSE34n4ESiTTU8r0wnmq3gZoSfgmH8Y5lip_5xpnjHcpIFmKnFWcaoSssQ-uWaO654oj1p0i60JZsTIbCYEjzx1wBUlM1gpNIr9VMl6Py7hpXjOmpUMVLCasbs0xCWs6KS-iJZZpMeK2GwFbDWsnL4UFxgziidWPMuvAD2ZdyFhTibHtEO3Si_ifOwSA5m0IRmsffVvfT3E2P2LvkmSZoEcIupu0PBX64DVSrWrO8cIz8NnIprO3eWFExsS0DtUuY9bHs7rZGFg3cHp3oXH2R16gRMafr3aJw7OfEwkcOXoysRWtr3kIXoPVFxQ0KBlFKIW_tudjzJAJfl0v_WoE_ramsXcCGary0HvopQ6b6EPbDaynW-0G00 "Диаграмма activity")

# Диаграмма sequence
![sequence_for_personal_call](lv0Agv4ofXS8JIPzvoP5FnxaoxaWIXcaSLmEFUSp5czrHBiccLXvKg6ZmQ9U6Jr7FF2ujGaGKiMXC3HPwLdWuQtkTzPFsapBKl9aJtFiY4sca8O11qUQ3hI4mgYNwphhj3jRZZoZHs3c "Диаграмма sequence")
