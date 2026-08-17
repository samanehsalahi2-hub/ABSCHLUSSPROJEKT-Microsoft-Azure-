# ABSCHLUSSPROJEKT-Microsoft-Azure-

ABSCHLUSSPROJEKT
Microsoft Azure – Kurs
NordPeak Consulting GmbH
Cloud-Infrastruktur komplett aufbauen
Bearbeitungszeit 3 Unterrichtstage (Nachmittagsblöcke)
Abgabe Dokumentation mit Screenshots + Live-Demo
Voraussetzung Azure-Subscription mit aktivem Credit (Demo-Umgebung)
1 Das Szenario
Du bist ab heute der Cloud-Administrator der NordPeak Consulting GmbH – einem wachsenden
Beratungsunternehmen in Wien. Bisher gab es keine geordnete Cloud-Infrastruktur. Der Chef hat
entschieden: Alles wird von Grund auf in Azure aufgebaut – strukturiert, sicher, dokumentiert, und mit
den Kosten immer im Blick.
Firma NordPeak Consulting GmbH
Branche IT-Beratung & Projektmanagement
Standort Wien, Österreich
Mitarbeiter 3 Personen + 1 Cloud-Administrator (du)
Ressourcengruppe rg-nordpeak
Azure Region Frei wählbar (aber überall dieselbe Region verwenden)
Die drei Mitarbeiter:
Anzeigename Rolle UPN
Martina Novak Geschäftsführung – braucht Lesezugriff auf
alles
m.novak@[deine
domain]
Tobias Krainer IT – Techniker, braucht vollen Zugriff t.krainer@[deine
domain]
Selin Leitner Praktikantin – kein Azure-Zugriff, nur
Entra User
s.leitner@[deine
domain]
2 Aufgaben
Achtung: Die Aufgaben bauen teilweise aufeinander auf. Lies jede Aufgabe vollständig durch, bevor
du beginnst. Wenn eine Aufgabe nicht funktioniert – dokumentiere das Problem und mach mit der
nächsten weiter.
Kapitel 0 – Planung
Ziel des Kapitels: Bevor du selbst etwas baust, trainierst du im Pricing Calculator den Blick für
unnötig hohe Kosten – eine zentrale AZ-900-Kompetenz.
A1 Kostenfalle finden
Thema: Azure Pricing Calculator, Kostenoptimierung
Ziel: Jemand hat eine Umgebung konfiguriert – aber ziemlich ungeschickt. Finde die Kostenfallen
und baue eine günstigere Alternative, bevor du im weiteren Projekt selbst konfigurierst.
Vorgaben:
Einstellung Vorgabe (fiktive Fehlkonfiguration)
Region Brazil South
VM D4s v3, Windows, Pay-as-you-go, 730 Stunden/Monat
Managed Disk 512 GB Premium SSD
Storage GRS (geo-redundant), 100 GB Blob
Nutzung Anwendung läuft nur Mo–Fr von 9–18 Uhr, die
VM aber trotzdem 24/7
Aufgabe:
• Trage die Konfiguration oben unverändert in den Azure Pricing Calculator ein und
notiere die Gesamtsumme pro Monat.
• Finde mindestens 3 konkrete Kostenfallen in dieser Konfiguration (denk an Region,
VM-Größe/OS, Disk Typ, Redundanz, Laufzeit).
• Baue im Calculator eine günstigere Alternative mit gleicher Funktion, aber sinnvolleren
Einstellungen. • Vergleiche beide Gesamtsummen.
Fragen (schriftlich beantworten):
• 1. Wie viel Prozent günstiger ist deine Alternative?
• 2. Welche einzelne Änderung hat den größten Effekt auf den Preis?
• 3. Gäbe es einen Grund, trotzdem bei der teureren Variante zu bleiben?
�� Screenshot-Pflicht: Beide Konfigurationen (Original und Alternative) im Pricing Calculator
mit ihren jeweiligen Gesamtsummen.
Kapitel A – Identität & Zugriff
Ziel des Kapitels: Bevor die ersten Ressourcen entstehen, baust du die Zugriffsstruktur auf.
So sitzen Berechtigungen von Anfang an korrekt, statt sie nachträglich zu reparieren.
A2 Entra-ID-Benutzer anlegen
Thema: Microsoft Entra ID, Benutzerverwaltung
Ziel: Die drei Personen aus dem Szenario müssen als echte Identitäten existieren, bevor du ihnen
Rechte geben kannst.
Aufgabe:
• Erstelle die drei Benutzer aus der Mitarbeitertabelle oben in Microsoft Entra ID (Anzeigename +
UPN wie angegeben, eigene Domain ergänzen).
• Vergib jeweils ein temporäres Kennwort.
�� Screenshot-Pflicht: Alle drei Benutzer in der Entra-ID-Benutzerliste sichtbar.
A3 Sicherheitsgruppe
Thema: Entra ID Gruppen
Ziel: Rechte sollen über Gruppen vergeben werden, nie direkt an einzelne Personen – wie schon
im Windows Server-Kurs gelernt.
Aufgabe:
• Erstelle eine Sicherheitsgruppe grp-it-admin.
• Füge Tobias Krainer als Mitglied hinzu.
�� Screenshot-Pflicht: Gruppe grp-it-admin mit Mitglied Tobias Krainer.
A4 RBAC-Rollen zuweisen
Thema: Access Control (IAM), RBAC
Ziel: Zugriffsrechte nach dem Prinzip der geringsten Berechtigung vergeben – bevor überhaupt
schützenswerte Ressourcen existieren.
Aufgabe:
• Lege die Ressourcengruppe rg-nordpeak an, falls noch nicht vorhanden (Region frei wählbar, aber
ab jetzt für alles verwenden).
• Weise auf rg-nordpeak folgende Rollen zu: Martina Novak → Reader; grp-it-admin →
Contributor • Überprüfe unter Access Control (IAM), ob beide Zuweisungen korrekt
erscheinen.
�� Screenshot-Pflicht: IAM-Tab von rg-nordpeak mit beiden Rollenzuweisungen.
Kapitel B – Netzwerk (Hub & Spoke)
Ziel des Kapitels: Eine saubere, isolierte Netzwerkstruktur nach dem Hub-&-Spoke-Prinzip – wie
in deiner Netzwerk-Übung, diesmal produktiv für das eigentliche Projekt.
B1 VNets und NSGs
Thema: Virtual Network, Subnetze, Network Security Groups
Ziel: Feste Adressräume sorgen dafür, dass später beim Peering und bei den VMs alles
zusammenpasst – halte dich daher exakt an die Vorgaben.
Vorgaben:
Netzwerk Adressraum / Subnetz
vnet-hub 10.20.0.0/24, Subnetz snet-hub: 10.20.0.0/24
vnet-spoke-app 10.21.0.0/24, Subnetz snet-app: 10.21.0.0/24
vnet-spoke-data 10.22.0.0/24, Subnetz snet-data: 10.22.0.0/24
Aufgabe:
• Erstelle die drei VNets mit exakt diesen Adressräumen und Subnetzen in
rg-nordpeak. • Erstelle zwei Network Security Groups:
◦ nsg-app (zugewiesen zu snet-app): Inbound-Regel SSH (Port 22) erlauben, Priorität 100 ◦
nsg-data (zugewiesen zu snet-data): Inbound-Regel SSH (Port 22) erlauben, Priorität 100 –
UND zusätzlich eine Regel, die jeglichen weiteren eingehenden Traffic verweigert (Deny All
Inbound, Priorität 200). Das bildet einen bewusst stärker abgesicherten Datenbereich ab.
�� Screenshot-Pflicht: Alle drei VNets mit Subnetzen + beide NSGs mit ihren Regeln.
B2 Peering einrichten
Thema: VNet Peering
Ziel: Hub und Spokes müssen direkt miteinander verbunden werden, damit später Traffic
zwischen ihnen fließen kann.
Aufgabe:
• Richte Peering ein zwischen vnet-hub ↔ vnet-spoke-app und vnet-hub ↔ vnet-spoke-data (jeweils
in beide Richtungen).
• Verifiziere, dass alle vier Peering-Einträge den Status „Verbunden“ zeigen.
�� Screenshot-Pflicht: Peerings-Übersicht aller drei VNets, Status „Verbunden“.
Kapitel C – Compute
Ziel des Kapitels: Zwei VMs in unterschiedlichen Spokes aufsetzen und anschließend live erleben,
wie NSGs den Zugriff zwischen ihnen steuern.
C1 VM im App-Spoke
Thema: Azure Virtual Machine (Linux)
Aufgabe:
• Erstelle vm-app01 (Ubuntu Server, aktuelle LTS-Version, Größe B1s) im Subnetz snet-app mit
nsg-app. • Diese VM braucht eine öffentliche IP-Adresse (aktivieren) – sie ist dein Einstiegspunkt
von außen. • Verbinde dich per SSH und führe hostname aus, um die Verbindung nachzuweisen.
�� Screenshot-Pflicht: VM-Status „Running“ + SSH-Session mit hostname-Output.
C2 VM im Data-Spoke
Thema: Azure Virtual Machine in zweitem Subnetz
Ziel: Eine zweite VM in einem anderen Spoke, um in C3 die NSG-Grenzen zwischen den Bereichen
zu testen. Aufgabe:
• Erstelle vm-data01 (Ubuntu Server, gleiche LTS-Version, B1s) im Subnetz snet-data mit nsg-data.
• Diese VM braucht KEINE öffentliche IP-Adresse – sie bleibt komplett privat, Zugriff später nur
über vm app01 als Sprungbrett.
�� Screenshot-Pflicht: VM-Status „Running“, private IP-Adresse sichtbar im Portal.
C3 NSG-Verifikation
Thema: Wirkung von Network Security Groups testen
Ziel: In der Theorie weißt du, dass NSGs den Zugriff steuern – hier erlebst du es live und lernst, eine
blockierte Verbindung gezielt zu debuggen, statt nur eine fertige Regel abzutippen.
Aufgabe:
• Verbinde dich per SSH auf vm-app01 (öffentliche IP).
• Ping von dort aus die private IP-Adresse von vm-data01 an. Dokumentiere das Ergebnis. • Da der
Ping vermutlich fehlschlägt: Prüfe die Regeln von nsg-data. Ergänze gezielt eine Inbound-Regel, die
ICMP-Traffic vom Dienst-Tag VirtualNetwork erlaubt – mit einer Priorität, die niedriger ist als die Deny
All-Regel aus B1 (also numerisch kleiner, z. B. 150).
• Teste den Ping erneut.
�� Tipp: Priorität funktioniert umgekehrt zur Intuition: Eine niedrigere Zahl wird zuerst ausgewertet
und gewinnt. Deine neue Regel muss also eine kleinere Prioritätszahl als 200 bekommen, sonst
greift weiterhin die Deny-All-Regel zuerst.
�� Screenshot-Pflicht: Ping-Versuch VORHER (Timeout) und NACHHER (Antwort) + die
ergänzte NSG Regel.
�� Danach: Beide VMs stoppen (werden in Kapitel G und H erneut gebraucht).
Kapitel D – Storage: Blob
Ziel des Kapitels: Objektspeicher für unstrukturierte Dateien aufbauen – die Grundlage für
viele Cloud Anwendungen.
D1 Storage Account & Blob Container
Thema: Azure Blob Storage
Aufgabe:
• Erstelle einen Storage Account stnordpeak[deineinitialen] (global eindeutiger Name),
Standard Performance, LRS-Redundanz.
• Erstelle einen Blob Container dokumente mit Zugriffsebene „Privat“.
• Lade mindestens 2 Testdateien in den Container hoch.
• Generiere eine SAS-URL für eine der Dateien mit 1 Stunde Gültigkeit und öffne sie im
Browser. �� Screenshot-Pflicht: Blob Container mit hochgeladenen Dateien + SAS-URL
im Browser geöffnet.
Kapitel E – Storage: Azure Files + lokales Mounting
Ziel des Kapitels: Den Unterschied zwischen Blob Storage (App-Zugriff über API/SAS) und File
Storage (klassischer Netzwerkzugriff wie bei einem Dateiserver) direkt selbst erleben.
E1 File Share anlegen
Thema: Azure Files
Aufgabe:
• Lege im selben Storage Account (aus D1) eine File Share namens freigabe an (Kontingent z.
B. 5 GB). • Lade 2–3 Testdateien in die File Share hoch.
�� Screenshot-Pflicht: File Share mit hochgeladenen Dateien im Portal.
E2 Mounting am eigenen Laptop
Thema: Azure Files Mounting über SMB
Ziel: Zeig dir selbst, dass sich eine Azure File Share wie ein ganz normales Netzlaufwerk verhält –
genau wie eine Windows-Server-Freigabe, nur eben in der Cloud gehostet.
Aufgabe:
• Öffne die File Share im Portal und klicke auf „Verbinden“ (Connect) – Azure generiert automatisch
das passende Skript inklusive Storage-Key (Windows: PowerShell-Befehl mit net use;
macOS/Linux: mount Befehl).
• Führe dieses Skript auf deinem EIGENEN Laptop aus – nicht in einer VM.
• Öffne das gemountete Laufwerk im Explorer/Finder, lege dort eine neue Testdatei ab und prüfe im
Azure Portal, ob sie in der File Share erscheint.
�� Screenshot-Pflicht: Gemountetes Laufwerk im Explorer/Finder + neue Datei anschließend im
Azure Portal sichtbar.
Kapitel F – Azure SQL Database (Free Tier)
Ziel des Kapitels: Eine dritte Servicekategorie kennenlernen: eine verwaltete Datenbank (PaaS) –
im Gegensatz zur VM (IaaS, Kapitel C) und zum App Service (PaaS-Compute, Kapitel J).
F1 SQL-Datenbank erstellen
Thema: Azure SQL Database, Free Offer
Ziel: Erlebe den Unterschied zwischen „du verwaltest den Server“ (VM) und „Microsoft verwaltet den
Server, du verwaltest nur die Daten“ (PaaS).
Aufgabe:
• Suche im Portal nach „Azure SQL“ → SQL databases → „+ Create“ → wähle explizit „SQL database
(Free offer)“ (nicht die normale kostenpflichtige Variante).
• Name z. B. sqldb-nordpeak, dazu einen neuen SQL-Server anlegen. Notiere die
Admin-Anmeldedaten. • Aktiviere nach der Erstellung unter Networking die Firewall-Regel „Add
current client IP address“.
• Verbinde dich über den Query-Editor im Portal, lege eine einfache Tabelle an (z. B. Kunden mit
Spalten Id, Name) und füge per INSERT eine Testzeile ein.
�� Screenshot-Pflicht: Erstellte Datenbank im Übersichtsblatt + Query-Editor mit erfolgreichem
SELECT Ergebnis.
Kapitel G – Backup (Recovery Services Vault)
Ziel des Kapitels: Natives Azure-Backup kennenlernen. Im Unterschied zum MARS-Agent aus der
Hybrid Übung (dort: Dateiebene eines on-prem-Servers) sicherst du hier waschechte
Azure-Ressourcen direkt über den Vault.
G1 Recovery Services Vault erstellen
Thema: Azure Backup, Recovery Services Vault
Aufgabe:
• Erstelle einen Recovery Services Vault rsv-nordpeak in rg-nordpeak.
• Stelle VOR der ersten Sicherung in den Eigenschaften des Vaults die Redundanz auf „lokal
redundant (LRS)“ um (spart Kosten – lässt sich danach nicht mehr ändern, sobald ein Backup
existiert).
�� Screenshot-Pflicht: Vault-Übersicht mit umgestellter LRS-Einstellung.
G2 Eigene Backup Policy definieren
Thema: Backup Policy
Ziel: Statt die Standard-Policy zu übernehmen, legst du selbst fest, wie oft und wie lange gesichert
wird – und verstehst, wofür diese Werte in der Praxis wichtig sind.
Aufgabe:
• Definiere eine eigene Backup Policy, z. B. tägliche Sicherung um 07:00 Uhr, Aufbewahrung 7
Tage. • Begründe kurz schriftlich: Warum reichen diese Werte für ein Testszenario, und wo wären
sie in einer echten Produktivumgebung zu knapp bemessen?
�� Screenshot-Pflicht: Konfiguration der eigenen Backup Policy.
G3 VM-Backup
Thema: Native Azure VM Backup
Aufgabe:
• Sichere vm-app01 über die native Azure-VM-Backup-Erweiterung im Vault, unter Verwendung der
Policy aus G2.
• Stoße einen einmaligen Backup-Job manuell an („Jetzt sichern“).
�� Screenshot-Pflicht: Backup-Job für vm-app01 mit Status im Vault.
G4 Azure Files-Backup
Thema: Azure Files Backup
Aufgabe:
• Sichere die File Share freigabe (aus E1) über denselben Vault, ebenfalls mit der Policy
aus G2. �� Screenshot-Pflicht: Sicherungselement der File Share mit
Wiederherstellungspunkt.
G5 Verifizieren
Thema: Kontrolle der Sicherungen
Aufgabe:
• Prüfe im Vault unter „Sicherungselemente“, ob beide Sicherungen (VM und File Share) mit
mindestens einem Wiederherstellungspunkt gelistet sind.
�� Screenshot-Pflicht: Übersicht beider Sicherungselemente im Vault.
Kapitel H – Monitoring & Kosten
Ziel des Kapitels: Ressourcen aktiv überwachen (Performance) und Kosten proaktiv im Blick
behalten – statt erst am Monatsende überrascht zu werden.
H1 Log Analytics & Alert
Thema: Azure Monitor, Log Analytics
Aufgabe:
• Erstelle einen Log Analytics Workspace.
• Verbinde vm-app01 damit (Azure Monitor Agent) – dafür muss die VM aus C3 wieder gestartet
werden. • Erstelle eine Alert Rule: Bedingung CPU-Auslastung > 80 %, Name alert-cpu-hoch,
Aktion E-Mail Benachrichtigung an deine eigene Adresse.
�� Screenshot-Pflicht: Workspace mit verbundener VM + konfigurierte Alert Rule.
H2 Budget-Alert
Thema: Cost Management, Budgets
Ziel: Kosten nicht nur im Nachhinein analysieren, sondern von vornherein eine Warnschwelle
einziehen. Aufgabe:
• Erstelle im Cost Management ein Budget für rg-nordpeak mit einem für das Projekt sinnvollen
Monatslimit. • Richte eine Benachrichtigung bei 80 % des Budgets ein.
�� Screenshot-Pflicht: Budget-Konfiguration mit Alert-Schwelle bei 80 %.
Kapitel I – Security & Governance
Ziel des Kapitels: Sicherheitsstatus systematisch bewerten und Regeln automatisch
durchsetzen, statt nur manuell zu kontrollieren.
I1 Defender for Cloud
Thema: Microsoft Defender for Cloud
Aufgabe:
• Öffne Defender for Cloud, notiere den aktuellen Secure Score.
• Filtere die Empfehlungen nach rg-nordpeak, lies mindestens 3 Empfehlungen durch. •
Setze mindestens eine Empfehlung um oder begründe schriftlich, was du tun würdest und
warum.
�� Screenshot-Pflicht: Secure Score + gefilterte Empfehlungsliste + eine geöffnete Empfehlung.
I2 Azure Policy: Pflicht-Tag erzwingen
Thema: Azure Policy, Governance
Ziel: Bisher hast du Tags höchstens manuell vergeben. Hier erzwingst du sie automatisch über eine
Richtlinie, sodass niemand mehr vergessen kann, eine Ressource korrekt zu kennzeichnen.
Aufgabe:
• Weise auf rg-nordpeak eine eingebaute Policy-Definition zu, die einen bestimmten Tag erzwingt
(z. B. „Require a tag on resources“, Tag-Name Kostenstelle).
• Teste die Wirkung: Versuche, eine neue kleine Ressource ohne diesen Tag anzulegen. Was
passiert? �� Screenshot-Pflicht: Policy-Zuweisung + Testversuch (Fehlermeldung bzw.
erzwungene Tag-Eingabe).
Kapitel J – App Service
Ziel des Kapitels: PaaS-Compute kennenlernen: eine Web-App betreiben, ohne eine eigene VM zu
verwalten.
J1 Web App erstellen
Thema: Azure App Service
Aufgabe:
• Erstelle einen App Service Plan asp-nordpeak (Linux, F1/Free-Tier).
• Erstelle eine Web App app-nordpeak-[deineinitialen] auf diesem Plan.
• Öffne die Standard-URL der Web App im Browser.
• Füge unter Configuration → Application Settings eine neue Einstellung UMGEBUNG=Test
hinzu. �� Screenshot-Pflicht: Laufende Web App im Browser + App Setting sichtbar.
Kapitel K – Automatisierung (Cloud Shell)
Ziel des Kapitels: Erste Schritte mit PowerShell in der Azure Cloud Shell – Ressourcen per
Skript statt per Klick verwalten.
K1 Blob-Container per Skript anlegen
Thema: Azure Cloud Shell, PowerShell
Aufgabe:
• Öffne die Cloud Shell im Portal im PowerShell-Modus.
• Lege per Skript einen weiteren Blob Container logs im bestehenden Storage Account (aus
D1) an. • Lade per Skript eine Testdatei in diesen Container hoch.
�� Tipp: Kennst du die genauen Cmdlet-Namen nicht: Get-Command *StorageContainer*
zeigt passende Befehle, oder frag eine KI nach dem richtigen Cmdlet für „Blob Container per
PowerShell erstellen“.
�� Screenshot-Pflicht: Terminal-Output der ausgeführten Befehle + neuer Container im Portal
sichtbar.
K2 (Optional) VM-Status per Skript
Thema: Get-AzVM
Aufgabe:
• Schreibe ein kurzes Skript, das alle VMs in rg-nordpeak mit ihrem aktuellen Status
(läuft/gestoppt) auflistet.
�� Screenshot-Pflicht: Terminal-Output mit VM-Liste und Status.
★ Bonus – Hybrid (Azure Arc & Backup)
Ziel des Kapitels: Für alle, die schneller fertig sind: den Unterschied zwischen einem
„waschechten“ Azure Backup (Kapitel G) und dem MARS-Agent-Backup eines on-prem-Servers
noch einmal ganz konkret erleben.
Bonus Arc-Registrierung + MARS-Backup wiederholen
Thema: Azure Arc, MARS-Agent
Aufgabe:
• Falls deine Hybrid-Cloud-VM aus der vorherigen Übung noch existiert: Registriere sie erneut in
Azure Arc (oder neu, falls sie gelöscht wurde).
• Richte ein MARS-Agent-Backup für einen Testordner ein.
• Vergleiche abschließend schriftlich: Was sichert MARS (Dateiebene) im Gegensatz zu deinem
nativen VM-Backup aus G3 (komplette VM)?
�� Screenshot-Pflicht: Arc-Status „Verbunden“ + erfolgreicher MARS-Backup-Job.
3 Aufräumen – Ressourcen löschen
Wichtig! Lösche am Ende alle Ressourcen, um Credit zu sparen. Am einfachsten: rg-nordpeak im
Portal öffnen → „Ressourcengruppe löschen“. Prüfe vorher, ob der Recovery Services Vault noch
aktive Sicherungen enthält
– diese musst du zuerst stoppen und die Daten löschen, sonst lässt sich der Vault nicht entfernen
und blockiert das Löschen der Ressourcengruppe.
4 Abgabe-Checkliste
0 – Planung
• Original-Konfiguration und Alternative im Pricing Calculator
• Alle 3 Fragen beantwortet
A – Identität & Zugriff
• 3 Entra-ID-Benutzer angelegt
• Gruppe grp-it-admin mit Mitglied
• RBAC-Rollen auf rg-nordpeak korrekt
B – Netzwerk
• 3 VNets mit exakten Adressräumen
• 2 NSGs mit allen Regeln
• Peering in beide Richtungen verbunden
C – Compute
• vm-app01 läuft, SSH funktioniert
• vm-data01 läuft, privat
• NSG-Test dokumentiert (vorher/nachher)
D – Blob Storage
• Container mit Testdateien
• SAS-URL funktioniert
E – Azure Files
• File Share mit Testdateien
• Laufwerk am Laptop gemountet und getestet
F – Azure SQL
• Free-Tier-Datenbank erstellt
• Tabelle angelegt, Testzeile eingefügt
G – Backup
• Vault mit LRS
• Eigene Backup Policy definiert
• VM-Backup läuft
• Files-Backup läuft
• Beide Wiederherstellungspunkte sichtbar
H – Monitoring & Kosten
• Log Analytics Workspace verbunden
• CPU-Alert konfiguriert
• Budget mit 80%-Alert eingerichtet
I – Security & Governance
• Secure Score notiert, Empfehlung umgesetzt
• Policy zur Tag-Pflicht zugewiesen und getestet
J – App Service
• Web App läuft, URL offen
• App Setting gesetzt
K – Automatisierung
• Blob Container per Skript erstellt
• (Optional) VM-Status-Skript ausgeführt
★ Bonus
• Arc-Registrierung + MARS-Backup wiederholt und verglichen
Viel Erfolg! Bei Problemen: Fehlermeldung genau lesen, Doku/KI nutzen, Mitschüler fragen.
Jeder Cloud Admin hatte am Anfang diese Probleme.
