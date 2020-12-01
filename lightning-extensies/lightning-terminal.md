# Lightning Terminal (LiT)

{% hint style="info" %}
Tijd: 25 minuten
{% endhint %}

### Use case
* Een visueel overzicht van de balans van jouw Lightning kanalen
* Kanalen balanceren via [Lightning Loop](https://lightning.engineering/loop/) met behulp van submarine swaps
* Balanceren doe je met on-chain satoshis (Loop in)
* Je betaalt minder fees als je meerdere kanalen tegelijk balanceert
* Eenvoudig satoshis versturen naar je on-chain wallet (Loop out)

Demo video: https://lightning.engineering/static/terminal-2c00f93b062f44e5c2d1db067f7ee8cd.mp4

### Benodigdheden
* [golang](../lightning/golang-installatie.md)
* protoc
* nodejs
* yarn

## Installatie Lightning Terminal

#### NodeJS
Download en installeer NodeJS.
```bash
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt install nodejs -y
```

Controleer of NodeJS is geïnstalleerd.
```bash
node --version
# Verwachte output: v14.15.0
```

#### Yarn

Download en installeer [Yarn](https://classic.yarnpkg.com/en/docs/install).
```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install yarn
```

Controleer of Yarn is geïnstalleerd.
```bash
yarn --version
Verwachte output: 1.22.5
```

Download de broncode van Lightning Terminal.
```bash
git clone https://github.com/lightninglabs/lightning-terminal.git
```

Duik de code in.
```bash
cd lightning-terminal
```

Installeer Lightning Terminal.
```bash
make install
```

## LND configureren voor Loop
We gaan er vanuit dat je LND al hebt geïnstalleerd en geconfigureerd. 
Je moet de .macaroon bestanden verwijderen in de lnd map en daarna lnd herstarten.   
*Als je LND nog niet hebt geinstalleerd, volg dan [deze stappen](../lightning/installatie.md) en voer `make install tags="signrpc walletrpc chainrpc invoicesrpc"` bij de installatie stap.*

Stop LND indien deze actief is.
```bash
lncli stop
```

Ga naar de bronbestanden map van LND om LND opnieuw te installeren.
```bash
cd ~/lnd
```

Installeer LND.
```bash
make install tags="signrpc walletrpc chainrpc invoicesrpc"
```

Check voor macaroon bestanden.
```bash
ls -la ~/.lnd/data/chain/bitcoin/mainnet
```
De .macaroon bestanden die je moet verwijderen zijn.
`admin.macaroon`, 
`invoice.macaroon`, 
`readonly.macaroon`
`router.macaroon` .

Verwijder de macaroon bestanden.
```bash
rm -i ~/.lnd/data/chain/bitcoin/mainnet/*.macaroon
```
Beantwoord de vragen met `yes` om elk bestand te verwijderen.

Start lnd
```bash
lnd
```
Open een tweede terminal scherm om je wallet te unlocken.

```bash
lncli unlock
```
Vul je wallet wachtwoord in.

## Installatie Loop
Om kanalen te kunnen balanceren, hebben we de Loop software nodig.  
Download de broncode
```bash
git clone https://github.com/lightninglabs/loop.git
``` 

Ga naar `loop/cmd`.
```bash
cd loop/cmd
```
Installeer de `loopd` software.
```bash
go install ./...
```

Test of het gelukt is.
```bash
loopd
```
In de output zul je lezen dat Loop verbonden is met je LND. 
```
2020-12-01 09:53:40.186 [INF] LOOP: Connected to lnd node '<jouw_node_naam>' with pubkey <public_key_van_jouw_node> (version v0.11.99-beta, build tags 'signrpc,walletrpc,chainrpc,invoicesrpc')
```

## Automatisch opstarten

Lightning Terminal automatisch opstarten.  
Maak het Lightning Terminal service bestand.
```bash
sudo nano /etc/systemd/system/lit.service
```

Plak er dit in.
```bash
[Unit]
Description=Lightning Terminal
Wants=lnd.service
After=lnd.service

[Service]
User=pi
ExecStart=/home/pi/go/bin/litd --uipassword=<JOUW_WACHTWOORD_MET_MINIMAAL_8_KARATERS>
PIDFile=/home/pi/.lit/lit.pid
Restart=always
TimeoutSec=120
RestartSec=30

[Install]
WantedBy=multi-user.target
```

Vervang `<JOUW_WACHTWOORD_MET_MINIMAAL_8_KARATERS>` met een door jouw gekozen wachtwoord. Dit wachtwoord gebruik je om in te loggen in Lightning Terminal.

Sla de wijzigingen op met Control + X en bevestig met Y.

Breng het systeem op de hoogte gesteld van de nieuwe service.

```bash
sudo systemctl enable lit
```

Start de service.
```bash
sudo systemctl start lit
```

Wil je zien of de service is opgestart, voer dan dit uit.

```bash
systemctl status lit
```

Wil je een overzicht van de status over meerdere sessies, gebruik dan dit commando.

```bash
sudo journalctl -f -u lit
```

## Start Lightning Terminal

Open **https://&lt;het ip adres van je Pi&gt;:8443** in de browser om in te loggen in Lightning Terminal en aan de slag te gaan met de tool.

## Aan de slag met een walktrough
Aan de slag met het LiT dashboard? Volg dan [deze walkthrough](https://github.com/lightninglabs/lightning-terminal/blob/master/doc/WALKTHROUGH.md) van Lightning Labs.



