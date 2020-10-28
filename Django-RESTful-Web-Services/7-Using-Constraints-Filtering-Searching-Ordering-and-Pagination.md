# Using Contraints, Filtering, Searching, Ordering, and Pagination

If there are multiple table rows with equal indexed values, an error `DETAIL:  Key (name)=(Peter Perfect) is duplicated.` will occur while executing `python manage.py migrate`

Before adding `unique=True`

```bash
drones=# \d drones_drone
                                           Table "public.drones_drone"
       Column       |           Type           | Collation | Nullable |                 Default
--------------------+--------------------------+-----------+----------+------------------------------------------
 id                 | integer                  |           | not null | nextval('drones_drone_id_seq'::regclass)
 name               | character varying(250)   |           | not null | 
 manufacturing_date | timestamp with time zone |           | not null | 
 has_it_competed    | boolean                  |           | not null | 
 inserted_timestamp | timestamp with time zone |           | not null | 
 drone_category_id  | integer                  |           | not null | 
Indexes:
    "drones_drone_pkey" PRIMARY KEY, btree (id)
    "drones_drone_drone_category_id_214d98cf" btree (drone_category_id)
Foreign-key constraints:
    "drones_drone_drone_category_id_214d98cf_fk_drones_dr" FOREIGN KEY (drone_category_id) REFERENCES drones_dronecategory(id) DEFERRABLE INITIALLY DEFERRED
Referenced by:
    TABLE "drones_competition" CONSTRAINT "drones_competition_drone_id_4ef19446_fk_drones_drone_id" FOREIGN KEY (drone_id) REFERENCES drones_drone(id) DEFERRABLE INITIALLY DEFERRED

drones=# \d drones_dronecategory
                                    Table "public.drones_dronecategory"
 Column |          Type          | Collation | Nullable |                     Default
--------+------------------------+-----------+----------+--------------------------------------------------
 id     | integer                |           | not null | nextval('drones_dronecategory_id_seq'::regclass)
 name   | character varying(250) |           | not null |
Indexes:
    "drones_dronecategory_pkey" PRIMARY KEY, btree (id)
Referenced by:
    TABLE "drones_drone" CONSTRAINT "drones_drone_drone_category_id_214d98cf_fk_drones_dr" FOREIGN KEY (drone_category_id) REFERENCES drones_dronecategory(id) DEFERRABLE INITIALLY DEFERRED

drones=# \d drones_pilot
                                           Table "public.drones_pilot"
       Column       |           Type           | Collation | Nullable |                 Default
--------------------+--------------------------+-----------+----------+------------------------------------------
 id                 | integer                  |           | not null | nextval('drones_pilot_id_seq'::regclass)
 name               | character varying(150)   |           | not null | 
 gender             | character varying(2)     |           | not null | 
 races_count        | integer                  |           | not null | 
 inserted_timestamp | timestamp with time zone |           | not null | 
Indexes:
    "drones_pilot_pkey" PRIMARY KEY, btree (id)
Referenced by:
    TABLE "drones_competition" CONSTRAINT "drones_competition_pilot_id_84db5b9e_fk_drones_pilot_id" FOREIGN KEY (pilot_id) REFERENCES drones_pilot(id) DEFERRABLE INITIALLY DEFERRED
```

After

```bash
drones=# \d drones_drone
                                           Table "public.drones_drone"
       Column       |           Type           | Collation | Nullable |                 Default
--------------------+--------------------------+-----------+----------+------------------------------------------
 id                 | integer                  |           | not null | nextval('drones_drone_id_seq'::regclass)
 name               | character varying(250)   |           | not null |
 manufacturing_date | timestamp with time zone |           | not null |
 has_it_competed    | boolean                  |           | not null |
 inserted_timestamp | timestamp with time zone |           | not null |
 drone_category_id  | integer                  |           | not null |
Indexes:
    "drones_drone_pkey" PRIMARY KEY, btree (id)
    "drones_drone_name_85faecee_uniq" UNIQUE CONSTRAINT, btree (name)
    "drones_drone_drone_category_id_214d98cf" btree (drone_category_id)
    "drones_drone_name_85faecee_like" btree (name varchar_pattern_ops)
Foreign-key constraints:
    "drones_drone_drone_category_id_214d98cf_fk_drones_dr" FOREIGN KEY (drone_category_id) REFERENCES drones_dronecategory(id) DEFERRABLE INITIALLY DEFERRED
Referenced by:
    TABLE "drones_competition" CONSTRAINT "drones_competition_drone_id_4ef19446_fk_drones_drone_id" FOREIGN KEY (drone_id) REFERENCES drones_drone(id) DEFERRABLE INITIALLY DEFERRED

drones=# \d drones_dronecategory
                                    Table "public.drones_dronecategory"
 Column |          Type          | Collation | Nullable |                     Default
--------+------------------------+-----------+----------+--------------------------------------------------
 id     | integer                |           | not null | nextval('drones_dronecategory_id_seq'::regclass)
 name   | character varying(250) |           | not null | 
Indexes:
    "drones_dronecategory_pkey" PRIMARY KEY, btree (id)
    "drones_dronecategory_name_dedead86_uniq" UNIQUE CONSTRAINT, btree (name)
    "drones_dronecategory_name_dedead86_like" btree (name varchar_pattern_ops)
Referenced by:
    TABLE "drones_drone" CONSTRAINT "drones_drone_drone_category_id_214d98cf_fk_drones_dr" FOREIGN KEY (drone_category_id) REFERENCES drones_dronecategory(id) DEFERRABLE INITIALLY DEFERRED

drones=# \d drones_pilot
                                           Table "public.drones_pilot"
       Column       |           Type           | Collation | Nullable |                 Default
--------------------+--------------------------+-----------+----------+------------------------------------------
 id                 | integer                  |           | not null | nextval('drones_pilot_id_seq'::regclass)
 name               | character varying(150)   |           | not null |
 gender             | character varying(2)     |           | not null |
 races_count        | integer                  |           | not null |
 inserted_timestamp | timestamp with time zone |           | not null |
Indexes:
    "drones_pilot_pkey" PRIMARY KEY, btree (id)
    "drones_pilot_name_3b56f2a1_uniq" UNIQUE CONSTRAINT, btree (name)
    "drones_pilot_name_3b56f2a1_like" btree (name varchar_pattern_ops)
Referenced by:
    TABLE "drones_competition" CONSTRAINT "drones_competition_pilot_id_84db5b9e_fk_drones_pilot_id" FOREIGN KEY (pilot_id) REFERENCES drones_pilot(id) DEFERRABLE INITIALLY DEFERRED
```

## Browsing the API with resources and relationships

## Defining unique constraints

## Working with unique constraints

## Understanding pagination

## Configuring pagination classes

## Making requests that paginate results

## Working with customized pagination classes

We enabled pagination to limit the size for the result sets. However, any client or user is able to specify a large number for the limit value, such as 10000, and generate a huge result set. In order to specify the maximum number that is accepted for the limit query parameter, it is necessary to create a customized version of the limit/offset pagination scheme that the Django REST framework provides us.

Here is snippet in `drones/custompagination.py`

```Python
from rest_framework.pagination import LimitOffsetPagination

class LimitOffsetPaginationWithUpperBound(LimitOffsetPagination):
    # Set the maximum limit value to 8
    max_limit = 8
```

Here is snippet in `restful01/settings.py`

```Python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'drones.custompagination.LimitOffsetPaginationWithUpperBound',
    'PAGE_SIZE': 4
    }
```

### Question

If `max_limit` is set to 2 globally, the drone category is limited to 2, but the drones in drone category are still not limited.
Do we need to limit the drone number when access drone category?

## Making requests that use customized paginated results

## Configuring filter backend classes

Bookmark

## Adding filtering, searching, and ordering

It is said that 'Hence, we will make changes to all the classes with the List suffix in the views.py file: DroneCategoryList, DroneList, PilotList, and CompetitionList'.

Why does `filter_fields`, `search_fields` and `ordering_fields` exist in DroneCategoryDetail? Is it a mistake?

## Working with different types of Django filters

## Making requests that filter results

## Composing requests that filter and order results

## Making requests that perform starts with searches

## Using the browsable API to test pagination, filtering, searching, and ordering
