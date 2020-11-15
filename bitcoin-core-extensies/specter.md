# Specter

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

[Specter](https://github.com/cryptoadvance/specter-desktop) is in het leven geroepen om het opzetten van een multisig constructie makkelijker te maken. Het biedt een overzichtelijke tool welke je kunt inzien in je browser. Om dit onderdeel van de guide enigszins simpel te houden, moet je voor het gebruik van Specter fysiek toegang hebben tot je node. Om Specter te gebruiken en een [multisig](https://youtu.be/yeLqe_gg2u0) op te zetten, moet je namelijk jouw hardware wallets aansluiten op de Pi. Een duidelijke uitleg over het gebruik van Specter is onderaan de pagina te vinden. In dit onderdeel gaan we in op de installatie en het openen van Specter.

SSH in je Pi en voer het installatie commando uit voor de nodige tools.

```bash
sudo apt install libusb-1.0-0-dev libudev-dev python3-pip -y
```

Daarna installeer je Specter.

```bash
pip3 install cryptoadvance.specter
```

En tot slot start je Specter met:

```bash
python3 -m cryptoadvance.specter server --daemon --host 0.0.0.0
```

De tool zal nu in de achtergrond draaien op poortnummer **:25441**. Open je browser en ga naar **\<het ip van je pi:poortnummer\>**. In mijn geval is dat 192.168.1.6:25441.

# Gebruik van Specter

https://www.youtube.com/watch?v=ZQvCncdFMPo
