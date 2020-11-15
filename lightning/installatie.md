# Installatie

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

De [Lighting Network Daemon](https://github.com/lightningnetwork/lnd#lightning-network-daemon) \(LND\) is een implementatie van een Lightning Network node. Het is een tweede laag op Bitcoin, waarbij bitcoind \(of software equivalent\) de eerste laag vormt. Maar als je LND wil installeren dan weet je dat waarschijnlijk al.

Zorg dat je in home bent.

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

En installeer LND.

```bash
make install
```

