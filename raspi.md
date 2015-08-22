# Raspberry Pi

## Raspberry Pi als Komprimierungs-Proxy für langsame Datenverbindungen

Da ich häufig über mein mobiles Datenlimit vom 500 MB komme, suchte ich nach einer Möglichkeit, den anfallenden Traffic zu verringern. 
Im Google Chrome oder auch im Opera mobile gibt es die Option, über einen Datenkomprimierungs-Proxy zu surfen und dadurch den Traffic 
zu verkleinern. Dabei wird der Datenverkehr über Server von Google bzw. Opera geschleust, komprimiert und dann erst ans Handy ausgeliefert.

Der Nachteil dabei ist, dass sämtlicher (unverschlüsselter) Datenverkehr über die o.g. Server läuft und theoretisch protokolliert und ausgewertet
werden kann. Google und Opera sagen zwar, das so etwas nicht getan wird, aber man weiß ja nie.

Daher kam ich auf die Idee, diese Funktionialität auf dem RasPi nachzubilden, um diesen Nachteil zu umgehen.

Dabei bin ich auf ``Ziproxy`` gestoßen. Ein Proxy-Server, welcher genau diese Komprimierung anbietet und der als Paket in Raspbian enthalten ist.

Installiert wird die Software auf dem üblichen Wege über apt-get:

```bash
sudo apt-get install ziproxy
```
