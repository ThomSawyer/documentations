Hier finden Sie eine Dokumentation zu API-Methoden.

Hier sind zunächst die Spezifikationen (JSON RPC 2.0) :
<http://www.jsonrpc.org/specification>

Der Zugriff auf die API erfolgt über die URL : *URL\_JEEDOM*/core/api/jeeApi.php

Hier ist ein Beispiel für die Konfiguration eines Json-Objekts, das im Hauptteil einer Anfrage eines HTTP-Agenten verwendet werden kann:
`` json
{
    "jsonrpc": "2.0",
    "id": "007",
    "method": "event::changes",
    "params": {
        "apikey": "{{apikey}}",
        "datetime": "0"
    }
}
`` ''

Divers
======

ping
----

Pong zurückgeben, Kommunikation mit Jeedom testen

version
-------

Gibt die Version von Jeedom zurück

datetime
--------

Gibt die Jeedom-Datumszeit in Mikrosekunden zurück

Konfigurations-API
==========

config::byKey
-------------

Gibt einen Konfigurationswert zurück.

Json-Einstellungen :

-   String-Schlüssel : Konfigurationswertschlüssel, der zurückgegeben werden soll

-   String Plugin : (optional), Konfigurationswert-Plugin

-   Zeichenfolge Standard : (optional), Wert, der zurückgegeben werden soll, wenn der Schlüssel nicht vorhanden ist

config::save
------------

Speichert einen Konfigurationswert

Json-Einstellungen :

-   Zeichenfolgenwert : Wert aufzuzeichnen

-   String-Schlüssel : Konfigurationswertschlüssel zum Speichern

-   String Plugin : (optional), Plugin des zu speichernden Konfigurationswerts

JSON-Ereignis-API
==============

event::changes
--------------

Gibt die Liste der Änderungen seit dem im Parameter übergebenen Datum / Uhrzeit zurück (muss in Mikrosekunden angegeben werden)). Sie haben in der Antwort auch die aktuelle Datumszeit von Jeedom (die für die folgende Abfrage wiederverwendet werden soll)

Json-Einstellungen :

-   int datetime

JSON Plugin API
===============

plugin::listPlugin
------------------

Gibt die Liste aller Plugins zurück

Json-Einstellungen :

-   int activOnly = 0 (gibt nur die Liste der aktivierten Plugins zurück)

-   int orderByCaterogy = 0 (gibt die Liste der Plugins nach Kategorie sortiert zurück)

Objekt-JSON-API
==============

jeeObject::all
-----------

Gibt die Liste aller Objekte zurück

jeeObject::full
------------

Gibt die Liste aller Objekte zurück, mit für jedes Objekt alle seine Geräte und für jedes Gerät alle seine Befehle sowie deren Status (für Befehle vom Typ info)

jeeObject::fullById
----------------

Gibt ein Objekt mit all seinen Geräten und für jedes Gerät alle seine Befehle sowie deren Status zurück (für Befehle vom Typ info)

Json-Einstellungen :

-   int-ID

jeeObject::byId
------------

Gibt das angegebene Objekt zurück

Die Einstellungen:

-   int-ID

jeeObject::fullById
----------------

Gibt ein Objekt, seine Ausrüstung und für jede Ausrüstung alle seine Befehle sowie die Zellenzustände zurück (für Befehle vom Typ Info)

jeeObject::save
------------

Gibt das angegebene Objekt zurück

Die Einstellungen:

-   int id (leer, wenn es sich um eine Kreation handelt)

-   Zeichenfolgenname

-   int Vater\_id = null

-   int isVisible = 0

-   int position

-   Array-Konfiguration

-   Array-Anzeige

JSON-Zusammenfassungs-API
================

summary::global
---------------

Gibt die globale Zusammenfassung für den im Parameter übergebenen Schlüssel zurück

Die Einstellungen:

-   String-Schlüssel : (optional), Schlüssel der gewünschten Zusammenfassung. Wenn leer, gibt Jeedom die Zusammenfassung für alle Schlüssel zurück

summary::byId
-------------

Gibt die Zusammenfassung für die Objekt-ID zurück

Die Einstellungen:

-   int-ID : Objekt-ID

-   String-Schlüssel : (optional), Schlüssel der gewünschten Zusammenfassung. Wenn leer, gibt Jeedom die Zusammenfassung für alle Schlüssel zurück

JSON EqLogic API
================

eqLogic::all
------------

Gibt die Liste aller Geräte zurück

eqLogic::fullById
-----------------

Gibt ein Gerät und seine Befehle sowie deren Status zurück (für Befehle vom Typ "Info")

Die Einstellungen:

-   int-ID

eqLogic::byId
-------------

Gibt das angegebene Gerät zurück

Die Einstellungen:

-   int-ID

eqLogic::byType
---------------

Gibt alle Geräte zurück, die zum angegebenen Typ gehören (Plugin)

Die Einstellungen:

-   Zeichenfolgentyp

eqLogic::byObjectId
-------------------

Gibt alle Geräte zurück, die zum angegebenen Objekt gehören

Die Einstellungen:

-   int Objekt\_id

eqLogic::byTypeAndId
--------------------

Gibt eine Gerätetabelle gemäß den Parametern zurück.

Die Rückgabe erfolgt vom Formulararray (&#39;eqType1&#39; ⇒array (&#39;id&#39;⇒…,&#39; cmds &#39;⇒)
Array (….)), &#39;eqType2&#39; ⇒array (&#39;id&#39;⇒…,&#39; cmds &#39;⇒ Array (….))….,id1 ⇒
Array (&#39;id&#39;⇒…,&#39; cmds &#39;⇒ Array (….)), id2 ⇒ Array (&#39; id&#39;⇒…, &#39;cmds&#39; ⇒
array(…​.))..)

Die Einstellungen:

-   string \ [\] eqType = Tabelle der erforderlichen Gerätetypen

-   int \ [\] id = Tabelle der gewünschten benutzerdefinierten Geräte-IDs

eqLogic::save
-------------

Gibt das registrierte / erstellte Gerät zurück

Die Einstellungen:

-   int id (leer, wenn es sich um eine Kreation handelt)

-   Zeichenfolge eqType\_name (Skripttyp, virtuelle Ausrüstung…)

-   Zeichenfolgenname

-   Zeichenfolge logische ID = ''

-   int object\_id = null

-   int eqReal\_id = null

-   int isVisible = 0

-   int isEnable = 0

-   Array-Konfiguration

-   int timeout

-   Array-Kategorie

JSON Cmd API
============

cmd::all
--------

Gibt die Liste aller Befehle zurück

cmd::byId
---------

Gibt den angegebenen Befehl zurück

Die Einstellungen:

-   int-ID

cmd::byEqLogicId
----------------

Gibt alle Bestellungen zurück, die zum angegebenen Gerät gehören

Die Einstellungen:

-   int eqLogic\_id

cmd::execCmd
------------

Führen Sie den angegebenen Befehl aus

Die Einstellungen:

-   int-ID : Befehls-ID oder ID-Array, wenn Sie mehrere Befehle gleichzeitig ausführen möchten

-   \ [Optionen \] Liste der Befehlsoptionen (abhängig von Typ und Untertyp des Befehls)

cmd::getStatistique
-------------------

Gibt die Statistiken zur Bestellung zurück (funktioniert nur bei Informationen und historischen Bestellungen)

Die Einstellungen:

-   int-ID

-   Zeichenfolge startTime : Startdatum der Statistikberechnung

-   Zeichenfolge endTime : Enddatum der Statistikberechnung

cmd::getTendance
----------------

Gibt den Trend der Bestellung zurück (funktioniert nur bei Informationen und historischen Bestellungen)

Die Einstellungen:

-   int-ID

-   Zeichenfolge startTime : Startdatum der Trendberechnung

-   Zeichenfolge endTime : Enddatum der Trendberechnung

cmd::getHistory
---------------

Gibt den Bestellverlauf zurück (funktioniert nur bei Informationen und historischen Aufträgen)

Die Einstellungen:

-   int-ID

-   Zeichenfolge startTime : Startdatum der Geschichte

-   Zeichenfolge endTime : Enddatum der Geschichte

cmd::save
---------

Gibt das angegebene Objekt zurück

Die Einstellungen:

-   int id (leer, wenn es sich um eine Kreation handelt)

-   Zeichenfolgenname

-   Zeichenfolge logische ID

-   Zeichenfolge eqType

-   Zeichenfolgenreihenfolge

-   Zeichenfolgentyp

-   String-Subtyp

-   int eqLogic\_id

-   int isHistorized = 0

-   String-Einheit = ''

-   Array-Konfiguration

-   Array-Vorlage

-   Array-Anzeige

-   Array HTML

-   intvalue=null

-   int isVisible = 1

-   Array-Alarm

cmd::event
-------------------

Ermöglicht das Senden eines Werts an eine Bestellung

Die Einstellungen:

-   int-ID

-   Zeichenfolgenwert : valeur

-   Zeichenfolge datetime : (optional) Datum / Uhrzeit-Wert

JSON-Szenario-API
=================

scenario::all
-------------

Gibt die Liste aller Szenarien zurück

scenario::byId
--------------

Gibt das angegebene Szenario zurück

Die Einstellungen:

-   int-ID

scenario::export
----------------

Gibt den Export des Szenarios sowie das zurück *menschlicher Name* aus dem Skript

Die Einstellungen:

-   int-ID

scenario::import
----------------

Ermöglicht das Importieren eines Szenarios.

Die Einstellungen:

-   int-ID : ID des zu importierenden Szenarios (leer bei Erstellung)

-   Zeichenfolge humanName : *menschlicher Name* des Szenarios (leer bei Erstellung)

-   Array-Import : Szenario (aus dem Feld Exportszenario::export)

scenario::changeState
---------------------

Ändert den Status des angegebenen Szenarios.

Die Einstellungen:

-   int-ID

-   Zeichenfolgenstatus: \ [Run, Stop, aktivieren, deaktivieren \]

JSON-Protokoll-API
============

log::get
--------

Ermöglicht das Abrufen eines Protokolls

Die Einstellungen:

-   Zeichenfolgenprotokoll : Name des abzurufenden Protokolls

-   String-Start : Zeilennummer, auf der mit dem Lesen begonnen werden soll

-   Zeichenfolge nbLine : Anzahl der wiederherzustellenden Zeilen

log::add
--------

Ermöglicht das Schreiben in ein Protokoll

Die Einstellungen:

-   Zeichenfolgenprotokoll : Name des abzurufenden Protokolls

-   Zeichenfolgentyp : Protokolltyp (Debug, Info, Warnung, Fehler)

-   Zeichenfolge Nachricht : SMS zu schreiben

-   Zeichenfolge logische ID : logische ID der generierten Nachricht


log::list
---------

Holen Sie sich die Jeedom-Protokollliste

Die Einstellungen:

-   String-Filter : (optional) Filtern Sie nach dem Namen der abzurufenden Protokolle

log::empty
----------

Leeren Sie ein Protokoll

Die Einstellungen:

-   Zeichenfolgenprotokoll : Name des zu leeren Protokolls

log::remove
-----------

Ermöglicht das Löschen eines Protokolls

Die Einstellungen:

-   Zeichenfolgenprotokoll : Protokollname zum Löschen

JSON-Datenspeicher-API (Variable)
=============================

datastore::byTypeLinkIdKey
--------------------------

Ruft den Wert einer im Datenspeicher gespeicherten Variablen ab

Die Einstellungen:

-   Zeichenfolgentyp : Art des gespeicherten Werts (für Szenarien ist es Szenario)

-   id linkId : -1 für das globale (Wert für die Standardszenarien oder die Szenario-ID)

-   String-Schlüssel : Wertname

datastore::save
---------------

Speichert den Wert einer Variablen im Datenspeicher

Die Einstellungen:

-   Zeichenfolgentyp : Art des gespeicherten Werts (für Szenarien
    Es ist ein Szenario)

-   id linkId : -1 für global (Wert für Standardszenarien,
    oder die Szenario-ID)

-   String-Schlüssel : Wertname

-   gemischter Wert : Wert aufzuzeichnen

JSON-Nachrichten-API
================

message::all
------------

Gibt die Liste aller Nachrichten zurück

message::add
--------

Ermöglicht das Schreiben in ein Protokoll

Die Einstellungen:

-   Zeichenfolgentyp : Protokolltyp (Debug, Info, Warnung, Fehler)

-   Zeichenfolge Nachricht : message

-   String-Aktion : action

-   Zeichenfolge logische ID : logicalId

message::removeAll
------------------

Löschen Sie alle Nachrichten

JSON-Interaktions-API
====================

interact::tryToReply
--------------------

Versuchen Sie, eine Anfrage mit einer Interaktion abzugleichen, führen Sie die Aktion aus und antworten Sie entsprechend

Die Einstellungen:

-   Abfrage (Anforderungsphrase)

-   int Antwort\_cmd = NULL : Befehls-ID, die zum Antworten verwendet werden soll,
    Wenn nicht angegeben, gibt Jeedom die Antwort an Sie im JSON zurück

interactQuery::all
------------------

Gibt die vollständige Liste aller Interaktionen zurück

JSON-System-API
===============

jeedom::halt
------------

Stoppen Sie Jeedom

jeedom::reboot
--------------

Starten Sie Jeedom neu

jeedom::isOk
------------

Lässt Sie wissen, ob der globale Zustand von Jeedom in Ordnung ist

jeedom::update
--------------

Starten wir ein Jeedom-Update

jeedom::backup
--------------

Ermöglicht das Starten eines Backups von Jeedom

jeedom::getUsbMapping
---------------------

Liste der USB-Anschlüsse und Namen der daran angeschlossenen USB-Sticks

JSON Plugin API
===============

plugin::install
---------------

Installation / Update eines bestimmten Plugins

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)

plugin::remove
--------------

Löschen eines bestimmten Plugins

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)

plugin::dependancyInfo
----------------------

Gibt Informationen zum Plugin-Abhängigkeitsstatus zurück

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)

plugin::dependancyInstall
-------------------------

Erzwingen Sie die Installation von Plugin-Abhängigkeiten

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)

plugin::deamonInfo
------------------

Gibt Informationen zum Status des Plugin-Daemons zurück

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)

plugin::deamonStart
-------------------

Zwinge den Dämon zu starten

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)

plugin::deamonStop
------------------

Dämonenstopp erzwingen

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)

plugin::deamonChangeAutoMode
----------------------------

Ändern Sie den Verwaltungsmodus des Dämons

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)
-   int-Modus : 1 für automatisch, 0 für manuell

JSON-Update-API
===============

update::all
-----------

Gibt eine Liste aller installierten Komponenten, ihrer Versionen und der zugehörigen Informationen zurück

update::checkUpdate
-------------------

Ermöglicht die Suche nach Updates

update::update
--------------

Ermöglicht das Aktualisieren von Jeedom und allen Plugins

update::doUpdate
--------------

Die Einstellungen:

-   int plugin\_id (optional) : Plugin ID
-   Zeichenfolge logische ID (optional) : Plugin-Name (logischer Name)

JSON-Netzwerk-API
================

network::restartDns
-------------------

Erzwingen Sie den (Neustart) des Jeedom DNS

network::stopDns
----------------

Erzwingt das Anhalten des DNS Jeedom

network::dnsRun
---------------

JSON-Timeline-API
===============

timeline::all
-----------

Gibt alle Elemente der Timeline zurück

timeline::listFolder
-----------

Gibt alle Ordner (Kategorie) der Timeline zurück

timeline::byFolder
-----------

Gibt alle Elemente des angeforderten Ordners zurück

Die Einstellungen:

-   String-Ordner : Ordnernamen

Gibt den Jeedom DNS-Status zurück

JSON-API-Beispiele
=================

Hier ist ein Beispiel für die Verwendung der API. Für das folgende Beispiel
ich benutze [diese PHP-Klasse](https://github.com/jeedom/core/blob/release/core/class/jsonrpcClient.class.php)
Dies vereinfacht die Verwendung der API.

Abrufen der Objektliste :

`` `{.php}
$jsonrpc = new jsonrpcClient('#URL_JEEDOM#/core/api/jeeApi.php', #API_KEY#);
if ($ jsonrpc-&gt; sendrequest ( ‚jeeObject::all ', Array())){
    print_r ($ jsonrpc-&gt; getResult ());
}else{
    echo $ jsonrpc-&gt; getError ();
}
`` ''

Ausführung eines Auftrags (mit der Option eines Titels und einer Nachricht)

`` `{.php}
$jsonrpc = new jsonrpcClient('#URL_JEEDOM#/core/api/jeeApi.php', #API_KEY#);
if ($ jsonrpc-&gt; sendrequest ( ‚cmd::execCmd ', array (' id' => #cmd_id#, 'options '=> array (' title '=>' Cuckoo ',' message '=>' Es funktioniert')))){
    Echo &#39;OK&#39;;
}else{
    echo $ jsonrpc-&gt; getError ();
}
`` ''

Die API kann natürlich auch mit anderen Sprachen verwendet werden (nur ein Beitrag auf einer Seite)
