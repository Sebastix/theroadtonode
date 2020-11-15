# Automatisering

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

Het open hebben van twee terminals is irritant. LND wil je in de achtergrond hebben draaien, net als bitcoind.

```bash
sudo nano /etc/systemd/system/lnd.service
```

Plak er dit in.

```bash
[Unit]
Description=Lightning Network Daemon
Requires=bitcoind.service
After=bitcoind.service

[Service]
User=pi
ExecStart=/home/pi/go/bin/lnd
PIDFile=/home/pi/.lnd/lnd.pid
Restart=always
TimeoutSec=180
RestartSec=60

[Install]
WantedBy=multi-user.target
```

Sla het weer op met `Control + X` en bevestig met `Y`.

Het systeem moet op de hoogte gesteld worden van de nieuwe service en kan daarna gestart worden.

```bash
sudo systemctl enable lnd
```

```bash
sudo systemctl start lnd
```

Wil je zien of alles goed is opgestart, voer dan dit uit:

```bash
systemctl status lnd
```

Wil je een overzicht van de status over meerdere sessie, gebruik dan dit:

```bash
sudo journalctl -f -u lnd
```
