## refs
- https://sdk.operatorframework.io/docs/building-operators/golang/quickstart/

## command

```
mkdir memcached-operator
cd memcached-operator
operator-sdk init --domain=example.com --repo=github.com/example-inc/memcached-operator
operator-sdk create api --group cache --version v1 --kind Memcached --resource=true --controller=true\n
```