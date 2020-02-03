# My awesome Project
Dieses Projekt ist ein Nachbau des Spiels "Space Invaders". Einige Funktionen des Originalspiels sind bereits möglich, jedoch längst nicht alle, da es kein fertig geschriebenes Programm ist. Man kann mit einem Spaceship Invaders abschießen, sowie auch von Invaders abgeschossen zu werden.
Dieses Spiel war das Projekt von IoT - Erstsemestern, um JavaScript zu lernen.
Es basiert auf dem Grundgerüst unseres Professors Florian Geiselhart, welches schon einige Funktionen enthielt. Mit dieser Basis haben wir dann das Spiel weiterprogrammiert.

## Usage
Um das Spiel zum Laufen zu bringen, muss man auf GitHub die html - Datei in einem beliebigen Browser öffnen. Es startet automatisch, sobald die Seite geladen hat. Nun bewegen sich die Invaders langsam von links nach rechts, rücken eine Reihe nach unten und bewegen sich nun nach links. Mit den "links" und "rechts" Pfeiltasten lässt sich die Position des Spaceships verändern. Mit der Leertaste kann man nun Bullets in Richtung der Invaders schießen. Bei einem Treffer explodieren die Invaders und der Score (links oben in der Ecke) zählt um eins hoch. Möchte man die Invaders schießen lassen, so muss man die Pfeiltaste "unten" drücken. Momentan können leider nur alle Invaders gleichzeitig auf das Spaceship schießen. Durch das Hindernis kann man sich vor den Kugeln schützen. Eigentlich müsste es Stück für Stück kaputt gehen, jedoch verschwinden zu diesem Zeitpunkt lediglich die Kugeln. Sobald man getroffen wurde, ist das Spiel vorbei, hat man alle Invaders abgeschossen, so hat man das Spiel gewonnen. Durch einen Button links oben in der Ecke, kann man ein neues Spiel beginnen.

## Structure
**Klassen:**
* **Invader:** Eine Klasse um ein Invader in Code abzubilden. Sie enthält diese Eigenschaften:
  * `width`: Die Breite des Invaders
  * `height`: Die Höhe des Invaders
  * `x`: Die x-Position des Invaders
  * `y`: Die y-Position des Invaders
  * `appearance`: Wie der Invader aussieht
  * `id`: Die jeweilige ID des Invaders
  
**Funktionen**
  * `function generateInvaders()`: Eine Funktion, die die Invaders generieren lässt.
  * `function fireBulletInvaders()`: Diese Funktion lässt die Invaders Kugeln nach unten schießen.
  * `function renderUI(Treffer)`: Eine Funktion, die den aktuellen Punktestand anzeigen lässt.
  * `function renderBullets()`: Diese Funktion beinhaltet viele verschiedene Aktionen. Als erstes prüft sie, ob eine Kugel einen Invader trifft, wenn ja so lässt sie diesen explodieren und zählt die Trefferanzahl um eins hoch.
  Dann überprüft sie, ob eine Kugel der Invaders das Spaceship trifft, wenn ja so lässt sie das Spaceship verschwinden, friert das Spiel ein und zeigt Game Over auf dem Screen an.
  Desweiteren prüft sie, ob eine Spaceship Kugel ein Obstacle trifft, wenn ja, so lässt sie die Kugel abprallen und verschwinden.
  Sie prüft außerdem, ob eine Invader Kugel ein Obstacle trifft, wenn ja  so lässt sie die Kugel ebenfalls abprallen und verschwinden.
  Zuletzt entfernt sie Kugeln, die nichts getroffen haben und den oberen oder unteren Rand erreichen, und bewegt die Kugeln, einen Schritt weiter und rendert sie dann erneut.
  * `function renderInvaders(invader, pos)`: Eine Funktion, die die Invaders, sobald sie einen Rand erreicht haben, einen Schritt nach unten rücken und in die Entgegengesetzte Richtung weitergehen lassen. Außerdem rendert sie die Invaders.
  * `function removeInvadersAnimation()`: Eine Funktion, die das Array mit der Explosion eines Invaders nur kurz anzeigen lässt und die Invaders dann verschwinden lässt.
  * `function render()`: Eine Funktion die alle Funktionen des Programms rendert und außerdem den "Game Over" oder "Game Won" Screen anzeigt.

## ToDos
1. Man muss die Invaders einzeln und vor allem selbstständig und zufällig schießen lassen.
2. Es könnten noch mehrere Hindernisse hinzugefügt werden.
3. Das Hindernis muss, egal von welchen Kugeln es getroffen wird, Stück für Stück kaputt gehen.
4. Man braucht mehrere Reihen der Space Invaders, wovon eine Reihe immer dieselben Invaders beinhaltet.
5. Sobald ein Invader getroffen wurde, sollten sich die restlichen Invader bis zum Rand weiterbewegen, und nicht davor schon eine Reihe weiter runter rücken, da der abgeschossene Invader noch berücksichtigt wird.
6. Wenn die Invaders eine bestimmte y Höhe erreicht haben, hat man verloren, da man zu langsam war sie abzuschießen.
7. Mehrere Leben des Spaceships.
8. Ein besonderer Invader, der nur kurz auftaucht und bei einem Treffer extra Punkte bringt.
9. Hintergrundmusik und Soundeffekte.
10. Mehrere Level, mit unterschiedlichen Schwierigkeitsstufen.
11. Start- und Pause-Button
