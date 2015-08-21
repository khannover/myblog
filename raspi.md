# Raspberry Pi


***

### (2013/05/30) Rasperry Pi als Mediacenter

Ich gehörte zu den ersten, die sich einen [Raspberry Pi] bestellt haben. Nach meinem Umzug verstaubte das gute Stück bisher leider ungenutzt im Keller, bis ich kürzlich wieder darüber gestolpert bin. 

[raspberry pi]: http://www.raspberrypi.org "Raspberry Pi Store"

Um meinen [Fernseher] ordentlich mit Content zu betanken, hab ich mich kurzerhand entschlossen, den Pi unter anderem als Mediacenter einzusetzen. 

[fernseher]: http://www.philips.de/47pfl4007k/12 "Philips 47pfl4007k/12"

Als Softwareentwickler will ich aber natürlich auch anderweitig mit dem Pi herumspielen. Am liebsten wollte ich eine Multiboot-Installation. Eine Suche bei Google später stieß ich auf [BerryBoot][].

[BerryBoot]: http://www.berryterminal.com/doku.php/berryboot "BerryBoot Homepage"

Man entpackt BerryBoot auf eine FAT-Formatierte SD-Karte und bootet anschließend den Pi. BerryBoot bietet dann eine Auswahl an Distributionen, die automatisch heruntergeladen und auf der SD-Karte installiert werden. Die Auswahl umfasst u.a. [Raspbian][] und [OpenELEC][OpenELEC_HP]. Es gibt noch weitere Distributionen, die von vornherein auswählbar sind, z.B. [Puppy Linux][], [BerryWebserver und BerryTerminal][]. Es lassen sich aber auch eigene in BerryBoot [einbinden][].

[Raspbian]: http://www.raspbian.org "Raspbian Homepage"
[OpenELEC_HP]: http://www.openelec.tv "OpenELEC Homepage"
[Puppy Linux]: http://puppylinux.org "Puppy Linux Homepage" 
[BerryWebserver und BerryTerminal]: http://berryterminal.com
[einbinden]: http://www.berryterminal.com/doku.php/berryboot/adding_custom_distributions

Ich habe mich dann für OpenELEC als Mediacenter und Raspbian als Entwicklungsumgebung entschieden. OpenELEC wurde entworfen, um darin [XBMC][XBMC_HP] laufen zu lassen und ist damit perfekt geeignet für meine Mediencenter-Ambitionen. 

[XBMC_HP]: http://xbmc.org "XBMC Homepage"

Raspbian hingegen ist ein für den Raspberry Pi optimiertes Debian und bringt einen großen Blumenstrauß an Applikationen mit, welche es universell einsetzbar machen. Da mein Pi bekanntlich am Fernseher hängt, bietet es sich für mich an, unter Raspbian mit diversen Emulatoren (SNES, PSX, ...) und nativen Games ein kleines (aber feines?) Spielesystem aufbauen. Aber erstmal zurück zum OpenELEC.

Nach der problemlosen Installation mit BerryBoot startete mein Pi durch ins OpenELEC, wo mich eine schlichte aber schöne Oberfläche begrüßte. Erfreulicherweise lässt sich die Oberfläche problemlos ohne Maus (und zu meiner Überraschung sogar mit der Fernbedienung des TVs) bedienen. [^Kommentar 1]

[^Kommentar 1]: Das Feature, welches hierfür verantwortlich ist, nennt sich CEC (Consumer Electronics Control). Siehe http://de.wikipedia.org/wiki/HDMI#Fernbedienungsfunktionen

Die Bedienung an sich ist flüssig, aber sobald Menüpunkte aufgerufen werden und Dinge nachgeladen werden müssen, kann es sich schon einige Sekunden (zweistelliger Bereich) hinziehen, bis ein Ergebnis auf dem Bildschirm angezeigt wird. Eine Suche bei Youtube beispielsweise dauert gut und gerne 15-20 Sekunden. Die Wiedergabe von Videos hingegen ist selbst in Full-HD kein Problem für den kleinen Rechner dank Unterstützung durch den Grafikchip.Durch ein wenig Tuning lässt sich hier aber noch etwas optimieren. 

Erste Amtshandlung war das *Abschalten des RSS-Tickers*, welcher im unteren Bildschirmbereich aktuelle News über OpenELEC zeigt. Diese Einstellung befindet sich unter `System -> Darstellung` und bringt nach Abschaltung bereits einen merkbaren Performanceschub.

Die zweite Maßnahme war das Übertakten von CPU und Grafikchip. Unter `System -> Dienste` lässt sich auch SSH aktivieren. Anschließend per SSH-Client (z.B. [Putty][]) mit dem Pi verbinden und unter `/flash` die Datei config.txt mit folgendem Inhalt ablegen:

	arm_freq=800  
	gpu_freq=300

Nach einem Reboot ist das Overclocking dann aktiv und der Pi ein weiteres Stückchen schneller :-) 

[Putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html

Unter Raspbian ist die Übertaktung bereits Teil des Betriebssystems und heisst dort "[Turbo-Modus][]". Damit lässt sich der Pi **ohne Garantieverlust** dynamisch auf bis zu 1GHz übertakten. Dynamisch deswegen, weil dies nur unter Last passiert und im Leerlauf oder bei einer CPU-Temperatur von 85°C wieder auf die normale Frequenz heruntergestuft wird.

[Turbo-Modus]: http://www.raspberrypi.org/archives/2008
