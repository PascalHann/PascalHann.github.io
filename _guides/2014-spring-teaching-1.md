---
title: "Git beginners guide"
collection: guides
permalink: /guides/git-beginners-guide
---

This is a beginners guide for git. I originally wrote it for students at the technical university Vienna and migrated it from [here](https://gist.github.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6#file-gitbeginnerguide-md), that is why it is written in german.

## Inhaltverzeichnis

- [Inhaltverzeichnis](#inhaltverzeichnis)
- [Vorwort](#vorwort)
- [Software](#software)
  - [Git Bash und Git Gui](#git-bash-und-git-gui)
  - [Gitkraken](#gitkraken)
  - [Git und IntelliJ](#git-und-intellij)
- [Erste Schritte](#erste-schritte)
- [Git Funktionsweise](#git-funktionsweise)
  - [Erster Commit](#erster-commit)
  - [Branching and Merging](#branching-and-merging)
- [Git Workflow](#git-workflow)
  - [Branching Strategien](#branching-strategien)
    - [Personen-Branches](#personen-branches)
    - [Feature-Branches](#feature-branches)
- [Schlusswort](#schlusswort)
- [Troubleshooting](#troubleshooting)
  - [Gitkraken SSH Troubleshooting](#gitkraken-ssh-troubleshooting)
- [Further Reading](#further-reading)

## Vorwort

Das Ziel dieses Dokuments ist es, Beginner_Innen die noch nie oder selten mit Git gearbeitet haben, ein Set an Hilfestellungen, Tipps und Tricks zu Verfügung zu stellen. Dabei richte ich mich in erster Linie an Informatikstudierende, die im Rahmen einer Lehrveranstaltung, wie zum Beispiel 'Objektorientiertes Programmieren' (OOP) von der TU Wien, mit Git arbeiten sollen und dafür bereits ein Git Repository gestellt bekommen haben. Ich werde daher nicht auf das Erstellen von Repositories oder das Hosten und Verwalten von Git Servern eingehen. (Es sei denn ich erfahre das dafür Bedarf besteht)  

Zusätzlich sei gesagt, dass ich mit Windows Systemen arbeite, daher werde ich mich in erster Linie auf die Verwendung von Git auf Windows beziehen. Die vorgestellte Software bezieht sich ebenfalls auf die jeweilige Windows Version. Nichtsdestotrotz sollten sich die meisten Informationen ohne Weiteres auch auf andere Betriebssysteme anwenden lassen.

## Software

Um mit Git arbeiten zu können, müsst ihr es zunächst installieren: [Download Git](https://git-scm.com/downloads)  

Danach seid ihr eigentlich auch schon good to go. Allerdings gibt es eine Vielzahl an Tools, die bei der Verwendung von Git hilfreich sein können und die meisten modernen IDEs haben Git Funktionalität außerdem bereits fest in ihre Software integriert. 

### Git Bash und Git Gui

Mit der standard Windowsinstallation von Git erhaltet ihr sowohl die Git Bash, eine Emulation der klassischen Unix Shell namens 'Bash', als auch eine GUI, welche beide für die Verwendung von Git vollkommen ausreichen. 

Die Git Bash arbeitet mit der klassischen [Syntax die auf Unix Systemen](https://dev.to/awwsmm/101-bash-commands-and-tips-for-beginners-to-experts-30je) zum Einsatz kommt, jedoch braucht man nicht allzu viele Unix Befehle um die Bash für Git zu verwenden und da viele der Übungsumgebungen der TU LVs auf Linux Servern laufen kann man sich hier gleich damit vertraut machen. Alternativ kann man Git auch im Installationsdialog für die Windows Command Prompt (CMD) installieren. 

Mit der mitgelieferten Git GUI habe ich persönlich keine Erfahrung, weshalb ich sie hier nicht besprechen werde. Ihr könnt euch [hier](https://git-scm.com/book/en/v2/Appendix-A%3A-Git-in-Other-Environments-Graphical-Interfaces) selbst einlesen.

### Gitkraken

Gikraken ist eine Alternative zur Git GUI: [Gitkraken](https://www.gitkraken.com)  

Es bietet eine ansprechende und übersichtliche grafische Oberfläche für Windows, Mac und Linux Systeme und die meisten großen Git Services wie GitHub ([Github Student](https://education.github.com/students)) oder GitLab werden speziell unterstützt. Gerade für Anfänger ist die grafische Veranschaulichung meiner Meinung nach sehr hilfreich, allerdings kann es relativ kompliziert werden Gitkraken für die Git Server der TU richtig zu konfigurieren. Schaut euch den [Gitkraken Troubleshooting](#gitkraken-ssh-troubleshooting) Abschnitt dieses Dokuments an, falls ihr Probleme haben solltet.  
Gitkraken ist kostenlos nutzbar, als Teil des [Github Student Developer Packs](https://education.github.com/pack) könnt ihr auch die Pro Version 1 Jahr lang kostenlos nutzen.

### Git und IntelliJ

IntelliJ ist, zumindest zum Verfassungszeitpunkt dieses Dokuments, die standard Entwicklungsumgebung für Java Applikationen an der TU Wien.  
Sowohl die Community als auch die Ultimate Edition (die ihr für Studienzwecke übrigens gratis nutzen könnt, falls das jemand noch nicht wusste: [JetBrains Student](https://www.jetbrains.com/student/)), sowie Android Studio, welches auf IntelliJ basiert, haben Git Funktionalität bereits fest in ihre Software integriert.  
(Wie bereits erwähnt, tun das die meisten Entwicklungsumgebungen wie zum Beispiel auch Visual Studio, Eclipse etc. - Ich möchte in diesem Dokument jedoch speziell auf IntelliJ eingehen, da dies wahrscheinlich die IDE ist, mit der die meisten Informatik Student_Innen an der TU als erstes mit Git zu tun haben werden.)

## Erste Schritte

Wie bereits erwähnt, gehe ich davon aus, dass ihr ein Git Repository zu Verfügung gestellt bekommen habt.
Falls es nicht jedem_r klar sein sollte, dann kann man sich ein Repository vereinfacht wie ein normales Verzeichnis auf einem Computer vorstellen.

Kommunikation mit Git Servern läuft über SSH, daher müsst ihr bevor ihr euch zu eurem Repository verbinden könnt, euren privaten und öffentlichen SSH Schlüssel konfigurieren. Ihr könnt euch leicht ein solches Key Pair generieren lassen, indem ihr diesen Befehl in der Git Bash ausführt:

```Bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Die generierten Keys solltet ihr bei euch lokal im Ordner: **\<Nutzerverzeichnis>/.ssh/** als Dateien **id_rsa** (private key) und **id_rsa.pub** (public key) abspeichern

Nun müsst ihr euren öffentlichen Schlüssel noch am Git Server registrieren damit dieser ihn verwenden kann. Bei GitHub geht das beispielsweise sehr einfach: 

```
Settings > SSH and GPG Keys > New SSH Key > public Key (inhalt von id_rsa.pub) einfügen.
```

Die LVs der TU stellen zuzüglich zu ihren Repositories im Regelfall spezielle für euch registrierte Key Pairs zu Verfügung.
Wie diese beispielsweise für OOP konfiguriert werden (Bei anderen LVs funktioniert es meist analog), erklärt euch @[Luca Eichler](https://gitlab.com/luca.eichler) in seinem [Tutorial](https://gitlab.com/snippets/1902566).

Um nun das Repository zu verwenden, müsst ihr dieses zunächst auf eure Maschine klonen. Dazu dient der Befehl: [git clone](https://git-scm.com/docs/git-clone). In Git Bash könnt ihr folgenden Befehl im Verzeichnis eurer Wahl ausführen, um das Repository am angegebenen Server in dieses Verzeichnis zu kopieren:

```Bash
$ git clone ssh://XXXXXXXX@g0.complang.tuwien.ac.at/oopXXg
```

In Gitkraken könnt ihr entweder euren Github, Gitlab, Bitbucket etc. Account verknüpfen und von dort Repositories klonen, oder ebenfalls über eine URL:

```
File > Clone Repo (Str + N)
```

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/bb6100133868717b0d3ec2f74ff5e3e969a99089/Gitrkraken_Clone_Repo.png)

In IntelliJ ist der Vorgang ebenfalls sehr intuitiv:

```
(VCS) > Checkout from Version Control > Git
```

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/88a571187e58d09d8bfe4d8944295aff256c0420/IntelliJ_clone.png)

## Git Funktionsweise

Jetzt, da ihr Zugriff auf euer Repository habt - wie genau funktioniert eigentlich Git?

Das lokale Repository, das ihr eben auf eure Maschine geklont habt, ist eine Kopie des Verzeichnisses, wie es am Server liegt. Diese beiden Verzeichnisse synchronisieren sich nicht selbstständig. Wenn ihr Änderungen an den Dateien in eurer Kopie macht, werden diese nicht automatisch mit dem Verzeichnis am Server synchronisiert. Ebenso wenig umgekehrt.  
Um die beiden Verzeichnisse zu synchronisieren, gibt es die beiden Git Befehle [git pull](https://git-scm.com/docs/git-pull) und [git push](https://git-scm.com/docs/git-push).  
Vereinfacht gesagt, könnt ihr euch mit `git pull` den Stand des Servers in euer lokales Repository ziehen und mit `git push` umgekehrt euren Stand auf den Server schieben.

Dies ist jedoch eine stark vereinfachte Erklärung. Um den Prozess der Synchronisation in Git zu verstehen, fehlen uns noch zwei weitere wesentliche Konzepte: sogenannte '**Commits**' und '**Branches**'.  

Man kann sich den aktuellen Stand eines Repositorys auch als einen Ausgangsstand und die Summe der Änderungen, die an diesem Ausgangsstand vorgenommen wurden, um zum aktuellen Stand zu gelangen, vorstellen. Diese Änderungen werden in Git zu den erwähnten '**Commits**' zusammengefasst.

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/88a571187e58d09d8bfe4d8944295aff256c0420/Repository_als_Ausgang_plus_Summe_der_%25C3%2584nderungen.png)  
*Aktueller Stand als Ausgangsstand plus Summe der Änderungen. Die Änderungen werden in Commits zusammengefasst und in Anwendungsreihenfolge dargestellt.*  

Nun besteht oft Bedarf in einem Git Repository mehrere Stände gleichzeitig zu verwalten. Beispielsweise könnten zwei Entwickler_Innen gleichzeitig an verschiedenen Komponenten arbeiten und sich dabei nicht in die Quere kommen wollen.
Zu diesem Zweck gibt es die sogenannten '**Branches**'.  
Man könnte einen Branch als einen Kanal für die Änderungen beschreiben. Jeder Branch startet mit einem gewissen Ausgangsstand und verändert sich mit jedem Commit. Der Aktuelle Stand eines Branches ist also wieder der **Ausgangsstand + die Summe seiner Commits**.

In einem frischen Repository gibt es erst mal genau einen Branch den sogenannten '**Master**'. Alle weiteren Branches verzweigen sich von diesem Ursprung. Mit dem `git clone` Befehl kopiert man im Endeffekt den aktuellen Stand des Masters.

![](https://gist.github.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/c34b5e3702feab0743c7184c9cecaa534082479f/GitKrakenBranching.png)  
*Wie man hier sehen kann wurden am Stand des Commits 'ADD content to Test.txt' 2 Branches erstellt. Der Ausgangstand dieser neuen Branches ist der Stand dieses Commits, welcher sich wiederrum aus dem Ausgangsstand des Branches, aus dem die neuen Branches gezogen wurden - in diesem Fall der Master - und der Summe aller Commits bis zu dem Commit, an dem die neuen Branches erstellt wurden, zusammensetzt.  
Warum das Ganze? Anhand dieser Baumstruktur lassen sich alle Änderungen, die an einem Repository gemacht wurden, nachvollziehen und noch besser: man kann jeden Stand jedes Commits jederzeit als Ausgangspunkt eines neuen Branches verwenden, bzw. einen Branch jederzeit auf den Stand eines älteren Commits zurücksetzen.*  

Bevor wir nun unseren ersten eigenen Commit erstellen, möchte ich noch einmal daran erinnern, dass das **lokale** Repository eine **Kopie** des Server Repositorys darstellt. Dies gilt auch für die einzelnen Branches.  
Die Branches des Server Repositorys werden in euer lokales Repository als **lokale** Branches kopiert. Wichtig ist dabei, und das ist eine häufige Fehlerquelle: Der Stand auf dem sich ein **lokaler** Branch befindet, ist **nicht zwangsweise derselbe Stand**, auf dem sich der entsprechende **Branch am Server befindet**.  
Zur Erinnerung, die Synchronisation der lokalen und Server Branches muss bewusst mithilfe der Befehle `git pull` und `git push` vorgenommen werden.

### Erster Commit

Mit dem aus dem Weg, könnt ihr nun euren ersten Commit erstellen.  
Um sicherzustellen, dass sich in der Zwischenzeit - seit dem Klonen - der Stand am Server nicht verändert hat, führen wir als Erstes einen Pull durch.   
Der Befehl hierfür ist simpel. Öffnet einfach die Git Bash im Verzeichnis eures Repositorys und gebt Folgendes ein:

```Bash
$ git pull
```
In Gitkraken gibt es einen eigenen 'Pull' Button dafür und in Intellij können wir entweder die Schaltfläche am rechten oberen Bildschirmrand(STRG - T), oder das Menü **VCS > Git > Pull** verwenden.

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/e3795d5bdc6cab48fc004094fc615142817cff1c/Gitkraken_Navbar.png)  
*Aktionsleiste in Gitkraken mit Pull und Push Button*

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/e3795d5bdc6cab48fc004094fc615142817cff1c/IntelliJ_Navbar.png)  
*Aktionsleiste in Intellij mit Git Pull und Commit Buttons*

In jedem Fall wird Git sich nun den neusten Stand vom Server ziehen, und ihr könnt unbesorgt einen Commit erstellen. Hierzu nehmt ihr als Erstes einfach eine beliebige Änderung an den Dateien in eurem lokalen Repositorys vor. Man könnte beispielsweise eine simple Hello World Applikation hinzufügen.

Seid ihr mit euren Änderungen zufrieden, müsst ihr diese nun zu einem Commit zusammenfassen.  
In der Konsole könnt ihr hierzu die Befehle [git add](https://git-scm.com/docs/git-add) und [git commit](https://git-scm.com/docs/git-commit) verwenden. Der Befehl [git status](https://git-scm.com/docs/git-status) zeigt euch außerdem an, welche Dateien Änderungen aufweisen und hilft euch die Übersicht zu behalten, wenn ihr mit der Konsole arbeitet. Grafische Tools wie Gitkraken markieren geänderte Dateien von alleine.

Mit `git add <Filename>` könnt ihr eure Änderungen an einzelnen Dateien zum Commit freigeben. Man nennt diesen Prozess auch 'staging'. Nachdem ihr so eure geänderten Dateien freigegeben habt, könnt ihr mit `git commit` den Commit finalisieren, auch 'committen'.  
Sobald ihr den Befehl ausführt, verlangt Git von euch, dass ihr eine 'Commit Message' eingebt. Dieser kurze Text soll beschreiben, was ihr geändert habt. Mehr zu Commit Messages im Abschnitt [Git Workflow](#git-workflow).

In Gitkraken gibt es einen eigenen Staging-Bereich für diesen Vorgang und in IntelliJ erreichen wir eine ähnliche Funktion über die Commit Schaltfläche (STRG - K).

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/6e3d69340b1e90c1853136ed95620de10070cb30/Gitkraken%2520Staging.png)  
*Gitkraken Staging Bereich*

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/6e3d69340b1e90c1853136ed95620de10070cb30/IntelliJ_Commit.png)  
*IntelliJ Commit Dialog*

Euer lokaler Branch wird automatisch auf den neuen Commit upgedatet, jedoch ist dieser Commit vorerst noch nur **lokal**. Wenn zu diesem Zeitpunkt jemand vom Server pullen würde, würde er oder sie diese Änderungen nicht erhalten. Wir müssen den Stand am Server erst mit unserem synchronisieren, indem wir mit `git push` unsere lokalen Commits auf den Server schieben.

### Branching and Merging

Nun da ihr euren ersten Commit verfasst habt, ist es an der Zeit, ein weiteres, wichtiges Konzept von Git anzusprechen: '**merging**'.

Hierzu ein kleines Beispiel zur Motivation:  
Ich und meine Kollegin Lisa arbeiten gemeinsam an einem Projekt und verwenden Git zur Versionskontrolle. Wir möchten gleichzeitig Änderungen an der Datei 'HelloWorld.java' vornehmen und arbeiten im selben Branch.  
Wir nehmen beide unsere gewünschten Änderungen vor, Lisa ist etwas früher fertig als ich. Sie committet ihre Änderungen und pusht diese auf den Server. Sie informiert mich über ihre Änderungen und ich führe einen Pull durch, um ihre Änderungen zu erhalten.  
Was geschieht nun mit 'HelloWorld.java'? Welche Änderungen werden übernommen? Meine oder Lisas?

Um diese Frage zu beantworten, müssen wir verstehen, was im Hintergrund abläuft. Immer wenn Git einen Stand von einem Branch auf einen anderen übertragen soll, führt es einen '**Merge**' durch. Dabei werden die Dateien der beiden Stände miteinander verglichen, um zu entscheiden, wie diese zu einem neuen Stand zusammengefügt werden können.  
Selbst bei einem simplen Pull oder Push, wo man vielleicht annehmen könnte, dass man sich ja am selben Branch befindet, wird in Wahrheit ein Merge des lokalen und des Server Branches durchgeführt.

Git ist sehr gut im Vergleichen von Dateien und kann, sofern die zu mergenden Änderungen nicht an denselben Stellen, also an denselben Zeilen innerhalb der Dokumente, vorgenommen wurden, in der Regel selbstständig einen Merge durchführen.   
Liegen jedoch Änderungen an denselben Zeilen vor, kommt es zu einem sogenannten 'Merge Konflikt' und Git benötigt eine Entscheidung vom User, wie vorzugehen ist.

Ihr könnt hierzu manuell auswählen, welche Zeilen der beiden Quellen in den neuen gemergten Stand übernommen werden sollen und diese dann zu einem neuen Merge Commit zusammenfassen.

Im aktuellen Beispiel von mir und Lisa würde der Pull eine Meldung wie diese produzieren:

```Bash
CONFLICT (content): Merge conflict in HelloWorld.java
Automatic merge failed; fix conflicts and then commit the result.
```
Mit `git status` kann man sich auch anzeigen lassen. welche Dateien Konflikte aufweisen und bereinigt werden müssen.  
Git fügt diesen Dateien an den problematischen Stellen automatisch Markierungen hinzu:

```Java
<<<<<<< HEAD
System.out.printLn("Hello World");
=======
System.out.printLn("Lisa sagt Hallo");
>>>>>>> Lisas Commit
```

Der erste Code Block, gekennzeichnet durch HEAD bis zur Trennlinie, stammt aus meinen Änderungen, während der zweite Block von Lisas Commit stammt.  
Ich entscheide, dass Lisas Code an dieser Stelle besser geeignet ist und lösche daher meine Zeile sowie die von Git eingefügten Marker aus HelloWorld.java.  
Anschließend erstelle ich mit `git add HelloWorld.java` und `git commit`
einen neuen Merge Commit, so wie bereits besprochen.

In diesem Beispiel haben wir uns mit dem automatischen Mergen, das bei einem Pull bzw. Push passiert, befasst. Doch will man oft eher absichtlich zwei verschiedene Branches mergen.  
Gehen wir hierfür auch ein kurzes Beispiel durch:
Damit sich Lisa und ich nicht ständig in die Quere kommen und viel Zeit mit Mergen verbringen müssen, erstelle ich einen eigenen Branch für mich. Dazu nutze ich den Befehl [git branch](https://git-scm.com/docs/git-branch).  
Ohne Argumente kann ich mir damit alle **lokalen** Branches in meinem Repository anzeigen lassen. Mit dem Argument `-r` kann ich mir die Branches am Server und mit `-a` sowohl als auch anzeigen lassen.  
Aktuell gibt es nur den Master. Mit  

```Bash
$ git branch pasci_branch
```
erstelle ich den neuen **lokalen** Branch 'pasci_branch' mit dem aktuellen Commit des Branches, auf dem ich mich gerade befinde, also des Masters, als Ausgang.  
Mit dem Befehl [git checkout](https://git-scm.com/docs/git-checkout) oder [git switch](https://git-scm.com/docs/git-switch) wechsle ich nun zu meinem neuen Branch:

```Bash
$ git checkout pasci_branch
```
Damit meine Gruppenmitglieder diesen Branch auch am Server sehen können, führe ich einen push durch, lege dabei einen entsprechenden Branch am Server an und konfiguriere meinen **lokalen** Branch dazu, auf diesen neuen Branch am Server zu pushen bzw. davon zu pullen. Man kann in so einem Fall den Branch am Server auch als '**upstream**' vom lokalen Branch bezeichnen:

```Bash
$ git push --set-upstream origin pasci_branch
```

Nun nehme ich Änderungen auf diesem neuen Branch vor. Ich überarbeite HelloWorld.java erneut. Sobald ich zufrieden bin committe ich meine Änderungen und pushe sie auch auf den pasci_branch am Server.  
Nun bittet mich Lisa meine Änderungen in den Master zu mergen damit sie auf diese aufbauen kann. Hierzu verwende ich den Befehl [git merge](https://git-scm.com/docs/git-merge). Zuerst muss ich in den Branch wechseln in den ich mergen möchte:

```Bash
$ git checkout master
```

Nun merge ich meinen **lokalen** Branch pasci_branch in meinen **lokalen** Master:

```Bash
git merge pasci_branch
```

Wenn möglich führt Git den Merge automatisch durch und erstellt einen Merge Commit, oder im Falle eines Merge Konflikts müssen wir diesen selbst, so wie bereits besprochen, manuell erstellen.  
Damit dieser Merge nun auch am Server stattfindet, müssen wir den Merge Commit nun noch mit einem Push auf den Server schieben.

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/7175f8e1bbbf699724b35b0ce7125a124fa18177/Gitkraken_Branching.png)  
*In Gitkraken werden euch alle Branches auf der linken Seite angezeigt. Um auf einen Branch zu wechseln, braucht ihr nur doppelt draufzuklicken.  
Ihr könnt mit einem Rechtsklick auf einen Commit an dieser Stelle einen **lokalen** Branch erzeugen. Wenn ihr einen Remote Branch, also einen Branch vom Server, auscheckt, der noch keinen entsprechenden lokalen Branch hat, oder wenn ihr einen lokalen Branch pusht, der noch keinen Branch am Server hat, fragt Gitkraken automatisch, wie der entsprechende lokale oder Server Branch heißen soll.  
Ein wichtiger Hinweis: Die angezeigten Remote Branches müssen nicht aktuell sein. Erst bei einem Pull wird diese Anzeige mit dem Server synchronisiert.*  

![](https://gist.githubusercontent.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6/raw/7175f8e1bbbf699724b35b0ce7125a124fa18177/IntelliJ_Branching.png)  
*In IntelliJ erreicht ihr dieses Branching Menü über* **VCS > Git > Branches.** *Es ist relativ selbsterklärend zu bedienen, wenn man das Konzept von Branching verstanden hat.*  

Ich möchte an dieser Stelle nochmal darauf eingehen, dass man sich in Git einen aktuellen Stand immer als Ausgangsstand + Summe der darauf angewandten Änderungen, der Commits ansehen kann und wie man sich in diesem Zusammenhang einen Merge vorstellen kann.  
Bei einem Merge vergleicht Git die Commits des Ausgangsbranches mit den Commits des Zielbranches und versucht anschließend diejenigen, die am Zielbranch noch nicht vorhanden sind, auf diesen anzuwenden. Der neue Stand am Zielbranch ist also quasi dessen **Ausgangsstand + Summe der eignen Commits + Summe der gemergten Commits.**

Mergen bleibt in der Regel recht einfach, solange sich die beiden zu mergenden Branches nicht zu sehr unterscheiden. Versucht man jedoch Branches zu mergen, die bereits sehr weit voneinander abgewichen sind, so kann es zu komplexen Merge Konflikten, die schwer aufzulösen sind, kommen. Darum werden wir uns in der nächsten Sektion mit Strategien, Tipps und Tricks befassen, die helfen sollen, solche aufwendigen Merges zu vermeiden.

## Git Workflow

In dieser Sektion möchte ich ein paar Techniken vorstellen, wie man eine Zusammenarbeit mit Git möglichst reibungslos und erfolgreich gestalten kann.
Ich möchte mit ein paar generellen Tipps anfangen, die ich bei der Arbeit mit Git als hilfreich empfinde:

- **.gitconfig updaten!**  
in eurem Nutzerverzeichnis (Windows Taste + R > .) solltet ihr die Datei '.gitconfig' anlegen, falls diese nicht schon vorhanden ist. Hier könnt ihr festlegen, mit welchem Namen und welcher E-Mail eure Commits assoziiert werden. Aus Gründen der Nachvollziehbarkeit sollte dies unbedingt gemacht werden. Behaltet im Hinterkopf, dass ihr diese Config mit der .gitconfig im .git Ordner in eurem Repository überschreiben könnt, wenn ihr das wollt. [Mehr dazu](https://git-scm.com/book/de/v1/Los-geht%E2%80%99s-Git-konfigurieren).  
Hier eine einfache Vorlage für eure .gitconfig:
```
[user]
	email = your.name@mail.com
	name = Your Name
```
- **.gitignore**  
Legt in eurem Repository eine Datei mit dem Namen '.gitignore' an. In dieser Datei könnt ihr konfigurieren, welche Ordner und Dateitypen Git ignorieren soll. So können beispielsweise userspezifische IDE Konfigurationsdateien ignoriert werden. Ich habe eine [.gitignore](https://gist.github.com/PascalHann/ece75003fcb464b08b8d30eab3142ee6#file-gitignore) an dieses Dokument angefügt, die bereits eine Menge solcher Dateitypen beinhaltet und für die meisten Zwecke ausreichen sollte bzw. angepasst werden kann.
- **Sinnvolle, einheitliche Commit Messages!**  
Commit Messages richtig angewandt können eine enorm nützliche Art sein, euren Code über die Entwicklungsdauer hinweg zu dokumentieren. Um diese so übersichtlich und verständlich wie möglich zu gestalten, solltet ihr euch teamintern auf ein Format einigen. Beispielsweise kann man als erstes Schlagwort in der Commit Message ein einzelnes, großgeschriebenes Wort angeben, welches die Aktion beschreibt, die dieser Commit ausführt: ADD, REFORMAT, UPDATE etc. Auch macht es Sinn, sich vorab auf eine Sprache zu einigen, in der die Messages verfasst werden sollen. Lest [hier](https://git-scm.com/docs/git-commit#_discussion) und [hier](https://fatbusinessman.com/2019/my-favourite-git-commit) mehr zum Thema sinnvolle Commit Messages.
- **Niemals Code, der nicht kompiliert, auf einen Branch comitten, den außer dir noch jemand verwenden soll!**  
Es kann unglaublich anstrengend sein, wenn man sich an die Arbeit machen will und erst mal die Build Fehler eines_r Anderen fixen muss.
- **PULL, PULL, PULL!**  
Lieber einmal zu oft als einmal zu wenig pullen. Wenn man auf einen Branch pusht, der Commits hat, die man noch nicht auf den lokalen Branch gepullt hat, kann der entstehende Merge auf ungewünschte Art verlaufen, ohne dass man es beeinflussen kann. Es ist generell besser, Merges erst lokal durchzuführen und anschließend den fertigen Merge Commit zu pushen. Daher empfehle ich folgendes Vorgehen zu routinieren: **pull > commit > pull > push > pull** zum Pushen, sowie regelmäßige Pulls durchzuführen sofern möglich. (Das ist ein sehr vorsichtiges Vorgehen, aber gerade für Anfänger sinnvoll).
- **Zielbranch in den eigenen Branch mergen und dann erst umgekehrt!**  
Wenn ihr euren eigenen Branch in einen anderen Branch mergen wollt, empfehle ich euch, zuerst diesen Zielbranch in euren eigenen Branch zu mergen. Auf diese Weise könnt ihr Merge Konflikte auf eurem eigenen Branch auflösen und dann ohne Konflikte in den Zielbranch mergen. Der Zielbranch bleibt so möglichst unangetastet.
- **Eigene Branches regelmäßig auffrischen!**  
Wie ich erwähnt habe, werden Merges immer aufwendiger, je mehr die beiden Branches auseinandertreiben. Um das zu verhindern, empfiehlt es sich, den Branch, in den man den eigenen irgendwann überführen möchte, regelmäßig in den Eigenen zu mergen. So wird sichergestellt, dass diese nicht zu sehr voneinander abschweifen.

### Branching Strategien

Je größer ein Projekt und/oder die Gruppe die daran arbeitet wird oder je mehr sich die Arbeitszeiten der Teammitglieder überschneiden desto schwieriger wird es mit nur einem einzigen Master Branch zu arbeiten. Es empfiehlt sich eine einheitliche Branching Strategie anzuwenden um den Arbeitsfluss zu vereinfachen.

Generell ist der Master Stand als der defakto Stand eures Projektes anzusehen. Man könnte ihn als das aktuellste Release eurer Software ansehen. Klone des Repositorys werden vom Master aus erstellt und LV Leitungen der TU bewerten in der Regel den Stand der sich am Master befindet.  
Daher empfehle ich zusätzlich zum Master einen seperaten Entwicklungsbranch zu erstellen, in der Regel 'develop' genannt und nur bei größeren finlen Updates in den Master zu mergen. Quasi wenn man die nächste Version der Software soweit hat das sie veröffentlicht werden kann.

Zusätzlich dazu möchte ich die folgenden 2 Branching Strategien vorstellen: 

#### Personen-Branches

Bei diesem Vorgehen wird für jedes Teammitglied ein eigener Branch vom develop aus gezogen. Die Teammitglieder arbeiten auf diesen solange, bis sie einen Stand fertiggestellt haben und für die Anderen zugänglich machen wollen.  
Dazu mergen sie ihren Personenbranch in den develop. Die Teammitglieder sollten sich den develop regelmäßig in ihre Personenbranches mergen, um up-to-date zu bleiben. Diese Strategie eignet sich besonders für kleinere Projekte, in denen immer nur eine Person gleichzeitig an einem Teil/einer Komponente der Software arbeitet.  
Man kann diese Strategie bei Bedarf um ein 'buddy System' erweitern, um Qualitätssicherung in die Strategie zu integrieren. Dabei bekommt jedes Teammitglied ein anderes als 'buddy'. Wenn ein_e Entwickler_in nun einen Stand erreicht hat, den er oder sie in den develop mergen möchte, so gibt er oder sie seinem bzw. ihrem Buddy Bescheid. Dieser soll dann den Code kontrollieren und ist für den Merge in develop zuständig. So können sich die Teammitglieder gegenseitig kontrollieren.

#### Feature-Branches

Ein anderer, gängiger Ansatz ist, für einzelne Features einer Software Branches anzulegen, diese Features auf diesen Branches zu entwickeln und nach Fertigstellung in den develop zu mergen.
Der Vorteil ist, dass mehrere Personen an einem Feature gemeinsam arbeiten können. Und dass die Merge Commits eine Dokumentation liefern, wann welche Komponente der Software fertiggestellt wurde. 
Feature Branches werden in der Regel nach dem Merge in den develop nicht mehr benutzt und können gelöscht werden. Sollten nachträglich Änderungen an der Komponente vorzunehmen sein, kann man einen eigenen Änderungs/Bug Branch erstellen.  
Dieses Vorgehen eignet sich besser mit steigender Projektgröße und Komplexität.

Natürlich sind diese Strategien als Richtlinien anzusehen und man kann sie beliebig kombinieren und an die eigenen Bedürfnisse anpassen.

## Schlusswort

Obwohl wir hier nur an der Oberfläche gekratzt haben, ist dieses Dokument ohnehin schon viel länger geworden als ich ursprünglich geplant hatte, darum werde ich es erst einmal dabei belassen.
Die besprochenen Informationen sollten genügen, um euch bereit zu machen mit Git durchzustarten und für LVs der TU sollten sie auch erst einmal ausreichen. Ich hoffe, ich konnte jemandem dabei helfen, sich mit Git zurechtzufinden.  
Sollte ich Feedback erhalten, dass Bedarf nach mehr besteht, werde ich diesen Guide eventuell um weitere Themen wie stashing, cherry-picking oder reverting erweitern.

Ich bedanke mich bei @Konsti und @Theresa fürs Korrekturlesen.

## Troubleshooting

### Gitkraken SSH Troubleshooting
<a name="gitkraken_ssh_trouble"></a>

Solltet ihr Probleme mit Gitkraken auf Windows und der Verbindung zu eurem Repository durch SSH haben, könnt ihr Folgendes versuchen:  
Unter **File > Preferences > Authentication** könnt ihr zwischen dem lokalen und dem SSH Agent von Gitkraken wechseln. (Checkbox: Use local SSH Agent)  
Sollte der Gitkraken Agent nicht funktionieren, so versucht es mit dem Lokalen. Sollte der auch nicht funktionieren, könnt ihr versuchen, den Instruktionen in [dieser StackOverflow Antwort](https://stackoverflow.com/a/40720527) zu folgen.  
Wenn es dann immer noch nicht geht, dann weiß ich leider auch nicht mehr weiter. :(

## Further Reading

- [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials)  
Atlassian ist das Unternehmen hinter BitBucket und anderer bekannter Software wie Jira und Confluence.
- [Github Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)
- [Einführung in Branching von git-scm.com](https://git-scm.com/book/de/v1/Git-Branching-Einfaches-Branching-und-Merging)  
git-scm.com wird von verschiedenen Mitgliedern der Git Community betrieben und bietet ein umfangreiches Git Nachschlagewerk. Ich habe in diesem Dokument mehrmals detailierte Beschreibungen von Git Befehlen auf ihrer Seite verlinkt.
- [Weitere Ressourcen zusammengetragen von git-scm.com](https://git-scm.com/doc)