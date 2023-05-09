Partially updating a secret:

```
$ kubectl -n my-namespace patch secret my-secret -p '{"data": {"key_to_update": "base64_encoded_string"}}'
```
