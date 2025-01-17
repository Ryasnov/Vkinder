# Документация использования приложения VKinder <a name="TOC"></a>
<!-- TOC -->
* [Инструкция по установке приложения VKinder](#installation_guide)
* [Инструкция пользователя](#user_guide)
  * [Авторизация в боте](#user_auth)
  * [Элементы управления](#user_interface)
  * [Поиск](#user_search)
  * [Возрастной диапазон поиска](#user_search_age_params)
  * [Фотографии анкеты](#profile_photos)
  * [Избранное](#favorites)
  * [Черный список](#blacklist)
<!-- TOC -->
## Инструкция по установке приложения VKinder <a name="installation_guide"></a>
- Требуется установить СУБД **PostgreSQL** и создать базу данных;
- Требуется установить библиотеки, необходимые для работы скрипта, командой:  
`pip intstall -r requirements.txt`
- Перед запуском срипта необходимо задать следующие переменные переменные окружения:

| Имя переменной | Описание значения переменной                                                                        |
|----------------|-----------------------------------------------------------------------------------------------------|
| DB_NAME        | Имя базы данных, по умолчанию *vkinder*                                                             |
| DB_LOGIN       | Имя пользователя для подключения к базе данных, по умолчанию *postgres*                             |
| DP_PASS        | Пароль пользователя для подключения к базе данных, по умолчанию *postgres*                          |
| VK_APP_ID      | Идентификатор приложения VK                                                                         |
| VK_GROUP_ID    | Идентификатор группы VK                                                                             |
| VK_GROUP_TOKEN | Ключ сообщества (Access token), полученный в настройках сообщества (раздел настроек называется API) |
| *USER_TOKEN*   | Ключ пользователя (Access token) - указывать не обязательно, используется только в тестах.          |

## Инструкция пользователя <a name="user_guide"></a>
### Авторизация в боте <a name="user_auth"></a>
Когда пользователь написал впервые или ключ пользователя не активен, чат-бот требует авторизоваться.
Чтобы пройти авторизацию, необходимо:
1. Нажать кнопку <u>**Авторизоваться**</u>;
2. Дать запрашиваемые VK разрешения доступа;
3. Скопировать ссылку в адресной строке браузера и отправить её в чат;

![](docs/doc_auth.jpg?raw=true)

### Элементы управления <a name="user_interface"></a>
Описание текстовых команд показывается пользователю сразу после авторизации, 
можно вызвать эту справку нажав кнопку <u>**справка**</u> или отправив в чат цифру **5**.  
Пользователь может писать команды в чат или использовать кнопки. Действия, которые можно выполнить только нажатием на кнопку:
- поставить лайк фотографии;
- удалить анкету из избранного;

Чат-бот реагирует на каждое действие пользователя и сообщает о результате этого действия.

<img src="doc_menu.jpg?raw=true" width="350" />

### Поиск <a name="user_search"></a>
Параметры поиска:
- **город** - указан в профиле пользователя;
- **пол** - противоположен полу пользователя;
- **возрастной диапазон** определяется пользователем;  

Сначала пользователю показываются пользователи в статусе **в активном поиске**, затем в статусе **не женат/не замужем** 
(пользователи с другими статусами не показываются).  
Следующий вариант можно получить отправив в чат цифру **1** или нажав кнопку <u>**Следующий вариант**</u>.  
Все предложенные пользователю варианты хранятся в истории поиска и не будут показаны снова, 
даже если изменятся параметры поиска. 
Можно очистить историю поиска нажав на кнопку <u>**Очистить историю поиска**</u> или отправив в чат цифру 6. 
После этого будет сброшен и текущий фильтр поиска, будут показаны уже просмотренные варианты.
### Возрастной диапазон поиска <a name="user_search_age_params"></a>
Возрастной диапазон запрашивается в случаях когда:
- пользователь ранее не обращался в чат-бот
- пользователь нажал кнопку <u>**Изменить возрастной диапазон**</u> или отправил в чат цифру **0**

В ответ на запрос возрастного диапазона, необходимо ответить в формате *25-30* или *30 35*, 
где первая цифра это начало диапазона, а вторая - конец возрастного диапазона включительно.   
Например, указав диапазон *30-30*, будут показаны анкеты тридцатилетних пользователей.
<img src="https://github.com/fdm1try/VKinder/blob/main/docs/doc_age_request.jpg?raw=true" width="350" />
### Фотографии анкеты <a name="profile_photos"></a>
Показаны три самые популярные фотографии пользователя среди его аваторок и фотографий, на которых он отмечен.
Поставить лайк фотографии можно нажав на кнопку под анкетой c номером фотографии.

<img src="doc_profile_photos.jpg?raw=true" width="350" />

### Избранное <a name="favorites"></a>
Отправив в чат цифру **2**, в избранное будет добавлена последняя показанная пользователю анкета.
Можно добавить предложенный вариант в избранное нажав на кнопку под анкетой, 
даже если это не последняя анкета, показанная в чате.  
Удалить анкету из избранного можно только нажав на кнопку под анкетой.  
Посмотреть избранное можно нажав на кнопку <u>**Посмотреть избранное**</u> или отправив в чат цифру **4**. 
После чего в чат будут отправлены все анкеты из избранного.

<img src="doc_favorites.jpg?raw=true" width="350" />  


### Черный список <a name="blacklist"></a>
Анкеты в черном списке больше никогда не будут показаны пользователю, удалить записи из этого списка нельзя.
Отправив в чат цифру **3**, в черный список будет добавлена последняя анкета из чата.
Можно добавить в черный список любую анкету в чате нажав на кнопку под анкетой.
