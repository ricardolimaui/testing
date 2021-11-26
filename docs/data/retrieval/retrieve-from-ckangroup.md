## Retrieving all resources from a group

This snippet is useful to retrieve all resources belonging to one of four groups of the ckan instance: 

* `data`
* `service`
* `app`
* `guideline`

```javascript
//var uri = "YOUR CKAN URI"
var uri = "http://giv-oct.uni-muenster.de:5000";
//var id = "YOUR GROUP ID"
var id = "apps";

$.ajax({
  url: uri+"/api/3/action/package_search?q=groups:"+id+"&rows=3000",
  dataType:"json",
  async:true,
  success: function(json){
    console.log(json);
    //PARSE JSON    
  }
});
```