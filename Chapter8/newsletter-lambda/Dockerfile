FROM amazon/aws-lambda-go as build

RUN yum install -y golang
RUN go env -w GOPROXY=direct

COPY go.mod ./
COPY go.sum ./

RUN go mod download

COPY *.go ./

RUN go build -o /main

FROM amazon/aws-lambda-go
COPY --from=build /main /var/task/main

CMD [ "main" ]