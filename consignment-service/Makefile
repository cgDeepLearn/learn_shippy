build:
	# 命令以tab开头
	protoc -I. --go_out=$(GOPATH)/src/learn_shippy/consignment-service proto/consignment/consignment.proto --micro_out=$(GOPATH)/src/learn_shippy/consignment-service
	# 告知 Go 编译器生成二进制文件的目标环境：amd64 CPU 的 Linux 系统
	GOOS=linux GOARCH=amd64 go build
    # 根据当前目录下的 Dockerfile 生成名为 consignment-service 的镜像
    # 需手动指定 GOOS 和 GOARCH 的值，否则在 macOS 上编译出的文件是无法在 alpine 容器中运行的。
	docker build -t consignment-service .

run:
	docker run -p 50051:50051 \
	 -e MICRO_SERVER_ADDRESS=:50051 \
	 -e MICRO_REGISTRY=mdns \
	 consignment-service