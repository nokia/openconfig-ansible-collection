# OpenConfig proto files

---

Contains OpenConfig *.proto files extracted on November 4th, 2025 (gNMI v0.14.1) from 

Compilation:
```shell
pip install grpcio grpcio-tools protobuf
python -m grpc_tools.protoc -I . --python_out=. --grpc_python_out=. *.proto
sed -i '' 's/^import \(.*_pb2\)/from ansible_collections.nokia.openconfig.plugins.utils import \1/' *
sed -i 's/^import \(.*_pb2\)/from ansible_collections.nokia.openconfig.plugins.utils import \1/' *
```

> **NOTE**:
> Import paths have been updated to simplify compilation.