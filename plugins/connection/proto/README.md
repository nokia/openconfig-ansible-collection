# OpenConfig proto files

---

Contains OpenConfig *.proto files extracted on November 4th, 2025 (gNMI v0.14.1) from 

Compilation:
```shell
pip install grpcio grpcio-tools protobuf
python -m grpc_tools.protoc -I . --python_out=../pb --grpc_python_out=../pb *.proto
 ```

> **NOTE**:
> Import paths have been updated to simplify compilation.