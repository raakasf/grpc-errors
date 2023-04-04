# CPP gRPC

## Instructions

Generate protobuf files:

```sh
    protoc -I ../ --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` ../hello.proto

    protoc -I ../ --cpp_out=. ../hello.proto
```

Compile client and server:

```sh
    g++ -std=c++11 -I/workspace/third_party/centos/grpc_1480/include -pthread  -c -o hello.pb.o hello.pb.cc

    g++ -std=c++11 -I/workspace/third_party/centos/grpc_1480/include -pthread  -c -o hello.grpc.pb.o hello.grpc.pb.cc

    g++ -std=c++11 -I/workspace/third_party/centos/grpc_1480/include -pthread  -c -o client.o client.cpp

    g++ hello.pb.o hello.grpc.pb.o client.o -L/workspace/third_party/centos/grpc_1480/lib64 `pkg-config --libs grpc++ grpc` -lgrpc++_reflection -lprotobuf -lpthread -ldl -o client

    g++ -std=c++11 -I/workspace/third_party/centos/grpc_1480/include -pthread  -c -o server.o server.cpp

    g++ hello.pb.o hello.grpc.pb.o server.o -L/workspace/third_party/centos/grpc_1480/lib64 `pkg-config --libs grpc++ grpc` -lgrpc++_reflection -lprotobuf -lpthread -ldl -o server
```

Run client and server:

```sh
    ./server &
    ./client
```
