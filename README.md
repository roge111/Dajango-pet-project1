# Dajango-pet-project1

Привет. Это простой пример создания сайта на Django. Чтобы посмотреть подробнее про Django, переходи в репозиторий [Django_project_first](https://github.com/roge111/Django_project_first).

# 🏛️ Структура

Важно знать о структуре. Структура проекта тут такая. 
Идет самая главная папка. Папку можно назвать как угодно. Это проект внутри среды разработки. Это `Django`. 

`djungo_curse` — это уже проект на django со всеми его возможностями.
### django_curse
---
Внутри этой папки у нас имеется:
- папка `django_curse`, содержащая все настройки проекта, контроль над URL-ссылками и т.д.;
- папка `main`, являющаяся приложением, отвечающим за главную страницу;
- `manage.py` — это главный файл, созданный по умолчанию. Через него мы запускаем сервер и т.д.

### main
---

Внутри:

- папка `migrations` — это папка, содержащая миграции;
- `static/main` — это папки, содержащие статические файлы: css, картинки и скрипты;
- `templates` — папка, содержащая шаблон html (`pattern.html`) и две html страницы с шаблонизаторами. (Что это такое, можно найти в репозитории по ссылке в начале.)

### static/main
---
 Внутри:
- `css` — папка с css-файлами;
- `js` — папка с файлами javascript;
- `img` — папка с картинками.

# 👨‍💻 Про код

### Settings

В файле `settings.py` требуется в конце добавить следующий элемент:

```
STATICFILES_DIRS = [
    BASE_DIR / "static",
]
```

Это поможет проекту правильно находить статические файлы

### django_curse/urls.py
---

Также, согласно документации, `urls.py` в папке самого проекта изменяется на такой код:
```

from django.contrib import admin
from django.urls import path, include

from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls')),
    
] + static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)

```

Тут мы импортировали файл settings и импортировали static для дальнейшей корректной работы. А к `urlpatterns` добавили: `+ static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)`.

### templates/main/pattern.html

Тут мы подключаем Bootstrap для подгрузки уже готовых стилей.

```
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css">
```

Далее подключим файл со стилями `main.css`:

```
<link rel="stylesheet" href="{% static 'main/css/main.css' %}">
```

А также подключаем Fontawesome для использования готовых различных иконок:

```
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" integrity="sha512-...ваш_код..." crossorigin="anonymous" referrerpolicy="no-referrer" />
```
Далее в `body` я создаю два раздела: `aside` и `main`. `aside` отвечает за выдвигающуюся боковую панель с навигацией по сайту и лого. Лого загружается из папки `static/main/img`. В боковой панели я создаю три кнопки с переходом на сайт.
```
<ul>
        <a href="{% url 'home' %}"><li><i class="fas fa-house"></i> Главная</li></a>
        <a href="{% url 'about' %}"><li><i class="fa-solid fa-user"></i> О нас</li></a>
        <a href="{% url 'contacts' %}"><li><i class="fa-sharp-duotone fa-regular fa-comment"></i> Контакты</li></a>
</ul>
```
Всё, что в теге `i` — это иконки из сайта Fontawesome. Чтобы получить такой тег с классом для иконки, можно зайти на [официальный сайт](https://fontawesome.com/) и в поиске вбить название иконки, где уже потом увидите данный тег `i`. Его копируем и вставляем в тег `li`. А `"{% url 'contacts' %}"` — это обращение по имени к ссылке. Имя мы даем в `urls.py` внутри приложения.

Блок `main` содержит шаблон, куда из разных сайтов будет подставляться свой блок. И данный блок назван `content`. То же самое и с `title` в теге `head`.
```
<main>
    {% block content %}

    {% endblock %}
</main>
```

### statix/main/css/main.css

В данном файле описаны стили для сайта

```
body{
    background: #2a27d4;
}

#Logo{
    width: 100%;
    height: 30%;
}

aside{
    float: left;
    background: #2f2e2e;
    width: 20%;
    padding: 2.5%;
    height: 100vh;
    border-right: 5 px solid #c8c2c2;
    position: fixed;
    left: -200px;

    transition: left 0.4s ease;
    z-index: 1000;
}

aside:hover {
    left: 0;
}

aside ul {list-style: none;}

aside ul li{
    color: #fff;
    display:  block;
    margin-top: 10px;

    transition: 0.4s ease;
}

aside h3{
    color: #fff;
}
a {
  text-decoration: none;
}

aside ul li:hover, aside ul a:hover {
    color: #eb5959;
    text-decoration: none;
    transform: scale(1.30);
}

main {
  margin-left: 10%; /* или 250px, если панель выезжает полностью */
  padding: 20px;
  transition: margin-left 0.4s ease;
}

main .features{
    color: #fff;
}

main h1{
    color: #fff;
}
```


Изначально у нас боковая панель почти спрятана. Об этом свидетельствует `left: -200px` в этом участке кода.

```
aside{
    float: left;
    background: #2f2e2e;
    width: 20%;
    padding: 2.5%;
    height: 100vh;
    border-right: 5 px solid #c8c2c2;
    position: fixed;
    left: -200px;

    transition: left 0.4s ease;
    z-index: 1000;
}
```

Также с помощью `z-index` мы обеспечиваем, что наша панель будет поверх всего. Также тут указан цвет фона и т. д. А то, чтобы она выдвигалась при наведении, нам позволяет сделать вот этот код:

```
aside:hover {
    left: 0;
}
```

`hover` — функция, которая позволяет накладывать эффект при наведении.


```
aside ul {list-style: none;}
```
Это убирает у нас точки возле кнопок навигации.



```
aside ul li{
    color: #fff;
    display:  block;
    margin-top: 10px;

    transition: 0.4s ease;
}

aside ul li:hover, aside ul a:hover {
    color: #eb5959;
    text-decoration: none;
    transform: scale(1.30);
}
```

Эти участки кода позволяют нам сделать так, чтобы при наведении на кнопки навигации, которые спрятаны под тегами `li`, которые внутри `ul` и внутри `aside`, они увеличивались и делались красными. Но по умолчанию они у нас белого цвета.

```
main {
  margin-left: 10%; /* или 250px, если панель выезжает полностью */
  padding: 20px;
  transition: margin-left 0.4s ease;
}

main .features{
    color: #fff;
}

main h1{
    color: #fff;
}
```

Ну, это позволяет нам сделать так, чтобы главная часть страницы была видна.


### main/urls.py
---

```

from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='home'),
    path('about', views.about, name = 'about'),
    path('contacts', views.contats, name = 'contacts')
]

```

Тут мы внутри `path` с помощью аргумента `name` даем имена нашим ссылкам, которые потом используем в `html` как `"{% url 'contacts' %}"`, например.




### main/views.py

```
from django.shortcuts import render
from django.http import HttpResponse


def index(request):
    return render(request, 'main/index.html')

def about(request):
    return render(request, 'main/about.html')

def contats(request):
    return render(request, 'main/contacts.html')

```

Тут мы в каждой функции вызываем соответствующий html, используя render от django.
