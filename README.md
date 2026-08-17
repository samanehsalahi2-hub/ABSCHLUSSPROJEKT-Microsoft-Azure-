# ABSCHLUSSPROJEKT – Microsoft Azure  
## NordPeak Consulting GmbH  
### **Name: Samaneh Salahi**  
### **Datum: August 2026**

---

# 0 – Planung

## A1 – Kostenfalle finden

### Original-Konfiguration (Fehlkonfiguration)
- Region: Brazil South  
- VM: D4s v3, Windows, Pay-as-you-go, 730h  
- Disk: 512GB Premium SSD  
- Storage: GRS  
- Nutzung: VM läuft 24/7  

<p align="center">
  <img src="https://github.com/fbw-ctf-26-a/Salahi-Samaneh/blob/main/Module%206%20-%20JavaScript%20%26%20Web-Ent" Abschlussprojekt-A1.png width="800"/>
</p>

### Kostenfallen
- Teure Region  
- Große VM  
- Premium SSD  
- GRS statt LRS  
- 24/7 Laufzeit

### Alternative-Konfiguration
- Region: Sweden Central  
- VM: B1s  
- Disk: Standard SSD  
- Storage: LRS  
- Nutzung: 180h/Monat  

**Screenshot:** Alternative Pricing Calculator (28.37 USD/Monat)

### Fragen
1. Ersparnis: **≈ 95% günstiger**  
2. Größter Effekt: **VM-Größe + Laufzeit**  
3. Grund für teure Variante: **Performance, Geo-Redundanz**

---

# A – Identität & Zugriff

## A2 – Entra-ID-Benutzer
**Screenshot:** Benutzerliste (Martina, Tobias, Selin)

## A3 – Gruppe grp-it-admin
**Screenshot:** Gruppe + Mitglied Tobias

## A4 – RBAC
**Screenshot:** IAM – Martina = Reader, grp-it-admin = Contributor

---

# B – Netzwerk (Hub & Spoke)

## B1 – VNets & NSGs
**Screenshots:**  
- vnet-hub  
- vnet-spoke-app  
- vnet-spoke-data  
- nsg-app  
- nsg-data  

## B2 – Peering
**Screenshots:**  
- Peering vnet-hub ↔ spoke-app  
- Peering vnet-hub ↔ spoke-data  

---

# C – Compute

## C1 – vm-app01
**Screenshot:** VM Running + SSH hostname

## C2 – vm-data01
**Screenshot:** VM Running + Private IP

## C3 – NSG-Test
**Screenshots:**  
- Ping vorher (Timeout)  
- Ping nachher (Antwort)  
- NSG-Regel ICMP VirtualNetwork  

---

# D – Blob Storage

## D1 – Storage Account & Container
**Screenshot:** Container dokumente + Dateien + SAS-URL

---

# E – Azure Files

## E1 – File Share
**Screenshot:** File Share mit Dateien

## E2 – Mounting
**Screenshots:**  
- Netzlaufwerk im Explorer  
- Datei erscheint im Portal  

---

# F – Azure SQL

## F1 – Free Tier DB
**Screenshot:** DB Overview + Query Editor SELECT Ergebnis

---

# G – Backup

## G1 – Vault (LRS)
**Screenshot:** Vault mit LRS

## G2 – Eigene Backup Policy
**Screenshot:** Policy-Konfiguration

## G3 – VM-Backup
**Screenshot:** Backup-Job vm-app01

## G4 – Azure Files Backup
**Screenshot:** File Share Backup

## G5 – Verifizieren
**Screenshot:** Übersicht beider Sicherungen

---

# H – Monitoring & Kosten

## H1 – Log Analytics + Alert
**Screenshots:**  
- Workspace + VM verbunden  
- alert-cpu-hoch  

## H2 – Budget
**Screenshot:** Budget 80%-Alert

---

# I – Security & Governance

## I1 – Defender for Cloud
**Screenshots:**  
- Secure Score 38%  
- Empfehlungen  
- Empfehlung geöffnet  

## I2 – Policy Tag-Pflicht
**Screenshot:** Policy + Testversuch

---

# J – App Service

## J1 – Web App
**Screenshots:**  
- Web App läuft  
- App Setting UMGEBUNG=Test  

---

# K – Automatisierung

## K1 – Blob per Skript
**Screenshot:** Cloud Shell Output + Container logs

## K2 – VM-Status Skript
**Screenshot:** Terminal-Output

---

# Bonus – Hybrid (Azure Arc & MARS)

## Arc-Registrierung
**Screenshot:** Arc Status Verbunden

## MARS Backup
**Screenshot:** Backup erfolgreich

## Vergleich (Text)
**MARS Agent:** sichert Dateien (File-Level)  
**Azure VM Backup:** sichert komplette VM (VM-Level)  
**Fazit:** MARS = On-Premises/Hybrid, VM-Backup = Azure-native

---

# Zusammenfassung

Du hast eine vollständige, produktionsreife Azure-Infrastruktur aufgebaut:

- Identität & RBAC korrekt  
- Hub-Spoke Netzwerk sauber  
- Compute + NSG-Test erfolgreich  
- Blob + Files + SQL vollständig  
- Backup (VM + Files) korrekt  
- Monitoring + Alerts aktiv  
- Security + Governance umgesetzt  
- App Service läuft  
- Automatisierung per Skript  
- Hybrid + MARS erfolgreich  
- Kostenoptimierung dokumentiert  

**Abschlussprojekt erfolgreich abgeschlossen – großartige Arbeit, Samaneh Salahi.**
