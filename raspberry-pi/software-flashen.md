# Software flashen

{% hint style="info" %}
Tijd: 15 minuten
{% endhint %}

Het is tijd om iets met een beeldscherm te doen. De Pi moet een besturingssysteem hebben, namelijk [Raspberry Pi OS](https://downloads.raspberrypi.org/raspios_lite_armhf_latest). Om het besturingssysteem op zowel de SSD als de microSD te krijgen, gebruiken we het programma [Balena Etcher](https://www.balena.io/etcher/). Gebruik je Windows dan zou je ook [Rufus](https://github.com/pbatard/rufus/releases/download/v3.12/rufus-3.12.exe) kunnen gebruiken.

## Raspberry Pi OS

We beginnen met het flashen van Raspberry Pi OS naar de microSD. Open Balena Etcher, selecteer de Raspberry Pi OS image en microSD en druk op de knop "Flash!".

![Raspberry Pi OS flashen naar de microSD](../.gitbook/assets/screenshot-2020-10-31-at-12.20.41.png)

Zodra het klaar is zal de microSD uitgeworpen worden. Haal hem uit je computer en steek hem er opnieuw in zodat je computer de microSD weer ziet. [Open de Terminal](https://support.apple.com/nl-nl/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) en typ het volgende commando waarna je op enter drukt.

```bash
touch /Volumes/boot/ssh
```

Zit je [op Windows](https://arjanlobbezoo.nl/windows-10-programma-administrator-mode-openen/), dan zou iets in de trant van het volgende moeten werken. In dit voorbeeld zou je de D-schijf moeten aanpassen naar wat voor jou van toepassing is.

```bash
type nul > D:\ssh
```

Met bovenstaande commando's wordt een bestand aangemaakt op de microSD. Het bestand heet "ssh" en als de Pi opstart met dit bestand aan boord, maakt de Pi het mogelijk om zich te laten aansturen van buitenaf. We gaan namelijk met behulp van SSH de Pi aansturen vanaf onze computer. Werp tot slot de microSD uit en **herhaal alles voor de SSD**. Stop de microSD in de Pi.

{% hint style="info" %}
In de guide wordt gebruik gemaakt van Raspberry Pi OS Lite 32-bit als besturingssysteem. Tijdens het uitdenken van de tutorial werd aanvankelijk uitgegaan van [Ubuntu Server 20.04.1 LTS 64-bit](https://ubuntu.com/download/raspberry-pi), aangezien de Pi ARM64 ondersteunt. Het bleek echter een vervelend proces te zijn om Ubuntu werkend te krijgen vanaf een SSD. Ook de 32-bit versie deed lastig.

In de toekomst wordt de guide eventueel geüpdate om gebruik te maken van 64-bits architectuur.
{% endhint %}

