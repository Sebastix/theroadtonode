# Pool

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

Pool is 1 van de gaafste ontwikkelingen binnen Lightning. In principe maakt het obligaties mogelijk op het Lightning netwerk. Je kunt met behulp van Pool rente vangen op je bitcoin, zonder dat je het bij een derde partij onderbrengt. Je blijft dus altijd in beheer van je bitcoin.

## Benodigdheden

* [Golang](https://docs.theroadtonode.com/raspberry-pi/algemene-dependencies-installeren#golang) **\(update naar de nieuwste versie voordat je begint\)**

## Installatie

Ga eerst naar je home directory.

```bash
cd ~
```

Download de broncode.

```bash
git clone https://github.com/lightninglabs/pool
```

Ga de map in.

```bash
cd pool
```

Pak de laatste versie/tag/release.

```bash
git checkout v0.5.4-alpha
```

Installeer de Pool software.

```bash
make install
```

Test of het gelukt is door Pool tijdelijk op te starten.

```bash
poold
```

In de output zul je lezen dat pool verbonden is met je LND en met `Ctrl + C` kun je `poold` weer stop zetten.

Naast het Pool programma is er ook een CLI geinstalleerd. Je kunt deze controleren met `pool --version`.

## Firewall

Je kunt van buitenaf Pool benaderen op twee verschillende poorten.

```bash
sudo ufw allow 8281 comment "Port voor REST API van Pool"

sudo ufw allow 12010 comment "Port voor RPC van Pool"
```

## Automatiseren

Wil je Pool in de achtergrond draaien dan heb je weer een service nodig.

```bash
sudo nano /etc/systemd/system/pool.service
```

Plak dit erin.

```toml
[Unit]
Description=Pool
Requires=bitcoind.service
Requires=lnd.service
After=bitcoind.service
After=lnd.service

[Service]
User=ubuntu
ExecStart=/home/ubuntu/go/bin/poold
Restart=always
TimeoutSec=120
RestartSec=30

[Install]
WantedBy=multi-user.target
```

Sla de wijzigingen op met `Ctrl + X` en bevestig met `Y`.

Breng het systeem op de hoogte van de nieuwe service.

```bash
sudo systemctl enable pool
```

Start de pool service als volgt.

```bash
sudo systemctl start pool
```

Wil je zien of de service is opgestart, voer dan dit uit.

```bash
systemctl status pool
```

Wil je een overzicht van de status over meerdere sessies, gebruik dan dit commando.

```bash
sudo journalctl -f -u pool
```