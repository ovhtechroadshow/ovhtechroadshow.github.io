# Managed Kubernetes Service

1. Uruchomienie małego klastra Kubernetes (3 węzły)
1. Instalacja narzędzia kubectl -
   [instrukcja](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
1. Stworzenie połączenia z klastrem
    1. Pobranie pliku kubeconfig z panelu OVH
    ![download kubeconfig](img/kubeconfig.png)
    1. Skopiowanie pliku do instancji
    ```code
    scp -i ~/roadshow-workspace/key kubeconfig.yml ubuntu@<public_ip>:~/
    ```
    1. Użycie konfiguracji do połączenia
    ```code
    export KUBECONFIG=~/kubeconfig.yml
    ```
1. Listowanie węzłów klastra:
```code
kubectl get nodes
```
1. Stworzenie POD'a z obrazem serwera Nginx
```code
kubectl expose pod demo-nginx --type=LoadBalancer
```
1. Wylistowanie serwisu LoadBalancer stworzonego dla naszego POD'a
```code
kubectl get service demo-nginx
```
1. Sprawdzenie z przeglądarki adresu IP load balancera
