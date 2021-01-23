## Bitcoin core updaten

Ga naar de applicatie directory   
`cd ~/bitcoin`

Update de repository met de laatste wijzigingen via Git:  
`git fetch --all`

Toon de laatste versie (tag)  
```bash
git describe --tags `git rev-list --tags --max-count=1`
```

Haal de wijzigingen op van de laatste versie  
`git checkout <output van vorige stap> #voorbeeld: v0.21.0`

Stel bitcoin core opnieuw samen met de laatste wijzigingen  
`make`  
Dit zal even duren, mooi moment voor een biertje of kopje koffie.

Stop de service lnd  
`sudo systemctl stop lnd`

Stop de service bitcoin  
`sudo systemctl stop bitcoind`

Installeer nu de software  
`sudo make install`

Start de service bitcoin  
`sudo systemctl start bitcoind`

Start de service lnd  
`sudo systemctl start lnd`

Check de huidige versie van bitcoin core
`bitcoin-cli --version`  
De output zal lijken op `Bitcoin Core RPC client v0.21.0`

Bitcoin core is nu bijgewerkt!