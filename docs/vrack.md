# vRack

## 1. Utworzenie sieci vRack

W Managerze w sekcji Network klikamy na Private Network.

Pokaże się informacja, że projekt Public Cloud nie ma utworzonych jeszcze żadnych sieci vRack, więc tworzymy nową sieć klikając na przycisk **Create vRack** i potwierdzając operację w okienku popup.

## 2. Dodanie nowej sieci vRack

Po utworzeniu nowej sieci vRack należy dodajemy nową sieć prywatną. W tym celu klikamy na przycisk **Add Private Network**.

Address distribution: ustawić jako DHCP.

Region: najlepiej wybrać wszystkie.

Nazwa: dowolna.

## 3. Dodanie sieci prywatnej do VMki

W sekcji Compute klikamy na Instances.

Następnie klikamy w nazwę instancji którą chcemy edytować.

Po prawej stronie w kolumnie *Network* w sekcji **Private networks** pod przyciskiem z trzema kropkami wybieramy **Attach a network**.

![add private network](img/add_private_network.png)

## 4. Podniesienie interfejsu vRack

Aby zobaczyć wszystkie interfejsy sieciowe na VMce wykonujemy polecenie:

```
ip link
```

Aby podnieść interfejs vRack i uzyskać na nim adres IP przez DHCP:

```
sudo dhclient ens7
```

Aby zmiany zostały zachowane po restarcie można je dodać do konfiguracji sieciowej w `/etc/netplan/`.
