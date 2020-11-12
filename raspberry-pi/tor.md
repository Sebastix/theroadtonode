# Tor

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

Het [Tor netwerk](https://nl.wikipedia.org/wiki/Tor_%28netwerk%29) zorgt voor een extra laagje privacy bij het gebruik van Bitcoin.

SSH in je Pi en voer de volgende berg aan commando's uit.

```text
sudo apt install tor -y
```

```text
sudo systemctl enable tor
```

```text
sudo systemctl start tor
```

Tor moet een beetje aangepast worden. Hiervoor moeten wij een bestand wijzigen. Er staat veel troep in dus het is handig om het bestand eerst weg te gooien.

```bash
sudo rm /etc/tor/torrc
```

```text
sudo nano /etc/tor/torrc
```

Eenmaal in dit bestand voeg je onderaan \(of bovenaan als je daar zin in hebt\) deze drie regels toe:

```text
ControlPort 9051
CookieAuthentication 1
CookieAuthFileGroupReadable 1

HiddenServiceDir /var/lib/tor/bitcoin/bitcoind
HiddenServiceVersion 3
HiddenServicePort 8332 127.0.0.1:8332
```

Sla het bestand op met de toestencombinatie Control + X. Geef "Y" als antwoord op de vraag of je op wil slaan.

Maak mappen aan met:

```bash
sudo mkdir /var/lib/tor/bitcoin
```

```bash
sudo mkdir /var/lib/tor/bitcoin/bitcoind
```

Geef de juiste rechten met:

```bash
sudo chown -R debian-tor:debian-tor /var/lib/tor/bitcoin/bitcoind
```

```bash
sudo chmod 700 /var/lib/tor/bitcoin/bitcoind
```

Tor moet nu opnieuw opgestart worden.

```text
sudo systemctl restart tor
```

De juiste rechten moeten toegekend worden aan onze gebruiker genaamd pi.

```text
sudo usermod -a -G debian-tor pi
```

Om alles van kracht te laten zijn log je uit door "exit" te typen en op enter te drukken. **Vergeet dit niet!**

## Onion adres

De adressen heb je later nodig als je wil communiceren met je node. De eerste is voor het mainnet van Bitcoin, de tweede is voor Lightning.

```bash
sudo cat /var/lib/tor/bitcoin/bitcoind/hostname
```



