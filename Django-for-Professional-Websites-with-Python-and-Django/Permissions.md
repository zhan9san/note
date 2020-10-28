# Permissions

Relation between `permission_required` in `View` and `permissions` in `Custom Permission`

How does following code work to limit user access?

```Python
permission_required = 'books.special_status'
```

How does following code in test file to make user have specific access?

```Python
self.special_permission = Permission.objects.get(codename='special_status')
```
