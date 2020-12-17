# Port overzicht

Het volgende is een overzicht van alle ports die benaderbaar zijn op je Raspberry Pi. Je kunt bij bepaalde tools door in je favoriete browser het IP-adres van je Pi gevolgd door het poortnummer in te voeren. Bijvoorbeeld `192.168.1.6:3002` om BTC RPC Explorer in te zien. Wil je de tools benaderen over tor, zul je per tool het `torrc` bestand moeten aanpassen. Je kunt dan bepaale poorten benaderbaar maken voor buitenaf en doorsturen naar een lokale poort op je Pi. Hoe dit werkt staat binnen The Road to Node meestal uitgelegd in de tool naar keuze.

We gaan uit van de default waardes voor alle tools.

## Bitcoin Core

| Poort     | Functionaliteit                                                                                                                                                                                            |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **8332**  | De JSON-RPC poort. Met de juiste username/password combinatie kun je hier tegenaan praten.                                                                                                                 |
| **8333**  | Deze poort is verantwoordelijk voor de communicatie met andere clients op het Bitcoin netwerk.                                                                                                             |
| **28332** | De Bitcoin Daemon kan middels het ZeroMQ protocol block informatie versturen naar clients. Zo hoeven de clients niet iedere keer een request te doen via de JSON-RPC, maar gaat het op subscription basis. |
| **28333** | Hetzelfde als poort 28332, maar dan voor transacties in plaats van blocks.                                                                                                                                 |

## Tor

| Poort    | Functionaliteit                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **9050** | Als je wil dat een bepaalde applicatie communiceert over het tor netwerk, moet je de applicatie vertellen gebruik te maken van poort 9050. |

## BTC RPC Explorer

| Poort    | Functionaliteit                                    |
| -------- | -------------------------------------------------- |
| **3002** | De BTC RPC Explorer is benaderbaar via deze poort. |

## Electrum (zowel X als Personal Server)

| Poort     | Functionaliteit                                     |
| --------- | --------------------------------------------------- |
| **8000**  | Standaard RPC poort van het Electrum protocol.      |
| **50001** | Standaard poort voor TCP verbindingen.              |
| **50002** | Standaard poort voor SSL verbindingen.              |
| **50004** | Standaard poort voor secure websocket verbindingen. |

## Specter

| Poort     | Functionaliteit                                         |
| --------- | ------------------------------------------------------- |
| **25441** | Voer je deze poort in dan zie je het Specter overzicht. |

## Lightning Network Daemon

| Poort     | Functionaliteit                                                                                     |
| --------- | --------------------------------------------------------------------------------------------------- |
| **8080**  | De poort waarmee de REST API van LND zich benaderbaar maakt. Beveiligd met een zogenaamde macaroon. |
| **9735**  | De poort die connect met andere nodes. Een beetje zoals 8333 voor Bitcoin Core.                     |
| **10009** | De poort waarmee de RPC API van LND zich benaderbaar maakt. Beveiligd met een zogenaamde macaroon.  |

## Ride the Lightning

| Poort    | Functionaliteit                                                               |
| -------- | ----------------------------------------------------------------------------- |
| **3000** | De Ride the Lightning interface kun je gebruiken als je naar deze poort gaat. |
