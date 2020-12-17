# Port overzicht

Het volgende is een overzicht van alle ports die benaderbaar zijn op je Raspberry Pi. Je kunt bij bepaalde tools door in je favoriete browser het IP-adres van je Pi gevolgd door het poortnummer in te voeren. Bijvoorbeeld `192.168.1.6:3002` om BTC RPC Explorer in te zien. Wil je de tools benaderen over tor, zul je per tool het `torrc` bestand moeten aanpassen. Je kunt dat bepaale poorten benaderbaar voor buitenaf maken en doorsturen naar een lokale poort op je Pi. Hoe dit werkt staat in de guide meestal uitgelegd in de tool naar keuze.

We gaan uit van de default waardes.

## Bitcoin Core

| Poort     | Functionaliteit                                                                                                                                                                                            |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **8332**  | De JSON-RPC poort. Met de juiste username/password combinatie kun je hier tegenaan praten.                                                                                                                 |
| **8333**  | Deze poort is verantwoordelijk voor de communicatie met andere clients op het Bitcoin netwerk.                                                                                                             |
| **28332** | De Bitcoin Daemon kan middels het ZeroMQ protocol block informatie versturen naar clients. Zo hoeven de clients niet iedere keer een request te doen via de JSON-RPC, maar gaat het op subscription basis. |
| **28333** | Hetzelfde als poort 28332, maar dan voor transacties.                                                                                                                                                      |

## Tor

| Poort    | Functionaliteit                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------- |
| **9050** | Je moet een applicatie vertellen gebruik te maken van poort 9050 als je van tor gebruik wil maken. |

## BTC RPC Explorer

| Poort    | Functionaliteit                                    |
| -------- | -------------------------------------------------- |
| **3002** | De BTC RPC Explorer is benaderbaar via deze poort. |

## Electrum (zowel X als Personal Server)

| Poort     | Functionaliteit                                    |
| --------- | -------------------------------------------------- |
| **8000**  | De BTC RPC Explorer is benaderbaar via deze poort. |
| **50001** | De BTC RPC Explorer is benaderbaar via deze poort. |
| **50002** | De BTC RPC Explorer is benaderbaar via deze poort. |
| **50004** | De BTC RPC Explorer is benaderbaar via deze poort. |

## Specter

| Poort     | Functionaliteit                                    |
| --------- | -------------------------------------------------- |
| **25441** | De BTC RPC Explorer is benaderbaar via deze poort. |

## Lightning Network Daemon

| Poort     | Functionaliteit                                    |
| --------- | -------------------------------------------------- |
| **8080**  | De BTC RPC Explorer is benaderbaar via deze poort. |
| **9735**  | De BTC RPC Explorer is benaderbaar via deze poort. |
| **10009** | De BTC RPC Explorer is benaderbaar via deze poort. |

## Ride the Lightning

| Poort    | Functionaliteit                                    |
| -------- | -------------------------------------------------- |
| **3000** | De BTC RPC Explorer is benaderbaar via deze poort. |
