## GCP sql-proxy

## 在集群内部使用curl
kubectl run -l app=other --image=tutum/curl --restart=Never --rm -i -t test-1


## hello image
image: gcr.io/google-samples/hello-app:1.0

## 进入pod
kubectl exec my-nginx-585fbfd5f4-fpdb4 -i -t -- bash

## nginx绑定default.conf的配置只配置servcer
  server {
    listen 80;
    server_name my-nginx;
    location / {
      proxy_pass http://www.baidu.com;
    }
    location /h1 {
      proxy_pass http://my-web:8080;
    }
  }
	
##  kompose
使用kompose可以将swarm的docker compose转为k8s的yaml

## 访问docker私有仓库，需要经历regcred
kubectl create secret docker-registry regcred --docker-server=<your-registry-server> --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>

## 集群上测试postgresql
kubectl run -l app=other --image=jbergknoff/postgresql-client --restart=Never --rm -i -t test-pg-sql-1 postgresql://test:test@cloudsql-proxy-test-3:5432

## 集群上测试mysql
kubectl run -i --rm --tty mysql-client --image=mysql/mysql-server --restart=Never --command -- /bin/sh
mysql -h(host) -P(port) -u(user) -p(pwd)
