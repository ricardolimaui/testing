## Datastore_delete
##### Parameters
*   `resource_id` (string) – resource id that the data will be deleted from. (optional)
*	`force` (boolean (optional, default: `false`)) – set to `true` to edit a read-only resource
*	`filters` (dictionary) – filters to apply before deleting, e.g.: `{"name": "fred"}`. If missing delete whole table and all dependent views. (optional)

##### Javascript
```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');
    var resourceId = '450f2c55-425f-4797-8d70-33b5729d1f1d';

    var nfilters = {"region": 'KEN'};

    var search = client.action('datastore_delete', {
                resource_id:  resourceId,
                filters: nfilters,
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
#!/usr/bin/env python2
import ckanapi

remote = 'http://giv-oct.uni-muenster.de:5000'
apikey = '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39'
resource_id = 'c123ba85-41f9-4a04-80f5-a26368ba9204'

ckan = ckanapi.RemoteCKAN(remote, apikey)

filters = {"region": "KEN"} 

data = ckan.action.datastore_delete(resource_id=resource_id, filters=filters, force= True)
```
