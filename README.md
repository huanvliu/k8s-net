## GCP sql-proxy

## 在集群内部使用curl
kubectl run -l app=other --image=tutum/curl --restart=Never --rm -i -t test-1


## hello image
image: gcr.io/google-samples/hello-app:1.0

##internal loadbalancer
apiVersion: v1
kind: Service
metadata:
  name: test
  annotations:
    cloud.google.com/load-balancer-type: "Internal"
  labels:
    app: test-app
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 8080
      protocol: TCP
      name: http
  selector:
    app: test-app
