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
	
  
