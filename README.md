# Алгоритм

![image](https://github.com/YuliyaNemchaninova/Order/assets/47818848/2532e0fb-c5de-46a2-856a-aae4518e5a81)


# **Установка**

# Часть 0 Запуск minikube

minikube start

minikube addons enable ingress

minikube ip

Прописать <ip> arch.homework в системном файле etc/hosts

# Часть 1 Запуск **PosgtreSQL**

cd <путь в папку>\minikube deployment\postgresql

helm repo update

kubectl apply -f local-pv.yaml -f pv-claim.yaml

helm install postgresql-dev -f values.yaml bitnami/postgresql

# Часть 2 У**становить сервисы**

**inventory-сервис**

cd <путь в папку>\minikube deployment\inventory-deployment

kubectl apply -f inventory-config-map.yaml -f inventory-secret.yaml -f dp.yaml -f service.yaml

**billing-сервис**

cd <путь в папку>\minikube deployment\billing-deployment

kubectl apply -f billing-config-map.yaml -f billing-secret.yaml -f dp.yaml -f service.yaml

**order-сервис**

cd <путь в папку>\minikube deployment\order-deployment

kubectl apply -f order-config-map.yaml -f order-secret.yaml -f dp.yaml -f service.yaml

kubectl apply -f ingress.yaml

# Часть 3 Тестирование

В другом окне Командной строки

minikube tunnel

Выполнить тесты

newman run API Order.postman_collection.json --env-var "url=http://arch.homework” --env-var "inventoryUrl=http://arch.homework” --env-var "billingUrl=http://arch.homework”

Результат тестирования

![image](https://github.com/YuliyaNemchaninova/Order/assets/47818848/b45a87f8-ae6e-4a11-b739-ad9e1bb72b4e)

