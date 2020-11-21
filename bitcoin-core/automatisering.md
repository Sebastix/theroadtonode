# Automatisering

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

Het mooiste is als bitcoind automatisch opstart, in plaats van dat je het handmatig moet doen. Dit kan handig zijn na het opnieuw opstarten van je Pi of als bitcoind crasht. Linux heeft daar systemd services voor. Zorg voordat je aan de slag gaat met de automatisering, dat Bitcoin Core (bitcoind) uit staat. Doe dit met:

```bash
bitcoin-cli stop
```

Zodra bitcoind uit staat kunnen we een service aanmaken.

```bash
sudo nano /etc/systemd/system/bitcoind.service
```

Plak er dit in.

```bash
[Unit]
Description=Bitcoin Daemon
After=network.target

[Service]
User=pi
PIDFile=/home/pi/.bitcoin/bitcoind.pid
ExecStart=/usr/local/bin/bitcoind
Restart=always
TimeoutSec=120
RestartSec=30

[Install]
WantedBy=multi-user.target
```

Sla het weer op met `control + X` en bevestig met `Y`.

Het systeem moet op de hoogte gesteld worden van de nieuwe service en kan daarna gestart worden.

```bash
sudo systemctl enable bitcoind
```

```bash
sudo systemctl start bitcoind
```

Wil je zien of alles goed is opgestart, voer dan dit uit:

```bash
systemctl status bitcoind
```

Wil je een overzicht van de status over meerdere sessie, gebruik dan dit:

```bash
sudo journalctl -f -u bitcoind
```
