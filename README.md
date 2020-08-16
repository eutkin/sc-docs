# Сервис уведомлений о лидах
##
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

Facebook Module: 
```mermaid
graph TD;
A(Rest controller) -->|FacebookLead|B(FacebookEnrich)
B -->|FacebookEnrichedLead|C(FacebookEnrichedLeadConverter)
C -->|Lead|D(output)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ4NjMzOTIyMSw2NzQ4NTY5NjUsLTE1MT
Q5OTU0MjIsMjEyNTEyMTQ1NV19
-->