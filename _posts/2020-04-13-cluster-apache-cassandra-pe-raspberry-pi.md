---
layout: post
title: Cluster Apache Cassandra pe Raspberry PI & C.H.I.P.
categories: [Apache,Cassandra,Linux,Raspberry PI,C.H.I.P.,Cluster,DataStax]
excerpt: Apache Cassandra este un sistem distribuit de baze de date, de tip NoSQL. E folosit de multe companii importante în proiecte complexe, ce prelucrează volume mari de date. Printre firmele și organizațiile ce folosesc Apache Cassandra se numără CERN, GitHub, Instagram, Netflix și Reddit.
---

Apache Cassandra este un sistem distribuit de baze de date, de tip NoSQL. E folosit de multe companii importante în proiecte complexe, ce prelucrează volume mari de date. Printre firmele și organizațiile ce folosesc Apache Cassandra se numără CERN, GitHub, Instagram, Netflix și Reddit.

Acum câteva luni am început să parcurg cursurile de Apache Cassandra, oferite gratuit de către [DataStax](https://academy.datastax.com). Bineînțeles că au această platformă cu acces gratuit pentru a-și promova produsele enterprise. Totuși, cursurile sunt bine făcute, iar exercițiile chiar au sens.

La începutul cursului, am primit imaginea unei mașini virtuale Ubuntu, care conține tot ce trebuie pentru a experimenta cu unul, două sau trei noduri Apache Cassandra. Fiind un sistem distribuit de baze de date, nu are sens să pornești doar o instanță de Apache Cassandra.

Parcurgând exercițiile, devenea din ce în ce mai frustrant să lucrez cu acea mașină virtuală. O instalasem pe un VirtualBox și am observat că programul ăsta e un mare consumator de energie. Procesorul se încinge, ventilatoarele laptopului turează la maximum, iar bateria se duce mai repede decât ar trebui. În plus, nu simțeam că trăiesc cu adevărat experiența faptului că lucrez cu baze de date distribuite, de vreme ce toate cele trei noduri erau instalate pe aceeași mașină.

## Despre dispozitivele mici și Apache Cassandra

Așa mi-a venit ideea să folosesc trei dispozitive de tip SoC (*System on Chip*) pentru a-mi construi un cluster Apache Cassandra. Aveam deja două plăcuțe [*Raspberry PI*](https://www.raspberrypi.org) și o plăcuță [*C.H.I.P.*](http://www.chip-community.org/index.php/Main_Page) și m-am gândit că e timpul să le dau o utilitate.

Înainte de a mă apuca de lucru am făcut un pic de *research* despre cum să instalez Apache Cassandra pe Raspberry PI, iar rezultatele m-au cam dezamăgit. Am găsit foarte puține materiale, care nu erau deloc convingătoare.

Toate resursele pe care le-am găsit pentru combinația Raspberry PI + Apache Cassandra prezentau configurații complexe, cu pași mulți și greu de urmărit. Totuși, mi-am zis, sigur n-are cum să fie atât de complicat. Așa că am renunțat să mai caut articole specifice pentru *setup*-ul ăsta și m-am concentrat pe articole ce descriu cum se instalează Apache Cassandra pe mai multe mașini, pentru a forma un cluster.

Totuși, dintre resursele pe care le-am găsisem, mi s-a părut plină de inspirație prezentarea lui [Andy Cobley](https://www.youtube.com/watch?v=OW-OFv-Pq2Y), lector la Universitatea din Dundee. Chiar dacă e o prezentare veche, mi-a plăcut să urmăresc experiența lui cu Raspberry PI și Apache Cassandra.

Una dintre ideile ce mi-au atras atenția în prezentarea lui Andy a fost aceea că Raspberry PI e un [mini-computer](https://opensource.com/resources/raspberry-pi) construit inițial în [scop educativ](https://www.youtube.com/watch?v=IWif9eBJCIA). Așa că nu ar trebui să mă aștept să construiesc cu astfel de computere un cluster gata să fie pus în producție. Ar trebui să îl folosesc pentru a învăța să modelez și să operez baze de date distribuite, chiar dacă nu obțin performanță. Lucrul acesta mi-a dat încredere.

După ce am renunțat să mai caut articole specifice despre instalarea pe Raspberry PI, am fost foarte bucuros să dau peste articolul lui [James Farrell](https://opensource.com/article/19/8/how-set-apache-cassandra-cluster), în care arată cum se configurează un cluster simplu Apache Cassandra.

## IP-uri statice pentru dispozitive

Înainte de a configura clusterul Apache Cassandra, a fost nevoie câțiva pași preliminari. În primul rând, mi-am dat seama că trebuie să asignez fiecărui dispozitiv câte un IP static, pentru a le putea folosi mai apoi în fișierele de configurație.

Bineînțeles, în primul rând trebuie să avem conectivitate cu dispozitivele. Eu am ales să mă conectez *wireless* la acestea. Tot ce trebuie  să facem e să edităm fișierul `/etc/wpa_supplicant/wpa_supplicant.conf`, cu următoarele detalii:

```bash
country=RO
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
scan_ssid=1
ssid="your_ssid"
psk="your_password"
}
```

Pentru o primă conectare la Raspberry PI, am găsit informații foarte ușor de urmărit pe site-ul [Tom's Hardware](https://www.tomshardware.com/reviews/raspberry-pi-headless-setup-how-to,6028.html).

La plăcuța C.H.I.P. m-am conectat inițial prin [interfața serială](http://chip.jfpossibilities.com/docs/chip.html#control-chip-using-a-serial-terminal), având o conexiune USB prin cablu.

O dată ce dispozitivele s-au conectat la rețeaua wireless locală, le-am putut accesa prin *SSH*. Înainte să le asignez IP-uri statice a trebuit să le identific cumva IP-urile, dar asta nu a fost prea greu, neavând prea multe dispozitive conectate la rețea.

Pentru cele două plăcuțe Raspbery PI am folosit pașii prezentați în video-ul lui [Miguel de la AvoidErrors.net](https://www.youtube.com/watch?v=D1eD60_jhKI) și totul a mers bine.

Totuși, pentru plăcuța C.H.I.P., lucrurile nu au mers atât de bine. Deși toate indicațiile erau că, pentru Debian 8 (Jessie), trebuie editat fișierul `/etc/dhcpcd.conf` cu un conținut de genul,

```
interface wlan0
static ip_address=192.168.1.102/24
static routers=192.168.1.1
static domain_name_servers=8.8.8.8 8.8.4.4
```

nu a funcționat.

Am recurs la metoda ce era valabilă înainte de Debian 8, modificând fișierul `/etc/network/interfaces`:

```
auto lo
iface lo inet loopback

allow-hotplug wlan0
iface wlan0 inet manual
    wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

allow-hotplug wlan0

iface wlan0 inet static
    address 192.168.1.102
    netmask 255.255.255.0
    network 192.168.1.1
    gateway 192.168.1.1
    wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

dns-nameservers 8.8.8.8 8.8.4.4
```

Nici de data asta nu a mers. Dar apoi mi-am amintit că, mai demult, configurasem accesul la WiFi cu ajutorul unui tool numit [nmtui](http://www.chip-community.org/index.php/Turn_it_on#Configuring_WiFi).

Așa că am incercat să dezactivez acel *Network Manager*:

```
sudo systemctl stop NetworkManager.service

sudo systemctl disable NetworkManager.service
```

După toți pașii ăștia și câteva reboot-uri, a mers. Nu știu exact dacă e activă configurația din `/etc/dhcpcd.conf` sau cea din `/etc/network/interfaces`, dar nu mai contează. Mă bucur că am deblocat situația și am asignat plăcuței un IP static.

Apropo, pentru toată povestea asta cu asignarea IP-ului static pentru C.H.I.P., am folosit resursele următoare:

	- https://raspberrypi.stackexchange.com/questions/39785/differences-between-etc-dhcpcd-conf-and-etc-network-interfaces
	- https://unix.stackexchange.com/questions/319488/network-configuration-for-static-ip-and-automatic-wifi-connection
	- https://linuxconfig.org/how-to-setup-a-static-ip-address-on-debian-linux
		- stop and disable NetworkManager
			- configured using the nmtui command
			- configuration profiles stored at /etc/NetworkManager/system-connections/

## Pachete software necesare

Se pare că Apache Cassandra are nevoie de Java 8 și Python 2.7.

Python era deja pre-instalat atât pe Raspberry PI, cât și pe C.H.I.P.

Pentru instalarea unui JDK de Java 8, am rulat [următoarele comenzi](https://linuxize.com/post/install-java-on-raspberry-pi/):

```
sudo apt update
sudo apt install openjdk-8-jdk
```

Apoi, am verificat că executabilul de Java e în *path*, executând comanda `java -version`.

## Clusterul Apache Cassandra

Ultimul pas a fost instalarea pachetului Apache Cassandra pe fiecare dintre mașini și configurarea clusterului.
Pentru aceasta, am urmat pas cu pas ghidul lui [James Farrell](https://opensource.com/article/19/8/how-set-apache-cassandra-cluster), menționat și mai sus.

Cam ăsta a fost începutul poveștii clusterului meu Apache Cassandra. De-acum, pot face experimente mai concludente cu diverse configurații, iar învățarea mi se pare mult mai plăcută și interesantă.
