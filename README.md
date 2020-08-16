```mermaid
graph TD;
A(receive leads from facebook) --> B(encrich leads)
B --> C(transform to notification)
C --> D(send notification to channel)
```

- Поддержка разных источников лидов
- Поддержка разных каналов для уведомлений

## Модули
### Facebook модуль.
Содержит логику, характерную только для Facebook. 
Компоненты:
	- Rest контроллер/Webhook
	- Обогатитель лидов 

Модуль входные данные получает извне.
Выходные модуля – общая форма Лида
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MjAwNDQyMDcsNjc0ODU2OTY1LC0xNT
E0OTk1NDIyLDIxMjUxMjE0NTVdfQ==
-->