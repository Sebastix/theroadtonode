# Tor

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

Het [Tor netwerk](https://nl.wikipedia.org/wiki/Tor_%28netwerk%29) zorgt voor een extra laagje privacy bij het gebruik van Bitcoin.

SSH in je Pi en voer het onderstaande uit om Tor te installeren.

```bash
sudo apt install tor -y
```

De juiste rechten moeten toegekend worden aan onze gebruiker genaamd pi.

```bash
sudo usermod -a -G debian-tor pi
```

Tot slot kunnen we Tor activeren en opstarten.

```bash
sudo systemctl enable tor
```

```bash
sudo systemctl start tor
```

Tor is nu geïnstalleerd. We zullen meerdere keren in deze guide terug komen op de configuratie van Tor, maar dat kom je vanzelf tegen.
