# Installatie

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

[Lighting Network Daemon](https://github.com/lightningnetwork/lnd#lightning-network-daemon) \(LND\) is een implementatie van het Lightning Network protocol. Het is een tweede laag op Bitcoin, waarbij bitcoind \(of software equivalent\) de eerste laag vormt. Maar als je LND wil installeren dan wist je dat waarschijnlijk al.

{% hint style="info" %}
Let op: dit onderdeel is afhankelijk van de [Golang installatie](https://docs.theroadtonode.com/raspberry-pi/algemene-dependencies-installeren#golang). Je kunt niet verder als je Golang niet geinstalleerd hebt op de Raspberry Pi.
{% endhint %}

Zorg dat je in de home directory bent.

```bash
cd ~
```

Haal de broncode binnen.

```bash
git clone https://github.com/lightningnetwork/lnd
```

Ga de LND map in.

```bash
cd lnd
```

Haal door middel van git alle branches op.

```bash
git fetch --all
```

Toon de laatste versie/tag/release.

```bash
git describe --tags `git rev-list --tags --max-count=1`
```

Stap over naar de laatste release.

```bash
git checkout <OUTPUT VAN DE VORIGE STAP> #voorbeeld: v0.12.0-beta
```

En installeer LND. De tags zijn handig om alvast mee te geven, mocht je later gebruik willen maken van [Lightning Terminal](https://docs.theroadtonode.com/lightning-extensies/lightning-terminal).

```bash
make install tags="autopilotrpc signrpc walletrpc chainrpc invoicesrpc routerrpc watchtowerrpc"
```

