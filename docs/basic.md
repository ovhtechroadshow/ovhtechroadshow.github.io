# Podstawowe operacje na maszynie wirtualnej

W tej sekcji uruchomimy nową maszynę wirtualną, zalogujemy się na nią i przeprowadzimy podstawowe operacje.

## 1. Utworzenie instancji z dockerem

W Managerze w sekcji **Compute** w karcie **Instances** należy kliknąć na *Utwórz instancję*.

W wybierz model należy wybrać Discovery **D2-2** - instancja z publicznym IP 1 CPU i 2GB RAM.

Lokalizacja, dowolna.

System operacyjny: **Ubuntu 22.04**

Należy wybrać **klucz SSH** który wcześniej dodaliśmy.

Konfiguracja instancji: w skrypcie poinstalacyjnym należy podać

```
#include https://get.docker.com/
```

Rozliczenie: **godzinowe**

## 2. Logowanie się do nowo utworzonej maszyny wirtualnej

=== "Linux, MacOS"
    Wykorzystamy klient OpenSSH

    ```bash
    ssh -i ~/roadshow-workspace/key ubuntu@${IP}
    ```
    Na pytanie `The authenticity of host can't be established. Are you sure you want to continue connecting` odpowiadamy: `yes` 

=== "Windows"
    Wykorzystamy program `putty.exe`

    W programie putty w sekcji session trzeba podać adres IP.
    ![putty](img/putty_1.png)

    W sekcji Connection -> SSH -> Auth należy podać ścieżkę do pliku z kluczem prywatnym `priv.ppk`.  
    ![putty](img/putty_2.png)

    Na pytanie czy na pewno jest to host do którego chcemy się połączyć odpowiadamy *Accept*.
    ![putty](img/putty_3.png)

    Należy również wpisać na jakiego użytkownika chcemy się zalogować. W naszym przykładzie jest to `ubuntu`.
    ![putty](img/putty_4.png)

## 3. Sprawdzenie parametrów maszyny wirtualnej.  

Żeby sprawdzić podstawowe parametry maszyny wirtualnej użyjemy kilku podstawowych komend.

Aby wyświetlić ilość pamięci RAM:
```
free
```

Aby wyświetlić ilość rdzeni procesora:
```
nproc
```

Aby wyświetlić urządzenia blokowe:
```
lsblk
```

## 4. Dodanie dodatkowego dysku do instancji

Dodatkowy dysk do instancji możemy dodać przez Managera.

W sekcji **Storage** należy wejść w zakładkę **Block storage** i kliknąć na przycisk **Create a volume**

Ze względu na ograniczenia geograficzny należy wybrać tą samą lokalizację jak ta w której znajdują się maszyny wirtualne.

Po utworzeniu należy kliknąć na trzy kropki po prawej stronie i wybrać *Attach to instance*
![putty](img/attach_volume.png)

Po podłączeniu należy jeszcze raz wykonać polecenie `lsblk`.

### Przygotowanie dysku w systemie Linux

Tak dodany dysk jest suroway więc należy na nim utworzyć:

* tablicę partycji:

```
sudo parted -s /dev/sdb mklabel gpt
```

* partycję:

```
sudo parted -s /dev/sdb mkpart data 0% 100%
```

* system plików:

```
sudo mkfs.ext4 /dev/sdb1
```

### Sprawdzenie wydajności dysku

Należy zainstalować oprogramowanie fio

```
sudo apt update
sudo apt -y install fio
```

Przejście do katalogu `/mnt`
```
cd /mnt
```
Uruchomienie krótkiego testu fio:
```
sudo fio --name=test --bs=4k --ioengine=libaio --iodepth=4 --size=1g --direct=1 --runtime=30
```

### Uruchomienie kontenera docker z nginx

Aby uruchomić kontener z serwerem nginx i opublikować go na porcie 80 należy wykonać komendę:

```
sudo docker run -d -p 80:80 --name nginx nginx:latest
```

Po zakończeniu ćwiczeń z tego rozdziału można przejść do kolejnego.
