# Configuratie en starten

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

Bitcoin Core heeft allerhande instellingen. Net zoals jouw mobiel instellingen heeft. Het mooie aan het mobieltje is, is dat de instellingen overzichtelijk gegroepeerd onder elkaar staan. Je kunt ze makkelijk wijzigen met een druk op de knop. Bij Core werkt dat net even anders. Je moet eerst een lijst vinden met mogelijke instellingen, je inlezen en daarna bepalen wat je nodig hebt. Best wel een gedoe, daarom staat hieronder een configuratie bestand wat zou moeten werken voor deze guide.

## Configuratie

Voer uit:

```bash
mkdir .bitcoin
```

```bash
nano .bitcoin/bitcoin.conf
```

Net als bij het [torrc bestand](https://node.bitdeal.nl/raspberry-pi/tor) moeten we wat regels copy-pasten. Je kunt alle, inclusief de commentaar regels aangegeven met een \#, kopieëren en plakken.

```bash
# Maak het mogelijk JSON-RPC commando's te accepteren
server=1

# Draai Bitcoin Core (bitcoind) in de achtergrond
daemon=1

# Listening mode
listen=1

# Zorg ervoor dat Core een index bijhoudt van alle txs
txindex=1

# Cache grootte in MB's voor de database.
# Ophogen naar 3000 is wel lekker voor de IBD.
# Later kan het teruggeschroeft worden naar 500.
dbcache=3000

# Instellingen voor Tor
onlynet=onion
bind=127.0.0.1
proxy=127.0.0.1:9050

# Instellingen voor JSON-RPC
rpcuser=ZELF_VERZINNEN_A
rpcpassword=ZELF_VERZINNEN_B

# Nodig voor Lightning in een later stadium van de guide
zmqpubrawblock=tcp://127.0.0.1:28332
zmqpubrawtx=tcp://127.0.0.1:28333
```

Wacht even met gulzig op `Control + X` drukken om op te slaan! Op regel 24 en 25 staan twee waardes die je zelf moet invullen. Verander dus de woorden **ZELF\_VERZINNEN\_A** en **ZELF\_VERZINNEN\_B** naar iets wat je zelf leuk vindt. Druk daarna op `Control + X` en daarna `Y`om op te slaan.

## Starten

Dan is het nu tijd om deel te nemen aan het Bitcoin netwerk. Knal dit je Pi in:

```bash
bitcoind
```

Done! Je kunt live bijhouden wat er gebeurt met:

```bash
tail -n 200 -f ~/.bitcoin/debug.log
```

Per block dat gecontroleerd wordt, zie je de tekst "progress=xxxxx" voorbij komen. Dit is een getal van 0 tot 1. Nul betekent dat je nog niets gesynchroniseerd hebt, 1 betekent dat je klaar bent. Met `Control + C` zet je de live feed weer stop.

De initiële block download \(IBD\) zal zo'n 60 uur duren.

Met de installatie van Core heb je ook een tool geïstalleerd genaamd "bitcoin-cli". Hiermee kun je met bitcoind praten.

```bash
bitcoin-cli getnetworkinfo
```

Met dit commando krijg je wat informatie over het netwerk. Als het goed is ziet het er ongeveer zo uit.

```bash
"networks": [
    {
      "name": "ipv4",
      "limited": true,
      "reachable": false,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    },
    {
      "name": "ipv6",
      "limited": true,
      "reachable": false,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    },
    {
      "name": "onion",
      "limited": false,
      "reachable": true,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    },
  ],
  "localaddresses": [
    {
      "address": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.onion",
      "port": 8333,
      "score": 4
    }
  ]
```

Hieraan zie je het volgende:

* IPv4 is niet bereikbaar
* IPv6 is niet bereikbaar
* Onion is wel bereikbaar \(Tor\)
* Jouw .onion-adres binnen het "localaddresses" blok

