---
id: "Stoppmotion"
title: "Stoppmotion"
language: deutsch
level: Leicht
talkType: Conference #<-- "Conference" "Quickie" "Keynote" -->
speakers:
  - dirk_re
  - jotilux
tags:
  - E
presentation: #http://slideshare.....
videoId: yOP15Ep4gPU
---

Stop motion is an animated-film making technique in which objects are physically manipulated in small increments between individually photographed frames so that they will appear to exhibit independent motion when the series of frames is played back as a fast sequence. Dolls with movable joints or clay figures are often used in stop motion for their ease of repositioning. Stop-motion animation using plasticine figures is called clay animation or "clay-mation". Not all stop motion, however, requires figures or models: stop-motion films can also be made using humans, household appliances, and other objects, usually for comedic effect. Stop motion using humans is sometimes referred to as pixilation or pixilate animation.


# How to
In dieser Anleitung wird beschrieben wie ein Stopmotion Video auf einem Debian-basierten System mit einer USB-Videoquelle erstellt werden kann.
## Installation und Erste Schritte
* Das Programm "Stopmotion" aus den Paketquellen installieren
``` 
sudo apt install stopmotion
```
* Den gewünschten Benutzer der Gruppe "Video" hinzufügen. Bei dem Befehl bitte den Benutzer anpassen.
``` 
sudo usermod -aG Video BENUTZER
```
* USB-Videoquelle anschliessen
* Das Programm "Stopmotion" starten
## Einstellungen
  * In der Menüleiste: Einstellungen -> Stopmotion konfigurieren
    > Die Markierte Zeile gilt als ausgewählt. Mit "Anwenden" wird die auswahl übernommen und ist aktiv
### Video-Gerät
* die Zeile mit "/dev/video0" auswählen, sofern kein anderer Video-Input angeschlossen ist
### Video-Import
* "uvccapture" auswählen
* auf bearbeiten drücken und in dem Eingabefeld "Pre-poll command" muss folgendes stehen
        ```
        uvccapture -d$VIDEODEVICE -x1920 -y1080 -o\$IMAGEFILE
        ```
      * die Auflösung (also x und y) müssen dem entsprechenden Video-Input angepasst werden
### Video export
* die Zeile "mencoder" mit mpeg2 in der Beschreibung
  * In den Einstellungen dieses encoders müssen wie folgt aussehen
        ```
        mencoder "mf://\$IMAGEPATH/*.jpg" -mf w=640:h=480:fps=$FRAMERATE:type=jpg -ovc lavc -lavcopts vcodec=mpeg2video -oac copy -o "\$VIDEOFILE"
        ```
### Aufnahme von Bildern
* mit dem Button mit dem Camcorder-Symbol unten links kann das Live-Bild gestartet werden
* mit dem Kamera-Symbol das darüber erscheint kann abhängig vom eingestellten Modus ein Bild aufgenommen werden
    * Wenn "Mix" eingestellt ist werden die aufgenommenen Bilder zur Orientierung übereinander gelegt. Mit dem Schieber darunter kann eingestellt werden, wie viele Bilder übereinandergelegt werden
      * Jedes Bild muss einzeln aufgenommen werden. Die Aufnahme kann auch mit der Leertaste getriggert werden
    * Es kann auch eine Zeitsteuerung eingestellt werden
       * Den Modus auf "Auto" umstellen und einen Intervall aussuchen (Sekunde, Minute, Stunde). Die Aufnahme wird sofort gestartet.
