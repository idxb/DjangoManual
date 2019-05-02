# DjangoManual

## Общая концепция работы Django

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
