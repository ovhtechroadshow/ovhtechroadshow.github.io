# NAS-HA

## Jak podłączyć wolumen NAS-HA

### Linux

Zainstaluj klienta NFS:
```code
sudo apt-get install nfs-common
```

Utwórz nowy katalog:
```code
sudo mkdir /media/NasHA
```

Zamontuj wolumen serwera plików:
```code
sudo mount -t nfs -o _netdev,mountproto=tcp 10.201.27.176:zpool-128495/RoadShow /media/NasHA
```

### Windows

Uruchom PowerShell albo konsolę i wykonaj komendę:

```code
net use z: \\10.201.27.176\zpool-128495_RoadShow
```