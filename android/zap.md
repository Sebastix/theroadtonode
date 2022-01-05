# Zap

{% hint style="info" %}
Tijd: 10 minuten
{% endhint %}

De [Zap: Bitcoin Lightning Wallet](https://play.google.com/store/apps/details?id=zapsolutions.zap)-app is nog in ontwikkeling maar daarom niet minder bruikbaar. Hij heeft een mooie interface en je kunt hem aan je eigen node hangen via Tor. 

## Voorbereiding

Omdat we een headless server draaien, hebben we geen QR-code die we straks kunnen scannen dus moeten we een connectiestring plakken. Deze connectiestring maken we met [lndconnect](https://docs.theroadtonode.com/lightning-extensies/lnd-connect) op je Pi. SSH je Pi in en typ:

```bash
lndconnect --host=xxx.onion --port=10009 -j
```

Waar **xxx.onion** staat, vul je natuurlijk [jouw onion-adres](https://docs.theroadtonode.com/lightning-extensies/lnd-connect) in voor de **RPC** API van LND. Er zal een lap tekst verschijnen dat iets weg heeft van het volgende:

```bash
lndconnect://xxx.onion:10009?cert=heel_veel_tekens&macaroon=heel_veel_tekens
```

Kopieer die lap tekst vanuit SSH en plak die bijvoorbeeld in een Google Docs document \(want we willen die tekst straks op onze telefoon hebben\).

## Zap

1. Switch op je telefoon naar dit Google Docs document en kopieer de gehele string \(`lndconnect://xxx.onion:10009?cert=heel_veel_tekens&macaroon=heel_veel_tekens`\).
2. Open Zap
3. Tap op Wallet instellen
4. Plak
3. OK

Je bent nu verbonden met je eigen Node.

Via `Beheer...` kun je naam van je wallet aanpassen. Standaard krijgt die de naam van je Tor-adres namelijk.