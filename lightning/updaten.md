# Updaten

Backup eerst je channels via RTL, Thunderhub of LNCLI.

Stop nu de services die afhankelijk zijn van LND zoals [Ride The Lightning](ride-the-lightning.md) of [Thunderhub](thunderhub.md) en LND zelf.

```bash
sudo systemctl stop rtl.service
sudo systemctl stop lnd.service
```

Update de repository met de laatste wijzigingen via Git.

```bash
cd ~/lnd
git pull
```

Toon de laatste versie / tag.

```text
git describe --tags `git rev-list --tags --max-count=1`
```

Haal de wijzigingen op van de laatste versie.

```bash
git checkout <OUTPUT VAN DE VORIGE STAP> #voorbeeld: v0.12.0-beta
```

Installeer nu de software.

```bash
sudo make install
```

Start de service lnd en monitor de voortgang van het opstarten. Wees geduldig dit kan even duren.

```bash
sudo systemctl start lnd
sudo journalctl -f -u lnd.service
```

Zodra je in de output voorbij ziet komen dat je de wallet kunt unlocken start je een tweede putty venster.

```bash
lncli unlock
```

Vul nu je passphrase in van je wallet. Nu zie je in het andere venster de GossipSyncer wat betekent dat LND weer in de lucht is.

Check de huidige versie van LND

```bash
lncli --version
```

De output zal lijken op `lncli version 0.12.0-beta commit=v0.12.0-beta`

LND is nu bijgewerkt!


Start de andere services die afhankelijk zijn van LND zoals RTL of Thunderhub.

```bash
sudo systemctl start rtl
```