# Electrum Personal Server

{% hint style="info" %}
Tijd: 30 minuten
{% endhint %}

Als je de wallet software van [Electrum](https://electrum.org/#home) gebruikt is het een logische stap om ervoor te zorgen dat Electrum babbelt met je eigen node. Dit kan niet rechtstreeks maar moet verlopen via een Electrum Server. De Electrum wallet software connect namelijk normaal gesproken met Electrum Servers waarvan je niet weet wie die in de gaten houd. De wallet houdt namelijk de adressen in de gaten waar je Bitcoin op hebt ontvangen heb en zo kunnen verschillende adressen terug te herleiden zijn naar jouw IP. Dat wil je natuurlijk niet. De oplossing: draai je eigen Electrum Server. Er zijn verschillende forks beschikbaar zoals ElectrumX en Electrum Personal Server. Dit document beschrijft de installatie van [Electrum Personal Server](https://github.com/chris-belcher/electrum-personal-server).


## Voorbereidingen
SSH in je Pi en voer het installatie commando uit voor de nodige tools.

```bash
sudo apt install -y python3 python3-pip
sudo pip3 install setuptools
```

Check dat er in bitcoin.conf een regel staat disablewallet = 0.

```bash
sudo nano /home/bitcoin/.bitcoin/bitcoin.conf
```

Als dat nog niet het geval is voeg je deze toe, sla je het bestand op (met Ctrl-X) en herstart je de bitcoind service.

```bash
sudo systemctl restart bitcoind
```

## Installatie
Nu kunnen we verder gaan met het downloaden van de source en het installeren van Electrum Personal Server.

```bash
mkdir .eps
cd .eps
```

Download vanaf de Github de [nieuwste release](https://github.com/chris-belcher/electrum-personal-server/releases) van Electrum Personal Server. Kopiëer de link van Source code (tar.gz), pak deze uit en gooi de download weg.

```bash
wget https://github.com/chris-belcher/electrum-personal-server/archive/eps-v0.2.1.1.tar.gz
tar -xvf eps-v0.2.1.1.tar.gz
rm eps-v0.2.1.1.tar.gz

```

Maak een kopie van het configuratie bestand en pas deze aan.

```bash
cp electrum-personal-server-eps-v0.2.0/config.ini_sample config.cfg
nano config.cfg
```
Deze config-file bevat veel commentaar en tips wat je waar moet invullen. Kijk in ieder geval even naar de volgende secties:

[master-public-keys] — zoek in Electrum je master public key op via het menu Wallet > Information
[bitcoin-rpc] — kies voor de methode rpcuser en rpcpassword deze kun je opzoeken in je bitcoin.conf bestand
[electrum-server] — kies hier voor 0.0.0.0 ipv 127.0.0.1

let bij het laatste commando in onderstaand blokje op de punt (.) aan het einde van de regel

```bash
cd electrum-personal-server-eps-v0.2.0
pip3 install wheel
pip3 install use .
```

## Opstarten
Electrum Personal Server is nu geïnstalleerd (in ~/.local/bin) en klaar om voor het eerst te worden gestart. Deze roep je aan door ook het pad naar de config-file mee te geven. Dit kan ~10 minuten duren. Daarna zal het programma stoppen.

```bash
~/.local/bin/electrum-personal-server ~/.eps/config.cfg
```

Nu moeten EPS de blockchain van scannen op zoek naar adressen en transacties horend bij de public keys die je in de config-file hebt opgenomen. Als er wordt gevraagd naar de startdatum is het handig als je de datum opgeeft van de eerste transactie naar een adres horend bij die wallet.

```bash
~/.local/bin/electrum-personal-server-rescan ~/.eps/electrum-personal-server/config.cfg
```

Je kunt de voorgang monitoren door de log-file van bitcoin in de gaten te houden via een tweede Putty venster:

```bash
sudo tail -f -n 200 /home/bitcoin/.bitcoin/bitcoin/debug.log
```
Als deze klaar is start je EPS nog een keer

```bash
~/.local/bin/electrum-personal-server ~/.eps/electrum-personal-server/config.cfg
```

## Automatisering
Nu moeten we alleen nog zorgen de EPS als een Service gaat draaien. Je hebt als het goed is twee vensters open. Eentje met de output van de bitcoin log en eentje waarin EPS draait.

```bash
sudo nano /etc/systemd/system/eps.service
```

[Unit]
Description=Electrum Personal Server
After=bitcoind.service

[Service]
ExecStart=/usr/bin/python3 /home/pi/.local/bin/electrum-personal-server /home/pi/.eps/config.cfg
User=pi
Group=pi
Type=simple
KillMode=process
TimeoutSec=60
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target

Sluit het bestand af en sla de wijzigingen op. Vervolgens de service inschakelen en starten.

sudo systemctl enable eps.service
sudo systemctl start eps.service

Je kunt de voortgang van het opstarten van EPS volgen door het log-bestand te bekijken:

```bash
sudo tail -f -n 200 /tmp/electrumpersonalserver.log
```

## Electrum Wallet
Start nu Electrum Wallet op je PC met "C:\Program Files (x86)\Electrum\electrum-4.0.5.exe" --server 192.168.2.1:50002:s --oneserver
Kies in het Tools-menu voor Network
Open de Server-tab
Haal het vinkje weg bij “select server automatically”
Vul bij server het IP-adres in van je RPi4
Klik op Close

Als alles goed is gegaan heb je rechtsonder in het venster van Electrum een groene cirkel die aangeeft verbonden te zijn. Je kunt ook nog

Kies in het View-menu voor Show Console
Klik op de Console tab

Hier zie je nu dat je bent verbonden met een EPS en jouw Bitcoin Node!
