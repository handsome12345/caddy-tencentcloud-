# caddy-tencentcloud-
caddy-tencentcloud 

caddy整合tencentcloud插件

创建 Dockerfile 文件名为dockerfile

# 第一阶段：构建自定义 Caddy
FROM caddy:builder AS builder

# 设置国内 Go 模块代理，加速依赖下载
ENV GOPROXY=https://goproxy.cn,direct
# 阿里云：https://mirrors.aliyun.com/goproxy/
# 七牛云：https://goproxy.cn（即当前使用的）
# 腾讯云：https://mirrors.tencentyun.com/go

# 编译包含腾讯云 DNS 插件的 Caddy
RUN xcaddy build \
    --with github.com/caddy-dns/tencentcloud

# 第二阶段：生成最终镜像
FROM caddy:latest
COPY --from=builder /usr/bin/caddy /usr/bin/caddy

docker pull ccr.ccs.tencentyun.com/handsome1234/caddy-tencentcloud:v202610031838

docker pull crpi-igxq9o2ogrm2v070.cn-zhangjiakou.personal.cr.aliyuncs.com/handsome1234/handsome1234:v202610031950
