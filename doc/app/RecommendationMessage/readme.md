# RecommendationMessage - временный рекомендательный сервис

## 1. Общая информация

RecommendationMessage - Временный рекомендательный сервис, это упрощенная версия 
рекомендательного сервиса, создана для скорейшего запуска проекта, в связи с тем, 
что основной сервис пока не доделан и требует еще минимум 2-3 недели доработок до 
mvp версии

Сервис представлен в виде чата. Будет использоваться верстка тех поддержки. 
Пользователю будут в ручном режиме приходить рекомендации от администратора сайта, 
которые он будет выполнять (добавить карьеру, выбрать курс и т д).

Администратор сайта будет отслеживать каждого пользователя как они выполняют рекомендации
и по мере выполнения будет создавать новые рекомендации.

Пользователь может отвечать или уточнять рекомендации, которые ему направляет
администратор

Администратор пишет рекомендации используя админку, раздел "Рекомендации", где может
используя фильтры быстро выбрать нужного пользователя и просмотреть всю переписку,
а также ответить на рекомендации

В дальнейшем можно к примеру автоматизировать этот сервис, добавив оповещения для 
администратора о том что те или иные рекомендации пользователем выполнены, чтобы была
более быстрая реакция и предложение новых рекомендаций


## 2. Описание сущностей и кода

- `RecommendationMessage` - основная сущность сервиса, харатеризует рекомендацию 
   и ответ пользователя. По сути это сообщения из которых создается чат пользователя
   с администратором сайта
- `personal-area/page/recommendation_messages` - эндпоинт рекомендаций, по которому
   можно получить все сообщения для конкретного акаунта пользователя. Можно использовать
   параметры `limit` и `offset` для разбиения на страницы или lazy-load подгрузки 
   сообщений
- `personal-area/handler/recommendation_message` - хендлер добавления рекомендаций
- `personal-area/handler/recommendation_message/is_seen_status/update` - хендлер обновления
   статуса сообщений isSeen о том, что они просмотрены. С каждым списком рекомендаций
   для каждого сообщения приходит статус isSeen = true/false. И если хоть одно из сообщений
   имеет статус isSeen = false, значит на фронтенде должен появиться колокольчик-оповещение
   для пользователя, где-то в углу с верху например, чтобы пользователь открыл чат 
   рекомендаций и просмотрел сообщения. После промотра пользовавателем всех сообщений
   фронтенд должен вызвать этот хендлер, чтобы обновить статус всех рекомендаций, что они
   просмотрены
