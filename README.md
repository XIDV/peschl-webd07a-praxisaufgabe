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
      - [Script-Bereich von ***Main.vue*** \[Inhalt\]](#script-bereich-von-mainvue-inhalt)
        - [Import zusätzlicher Pakete in ***Main.vue*** \[Inhalt\]](#import-zusätzlicher-pakete-in-mainvue-inhalt)
        - [Import von Komponenten in ***Main.vue*** \[Inhalt\]](#import-von-komponenten-in-mainvue-inhalt)
        - [Registrierung der Emits von ***Main.vue*** \[Inhalt\]](#registrierung-der-emits-von-mainvue-inhalt)
        - [Registrierung der Props von ***Main.vue*** \[Inhalt\]](#registrierung-der-props-von-mainvue-inhalt)
        - [Registrierung der Watcher von ***Main.vue*** \[Inhalt\]](#registrierung-der-watcher-von-mainvue-inhalt)
        - [Data-Return-Objekt von ***Main.vue*** \[Inhalt\]](#data-return-objekt-von-mainvue-inhalt)
        - [Methoden von ***Main.vue*** \[Inhalt\]](#methoden-von-mainvue-inhalt)
        - [Die Methode `created()` von ***Main.vue*** \[Inhalt\]](#die-methode-created-von-mainvue-inhalt)
        - [Registrierung der Computed-Properties von ***Main.vue*** \[Inhalt\]](#registrierung-der-computed-properties-von-mainvue-inhalt)
      - [Template-Bereich von ***Main.vue*** \[Inhalt\]](#template-bereich-von-mainvue-inhalt)

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

| Komponente | (Kurz)-Erläuterung |
| --- | --- |
| **Sidebar** | Seitenleiste welche Werkzeuge zum erstellen neuer Listen, zum exportieren der aller Aufgaben als Datei und für den Dateiimport beinhaltet. |
| **Main** | Primärer Anzeigebereich der Anwendung |
| **CreateListButton** | Eine Schaltfäche. |

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
| `closeCreateListDialog()` | Schließt den modalen Dialog mit der `id="createListDialog"` und setzt den Wert der Property `showInfo` auf **false**. ([s. hier](#data-return-objekt-von-appvue-inhalt)) |
| `openDelDialog(name)` | Setze den Wert von `listName` (s. [hier](#data-return-objekt-von-appvue-inhalt)) auf den Wert des der Methode übergebenen Parameters `name` und zeige den modalen Dialog mit der `id="delListDialog"` an. |
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

Beide Buttons sind jeweils mit einer `@click`-Direktive versehen welche die entsprechende Methode ([s. hier](#methoden-von-appvue-inhalt)) aufruft:

| Button | Methodenaufruf bei `@click` |
| --- | --- |
| `id="cancelDelete"` | `closeDelDialog()` |
| `id="confirmDelete"` | `triggerListDelete()` |

##### Der Dialog `id="createListDialog"` [[Inhalt](#inhalt)]

Der Dialog `id="createListDialog"` stellt der Anwenderin / dem Anwender die Möglichkeit neue Listen zu erstellen zur Verfügung.  
Zur Benennung der neuen Liste wird ein einfaches Eingabeformular angezeigt. Das `<input>`-Element mit der `id="listName"` ist mittels der `v-model`-Direktive mit der Property `newListName` ([s. hier](#data-return-objekt-von-appvue-inhalt)) verknüpft.

Der Anwenderin / dem Anwender werden zwei Auswahlmöglichkeiten angeboten:

1. Ein Button mit der zum erstellen einer neuen Liste in Gestalt der Komponente `<CreateListButton />`
2. Ein Link mit der `ìd="calcelCreation"` zum abbrechen und schließen des Dialogs.

Der Button, bzw. der Link sind mit `@click`-Direktive versehen, welche entsprechende Methoden ([s. hier](#methoden-von-appvue-inhalt)) aufrufen:

| Button (Komponente) / Link | Methodenaufruf bei `@click` |
| --- | --- |
| `<CreateListButton />` | `createNewList()` |
| `ìd="calcelCreation"` | `closeCreateListDialog()` |

##### Die Komponente `<Sidebar />` innerhalb von ***App.vue*** [[Inhalt](#inhalt)]

`<Sidebar />` ist eine der primären Komponenten der Anwendung. (Detailierte Informationen zu dieser Komponente finden Sie [hier](#sidebarvue-inhalt))

Die Komponente emittiert Events vom Typ `showCreateListDialogEvent` und `triggerFileOpEvent`. Diese werden hier im Template abgefangen führen zum Aufruf der entsprechenden Methode, `showCreateListDialog()`, bzw. `triggerFileOp`. (s. [hier](#methoden-von-appvue-inhalt))

Ferner erhält `<Sidebar />` in form des Props `:changeTrigger` den Wert der Property `changer` übergeben.

##### Die Komponente `<Main />` innerhalb von ***App.vue*** [[Inhalt](#inhalt)]

Die Komponente `<Main />` stellt den primären Anzeigebereich der Anwendung dar. (Detailierte Informationen zu dieser Komponente finden Sie [hier](#mainvue-inhalt))

`<Main />` fängt Events folgender Typen welche zur Ausführung der entsprechenden Methoden (s. [hier](#methoden-von-appvue-inhalt)), bzw. der dirkten Manipulation einer Property (s. [hier](#data-return-objekt-von-appvue-inhalt)) führen:

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

**Main** definiert den Anzeigebereich für alle weiteren Komponenten / Elemente der Anwendung.  
Hier werden der Anwenderin / dem Anwender neben einem Eingabeformular für neue Aufgaben und die existierenden Aufgabenlisten, eine Übersichtsleiste (am rechten Rand der Anwendung), sowie das aktuelle Datum und die Uhrzeit präsentiert.

Darüber hinaus finden in **Main** alle Operationen (erstellen, löschen, statuswechsel) an Aufgaben bzw. Listen statt.

#### Script-Bereich von ***Main.vue*** [[Inhalt](#inhalt)]

##### Import zusätzlicher Pakete in ***Main.vue*** [[Inhalt](#inhalt)]

| Paket | Erläuterung | Weitere Infos auf *npmjs.com* |
| --- | --- | --- |
| `lodash` | Paket zur Vereifachung von Array-Operationen | [lodash](https://www.npmjs.com/package/lodash) |
| `file-saver` | Paket zum Speichern von Dateien auf Client-Seite  | [file-saver](https://www.npmjs.com/package/file-saver) |

##### Import von Komponenten in ***Main.vue*** [[Inhalt](#inhalt)]

| Komponente | (Kurz)-Erläuterung |
| --- | --- |
| **Tasklist** | Definiert eine Augabenliste. |
| **Inbobar** | Definiert eine Informationsleiste welche Eine Übersicht über ausstehende und erledigte Aufgaben präsentiert. |

##### Registrierung der Emits von ***Main.vue*** [[Inhalt](#inhalt)]

**Main** kann vier Event-Typen emittieren:

- `delListEvent`
- `resetNewListNameEvent`
- `resetDelListNameEvent`
- `fileOpCompleted`

##### Registrierung der Props von ***Main.vue*** [[Inhalt](#inhalt)]

| Prop | Datentyp | Erläuterung |
| --- | --- | --- |
| `newName` | **String** | Definiert den Namen einer neuen Liste. |
| `delListName` | **String** | Definiert den Namen einer zu löschenden Liste. |
| `declaredFileOp` | **String** | Definiert die Art der Dateioperation, die durchgeführt werden soll. |

##### Registrierung der Watcher von ***Main.vue*** [[Inhalt](#inhalt)]

Die Watcher überwachen den Status, bzw. den Wert der entsprechenden Prop und führen bei einer Änderung die definierten Operationen aus:

| Watcher | Erläuterung |
| --- | --- |
| `newName(wert)` | Führt die Methode `addListNames(wert)` aus. |
| `delListName(list)` | Führt die Methode `delList(list)` aus. |
| `declaredFileOp(op)` | <ol><li>Wenn der Wert des Parameters `op` den Wert **'import'** hat, dann wird die Methode `importTaskData()` aufgerufen.</li><li>Wenn der Wert des Parameters `op` hingegen den Wert **'export'** hat, dann führe die Methode `expTaskData()` aus und emittiere danach ein Event vom Typ `fileOpCompleted'.</li></ol>

##### Data-Return-Objekt von ***Main.vue*** [[Inhalt](#inhalt)]

| Property | Erläuterung | initialer Wert |
| --- | --- | --- |
| `date` | ein Datum-Objekt | `new Date()` |
| `allLists` | Speicher für alle Listennamen | `[]` |
| `showInfo` | Indikator ob der Anwenderin / dem Anwender eine Information / Fehlermeldung angezeigt wird. | **false** |
| `newTaskData` | Zwischenspeicher für die von der Anwenderin / dem Anwender eingegebenen Daten beim erstellen einer neuen Aufgabe. | `{ list: '', stat: '', end: '', title: '', done: false }` |
| `inputDataOK` | Indikator ob die eingegebenen Daten beim erstellen einer neuen Aufgabe valide sind. | **false** |
| `infoMessage` | Fehler- / Hinweisnachricht | `''` |
| `importData` | Zwischenspeicher für Aufgabendaten bei einem Dateiimport | `''` |
| `tasks` | Speicherort für alle existierenden Aufgaben-Objekte | Bei initialem Aufruf der Anwendung eine Sammlung vordefinierter (Tutorial-)Aufgaben. |

##### Methoden von ***Main.vue*** [[Inhalt](#inhalt)]

| Methode | Erläuterung |
| --- | --- |
| `setDate()` | Aktualisiere die Property `date` durch ein neues Date-Objekt. |
| `addListNames(newList)` | Aktualisiere / Ergänze den Inhalt der Property `allLists`: <ol><li>Überschreibe den Inhalt der Property `allLists` mit dem Inhhalt der Computed-Property `lists`.</li><li>Prüfe ob der Methode ein Parameter `newList` übergeben wurde **und** prüfe, dass wenn ein Parameter `newList` übergeben wurde, dass sich dessen Wert ***nicht*** bereits in der Property `allLists` befindet. Wenn diese Prüfung **true** liefert, dann füge den Wert von `newList` als weiters Element der Property `allLists` hinzu.</li><li>Emittiere abschließend ein Event vom Typ `resetNewListNameEvent` (Dieses Ereignis wird in ***App*** verarbeitet. [s. hier](#die-komponente-main--innerhalb-von-appvue-inhalt)) |
| `addNewTask()` | <ol><li>Füge der Property `tasks` ein weiteres Objekt hinzu. Verwende hierbei die in der Property `newTaskData` gesicherten Werte.</li><li>Rufe die Methode `addListNames()` auf um die Property `allLists` zu aktualisieren.</li><li>Rufe die Methode `saveTasksToLocalStorage()` auf. (Automatisches speichern der Aufgaben im LocalStorage des Browsers.)</li><li>Rufe die Methode `clearNewTaskForm()` auf.</li><li>Setze die Property `inputDataOK` auf den Wert **false** zurück.</li></ol> |
| `validateValues()` | Zusammenfassende Validierung der Eingaben im Rahmen der Erstellung einer neuen Aufgabe. Hier kommt die Promis-Helfermethode `Promise.all()` zum Einsatz. Erst wenn alle hierin registrierten Promises erfüllt sind ist auch dieses erfüllt. <ul><li>Wenn alle Promises erfüllt sind, dann ...</li><ol><li>setze den Wert der Property `inputDataOK` auf den Wert **true**,</li><li>setze den Wert der Property `showInfo` auf **false** und</li><li>setze den Wert der Property `infoMessage` auf `''`.</li></ol><li>So lange auch nur eines der Promises nicht erfüllt ist ...</li><ol><li>setze den Wert der Property `inputDataOK` auf den Wert **false**,</li><li>setze den Wert der Property `showInfo` auf **true** und</li><li>setze den Wert der Property `infoMessage` auf den Wert von `rej` des nicht erfüllten Promise.</li></ol></ul> |
| `validateString(str)` | Liefert ein Promise zurück welches nur dann erfüllt wird, wenn der Aufruf der Methode `validString(str)` in der Parent-Komponente (`this.$parent`) den Wert **true** liefert. |
| `validateDateLogic(start, end)` | Liefert ein Promise zurück welches nur dann erfüllt wird, wenn (a) der Parameter `start` genau gleich **null** ist ***oder*** (b) der Wert des Parameters `start` kleiner als der Wert des Parameters `end` ist. |
| `clearNewTaskForm()` | Zurücksetzen der `input`-Elemente und des `select`-Elements im Formular zur Erstellung neuer Aufgaben durch Manipulation der Elemente der Property `newTaskData`. |
| `delTask(task)` | Lösche eine spezifische Aufgabe, welche durch den Wert des Parameters `task` spezifiziert wird. Der Löschvorgang wird durch die Kombination der Methoden `splice()` und `indexOf()` realisiert. Nach dem Löschvorgang werden die Methoden `addListNames()` und ``saveTasksToLocalStorage()` aufgerufen. |
| `delList(list)` | Löscht alle Aufgaben-Objekte aus der Property `tasks` welche bzgl. dem Wert ihrer jeweiligen `list`-Property dem Wert des übergebenen Parameters `list` entsprechen. Der Löschvorgang der Objekt erfolgt unter Verwendung der Methode `remove` aus dem Paket **lodash** ([s. hier](#zusätzliche-pakete-inhalt)). Die als Parameter übergebene Callback-Funktion gibt nur diejenigen Aufgabenobjekte zurück welche ***nicht*** dem Parameter `list` entsprechen. Somit wird der Inhalt der Property `tasks` neu generiert. Nach Abschluss des Löschvorgangs werden die Methoden `addListNames()` und `saveTasksToLocaleStorage()` aufgerufen, sowie ein Ereignis vom Typ `resetDelListNameEvent` emittiert. |
| `toggleTaskStatus(task)` | Manipuliert den Wert der `done`-Property des spezifizierten Aufgaben-Objektes. Die Methode erhält als Parameter das Aufgaben-Objekt dessen Status verändert werden soll. Durch die Verwendung der Methode `indexOf` in Kombination mit diesem Paramteter wird das entsprechende Objekt in der Property `tasks` isoliert was die gezielte Manipulation dessen `done`-Property (Invertierung des aktuellen Wertes) erlaubt. |
| `checkForLocalTasksData()` | Sofern im LocalStorage des Browsers ein Item mit dem Namen `savedTasks` befindet wird dieses an die aufrufende Stelle zurückgegeben. |
| `saveTasksToLocalStorage()` | Speichert den akturellen inhalt der Property `tasks` unter dem Namen `savedTasks` im LocalStorage des Browsers. (Die Methode `setItem()` wird hierbei mit der Methode `JSON.stringigy()` kombiniert.) |
| `importTaskData()` | Öffnet einen 'Datei öffnen...'-Dialog indem an ein verstecktes `<input>`-Element vom Type `file` die Methode `click()` ausgeführt wird. Direkt danach wird ein Event vom Typ `fileOpCompleted` emittiert. |
| `handleImportData(e)` | Diese Methode ist ein Event-Handler, welcher Ereignisse vom Typ `change` behandelt. Durch Verwendung der Methode `readAsText(file)` einer FileReader-Instanz wird die selektierte Datei gelesen. <ol><li>Erstelle ein Konstante mit dem Namen `file` und initialisiere diese mit dem Wert von `e.target.files[0]`. (`e` als Parameter entsprcht dem `change`-Event.)</li><li>Erstelle eine neue Instanz vom Typ `FileReader` und sichere diese in der Konstanten `fileReader`.</li><li>Prüfe ob es sich beim Typ von `file` um `application.json` handelt. Wenn dem so ist, dann registriere einen EventListener für Ereignisse vom Typ `load`. Wurde die Datei geladen erfolgt eine Sicherheitsabfrage mittels `confirm()`-Dialog. Nach positiver Bestätigung durch die Anwenderin / de, Anwender wird der Wert der `result`-Property von `fileRader` mit Hilfe der Methode `JSON.parse()` geparsed und die Property `tasks` überschrieben.</li><li>Wenn es sich bei dem Typ der Datei nicht um `application.json` handelt wird mittels `alert()` eine Fehlermeldung ausgegeben</li><li>Abschließend wird der Wert von `e.target.value` zurück auf `''` gesetzt.</li></ol> |
| `expTaskData()` | Speichern des aktuellen Inhaltes des LocalStorage des Browsers als Datei. <ol><li>Erstelle und initialisiere eine Variable `dataExport` vom Datentyp **Blob**. Die Initialisierung erfolgt durch Aufruf der Methode `checkForLocalTaskData()`.</li><li>Der Speichervorgang erfolgt durch Verwendung der Methode `saveAs()` des Paketes **file-saver** ([s. hier](#zusätzliche-pakete-inhalt)). Als Parameter erhält diese `dataExport` und einen (optionalen) Dateinamen.</li></ol> |

##### Die Methode `created()` von ***Main.vue*** [[Inhalt](#inhalt)]

Beim laden der Anwendung werden in dieser Komponente automatisch die folgenden Aktionen durchgeführt:

- Es wird mittels `setInterval()` ein Intervall gestartet, welcher jede Sekunde die Methode `setDate()` aufruft.
- Durch Aufruf der Methode `checkForLocalTaskData()` werten etwaige existierende im Browser gespeicherte Aufgaben in die lokale Variable `localTasks` geladen. Bei einem positiven Resultat der folgenden Prüfung wird die Property `tasks` mit diesen Daten überschrieben.
- Aufruf der Methode `addListNames()`.

##### Registrierung der Computed-Properties von ***Main.vue*** [[Inhalt](#inhalt)]

| Computed-Property | Erläuterung |
| --- | --- |
| `lists()` | Generiert aus der Property `tasks` und unter Verwendung der Methode `uniq()` aus dem Paket **lodash** eine Liste aus Listennamen. |
| `subLists()` | Generiert ein zweidimensionales Array. Aufgaben werden anhand des jeweiligen Wertes ihrer `list`-Property sortiert. Dies erfolgt durch die Komination der Methoden `forEach()`, `push()` und `filter()`. |
| `pendingList()` | Generiert eine Liste aller nicht erledigten Aufgaben. |
| `doneList()` | Generiert eine List aus allen erledigten Aufgaben. |
| `currentDate()` | Generiert einen individuellen Datum-String unter Verwendung der Property `date` und der Methoden `toLocaleString()`, `getUTCDate()`, `getMonth()` und `getFullYear()`. |
| `currentTime()` | Generiert einen individuellen Zeit-String. (Führende 0-en werden bei Stunden-, Minuten- u. Sekundenwerten die kleiner als 10 sind automatisch ergänzt.) |

#### Template-Bereich von ***Main.vue*** [[Inhalt](#inhalt)]

Das Template besteht aus vier Hauptelementen welche von einem `<div>`-Container mit der `id="mainWrapper"` umschlossen sind:

| Element | Erläuterung |
| --- | --- |
| `<div>` | Ein Container welches ein `<input>`-Element mit der `id="fileSelect"` beinhaltet, welches via `@change`-Direktive mit der Methode `handleImportData()` verknüpft ist. Durch eine entsprechende Style-Anweisung ist dieses `<input>`-Element ausgeblendet. |
| `<header>` | In diesem Element sind die Anzeige für das aktuelle Datum, die Anzahl der unerledigten Aufgaben, sowie die Anzeige der aktuellen Uhrzeit untergebracht. Diese Elemente greifen auf die Computed-Properties `currentDate()`, `pendingList()` und `currentTime()` zu. |
| `<form>`-Element mit der `id="createNewTaskForm"` | Dieses Element ist via `@change`-Direktive mit der Methode `validateValues()` verknüpft. Die darin enthaltenen `<input>`-Elemente, bzw. das `<select>`-Element ist via `v-model`-Direktiven mit den entsprechenden Properties der `newTaskData`-Property verknüpft. <br> Die `<option>`-Elemente des `<select>`-Elements werden mittels einer `v-for`-Direktive in Verbindung mit der Property `allLists` dynamisch generiert. <br> Der Button mit der `id="createNewTaskButton"` ist über eine `@click`-Direktive mit der Methode `addNewTask()` verknüpft. Ob die Schaltfläche aktiv und somit für die Anwenderin / dem Anwender benutzbar ist, ist von dem Zustand der Property `inputDataOK` abhängig. Der Button erhält via `v-bind:class`-Direktive nur dann die Klasse `active` wenn diese Property den Wert **true** hat. <br> Das `<div>`-Element welches dem Button folgt wird nur dann angezeigt, wenn der Wert der Property `showInfo` den Wert **true** hat. Dies ist durch eine `v-if`-Direktive realisiert. |
| `<div>` mit der `id="contentWrapper"` | Innerhalb dieses Container-Elements werden die Aufgabenlisten sowie die Komponente ***Infobar*** angezeigt. Hierbei erfolgt die Gleiderung zunächst mithilfe der klassischen HTML-Elemente `<main>` für die Aufgabenlisten und `<aside>` für die ***Infobar***.<ul><h5>Die Komponenten ***TaskList*** und ***InfoBar*** im Template von ***Main.vue*** [[Inhalt](#inhalt)]</h5><li>Die einzelnen Instanzen der ***TaskList***-Komponente werden innerhalb eines weiteren `<div>`-Containers mit der `id="listsContainer"` generiert</li><li>Die Generierung der einzelen Aufgabenlisten erfolgt mittels einer `v-for`-Direktive unter Verwendung der Computed-Property `subLists`.</li><li>Als Prop `:subTaskList` wird der Komponte die aktuelle SubListe übergeben.</li><li>***TaskList*** fängt innerhalb von ***Main.vue*** zwei Event-Typen: <ul><li>`delTaskEvent` ruft Methode `delTask()` auf.</li><li>`taskStatusToggleEvent` ruft Methode `toggleTaskStatus()` auf.</li></ul></li><li>Innerhalb eines `<aside>`-Elements wird die Komponente ***Infobar*** gerendert. Diese übergibt als Prop `:doneAndPending` ein Objekt welches über die Attribute `done` und `pending` verfügt. Diese Attribute erhalten die Werte der Computed-Properties `doneList()` bzw. `pendingList()`.</li></ul>|

___

