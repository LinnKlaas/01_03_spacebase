# Game: Space Invaders
Dieses Projekt ist ein Nachbau des Spiels "Space Invaders". Einige Funktionen des Originalspiels sind bereits möglich, jedoch längst nicht alle, da es kein fertig geschriebenes Programm ist. Man kann mit einem Spaceship Invaders abschießen, sowie auch von Invaders abgeschossen werden. Hier einmal ein Screenshot, wie das momentane Spiel aussieht: <br><br/>
<img src = "Bildschirmfoto 2020-02-04 um 13.48.43.png" width="860"/> <br><br/>
Dieses Spiel war das Projekt von IoT - Erstsemestern, um JavaScript zu lernen. Als Inspiration diente ein YouTube - Video des ursprünglichen Spiels.
Es basiert auf dem Grundgerüst von unserem Professor Florian Geiselhart, welches schon einige Funktionen enthielt. Mit dieser Basis haben wir dann das Spiel weiterprogrammiert. Hier bekommt man die Base her: https://github.com/hfgcoding/01_03_spacebase <br><br/>
<img src = "Bildschirmfoto 2020-02-04 um 13.26.59.png"/>

## Usage
Um das Spiel zum Laufen zu bringen, muss man nur das GitHub Repository downloaden und danach die html - Datei in einem beliebigen Browser öffnen. Es startet automatisch, sobald die Seite geladen hat. Nun bewegen sich die Invaders langsam von links nach rechts, rücken eine Reihe nach unten und bewegen sich nun nach links. Mit den "links" und "rechts" Pfeiltasten lässt sich die Position des Spaceships verändern. Mit der Leertaste kann man nun Bullets in Richtung der Invaders schießen. Bei einem Treffer explodieren die Invaders und der Score (links oben in der Ecke) zählt um eins hoch. Möchte man die Invaders schießen lassen, so muss man die Pfeiltaste "unten" drücken. Momentan können leider nur alle Invaders gleichzeitig auf das Spaceship schießen. Durch das Hindernis kann man sich vor den Kugeln schützen. Eigentlich müsste es Stück für Stück kaputt gehen, jedoch verschwinden zu diesem Zeitpunkt lediglich die Kugeln. Sobald man getroffen wurde, ist das Spiel vorbei, hat man alle Invaders abgeschossen, so hat man das Spiel gewonnen. Durch einen Button links oben in der Ecke, kann man ein neues Spiel beginnen.

## Structure
**Klassen:**
* **Invader:** Eine Klasse um ein Invader in Code abzubilden. Sie enthält diese Eigenschaften:
  * `width`: Die Breite des Invaders (Property, 5 Pixel die gespiegelt werden (aufgrund Symmetrie) -> also insgesamt 10 Pixel)
  * `height`: Die Höhe des Invaders (Property, 5 Pixel)
  * `x`: Die x-Position des Invaders (Property)
  * `y`: Die y-Position des Invaders (Property)
  * `appearance`: Wie der Invader aussieht (Property, wird jedes Mal neu generiert)
  * `id`: Die jeweilige ID des Invaders (Property)
  
**Funktionen**
  * `function newGame()`: Eine Funktion, die ein neues Spiel generiert. Durch eine for - Schleife werden fünf verschiedene, zufällige Invaders generiert, sowie ein Obstacle in das Array "obstacles" gepusht. Die Funktion wird ganz am Schluss aufgerufen.
  * `function generateInvaders()`: Eine Funktion, die die Invaders generieren lässt. Sie lässt fünf mal (da die Breite des Invaders zehn ist, aber der Körper nach der Hälfte gespiegelt wird) eine zufällige Zahl erstellen, ist diese Zahl gleich oder größer 0.5, so zeichnet sie ein "#" an diese Stelle in das Array "invaderLine" (so hat man eine 50% Verteilung der Charaktere). Das wiederholt sie fünf mal, da die Höhe des Invaders fünf ist. Diese fünf Zeilen befinden sich nun alle im Array "invaderLine", welches nun in das Array "invaderLines" gepusht wird. Zum Schluss der Funktion, wird ein neues Objekt der Klasse "Invader" erzeugt, welches dann in die Klasse "Invader" gepusht wird.
  * `function fireBullet()` und `function fireBulletInvaders()` lässt das Spaceship, beziehungsweise die Invaders Kugeln abfeuern. Hier wird sicher gestellt, dass diese auch von der richtigen Position aus abgefeuert werden. Die Funktion wird mit einem keycode aufgerufen.
  * `function renderBullets()`: Diese Funktion beinhaltet viele verschiedene Aktionen. Als erstes prüft sie, durch zwei for - Schleifen und einer if - Bedingung, ob eine Kugel einen Invader trifft, wenn ja so lässt sie diesen explodieren und zählt die Trefferanzahl um eins hoch.
  Dann überprüft sie, ob eine Kugel der Invaders das Spaceship trifft, wenn ja so lässt sie das Spaceship verschwinden, friert das Spiel ein und zeigt Game Over auf dem Screen an. Das geschieht mit einer if - Bedingung in einer for - Schleife.
  Desweiteren prüft sie, ob eine Spaceship Kugel ein Obstacle trifft, wenn ja, so lässt sie die Kugel abprallen und verschwinden.
  Sie prüft außerdem, ob eine Invader Kugel ein Obstacle trifft, wenn ja  so lässt sie die Kugel ebenfalls abprallen und verschwinden. Beide Male prüft sie das mit einer doppelten for - Schleife mit einer if - Bedingung.
  Zuletzt entfernt sie Kugeln, die nichts getroffen haben und den oberen oder unteren Rand erreichen, und bewegt die Kugeln, einen Schritt weiter und rendert sie dann erneut.
  * `function renderInvaders(invader, pos)`: Eine Funktion, die die Invaders, sobald sie einen Rand erreicht haben, mit if - Bedingungen, einen Schritt nach unten rücken und in die Entgegengesetzte Richtung weitergehen lassen. Außerdem rendert sie die Invaders: Die ursprüngliche Breite (fünf) der Invader, wird hier nun gespiegelt, sodass der Körper symmetrisch aufgebaut ist. Die Startposition einer Invader Reihe wird hier festgelegt, sowie der Abstand zwischen den einzelnen Invadern.
  * `function removeInvadersAnimation()`: Sobald ein Invader abgeschossen wird, zeigt es an dieser Stelle durch die if - Bedingung in renderBullets() eine "Explosion" an. Da diese aber nur kurz anzeigt werden soll, habe ich diese Funktion erstellt. In einer if - Bedingung in einer for - Schleife, lasse ich mit "new Date().getTime() - invaders[i].exploded > 5" die Explosion nur für fünf Millisekunden anzeigen und ersetze diese dann mit einem leeren String. So ist nun an der Stelle, an der der Invader war, nichts mehr zu sehen.
  * `function renderUI(Treffer)`: Diese Funktion zeigt mithilfe "renderStr = setCharsAt", den Punktstand oben links in der Ecke an. Außerdem setzt sie bei einer Trefferzahl von fünf die Variable "gameWon" auf true, sodass die Funktion "render()" den Game Won Screen anzeigen kann.
  * `function render()`: Eine Funktion die alle Funktionen des Programms rendert und außerdem mit einer if - Bedingung prüft, ob der "Game Over" oder "Game Won" Screen anzeigt werden muss.
<br><br/>
Bei Beginn des Spiels werden also durch "newGame()" fünf Invaders generiert, welche sich durch "renderInvaders()" bewegen. Diese kann man durch das Spaceship mit Kugeln ("fireBullet()") beschießen. Falls man einen Invader trifft, so wird aufgrund "renderBullets()" und "removeInvadersAnimation()" der Invader explodieren und verschwinden, sowie der Punktestand um eins hochgezählt werden. Hat man alle getroffen, so hat man das Spiel gewonnen und der Screen friert ein und zeigt "YOU WON THE GAME", da die Variable "gameWon" in "renderUI()" nun auf true gesetzt wird. Sollte eine Kugel der Inavders ("fireBulletInvaders()") das Spaceship treffen, so hat man das Spiel verloren, da die Variable "gameOver" in "renderBullets()" nun auf true gesetzt wird. Treffen Kugeln das Obstacle, so werden diese in "renderBullets()" entfernt.

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
12. Highscore
