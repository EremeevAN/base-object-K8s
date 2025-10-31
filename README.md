### Домашнее задание к занятию «Базовые объекты K8S»
### Задание 1. Создать Pod с именем hello-world
Создаем pod с именем hello-world
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world
spec:
  containers:
  - name: hello-world
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```
выполняем команду: microk8s kubectl port-forward pods/hello-world 8080:8080. Результат:

![image](https://github.com/EremeevAN/base-object-K8s/blob/main/images/1.png)

### Задание 2. Создать Service и подключить его к Pod

Создаем pod с именем netology-web
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: netology-web
  labels:
    app: netology-web
spec:
  containers:
  - name: netology-web
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```

Создаем Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: netology-svc
spec:
  selector:
    app: netology-web
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
```

выполняем команду: microk8s kubectl port-forward services/netology-svc 3000:8080. Результат:

![image](https://github.com/EremeevAN/base-object-K8s/blob/main/images/2.png)