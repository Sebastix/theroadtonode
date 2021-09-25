# Updaten

{% hint style="info" %}
Tijd: 1.5 uur
{% endhint %}

Zorg voordat je van start gaat dat je Pi up-to-date is met `sudo apt update` en `sudo apt upgrade -y`.

Ga naar de applicatie directory.

```bash
cd ~/bitcoin
```

Update de repository met de laatste wijzigingen via Git.

```bash
git fetch --all
```

Toon de laatste versie/tag/release.

```text
git describe --tags `git rev-list --tags --max-count=1`
```

Haal de wijzigingen op van de laatste versie.

```bash
git checkout -f <OUTPUT VAN DE VORIGE STAP> #voorbeeld: v22.0
```

Build bitcoin core opnieuw op basis van de zojuist uitgecheckte versie van de broncode. Door de toevoeging van `-j $(nproc)` worden alle cores gebruikt van de CPU en zou de build sneller verlopen dan zonder deze toevoeging.

```bash
make -j $(nproc)
```

De build zal met ongeveer een uur klaar zijn. Mooi moment voor een biertje of kopje koffie!

Stop de LND service en andere services die afhankelijk zijn van Bitcoin zoals de btc-rpc-explorer en Electrum Personal Server of Electrum X mocht je die geïnstalleerd hebben.

```bash
sudo systemctl stop lnd
sudo systemctl stop rtl
sudo systemctl stop btc-rpc-explorer
sudo systemctl stop eps
```

Stop de bitcoind service.

```bash
sudo systemctl stop bitcoind
```

Installeer nu de software. Dit duurt maximaal 5 minuten.

```bash
sudo make install
```

Start de service bitcoin. De service zal vrij snel gestart zijn maar de blockchain moet mogelijk nog een aantal blocks downloaden, afhankelijk van hoe lang de service gestopt was.

```bash
sudo systemctl start bitcoind
```

Start de service LND \(vergeet deze niet te unlocken\) en andere services. LND unlocken zal pas kunnen nadat de blockchain van bitcoin weer synchroon is na de start. Controleer met `tail -f -n 200 .bitcoin/debug.log` hoe ver deze is. Services start je weer op deze manier:

```bash
sudo systemctl start lnd
```

Check de huidige versie van bitcoin core.

```bash
bitcoin-cli --version
```

De output zal lijken op `Bitcoin Core RPC client v0.22.0`

Bitcoin core is nu bijgewerkt!

