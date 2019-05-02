# Общая концепция работы Django

## Модели

---
1. Описываем в нашем приложении модель в файле `myapp/models.py`

```python
# Пример модели и ее методов для записи в блоге
# Определяем нашу модель с именем Post(и является наследованием от модели Django(models.Model))
class Post(models.Model):
    
    # Свойства модели Post
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    published_date = models.DateTimeField(blank=True, null=True)

    # Метод publish
    def publish(self):
        self.published_date = timezone.now()
        self.save()

    # Метод удобного отображения имени из поля title
    def __str__(self):
        return self.title
```
[Помощь по полям модели](https://docs.djangoproject.com/en/2.2/ref/models/fields/)

2. Делаем миграцию полей в базу с помощью командной строки

3. Добавляем поля в админку

---

## Url

Добавим файл `myapp.urls.py` в глобальный шаблон `mysite/urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    # Запрос к 127.0.0.1 отправит нас к myapp.urls
    path('', include('myapp.urls')),
]
```
1. Все адреса описываются в файле папки приложения `myapp/urls.py`

```python
# Импортируем функцию path и все views из приложения
from django.urls import path
from . import views

# Добавляем шаблон ссылки на соответствующий view
urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```
[Помощь по описанию ссылок](https://docs.djangoproject.com/en/2.0/topics/http/urls/)

---

## Представления

Все представления находятся в `myapp/views.py` и они выводятся, когда к ним обращаются через `urls.py`

1. Обращаемся чрез urls.py (составной ссылке, например)
2. Запрашиваем какой-то метод из views.py
3. И выводим результат в шаблон, который указан в методе или функции на вывод. Шаблон должен быть предварительно создан

`myapp/views.py`

```python
def post_list(request):
#   Возвращаем функцию render, которая принимает request в качестве аргумента
#   и дальше все собирается на  шаблоне post_list.html
    return render(request, 'blog/post_list.html', {})
```    
    [Помощь по предствалениям](https://docs.djangoproject.com/en/2.2/topics/http/views/)
    
---

## Шаблоны

Шаблоны создаются в папке `myapp/templates/myapp`

Что бы интерактивно выводить данные в представления, нам нужно воспользоваться API QuerySet в файле представлений и сформировать правильный запрос.

[Огромная помощь по QuerySet API](https://docs.djangoproject.com/en/2.2/ref/models/querysets/)
