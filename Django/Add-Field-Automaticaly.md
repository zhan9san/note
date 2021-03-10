# Add Field

In `admin.py`

```Python
class JobAdmin(admin.ModelAdmin):
    def save_model(self, request, obj, form, change):
        obj.creator = request.user
```
