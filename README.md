# Dokumentation zur Lösung der Praxisaufgabe der ESA 11

**DoIt! - Aufgabenverwaltung**: Eine Browseranwendung auf Basis von Vue.js, entwickelt unter Verwendung von Vite.

![DoIt-App_Icon](./public/DoIt-App_Icon.png)

&copy; Sebastian Peschl (2023)

___

## Inhalt

- [Dokumentation zur Lösung der Praxisaufgabe der ESA 11](#dokumentation-zur-lösung-der-praxisaufgabe-der-esa-11)
  - [Inhalt](#inhalt)
  - [Quickstart \[Inhalt\]](#quickstart-inhalt)
  - [Projektbeschreibung \[Inhalt\]](#projektbeschreibung-inhalt)
  - [Verzeichnisstruktur \[Inhalt\]](#verzeichnisstruktur-inhalt)
  - [Dateiübersicht \[Inhalt\]](#dateiübersicht-inhalt)
  - [Zusätzliche Pakete \[Inhalt\]](#zusätzliche-pakete-inhalt)
  - [Projektdateien im Detail \[Inhalt\]](#projektdateien-im-detail-inhalt)
    - [index.html \[Inhalt\]](#indexhtml-inhalt)
    - [main.js \[Inhalt\]](#mainjs-inhalt)
    - [App.vue \[Inhalt\]](#appvue-inhalt)
      - [Script-Bereich von ***App.vue*** \[Inhalt\]](#script-bereich-von-appvue-inhalt)
        - [Imports von ***App.vue*** \[Inhalt\]](#imports-von-appvue-inhalt)
        - [Data-Return-Objekt von ***App.vue*** \[Inhalt\]](#data-return-objekt-von-appvue-inhalt)
        - [Methoden von ***App.vue*** \[Inhalt\]](#methoden-von-appvue-inhalt)
      - [Template-Bereich von ***App.vue*** \[Inhalt\]](#template-bereich-von-appvue-inhalt)
        - [Der Dialog `id="delListDialog"` \[Inhalt\]](#der-dialog-iddellistdialog-inhalt)
        - [Der Dialog `id="createListDialog"` \[Inhalt\]](#der-dialog-idcreatelistdialog-inhalt)
        - [Die Komponente `<Sidebar />` innerhalb von ***App.vue*** \[Inhalt\]](#die-komponente-sidebar--innerhalb-von-appvue-inhalt)
        - [Die Komponente `<Main />` innerhalb von ***App.vue*** \[Inhalt\]](#die-komponente-main--innerhalb-von-appvue-inhalt)
    - [Sidebar.vue \[Inhalt\]](#sidebarvue-inhalt)
      - [Script-Bereich von ***Sidebar.vue*** \[Inhalt\]](#script-bereich-von-sidebarvue-inhalt)
        - [Imports von ***Sidebar.vue*** \[Inhalt\]](#imports-von-sidebarvue-inhalt)
        - [Registrierung der Emits von ***Sidebar.vue*** \[Inhalt\]](#registrierung-der-emits-von-sidebarvue-inhalt)
        - [Registrierung der Props von ***Sidebar.vue*** \[Inhalt\]](#registrierung-der-props-von-sidebarvue-inhalt)
        - [Registrierung der Watcher von ***Sidebar.vue*** \[Inhalt\]](#registrierung-der-watcher-von-sidebarvue-inhalt)
        - [Data-Return-Objekt von ***Sidebar.vue*** \[Inhalt\]](#data-return-objekt-von-sidebarvue-inhalt)
        - [Methoden von ***Sidebar.vue*** \[Inhalt\]](#methoden-von-sidebarvue-inhalt)
        - [Die Methode `created()` von ***Sidebar.vue*** \[Inhalt\]](#die-methode-created-von-sidebarvue-inhalt)
      - [Template-Bereich von ***Sidebar.vue*** \[Inhalt\]](#template-bereich-von-sidebarvue-inhalt)
    - [Main.vue \[Inhalt\]](#mainvue-inhalt)

___

## Quickstart [[Inhalt](#inhalt)]

1. Nach dem das Repository geklont bzw. entpackt wurde, wechseln Sie im Terminal in das entsprechende Verzeichnis.
2. Führen Sie hier den Befehl `npm i` aus um die erfoderlichen Pakete zu installieren.
3. Starten Sie mit `npm run dev` einen Entwicklungsserver und rufen Sie die im Terminal angezeigte IP in Ihrem Browser auf. Führen Sie (wenn gewünscht) Änderungen an den Quelldateien durch.
4. Mit `npm run build` können Sie das Projekt bauen lassen. Im Projektverzeichnis finden Sie nun das Verzeichnis *dist*.

## Projektbeschreibung [[Inhalt](#inhalt)]

Das vorliegende Projekt entstand im Rahmen eines Fernstudiengangs zum Webentwickler und stellt die Lösung für eine Einsendeaufgabe dar.

Die Aufgabenstellung forderte eine einfache ToDo-Liste mit Vue zu erstellen. Es sollten Einträge über ein Formular hinzugefügt werden, sowie über entsprechende Buttons gelöscht und als erledigt markiert werden können. Außerdem sollte die Anwendung zwei Übersichtslisten bereitstellen, welche den Anwender über die noch ausstehenden, sowie die erledigten Aufgaben informiert.

Der Funktionsumfang sowie der Lösungsweg wurden von mir erweitert bzw. modifiziert.  
Neben den geforderten Funktionen bietet meine Lösung folgende Features:

- Jede Aufgabe kann bei der Erstellung von der Anwenderin / dem Anwender, neben einem obligatorischen Fälligkeitsdatum, mit einem Startdatum versehen werden.
- Die Userin / der User kann eine (quasi) unbegrenzte Anzahl von Aufgabenlisten erstellen die es ihr / ihm erlauben Aufgaben nach Themengebieten zu Kategorisieren.
- Neben der geforderten Möglichkeit einzelne Aufgaben löschen zu können, ist es auch möglich ganze Listen inclusive aller entsprechenden Aufgaben zu entfernen.
- Alle Aufgaben werden von der Anwendung automatisch im LocalStorage des Browsers gesichert.
- Zusätlich besteht die Möglichkeit die Aufgaben in einer Datei zu speichern.
- Diese Sicherungskopie kann in die Anwendung importiert werden.
- Die Übersichtsliste der erledigten Aufgaben bietet die Funktion einzelne Aufgaben zu löschen.
- Die gesamte App ist responsive de­signt. Die Anwendung sollte auf jedem Device reibungslos funktionieren und dabei gut aussehen.
- Am oberen Rand der Anwendung wird der Anwenderin / dem Anwender das aktuelle Datum sowie die Uhrzeit angezeigt.

## Verzeichnisstruktur [[Inhalt](#inhalt)]

- / (root)
  - src
    - assets
    - components
  - public
  - node_modules
  - .vscode
  - .git

## Dateiübersicht [[Inhalt](#inhalt)]

| Datei | Pfad | Kategorie | Kurzbeschreibung |
| --- | --- | --- | --- |
| [index.html](#indexhtml-inhalt) | / | html-Datei | Datei zur Darstellung der Anwendung |
| [main.js](#mainjs-inhalt) | /src/ | javascript-Datei | Erstellen und mounten der Anwendung |
| [App.vue](#appvue-inhalt) | /src/ | Vue-Komponente | Wurzelkomponente der Anwendung |
| --- | --- | --- | --- |
| --- | --- | --- | --- |

## Zusätzliche Pakete [[Inhalt](#inhalt)]

Neben den mit Vue mitgelieferten Paketen kommt das Build-Tool Vite zum Einsatz. Darüber hinaus wurden zur Realisation des Projekts die Pakete **lodash** und **file-saver** installiert.

## Projektdateien im Detail [[Inhalt](#inhalt)]

Nachfolgend werden die diesem Projekt zugrunde liegenden Quelldateien und deren Funktionsweise erleutert.

### index.html [[Inhalt](#inhalt)]

Die *index.html* bildet den Darstellungsraum der App. Im `<body>` findet sich ein `div` mit der `id="app"`. Dies ist das Container-Element in dem die Anwendung eingehängt wird.

Das `<script>`-Element vor dem `</body>`-Tag bindet die Datei [*main.js*](#mainjs-inhalt) als **module** ein.

### main.js [[Inhalt](#inhalt)]

Die Datei *main.js* initialisiert und mounted die Anwendung.  
Hierfür wird die Methode `createApp()` aus dem Paket **vue**, sowie die primäre Komponente **App** aus [*App.vue*](#appvue-inhalt) importiert. Außerdem wird die Datei *main.css* importiert welche einige grundlegende Stylin-Parameter bereithält.

Durch aufrufen der Methode `createApp(App)` wird eine neue Vue.js-Instanz erstellt und mit Hilfe der Methode `mount('#app')` im Element mit der `id="app"` (s. [index.html](#indexhtml-inhalt)) im DOM eingehängt.

___

### App.vue [[Inhalt](#inhalt)]

*App.vue* stellt die Wurzelkomponente der Anwendung dar in welcher die Komponenten **Sidebar** ([*Sidebar.vue*](#sidebarvue-inhalt)) und **Main** ([*Main.vue*](#mainvue-inhalt)) eingebunden sind.

Darüber hinaus stellt **App** in ihrem Template modale Dialoge zum Löschen und erstellen von Listen bereit.

#### Script-Bereich von ***App.vue*** [[Inhalt](#inhalt)]

##### Imports von ***App.vue*** [[Inhalt](#inhalt)]

- Komponente **Sidebar**
- Komponente **Main**
- Komponente **CreateListButton**

##### Data-Return-Objekt von ***App.vue*** [[Inhalt](#inhalt)]

| Property | Erläuterung | initialer Wert |
| --- | --- | --- |
| `newListName` | Speicher für den Namen der neu zu erstellenden Liste. Bidirektionale Datenverbindung mit dem `<input>`-Element mit der `id="listName"` ([s. hier](#der-dialog-idcreatelistdialog-inhalt)). | `''` |
| `newListNameTemp` | Temporärer Speicher f. den Namen der neu zu erstellenden Liste. | `''` |
| `listName` | Enthält den Namen einer Aufgabenliste die gelöscht werden soll. | `''` |
| `delListName` | Erhält den Wert von `listName` um den Löschvorgang der Aufgabenliste zu triggern. | `''` |
| `showInfo` | Wert definiert ob eine Infonachricht angezeigt wird. | **false** |
| `changer` | Indikator dessen Wert beim erstellen einer neuen Liste invertiert wird. | **false** |
| `fileOperation` | Wert definiert eine spezifische Dateioperation (import o. export) | `''` |

##### Methoden von ***App.vue*** [[Inhalt](#inhalt)]

| Methode | Erläuterung |
| --- | --- |
| `showCreateListDialog()` | Aneige des modalen Dialogs mit der `id="createListDialog"` |
| `closeCreateListDialog()` | Schließt den modalen Dialog mit der `id="createListDialog"` und setzt den Wert der Property `showInfo` auf **false**. (s. [hier](#data-return-objekt-von-appvue)) |
| `openDelDialog(name)` | Setze den Wert von `listName` (s. [hier](#data-return-objekt-von-appvue)) auf den Wert des der Methode übergebenen Parameters `name` und zeige den modalen Dialog mit der `id="delListDialog"` an. |
| `closeDelDialog()` | Schließe den modalen Dialog mit der `id="delListDialog"`. |
| `triggerListDelete()` | Setze den Wert der Property `delListName` auf den der Property `listName` und rufe die Methode `closeDelDialog` auf. |
| `validString(stringToValidate)` | Prüfe ob der Wert des Parameters ein valider String ist. Die Methode liefert **true** wenn es sich ***nicht*** um einen leeren String handelt und der String ***nicht*** ausschließlich aus Leerzeichen besteht. |
| `createNewList()` | <ol><li>Der Wert der Property `newListName` wird in der Konstanten `listName` gespeichert.</li><li>Es wird geprüft ob es sich bei dem Wert von `listName` um einen validen String handelt. Hierfür wird die Methode `validString(listName)` aufgerufen.</li><li>Wenn der String valide ist, also `validString(listName)` **true** liefert, dann ...</li><ol><li>Setze den Wert der Property `newListNameTemp` auf den Wert von `listName`.</li><li>Schließe den Dialog zum erstellen neuer Listen indem die Methode `closeCreateListDialog()` aufgerufen wird.</li><li>Invertiere den Wert der Property `changer`.</li></ol><li>Wenn `validString(listName)` **false** liefert dann setze die Property `showInfo` auf **true**</li><li>Setze abschließend den Wert der Property `newListName` auf einen leeren String.</li></ol> |
| `triggerFileOp(operation)` | Setze die Property `fileOperation` auf den Wert des übergebenen Paramers `operation` |
| `resetFileOperation()` | Setze die Property `fileOperation` auf einen leeren String zurück. |

#### Template-Bereich von ***App.vue*** [[Inhalt](#inhalt)]

Das ***root***-Element des Templates bildet das `div` mit der `id="primeContainer"`. Dieses Beinhaltete die folgenden Elemente, bzw. Komponenten:

##### Der Dialog `id="delListDialog"` [[Inhalt](#inhalt)]

`id="delListDialog"` stellt für die Anwenderin / den Anwender einen Bestätigungsdialog bereit. Dieser informiert darüber, dass das löschen einer Liste unwiederruflich ist und erwartet eine Reaktion.

Zum triggern einer Reaktion stellt der Dialog zwei Buttons bereit. `id="cancelDelete"` zum abbrechen der Operation und `id="confirmDelete"` zur Bestätigung, dass der Löschvorgang gestartet werden soll.

Beide Buttons sind jeweils mit einer `@click`-Direktive versehen welche die entsprechende Methode ([s. hier](#methoden-von-appvue)) aufruft:

| Button | Methodenaufruf bei `@click` |
| --- | --- |
| `id="cancelDelete"` | `closeDelDialog()` |
| `id="confirmDelete"` | `triggerListDelete()` |

##### Der Dialog `id="createListDialog"` [[Inhalt](#inhalt)]

Der Dialog `id="createListDialog"` stellt der Anwenderin / dem Anwender die Möglichkeit neue Listen zu erstellen zur Verfügung.  
Zur Benennung der neuen Liste wird ein einfaches Eingabeformular angezeigt. Das `<input>`-Element mit der `id="listName"` ist mittels der `v-model`-Direktive mit der Property `newListName` ([s. hier](#data-return-objekt-von-appvue)) verknüpft.

Der Anwenderin / dem Anwender werden zwei Auswahlmöglichkeiten angeboten:

1. Ein Button mit der zum erstellen einer neuen Liste in Gestalt der Komponente `<CreateListButton />`
2. Ein Link mit der `ìd="calcelCreation"` zum abbrechen und schließen des Dialogs.

Der Button, bzw. der Link sind mit `@click`-Direktive versehen, welche entsprechende Methoden ([s. hier](#methoden-von-appvue)) aufrufen:

| Button (Komponente) / Link | Methodenaufruf bei `@click` |
| --- | --- |
| `<CreateListButton />` | `createNewList()` |
| `ìd="calcelCreation"` | `closeCreateListDialog()` |

##### Die Komponente `<Sidebar />` innerhalb von ***App.vue*** [[Inhalt](#inhalt)]

`<Sidebar />` ist eine der primären Komponenten der Anwendung. (Detailierte Informationen zu dieser Komponente finden Sie [hier](#sidebarvue-inhalt))

Die Komponente emittiert Events vom Typ `showCreateListDialogEvent` und `triggerFileOpEvent`. Diese werden hier im Template abgefangen führen zum Aufruf der entsprechenden Methode, `showCreateListDialog()`, bzw. `triggerFileOp`. (s. [hier](#methoden-von-appvue))

Ferner erhält `<Sidebar />` in form des Props `:changeTrigger` den Wert der Property `changer` übergeben.

##### Die Komponente `<Main />` innerhalb von ***App.vue*** [[Inhalt](#inhalt)]

Die Komponente `<Main />` stellt den primären Anzeigebereich der Anwendung dar. (Detailierte Informationen zu dieser Komponente finden Sie [hier](#mainvue-inhalt))

`<Main />` emittiert Events folgender Typen welche zur Ausführung der entsprechenden Methoden (s. [hier](#methoden-von-appvue)), bzw. der dirkten Manipulation einer Property (s. [hier](#data-return-objekt-von-appvue)) führen:

| Event | Methode / Property-Manipulation |
| --- | --- |
| `delListEvent` | `openDelDialog()` |
| `resetNewListNameEvent` | `newListNameTemp = ''` |
| `resetDelListNaveEvent` | `delListName = ''` |
| `fileOpCompleted` | `resetFileOperation()` |

Auch `<Main />` bekommt Werte in Form von Props übergeben. Diese sind:

| Prop | Wert der Property |
| --- | --- |
| `:declaredFileOp` | `fileOperation` |
| `:newName` | `newListNameTemp` |
| `:delListName` | `delListName` |

___

### Sidebar.vue [[Inhalt](#inhalt)]

Die **Sidebar**-Komponente ist eines von zwei primären Komponenten der Anwendung. Neben dem Titel und Subtitel der Anwendung beherbergt die **Sidebar** Tools zum erstellen neuer Aufgabenlisten, sowie zum importieren und exportieren aller Aufgaben.

#### Script-Bereich von ***Sidebar.vue*** [[Inhalt](#inhalt)]

##### Imports von ***Sidebar.vue*** [[Inhalt](#inhalt)]

Hier wird nur die Komponente **CreateListButton** benötigt.

##### Registrierung der Emits von ***Sidebar.vue*** [[Inhalt](#inhalt)]

Die Komponente kann zwei Typen von Events emittieren:

- `triggerFileOpEvent`
- `schowCreateListDialogEvent`

Diese Events werden von der Komponente [***App.vue***](#die-komponente-sidebar--innerhalb-von-appvue-inhalt) gefangen und verarbeitet.

##### Registrierung der Props von ***Sidebar.vue*** [[Inhalt](#inhalt)]

`changeTrigger` ist vom Typ **Boolean** und ist die einzige Prop dieser Komponente.

##### Registrierung der Watcher von ***Sidebar.vue*** [[Inhalt](#inhalt)]

Der Watcher der einzigen Prop dieser Komponente ist `changeTrigger()`. Verändert sich der Wert der Prop `changeTrigger` wird die Methode `checkWindowWidth()` aufgerufen.

##### Data-Return-Objekt von ***Sidebar.vue*** [[Inhalt](#inhalt)]

Einzige Property der Komponente ist `sidebarVisibel` vom Typ **Boolean**. Ihr initialer Wert ist **true**.

##### Methoden von ***Sidebar.vue*** [[Inhalt](#inhalt)]

| Methode | Erläuterung |
| --- | --- |
| `toggleVisibility()` | Invertiert den aktuellen Wert der Property `sidebarVisible`. |
| `checkWindowWidth()` | Manipuliert in Abhängigkeit von der aktuellen Breite des VP den Wert der Property `sidebarVisible`. Ist der ermittelte Wert kleiner als **880px** wird der Wert auf **false** gesetzt, andernfalls auf **true**. Dies Bewirkt ein automatisches Ausblenden der Seitenleist bei Viewports die eine geringere innere Breite als **880px** aufweisen. |

##### Die Methode `created()` von ***Sidebar.vue*** [[Inhalt](#inhalt)]

Die folgenden Operationen werden beim erstellen der Komponente ausgeführt:

- Aufruf der Methode `checkWindowWidth()`
- Registrierung eines EventListeners f. Events vom Typ `resize`. Bei jedem Auftreten dieses Ereignisses wird die Methode `checkWindowWidth()` aufgerufen.

#### Template-Bereich von ***Sidebar.vue*** [[Inhalt](#inhalt)]

Ein `div` mit der `id="sidebar"` stellt das Container-Element dieser Komponente dar. Dieses Element erhält die Klasse `hidden`, wenn die Property `sidebarVisible` den Wert **false** hat. Dies wird durch eine `v-bind:class`-Direktive erreicht.

Dieses Container-Element beherbergt vier Sub-Elemente:

| Sub-Element | Erläuterung |
| --- | --- |
| `div` mit der `id="hideBarButton"` | Eine Schaltfläche zum ein- und ausblenden der Sidebar. Das Element ist mittels einer `@click`-Direktive mit der Methode `toggleVisibility()` verknüpft. |
| `header` | Beinhaltet den Titel und den Subtitel der Anwendung. |
| `div` mit der `id="toolContainer"` | Dieses Element umschließt drei Schaltflächen mit denen der Anwenderin / dem Anwender die Funktionen zum (1) erstellen einer neuen Aufgabenliste, das (2) exportieren aller Aufgaben in eine Datei und das (3) importieren von Aufgaben aus einer Datei verfügbar gemacht werden. <br> Bei (1) wird hierbei als Schaltfläche die Komponente `<CreateListButton />` verwendet. Über eine `@click`-Direktive wird bei einem Klick-Event, unter Verwendung von `$emit()` ein `showCreateListDialogEvent` gefeuert. (Dieser wird innerhalb von ***App.vue*** gefangen und weiter verarbeitet. [s. hier](#die-komponente-sidebar--innerhalb-von-appvue-inhalt)) |
| `footer` | Urheberinformation zur Anwendung |

___

### Main.vue [[Inhalt](#inhalt)]

...