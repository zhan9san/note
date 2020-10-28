# Content

## Defining the requirements for a complex RESTful Web Service

1. The related_name argument for the django.db.models.ForeignKey class initializer specifies the name to use for the relation from the related object back to this object

1.

```Python
class Drone(models.Model):
    pass
    class Meta:
        ordering = ('name',)
```

While using `Drone.objects.all()`, the result will be sorted by `name`.

### DroneCategory model

The drone category (DroneCategory model) just requires a name.

### Drone model

* A foreign key to a drone category (DroneCategory model)
* A name
* A manufacturing date
* A bool value indicating whether the drone participated in at least one competition or not
* A timestamp with the date and time in which the drone was inserted in the database

### Pilot model

* A name
* A gender value
* An integer value with the number of races in which the pilot participated
* A timestamp with the date and time in which the pilot was inserted in the database

### Competitoin model

* A foreign key to a pilot(Pilot model)
* A foreign key to a drone (Drone model)
* A distance value (measured in feet)
* A date in which the drone controlled by the pilot reached the specified distance value

## Creating a new app with Django

## Configuration a new web service

## Installing PostgreSQL

## Running migrations that generate relationships

## Analyzing the database

## Configuring serialization and deserialization with relationships

## Defining hyperlinks with serializers.HyperlinkedModelSerializer

## Working with class-based views

## Taking advantage of generic classes and generic views

## Generalizing and mixing behavior

## Working with routing and endpoints

## Making requests that interact with resources that have relationships

```Python
class PilotCompetitionSerializer(serializers.ModelSerializer):
    # Display the pilot's name
    pilot = serializers.SlugRelatedField(queryset=Pilot.objects.all(), slug_field='name')
    # Display the drone's name
    drone = serializers.SlugRelatedField(queryset=Drone.objects.all(), slug_field='name')

    class Meta:
        model = Competition
        fields = (
            'url',
            'pk',
            'distance_in_feet',
            'distance_achievement_date',
            'pilot',
            'drone')
```

If the names in different rows are the same, it will fail when create a new PilotCompetition. Is it related to `slug_field`?
