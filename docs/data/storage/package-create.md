## Package_create

##### Parameters

*	`name` (string) – the name of the new dataset, must be between 2 and 100 characters long and contain only lowercase alphanumeric characters, - and _, e.g.: `warandpeace`
*	`title` (string) – the title of the dataset (optional, default: same as name)
*	`author` (string) – the name of the dataset’s author (optional)
*	`author_email` (string) – the email address of the dataset’s author (optional)
*	`maintainer` (string) – the name of the dataset’s maintainer (optional)
*	`maintainer_email` (string) – the email address of the dataset’s maintainer (optional)
*	`license_id` (license id string) – the id of the dataset’s license, see `license_list()` for available values (optional)
*	`notes` (string) – a description of the dataset (optional)
*	`url` (string) – a URL for the dataset’s source (optional)
*	`version` (string, no longer than 100 characters) – (optional)
*	`state `(string) – the current state of the dataset, e.g. `"active"` or `"deleted"`, only active datasets show up in search results and other lists of datasets, this parameter will be ignored if you are not authorized to change the state of the dataset (optional, default: `"active"`)
*	`type` (string) – the type of the dataset (optional), IDatasetForm plugins associate themselves with different dataset types and provide custom dataset handling behaviour for these types
*	`resources` (list of resource dictionaries) – the dataset’s resources, see `resource_create()` for the format of resource dictionaries (optional)
*	`tags` (Array[Strings]) – list of tag dictionaries, see `tag_create()` for the format of tag dictionaries (optional)
*	`extras` (Array[Objects]) – list of dataset extra dictionaries (optional), extras are arbitrary, metadata items that can be added to datasets, each extra dictionary should have keys:
   *	`key` (string)
   *	`value` (string) - e.g.: `deleted`
*	`relationships_as_object` (list of relationship dictionaries) – see `package_relationship_create()` for the format of relationship dictionaries (optional)
*	`relationships_as_subject` (list of relationship dictionaries) – see `package_relationship_create()` for the format of relationship dictionaries (optional)
*	`groups` (list of dictionaries) – the groups to which the dataset belongs (optional), each group dictionary should have one or more of the following keys which identify an existing group: 
    *	`id` (string) - the id of the group
    *	`name` (string) - the name of the group
    *	`title` (string) - the title of the group, to see which groups exist call `group_list()`
*	`owner_org` (string) – the id of the dataset’s owning organization, see `organization_list()` or `organization_list_for_user()` for available values (optional)

##### Javascript

```javascript
<script>
    var client = new CKAN.Client('http://giv-oct.uni-muenster.de:5000', '5df62ec6-5fa7-4e2f-838a-a7d30c6aca39');
    client.action('package_create', {
                name:  'newtestsprova',
                owner_org: 'tests'
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

ckan = ckanapi.RemoteCKAN(remote, apikey)

package = ckan.action.package_create(name='packagetest', owner_org='tests')
```

##### R

```r
library('ckanr')
ckanr_setup(url = "http://giv-oct.uni-muenster.de:5000", key = "5df62ec6-5fa7-4e2f-838a-a7d30c6aca39")
# create a package
(res <- package_create("newpackage", owner_org='tests'))
```
