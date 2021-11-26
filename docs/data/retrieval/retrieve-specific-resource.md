## Retrieving a specific resource

This snippet is useful to retrieve a specific resource from our ckan instance.

```javascript
//var uri = "YOUR CKAN URI"
var uri = "http://giv-oct.uni-muenster.de:5000";
//var id = "YOUR RESOURCE ID"
var id = "abc-ancientwoods";

$.ajax({
  url: uri+"/api/3/action/package_show?id="+id,
  dataType:"json",
  async:true,
  success: function(json){
    console.log(json);
    //PARSE JSON    
  }
});
```