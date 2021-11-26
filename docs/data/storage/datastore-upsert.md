## Datastore_upsert
##### Parameters
*	`resource_id` (string) – resource id that the data is going to be stored under.
*	`force` (boolean (optional, default: `false`)) – set to `true` to edit a read-only resource
*	`records` (list of dictionaries) – the data, e.g.: `[{"dob": "2005", "some_stuff": ["a","b"]}]` (optional)
*	`method` (string) – the method to use to put the data into the datastore. Possible options are: `"upsert"`, `"insert"`, `"update"` (optional, default: `"upsert"`)

##### Methods
*	`upsert`: Update if record with same key already exists, otherwise insert. Requires unique key.
*	`insert`: Insert only. This method is faster that upsert, but will fail if any inserted record matches an existing one. Does not require a unique key.
*	`update`: Update only. An exception will occur if the key that should be updated does not exist. Requires unique key.


##### Javascript
```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');

    var data = [
        {'indicator_id': 'CHD.B.HUM.04.T6',
            'dataset_id': 'acled',
            'region': 'KEN',
            'value': '50000000',
            'period': '2016'}

    ];
    packageId = '450f2c55-425f-4797-8d70-33b5729d1f1d';

    client.action('datastore_upsert', {
                resource_id:  packageId,
                records: data,
                method: 'upsert',
                force: 'True'
            },
            function(err) {
                if (err) console.log(err);
                console.log('All done');
            })

</script>
```

##### Python
```python
import ckanapi

remote = 'http://giv-oct.uni-muenster.de:5000'
apikey = '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39'
resource_id = '450f2c55-425f-4797-8d70-33b5729d1f1d'

ckan = ckanapi.RemoteCKAN(remote, apikey)

newRecord = [
    {'indicator_id': 'CHD.B.HUM.04.T6',
     'dataset_id': 'acled',
     'region': 'KEN',
     'value': '50000000',
     'period': '2016'}
]

ckan.action.datastore_upsert(
            resource_id=resource_id,
            method='upsert',
            records=newRecord,
            force=True)
```
