# mico-client
Python 3 resolver for [go-micro](https://github.com/micro/go-micro) grpc
services.

## Examples

### Etcd
```python
    from micro_client.registry.etcdregistry import etcd, Registry
    from micro_client.common import Services

    s = Services(Registry(etcd.Client(port=2379), '/micro-registry'))
```


### Consul
```python
    import requests

    from micro_client.registry.consulregistry import Registry
    from micro_client.common import Services

    s = Services('http://127.0.0.1:8500/v1', session=requests.Session()))
```


### Use it!
```python
    service = s.resolve('some')
    print(service.connection_info)

    # Import the stub and grpc structures for use
    import grpc
    from some_pb2_grpc import SomeStub
    from some_pb2 import Input, Structures
    
    # Get the stub
    stub = services.insecure('some', SomeStub)
    # Call it
    result = stub.SomeCall(Input(Data=1), Structures(Some="data", ID=1))
```
