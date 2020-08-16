# Сервис уведомлений о лидах
## Общий алгоритм
```mermaid
graph TD;
A(получаем лиды из facebook) --> B(обогащаем лидов)
B --> C(преобразуем в уведомление)
C --> D(посылаем уведомление в каналы связи)
```

Требования:
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

### Телеграм
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg5NTczODUwNSw2NzQ4NTY5NjUsLTE1MT
Q5OTU0MjIsMjEyNTEyMTQ1NV19
-->