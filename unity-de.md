1. Download
Wir brauchen verschiedene Dateien, um mit Unity f�r die Ouya entwickeln zu k�nnen:
- Java JDK 1.6.045 32bit(!!!)
- Android SDK mit API 16
- Android NDK
und nat�rlich das Ouya Plugin von GitHub, welches dort als zip heruntergeladen werden kann.

2. Plugin
Nachdem alles heruntergeladen wurde entzippen wir das Plugin an einen zentralen Ort. Darin befinden sich folgende Dateien:
 

In Unity �ffnen wir nun ein neues Projekt (auch wenn es sich um ein bestehendes Spiel handelt). Wir navigieren zu den entzippeden Dateien, denn hierbei handelt es sich um ein Unity Projekt.
Nachdem Unity das Projekt ge�ffnet hat, starten wir Unity neu, um die Plugins zu laden. Wichtig: Nichts im Projekt ver�ndern, sonst funktioniert es nicht mehr!

 

Nach dem Neustart befinden sich in der Men�leiste von Unity zwei neue Reiter "OUYA" und "NGUI". Wir klicken auf "OUYA" und Exportieren das "Core Package", das "StarterKit Package" und das "Examples Package". Es empfiehlt sich, diese an einen Ort zu speichern, da wir diese gleich ben�tigen.
Nun �ffnen wir mit Unity unser Spiel, das wir auf die Ouya-Konsole bringen wollen. Nachdem das Projekt geladen hat, �ffnen wir den Windows Explorer und navigieren zu dem Ordner, indem wir die Packages exportiert haben. Diese ziehen wir einfach in die Assets unseres Spiels.
Nach einem etwas l�nger dauerndem Import wird Unity wieder neugestartet. Um zu �berpr�fen, ob alles geklappt hat gehen wir unter "Edit" dann "Project Settings" und w�hlen "Input". Wenn das Plugin richtig importiert wurde, gibt es hier nun 121 Axen (f�r die m�glichen 4 Controller, die man mit der Ouya verbinden kann). Das Plugin ist nun korrekt importiert und kann eingerichtet werden.

3. Einrichten des Plugins, Installation
Zun�chst stellen wir fest, ob unsere gew�hlte Plattform Android ist, das die Ouya-Konsole auf Android basiert. Seit Mai ist das Android Plugin kostenlos f�r Unity verf�gbar, und somit ist auch die Entwicklung f�r die Ouya kostenfrei.
Dazu gehen wir unter "File" dann "Build Settings" und w�hlen dann Android aus. Anschlie�end klicken wir auf "Switch Platform", sofern Android nicht schon ausgew�hlt ist.

 

Nun installieren wir die Android SDK. Dies hier zu erkl�ren, w�rde den Rahmen des Tutorials sprengen, es gibt aber gen�gend Tutorials zu diesem Thema im Internet. Nach erfolgreicher Installation der SDK, und dem Download der API 16 (die wir f�r die OUYA brauchen), muss der Pfad der SDK noch in Unity angegeben werden: Und zwar einmal f�r Unity und f�r das Ouya-Plugin.

Zun�chst �ffnen wir "Edit" und "Preferences". Im sich �ffnenden Fenster w�hlen wir den Reiter "External Tools", und k�nnen hier den Pfad der Android SDK angeben.

 

Nun �ffnen wir das "Ouya Panel". Dazu gehen wir unter "Window" in Unity auf "Open Ouya Panel". Das sich �ffnende Fenster ist das Kontrollzentrum f�r die Ouya-Konsole. Hier kann �berpr�ft werden, ob der Code stimmt und (f�r Unity Pro) auch direkt die apk-Datei erstellt werden. Uns interessiert zun�chst der Button "Android SDK", da hier nocheinmal der Pfad f�r die SDK angeben werden muss. Wenn dies erfolgreich war, werden die Pfadangaben scharz gedruckt, sollte etwas fehlen (zum Beispiel die API16) wird dies als grau angezeigt.

 

Nun installieren wir die heruntergeladene Java JDK und die Android NDK. Nach der Installation wird im Ouya-Panel unter dem jeweiligen Button der Pfad der installierten Dateien angeben - das hei�t wir sollten uns diesen bei der Installation m�glichst merken. Wenn wir alles richtig gemacht haben, ist kein Pfad schwarz gedruckt - dann hat das Ouya-Panel alle Dateien gefunden.
Bei "Android NDK" k�nnte der Pfad zu "NDK Make" graugedruckt sein: Dazu gibt es den Button "Select NDK Make Path...". Die make.exe lag bei mir an einer anderen Stelle als vorgesehen, vielleicht ist das bei euch ja auch der Fall.

 

Nun m�ssen nur noch Einstellungen in den Build Settings von Android vorgenommen werden, dann k�nnen wir auch schon f�r die Ouya builden.

4. Build Settings
Wir gehen zur�ck zu den Build Settings, und �ffnen dort die "Player Settings" von Android. Hier k�nnen nun alle f�r einen Android Build relevanten Dinge, wie der Name der App oder das Icon festgelegt werden. Auch hier empfiehlt es sich anderweitig nachzusehen, was alles gebraucht wird. Wir sehen uns nur die Einstellungen an, bei denen sich die Ouya von einem normalen Android Build unterscheidet. Unter "Resolution and Presentation" muss die Orientation auf "Landscape Left" gestellt werden - alles andere w�rde unser Spiel auf dem Kopf starten lassen.
Unter "Other Settings" muss das API Level auf 16 gestellt werden. Dazu w�hlen wir unter "Minimum API Level" die Android Version 4.1 "Jelly Bean" aus, bei der es sich um Version 16 handelt.
Nun sollten wir noch den Bundle Identifier eingeben und unserem Spiel einen Namen und eine Firma geben - das ist das mindeste was f�r einen Android Build gebraucht wird.

5. OUYA Szene
Bevor wir das Spiel builden k�nnen m�ssen wir noch die Ouya-Szene mit dem Ouya-GameObject in unser Projekt einf�gen. Diese finden wir in den Assets unter "OUYA" -> "StarterKit" -> "Scenes" und dann "SceneInit". Diese Szene �ffnen wir und bearbeiten das "OuyaGameObject". Erstens entfernen wir den Haken bei "Use Legacy Input" (da wir sp�ter einen OuyaInput in unseren Scripten benutzen) und geben unter "DEVELOPER_ID" unser ID an, die wir beim Einloggen in unser Developer Konto bei devs.ouya.tv auf dem Startbildschirm pr�sentiert bekommen. Nun m�ssen wir noch beim "OuyaSceneInit" Objekt die erste Szene unseres Spieles angeben, die beim Starten des Spiels geladen werden soll.

 

Die fertige Szene wird gespeichert und in den "Player Settings" vor alle andern gesetzt. Nun wird beim Starten des Spiels als erstes die OuyaInitScene geladen, die sich mit unserem Entwicklerkonto verbindet und dann automatisch das eigentliche Spiel l�dt.

6. Builden
Das wars auch schon, nun k�nnen wir unser Projekt im "OuyaPanel" mit den PlayerSettings verkn�pfen um den Build zu erm�glichen - Dazu wird unter dem Button "OUYA" der Button "Sync Bundle ID" ausgew�ht. Das Ouya-Plugin synchronisiert nun den Namen und den Bundle Identifier mit dem Android Manifest, welches f�r die Ouya ben�tigt wird.

 

Anschlie�end k�nnen wir auf "Compile" klicken um unser Projekt von dem Ouya-Plugin �berpr�fen zu lassen. Sollten in der Console keine kritischen Fehler auftauchen, ist das Projekt fertig zum exportieren. Besitzer einer Pro-Lizenz k�nnen dies direkt aus dem Ouya-Panel heraus, Standartbenutzern ist das nicht erlaubt. Das macht allerdings nichts, denn das Ouya-Panel arbeitet genauso mit dem Android-Builder von Unity. Wir gehen also wieder in die "Player Settings" und klicken dort auf den Button "Builden". Die erzeugte apk-Datei kann auf die Ouya geladen werden und dort erfolgreich gestartet werden.


Fertig! Dein Game l�uft nun auf der OUYA. Im n�chsten Teil k�mmern wir uns um den Input der Ouya-Controller, 
