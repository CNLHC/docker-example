FROM golang:alpine
RUN go version
# RUN echo 'export GO111MODULE=on' >> .bashrc
ENV GO111MODULE=on
RUN go env -w GOPROXY=https://goproxy.cn,direct
RUN go get golang.org/x/tour
RUN mkdir -p $GOPATH/src/golang.org/x/
RUN cp -r $GOPATH/pkg/mod/golang.org/x/tour* $GOPATH/src/golang.org/x/tour
CMD tour -http www.cnworkshop.xyz:20101

