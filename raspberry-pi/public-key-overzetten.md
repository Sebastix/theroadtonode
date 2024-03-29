# Public key overzetten

{% hint style="info" %}
Tijd: 2 minuten
{% endhint %}

Je eigen public key overzetten naar de Pi maakt het makkelijker om in te loggen. Zo hoef je bij het SSH'en niet meer je wachtwoord in te typen. Om dit te doen moet je op je eigen machine zitten en een terminal openen. Met het onderstaande commando zet je je public key over naar je Pi. Mocht je dat niet willen of lukt het niet, maakt dat ook niet uit. Je kunt altijd in loggen met de `ubuntu:WACHTWOORD` combinatie.

```bash
ssh-copy-id ubuntu@IP.ADRES.VAN.JE.PI
```

Nadat je het overhevelen van de public key hebt bevestigd met een wachtwoord, kun je als het goed is nu inloggen zonder je wachtwoord in te voeren.

## Disable wachtwoord login

{% hint style="warning" %}
Doe dit enkel als je weet wat je doet.
{% endhint %}

Je kunt nog een stapje verder gaan en enkel toestaan dat je mag inloggen via de public key. Let op: `USERNAME:PASSWORD` combinatie zet je dus hier mee uit.

```bash
sudo nano /etc/ssh/sshd_config
```

In het scherm dat opent kun je de volgende instellingen veranderen:

* `#PubkeyAuthentication yes` wordt `PubkeyAuthentication yes`
* `PasswordAuthentication yes` wordt `PasswordAuthentication no`
* `UsePAM yes` wordt `UsePAM no`

Sla het bestand op met `Ctrl + X` en bevestig met `Y`. Daarna even de SSH service herstarten met `sudo service sshd reload` en de nieuwe instellingen zijn van kracht.
