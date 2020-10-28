# Securing the API with Authentication and Permissions

## Understanding authentication and permissions in Django, the Django REST framework, and RESTful Web Services

## Authentication classes

## Security and permissions-related data to models

Question: when is `related_name` required?

```Python
owner = models.ForeignKey(
        'auth.User',
        related_name='drones',
        on_delete=models.CASCADE)
```

Anwser: See `https://docs.djangoproject.com/en/dev/topics/db/queries/#backwards-related-objects`
Note the attribute name difference below, the first is custom(__drones__) where the second is FOO_set(__competition_set__).

With `related_name` explictly

```Python
from drones.models import DroneCategory
s = DroneCategory.objects.get(id=1)
qs1 = s.drones.all()
print(qs1.query)

Output:
SELECT "drones_drone"."id", "drones_drone"."name", "drones_drone"."drone_category_id", "drones_drone"."manufacturing_date", "drones_drone"."has_it_competed", "drones_drone"."inserted_timestamp" FROM "drones_drone" WHERE "drones_drone"."drone_category_id" = 1 ORDER BY "drones_drone"."name" ASC
```

```Python
from drones.models import Drone
z = Drone.objects.get(id=1)
qs = z.competition_set.all()
print(qs.query)
print(qs.query)

Output:
SELECT "drones_competition"."id", "drones_competition"."pilot_id", "drones_competition"."drone_id", "drones_competition"."distance_in_feet", "drones_competition"."distance_achievement_date" FROM "drones_competition" WHERE "drones_competition"."drone_id" = 1 ORDER BY "drones_competition"."distance_in_feet" DESC
```

Document  
The code specifies the drones name that we specified as the string value for the `related_name` argument when we added the owner field as a `model.ForeignKey` instance in the Drone model.
Question: Does the specified name have to match the `related_name`?

Answer: Yes, they are required to be the same.

Document  
The new version of the `DroneSerializer` class declares an `owner` attribute as an instance of `serializers.ReadOnlyField` with the source argument equal to `owner.username`. This way, the serializer will serialize the value for the `username` field of the related `django.contrib.auth.User` instance stored in the `owner` field.

The code uses the `ReadOnlyField` class because the owner is automatically populated when an authenticated user creates a new drone. It will be impossible to change the owner after a drone has been created with an HTTP POST method call. This way, the `owner` field will render the username that created the related drone. In addition, we added `'owner'` to the `fields` string tuple within the `Meta` inner class.

## Working with object-level permissions via customized permission classes

## Saving information about users that make requests

Question: What if you need to set extra attributes on the saved model instance?  
For example: 'serializer.save(owner=request.user)'.  
Answer: Override the `perform_create` method in the View Class declared in the `views.py` file

```Python
    def perform_create(self, serializer):
        serializer.save(owner=self.request.user)
```

Related implementation in `ListSerializer` in `rest_framework/serializers.py`

```Python
        validated_data = [
            dict(list(attrs.items()) + list(kwargs.items()))
            for attrs in self.validated_data
        ]
```

## Setting permissions policies

## Creating the superuser for Django Creating a user for Django

## Making authenticated requests

Bookmark

## Browsing the secured API with the required authentication

## Working with token-based authentication

## Generating and using tokens

Question: How does token header works?
