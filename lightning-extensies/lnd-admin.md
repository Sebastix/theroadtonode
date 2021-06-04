# LND Admin

{% hint style="info" %}
Tijd: 10 minuten
{% endhint %}

Een tool afkomstig van dezelfde maker als [BTC RPC Explorer](https://docs.theroadtonode.com/bitcoin-core-extensies/btc-rpc-explorer). LND Admin doet eigenlijk hetzelfde als [Ride the Lightning](https://docs.theroadtonode.com/lightning-extensies/ride-the-lightning) en [Thunderhub](https://docs.theroadtonode.com/lightning-extensies/thunderhub). Er is in Lightning land veel variatie en voor ieder wat wils. Daarom mag [LND Admin](https://github.com/janoside/lnd-admin) zeker niet ontbreken.

### Benodigdheden

* [NodeJS](https://docs.theroadtonode.com/raspberry-pi/algemene-dependencies-installeren#nodejs)

## Broncode

Zorg eerst dat je in je home directory zit met `cd ~`. Haal dan de broncode binnen.

```bash
git clone https://github.com/janoside/lnd-admin
```

Navigeer daarna de map in.

```bash
cd lnd-admin
```

Pak de laatste versie/tag/release.

```text
git checkout v0.10.12
```

Installeer LND Admin met NPM.

```bash
npm install
```

## Firewall

We starten LND Admin niet direct. Eerst moet de firewall nog opengezet worden voor de juiste port.

```bash
sudo ufw allow 3004
```

## Automatiseren

Het automatiseren zorgt ervoor dat LND Admin automatisch opstart bij het opstarten van je Pi. Handig, want dan hoef je het niet met de hand te doen. Het automatiseren gaat op dezelfde wijze als in de rest van de gids. Maar eerst een service aan.

```bash
sudo nano /etc/systemd/system/lnd-admin.service
```

Plak er dit in.

```bash
[Unit]
Description=LND Admin
Wants=lnd.service
After=lnd.service

[Service]
User=pi
WorkingDirectory=/home/pi/lnd-admin
ExecStart=/usr/bin/npm start
Restart=always
TimeoutSec=120
RestartSec=30

[Install]
WantedBy=multi-user.target
```

{% hint style="info" %}
Mocht je gebruik maken van LiT, vervang dan `lnd.service` met `lit.service`
{% endhint %}

Sla het weer op met `Ctrl + X` en bevestig met `Y`. De applicatie wordt gestart op port 3004.

Het systeem moet op de hoogte gesteld worden van de nieuwe service en kan daarna gestart worden.

```bash
sudo systemctl enable lnd-admin
```

```bash
sudo systemctl start lnd-admin
```

Wil je zien of alles goed is opgestart, voer dan dit uit:

```bash
systemctl status lnd-admin
```

Wil je een overzicht van de status over meerdere sessie, gebruik dan dit:

```bash
sudo journalctl -f -u lnd-admin
```

## Opstarten

De eerste keer dat je LND Admin opstart, moet je de configuratie stappen doorlopen. Ga naar `<het IP adres van je Pi>:3004` met je favoriete browser. Bij mij is dat 192.168.1.6:3004. LND Admin wil een admin password hebben. Dit mag je zelf verzinnen. Daarna vraagt de configuratie om vier variabelen van LND.

* De host
* Het portnummer
* Het pad naar de admin macaroon
* En het pad naar het TLS certificaat

![Configuratie scherm met de juiste velden](../.gitbook/assets/image%20%281%29.png)

Vul dit in:

* Host: `localhost`
* Port: `10009`
* Admin Macaroon Filepath: `/home/pi/.lnd/data/chain/bitcoin/mainnet/admin.macaroon`
* TLS Certificate Filepath: `/home/pi/.lnd/tls.cert`

Na een seconde of 20 zal er een scherm verschijnen met de melding dat het gelukt is!



