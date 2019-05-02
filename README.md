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

Добавим файл `myapp.urls.py` в общий шаблон `mysite/urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```
1. Все адреса описываются в файле папки приложения `myapp/urls.py`




