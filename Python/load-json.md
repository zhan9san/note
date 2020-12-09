# Load Json

```Python
import json
with open('version.json') as f:
    data = json.load(f)
baseline = [(i['package_name']) for i in data['info'] if i['env'] == 'qa' and i['proj_name'] == 'Baseline']

```
