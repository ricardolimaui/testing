## Datastore_search

##### Parameters
*   `resource_id` (string) – id or alias of the resource to be searched against
*	`filters` (dictionary) – matching conditions to select, e.g `{"key1": "a", "key2": "b"}` (optional)
*	`q` (string) – full text query (optional)
*	`plain` (boolean) – treat as plain text query (optional, default: `true`)
*	`language` (string) – language of the full text query (optional, default: `"english"`)
*	`limit` (integer) – maximum number of rows to return (optional, default: `100`)
*	`offset` (integer) – offset this number of rows (optional)
*	`fields` (list or comma separated string) – fields to return (optional, default: all fields in original order)
*	`sort` (string) – comma separated field names with ordering e.g.: `"fieldname1, fieldname2 desc"`

##### Javascript
```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');
    var resourceId = '450f2c55-425f-4797-8d70-33b5729d1f1d';

    var nfilters = {"region": 'KEN'};

    var search = client.action('datastore_search', {
        resource_id:  resourceId,
        filters: nfilters
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
resource_id = 'c123ba85-41f9-4a04-80f5-a26368ba9204'

ckan = ckanapi.RemoteCKAN(remote, apikey)

filters = {"region": "KEN"} 

data = ckan.action.datastore_search(resource_id=resource_id, filters=filters)
for record in data['records']:
    print 'region: {x}, value: {y}'.format(x=record['region'], y=record['value'])
```

