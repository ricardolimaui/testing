## Datastore_create
##### Parameters
*	`resource_id` (string) – resource id that the data is going to be stored against.
*	`force` (boolean (optional, default: `false`)) – set to `true` to edit a read-only resource
*	`resource` (dictionary) – resource dictionary that is passed to `resource_create()`. Use instead of `resource_id` (optional)
*	`aliases` (list or comma separated string) – names for read only aliases of the resource. (optional)
*	`fields` (list of dictionaries) – fields/columns and their extra metadata. (optional)
*	`records` (list of dictionaries) – the data, e.g.: `[{"dob": "2005", "some_stuff": ["a", "b"]}]` (optional)
*	`primary_key` (list or comma separated string) – fields that represent a unique key (optional)
*	`indexes` (list or comma separated string) – indexes on table (optional)


##### Javascript

```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');

    var nfields = [
        {'id': 'dataset_id', 'type': 'text'},
        {'id': 'indicator_id', 'type': 'text'},
        {'id': 'region', 'type': 'text'},
        {'id': 'period', 'type': 'int'},
        {'id': 'value', 'type': 'float'}
    ];

    var data = [
        {
            'indicator_id': 'Population',
            'dataset_id': 'acled',
            'region': 'ITA',
            'value': '5000000',
            'period': '2016'
        }
    ];

    var resource = {
        "package_id": "packagetest",
        "format": "CSV",
        "name": "NameExample2"
    };

    client.action('datastore_create', {
        resource:  resource,
        records: data,
        primary_key: 'dataset_id'
    }, function(err) {
        if (err) console.log(err);
        console.log('All done');
    });

</script>
```

##### Python

```python
#!/usr/bin/env python2
import ckanapi

remote = 'http://giv-oct.uni-muenster.de:5000'
apikey = '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39'

ckan = ckanapi.RemoteCKAN(remote, apikey)

package = ckan.action.package_show(id='packagetest')

resource = {"package_id": package['id'],"format": "CSV", "name": "NameExample"}

newfields = [
    {'id': 'dataset_id', 'type': 'text'},
    {'id': 'indicator_id', 'type': 'text'},
    {'id': 'region', 'type': 'text'},
    {'id': 'period', 'type': 'int'},
    {'id': 'value', 'type': 'float'}
]

newRecords = [
    {	
        'indicator_id': 'Population',
        'dataset_id': 'acled',
        'region': 'ITA',
        'value': '5000000',
        'period': '2016'
    }
]

ckan.action.datastore_create(resource=resource, fields=newfields, records=newRecords, primary_key='dataset_id')
```
