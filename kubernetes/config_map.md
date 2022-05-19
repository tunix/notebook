# Config Map
## Storing files inside ConfigMap
It's possible to store binary or text files inside a ConfigMap. Binary files are usually encoded in base64 while text files are stored directly inside the markdown as they're.

It's also possible to store multiple files inside a single ConfigMap.

```
$ kubectx awesome-env

$ kubectl create \
    -n my-namespace \
    configmap my-certs \
    --from-file ~/Downloads/truststore.jks \
    --from-file ~/Downloads/certs.pem
```

