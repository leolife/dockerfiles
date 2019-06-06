ARG GO_VERSION=1.12.5

FROM golang:${GO_VERSION}-alpine as builder

ENV V2RAY_VERSION=v4.19.1
ENV CGO_ENABLED=0

RUN apk add --no-cache ca-certificates git tzdata

RUN git clone https://github.com/v2ray/v2ray-core.git /src

WORKDIR /src

RUN git checkout tags/${V2RAY_VERSION}

RUN go mod download

RUN go build -o /app/v2ray ./main
RUN go build -o /app/v2ctl ./infra/control/main

COPY config.json /app

FROM scratch as final

COPY --from=builder /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

COPY --from=builder /app /app

EXPOSE 8000

CMD [ "/app/v2ray", "-config=/app/config.json" ]
