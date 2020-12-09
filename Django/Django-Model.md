# Django Model

```html
    <ul>
        {% for student in students %}
            <li>{{ student.name }} - {{ student.get_status_display }}</li>
        {% endfor %}
    </ul>
```

Django will provide us a function to get the `status`

```Python
    STATUS_ITEMS = [
        (0, '申请'),
        (1, '通过'),
        (2, '拒绝'),
    ]
    status = models.IntegerField(choices=STATUS_ITEMS, default=0, verbose_name="审核状态")
```

In Django admin, Django will automatically invoke `get_status_display`, so there is no need to set extra configurations.
