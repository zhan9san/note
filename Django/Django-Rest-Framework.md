# Django Rest Framework

generics.py

```Python
class GenericAPIView(views.APIView): -> def get_queryset(self):
```

This method should always be used rather than accessing `self.queryset` directly, as `self.queryset` gets evaluated only once, and those results are cached for all subsequent requests.

```Python
queryset = queryset.all()
```

```Python
help(django.db.models.query.QuerySet)

all(self)
```

Returns a new QuerySet that is a copy of the current one. This allows a QuerySet to proxy for a model manager in some cases.
