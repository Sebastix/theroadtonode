# Golang installatie

{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

Golang \(Go\) is een programmeertaal ontwikkeld door Google. Het is een vrij jonge taal uitgebracht in 2009. De lightning implementatie genaamd LND is hierop gebouwd. Aangezien we LND zelf gaan compilen, hebben we Go nodig.

## Oude Go versie verwijderen \(optioneel\)

Dit deel is alleen nodig als je Go al een keer geïnstalleerd had op je Pi middels `sudo apt install`. De versie die je op die manier hebt geïnstalleerd, dient eerst te worden verwijderd.

```bash
sudo apt remove golang-go
```

```bash
sudo apt autoremove golang-go
```

```bash
sudo apt purge golang-go
```

## Nieuwe Go versie installeren

Nadat de oude versie verwijderd is, kunnen we de nieuwe installeren. Op moment van schrijven is [v1.15.4](https://golang.org/dl/) het meest recent. Als er een nieuwe versie is die je wil installeren \(of omdat een latere versie van LND dat vereist\), let er dan op dat je een ARMv6 versie van Go download.

```bash
wget https://golang.org/dl/go1.15.5.linux-armv6l.tar.gz
```

```bash
sudo tar -C /usr/local -xzf go1.15.5.linux-armv6l.tar.gz
```

```bash
rm go1.15.5.linux-armv6l.tar.gz
```

## Referencies updaten

Om Go lekker te laten werken moeten we wat paden aanpassen. Daarvoor passen we het profile bestand aan.

```bash
nano ~/.profile
```

Waarschijnlijk zie je al wat staan in het bestand. Dat is goed en moet je laten staan. Plak er het volgende onderaan erin:

```bash
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
export PATH=$PATH:$GOPATH/bin:/usr/local/go/bin
```

Sla het op met `control + X` en `Y`. Nadat het opgeslagen is kun je profile inladen.

```bash
. ~/.profile
```

Om zeker van de te zijn dat alles werkt log je uit met "exit" en start je een nieuwe SSH verbinding. Check de Go versie met:

```bash
go version
```

Als het goed is zie je `go version go1.15.5 linux/arm` verschijnen.
