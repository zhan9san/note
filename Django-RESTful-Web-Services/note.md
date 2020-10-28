# Note

How `serializers.ModelSerializer` implement `create` function

Main code snippet

```Python
ModelClass = self.Meta.model

instance = ModelClass._default_manager.create(**validated_data)

    @property
    def _default_manager(cls):
        return cls._meta.default_manager
```

What's the meaning of `remote_field`?  
[__setitem__](https://www.geeksforgeeks.org/__getitem__-and-__setitem__-in-python/)

```Python

def _get_fields(opts):
    fields = OrderedDict()
    for field in [field for field in opts.fields if field.serialize and not field.remote_field]:
        fields[field.name] = field
```

### Question

Taking advantage of content negotiation classes

### Question on `Django RESTful Web Services`

Which of the following classes is responsible for rendering the text/html content:  
__Errata__  
Errata Type: Typo | Page 148 and 170  

This:  
rest_framework.response.BrowsableAPIRenderer  

Should be:  
The rest_framework.render.BrowsableAPIRenderer class

#### Q

This way, we will be able to easily access all the drones that belong to a specific drone category. Whenever we delete a drone category, we want all the drones that belong to this category to be deleted, too, and therefore, we specified the models.CASCADE value for the on_delete argument.

how about only delete group?

### note

```Python
    drone_category = models.ForeignKey(
        DroneCategory,
        related_name='drones',
        on_delete=models.CASCADE)
```

The previous line uses the django.db.models.ForeignKey class to provide a many-to-one relationship to the DroneCategory model. The 'drones' value

specified for the related_name argument creates a backwards relation from the DroneCategory model to the Drone model. This value indicates the name to

use for the relation from the related DroneCategory object back to a Drone object.

```Python
    drone = models.ForeignKey(
        Drone,
        on_delete=models.CASCADE)
```

The previous line uses the django.db.models.ForeignKey class to provide a many-to-one relationship to the Drone model. In this case, we don't create a backwards relation because we don't need it. Thus, we don't specify a value for the related_name argument. Whenever we delete a drone, we want all the competitions in which the drone participated to be deleted too, and therefore, we specified the models.CASCADE value for the on_delete argument.
