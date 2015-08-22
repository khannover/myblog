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

Im Prinzip reicht das bereits aus, um den Pi vom LAN aus als Proxy nutzen zu können.

Über die Config-Datei ``/etc/ziproxy/ziproxy.conf`` kann ziproxy tiefer konfiguiert werden. 

Hier ein paar Optionen, die interessant sein könnten:

- Port auf dem Ziproxy lauscht

```bash
## Port to listen for proxy connections
## default: 8080
# Port = 8080
```

- User unter dem ziproxy läuft

```bash
## Run daemon as `RunAsUser` user.
## Switch from current user (in this case, typically `root`)
## to a less privileged one, as a security measure.
##
## default: unspecified (does not change user)
# RunAsUser = "ziproxy"
```

- Logging-Optionen (Debug, Error, Access)

```bash
## Disabled by default.
# DebugLog = "/var/log/ziproxy/debug.log"

## Default: undefined (dumps to stderr).
# ErrorLog = "/var/log/ziproxy/error.log"

## Disabled by default.
# AccessLog = "/var/log/ziproxy/access.log"
```

- Authentifizierung für Proxy (empfehlenswert, wenn der Proxy übers Internet erreichbar sein wird, damit nicht jeder Schabernack über meine IP treiben kann)
  - Die Passwort-Datei liegt standardmäßig unter ``/etc/ziproxy/http.passwd``, kann aber über die Option ``AuthPasswdFile`` angepasst werden

```bash
## Authentication mode to be used for proxy access:
## 0: none (no authentication required)
## 1: plain text file
## 2: SASL (auxprop, see /etc/ziproxy/sasl/ziproxy.conf)
##
## Notes:
## a) SASL support is optional (enabled during compilation time).
## b) SASL authentication does not require external SASL daemon
##    configuration/invocation, just Ziproxy's SASL configuration.
##
## Default: 0 (no authentication required)
## See also: AuthPasswdFile, AuthSASLConfPath
AuthMode = 1

## Plain text file containing authentication data.
## Should contain user:pass pairs, lines no longer than 128 chars.
## Password is unencrypted.
## Used only when AuthMode=1
##
## Default: (undefined)
## See also: AuthMode
AuthPasswdFile = "/etc/ziproxy/http.passwd"
```

