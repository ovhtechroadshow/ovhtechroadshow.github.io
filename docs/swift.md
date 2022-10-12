# Swift

## 1. Utworzenie publicznego bucketu/kontenera S3 o nazwie demo-container w panelu OVHcloud
![container creation](img/container.png)

## 2. Wysłanie pliku
1. Tworzymy plik file.txt z tekstem `hello world` w folderze roadshow-workspace
1. Wysyłamy plik do stworzonego kontenera przy pomocy panelu OVHcloud
![send file](img/send_file.png)
1. Sprawdzamy czy plik istnieje w danym kontenerze w przeglądarce.
!!! note
    Plik będzie dostępny pod adresem który ma strukturę: `<endpoint>/file.txt`
![endpoint](img/endpoint.png)

## 3. Pobranie pliku
Używamy tego samego adresu URL do ściągnięcia pliku na instancję

```code
curl <endpoint>/file.txt > ~/file.txt
```

```code
cat ~/file.txt
```

## 4. Połączenie do bucketu z poziomu klienta
1. Pobieramy i instalujemy klienta MinIO: [https://min.io/docs/minio/linux/reference/minio-mc.html#install-mc](https://min.io/docs/minio/linux/reference/minio-mc.html#install-mc)
1. Tworzymy użytkownika S3 w panelu OVHcloud
1. Konfiurujemy klienta tak, żeby był połączony do naszego Object Storage.
   ```code
   mc alias set demo <endpoint> <accessKey> <secretKey>
   ```
1. Listujemy istniejące buckety
    ```code
    mc ls demo
    ```
1. Listujemy obiekty z kontenera/bucketu
    ```code
    mc ls demo/demo-container
    ```
1. Pobieramy obiekt z kontenera
    ```code
    mc cp demo/demo-container/file.txt ~/
    ```
    ```code
    cat ~/file.txt
    ```
