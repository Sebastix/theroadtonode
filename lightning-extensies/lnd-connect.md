# LND Connect

{% hint style="info" %}
Tijd: 4 minuten
{% endhint %}

LND Connect \(vaak [lndconnect](https://github.com/LN-Zap/lndconnect) genoemd\) is een tool ontwikkeld door de makers van Zap wallet. De tool genereert een QR code of stuk tekst waarmee een wallet gekoppeld kan worden aan je node. In dit onderdeel van de guide zullen we enkel lndconnect installeren. Het gebruik komt terug in wallet onderdelen van deze guide, zoals het [Zap \(iOS\)](https://docs.theroadtonode.com/ios/zap) onderdeel.

SSH om te beginnen in je Pi. Als het goed is heb je [Go](https://docs.theroadtonode.com/raspberry-pi/algemene-dependencies-installeren#golang) al op je machine staan. Dat is mooi, want dan kunnen we direct van start. Ga eerst naar je home directory.

```bash
cd ~
```

Haal de broncode van lndconnect binnen.

```bash
git clone https://github.com/LN-Zap/lndconnect.git
```

Na het binnenhalen moeten we naar de juiste map. We moeten ook een paar extra go-commando's geven, omdat de sourcecode nog niet is aangepast voor recente versies van go.

```bash
cd lndconnect

go mod init github.com/LN-Zap/lndconnect

go get github.com/lightningnetwork/lnd/tor@v0.12.1-beta

go mod tidy
```

Ten slotte kunnen we het installeren.

```bash
make
```

En testen of het werkt.

```bash
lndconnect --host test123.onion --port=8080 --nocert -j
```

Als het goed is, krijg je output die lijkt op het volgende.

```bash
lndconnect://test123.onion:8080?macaroon=[EEN_LANGE_REGEL_MET_WILLEKEURIG_AANDOENDE_LETTERS_EN_CIJFERS]
```

