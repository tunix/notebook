# Forcing ES to have zero replicas

On environments like dev/test, we may want to have no replicas and to have cluster in green state. To achieve this, we
first need to set the `number_of_replicas` to 0:

```
PUT /_all/_settings
{
    "index" : {
        "number_of_replicas" : 0
    }
}
```

This will do for all **existing** indices. For this to affect new indices, we should also create a template with
highest order:

```
PUT _template/force_zero_replicas_template
{
   "index_patterns" : ["*"],
   "order" : 1,
   "settings" : {
       "number_of_replicas" : "0"
   }
}
```
