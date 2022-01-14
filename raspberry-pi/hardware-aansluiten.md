---
description: Als dit je niet lukt zou je niet mogen stemmen
---

# Hardware aansluiten

{% hint style="info" %}
Tijd: 15 minuten
{% endhint %}

De simpelste taak van de guide: het aansluiten van de hardware. Hier heb je de Raspberry Pi en heatsink nodig. Als je hebt gekozen voor de heatsink uit het [boodschappenlijstje](https://docs.theroadtonode.com/introductie/benodigdheden), is er nog een tip voor je: bij de heatsink wordt **warmtegeleidende pasta** geleverd in de vorm van dubbelzijdig tape. Als je niet heel erg thuis bent in het bouwen van computers, kan het zijn dat je hier geen raad mee weet. Plak de thermische tape als volgt.

![Raspberry Pi met thermische tape](../.gitbook/assets/paste-copy.png)

Nadat je alles in elkaar hebt geschroefd, kun je de ventilatoren aansluiten op de pinnen. De rode draad moet op GPIO PIN 04 en de zwarte op GPIO PIN 06. De pinnen staan respectievelijk voor [5V en ground](https://www.raspberrypi.org/documentation/usage/gpio/). Na het voltooien zou dit het eindresultaat moeten zijn.

![Raspberry Pi met heatsink](../.gitbook/assets/connected.png)

Tijdens het synchroniseren van de Bitcoin blockchain is met deze opzet de temperatuur van de CPU niet boven de 47 graden gekomen.

