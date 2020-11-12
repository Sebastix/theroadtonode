# Configuratie

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

De map waar LND gebruik wil maken, bestaat nog niet. Maak hem dus eerst aan.

```bash
mkdir ~/.lnd
```

Het configuratie bestand maak je aan met:

```bash
nano ~/.lnd/lnd.conf
```

En plak er de instellingen in.

```bash
[Application Options]
tlsautorefresh=true
restlisten=0.0.0.0:8080
rpclisten=0.0.0.0:10009
listen=127.0.0.1:9735
externalip=DIT_WEET_JE_A
maxpendingchannels=5
color=ZELF_VERZINNEN_A
alias=ZELF_VERZINNEN_B
minchansize=50000

[Tor]
tor.active=true
tor.v3=true
tor.streamisolation=true

[Bitcoin]
bitcoin.active=true
bitcoin.mainnet=true
bitcoin.node=bitcoind

[bitcoind]
bitcoind.dir=/home/pi/.bitcoin
bitcoind.rpcuser=DIT_WEET_JE_B
bitcoind.rpcpass=DIT_WEET_JE_C
bitcoind.zmqpubrawblock=tcp://127.0.0.1:28332
bitcoind.zmqpubrawtx=tcp://127.0.0.1:28333
```

In de tekst hierboven staan 5 dingen die je zelf moet regelen.

* **externalip**, verander DIT\_WEET\_JE\_A met het onion-adres wat je zojuist hebt aangemaakt. Je krijgt dan "externalip=xxx.onion:9735".
* **color**, verander ZELF\_VERZINNEN\_A naar een kleur naar keuze. Het is een hexadecimale waarde. Je krijgt dan "color=\#123ABC".
* **alias**, verander ZELF\_VERZINNEN\_B naar een naam naar keuze. Je krijgt dan "alias=nickname".
* **bitcoind.rpcuser**, verander DIT\_WEET\_JE\_B naar [de juiste user](https://node.bitdeal.nl/bitcoin-core/configuratie-en-starten).
* **bitcoind.rpcuser**, verander DIT\_WEET\_JE\_C naar [het juiste wachtwoord](https://node.bitdeal.nl/bitcoin-core/configuratie-en-starten).

Sla het bestand op met Control + X en Y.

