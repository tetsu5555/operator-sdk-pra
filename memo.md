## refs
- https://sdk.operatorframework.io/docs/building-operators/golang/quickstart/

## command

```
mkdir memcached-operator
cd memcached-operator
operator-sdk init --domain=example.com --repo=github.com/example-inc/memcached-operator
operator-sdk create api --group cache --version v1 --kind Memcached --resource=true --controller=true\n

make docker-build docker-push IMG=tetete1118/oprator-sdk-pra:hoge

make install

make deploy IMG=tetete1118/oprator-sdk-pra:hoge
```

```
~/hoge/memcached-operator % make install

/Users/tetsuo.yamamoto/hoge/memcached-operator/bin/controller-gen "crd:trivialVersions=true,preserveUnknownFields=false" rbac:roleName=manager-role webhook paths="./..." output:crd:artifacts:config=config/crd/bases
go: creating new go.mod: module tmp
Downloading sigs.k8s.io/kustomize/kustomize/v3@v3.8.7
go: downloading sigs.k8s.io/kustomize/kustomize/v3 v3.8.7
go: downloading sigs.k8s.io/kustomize/api v0.6.5
go: downloading sigs.k8s.io/kustomize/cmd/config v0.8.5
go: downloading k8s.io/client-go v0.18.10
go: downloading sigs.k8s.io/kustomize/kyaml v0.9.4
go: downloading k8s.io/apimachinery v0.18.10
go: downloading github.com/monochromegane/go-gitignore v0.0.0-20200626010858-205db1a8cc00
go: downloading github.com/go-openapi/validate v0.19.8
go: downloading github.com/xlab/treeprint v0.0.0-20181112141820-a009c3971eca
go: downloading github.com/go-errors/errors v1.0.1
go: downloading github.com/go-openapi/strfmt v0.19.5
go: downloading sigs.k8s.io/structured-merge-diff v0.0.0-20190525122527-15d366b2352e
go: downloading github.com/go-openapi/spec v0.19.5
go: downloading github.com/google/shlex v0.0.0-20191202100458-e7afc7fbc510
go: downloading k8s.io/kube-openapi v0.0.0-20200410145947-61e04a5be9a6
go: downloading go.starlark.net v0.0.0-20200306205701-8dd3e2ee1dd5
go: downloading github.com/yujunz/go-getter v1.4.1-lite
go: downloading github.com/qri-io/starlib v0.4.2-0.20200213133954-ff2e8cd5ef8d
go: downloading go.mongodb.org/mongo-driver v1.1.2
go: downloading github.com/go-openapi/errors v0.19.2
go: downloading github.com/hashicorp/go-version v1.1.0
go: downloading github.com/mitchellh/go-homedir v1.1.0
go: downloading github.com/bgentry/go-netrc v0.0.0-20140422174119-9fd32a8b3d3d
go: downloading github.com/hashicorp/go-multierror v1.1.0
go: downloading github.com/mitchellh/go-testing-interface v1.0.0
go: downloading github.com/asaskevich/govalidator v0.0.0-20190424111038-f61b66f89f4a
go: downloading k8s.io/api v0.18.10
go: downloading github.com/go-openapi/jsonpointer v0.19.3
go: downloading github.com/go-openapi/swag v0.19.5
go: downloading github.com/go-openapi/runtime v0.19.4
go: downloading github.com/go-openapi/jsonreference v0.19.3
go: downloading github.com/googleapis/gnostic v0.1.0
go: downloading github.com/mailru/easyjson v0.7.0
go: downloading github.com/ulikunitz/xz v0.5.5
go: downloading github.com/go-openapi/analysis v0.19.5
go: downloading github.com/hashicorp/go-cleanhttp v0.5.0
go: downloading github.com/mattn/go-runewidth v0.0.7
go: downloading github.com/go-stack/stack v1.8.0
go: downloading github.com/go-openapi/loads v0.19.4
go: downloading github.com/PuerkitoBio/purell v1.1.1
go: downloading github.com/gophercloud/gophercloud v0.1.0
go: downloading cloud.google.com/go v0.38.0
go: downloading golang.org/x/net v0.0.0-20200625001655-4c5254603344
go: downloading github.com/Azure/go-autorest/autorest v0.9.0
go: downloading github.com/emicklei/go-restful v0.0.0-20170410110728-ff4f55a20633
go: downloading golang.org/x/sys v0.0.0-20200323222414-85ca7c5b95cd
go: downloading github.com/mitchellh/mapstructure v1.1.2
go: downloading github.com/Azure/go-autorest/autorest/adal v0.5.0
go: downloading github.com/hashicorp/go-safetemp v1.0.0
go: downloading github.com/PuerkitoBio/urlesc v0.0.0-20170810143723-de5bf2ad4578
go: downloading github.com/Azure/go-autorest/autorest/date v0.1.0
/Users/tetsuo.yamamoto/hoge/memcached-operator/bin/kustomize build config/crd | kubectl apply -f -
customresourcedefinition.apiextensions.k8s.io/memcacheds.cache.example.com created
```

```
~/hoge/memcached-operator % make deploy IMG=tetete1118/oprator-sdk-pra:hoge
/Users/tetsuo.yamamoto/hoge/memcached-operator/bin/controller-gen "crd:trivialVersions=true,preserveUnknownFields=false" rbac:roleName=manager-role webhook paths="./..." output:crd:artifacts:config=config/crd/bases
cd config/manager && /Users/tetsuo.yamamoto/hoge/memcached-operator/bin/kustomize edit set image controller=tetete1118/oprator-sdk-pra:hoge
/Users/tetsuo.yamamoto/hoge/memcached-operator/bin/kustomize build config/default | kubectl apply -f -
namespace/memcached-operator-system created
customresourcedefinition.apiextensions.k8s.io/memcacheds.cache.example.com configured
role.rbac.authorization.k8s.io/memcached-operator-leader-election-role created
clusterrole.rbac.authorization.k8s.io/memcached-operator-manager-role created
clusterrole.rbac.authorization.k8s.io/memcached-operator-metrics-reader created
clusterrole.rbac.authorization.k8s.io/memcached-operator-proxy-role created
rolebinding.rbac.authorization.k8s.io/memcached-operator-leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/memcached-operator-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/memcached-operator-proxy-rolebinding created
configmap/memcached-operator-manager-config created
service/memcached-operator-controller-manager-metrics-service created
deployment.apps/memcached-operator-controller-manager created
```