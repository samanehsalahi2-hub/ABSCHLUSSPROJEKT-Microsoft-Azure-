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
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt.png" width="800"/>
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

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-A1.png" width="800"/>
</p>

### Fragen
1. Ersparnis: **≈ 95% günstiger**  
2. Größter Effekt: **VM-Größe + Laufzeit**  
3. Grund für teure Variante: **Performance, Geo-Redundanz**

---

# A – Identität & Zugriff

## A2 – Entra-ID-Benutzer

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-A2.png" width="800"/>
</p>

## A3 – Gruppe grp-it-admin

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-A3.png" width="800"/>
</p>

## A4 – RBAC
**Screenshot:** IAM – Martina = Reader, grp-it-admin = Contributor

---

# B – Netzwerk (Hub & Spoke)

## B1 – VNets & NSGs

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-B1_1.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-B1_2.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-B1_3.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-B1_4.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-B1_5.png" width="800"/>
</p>

## B2 – Peering

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-B2_1.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-B2_2.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-B2_3.png" width="800"/>
</p>


---

# C – Compute

## C1 – vm-app01

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-C1.png" width="800"/>
</p>


## C2 – vm-data01

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-C2.png" width="800"/>
</p>


## C3 – NSG-Test

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-C3-1.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-C3-2.png" width="800"/>
</p>

 
- Ping vorher (Timeout)  
- Ping nachher (Antwort)  
- NSG-Regel ICMP VirtualNetwork  

---

# D – Blob Storage

## D1 – Storage Account & Container

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-D1-1.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-D1-2.png" width="800"/>
</p>

---

# E – Azure Files

## E1 – File Share

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-E1-1.png" width="800"/>
</p>


## E2 – Mounting
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-E2-1.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-E2-2.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-E2-3.png" width="800"/>
</p>


- Netzlaufwerk im Explorer  
- Datei erscheint im Portal  

---

# F – Azure SQL

## F1 – Free Tier DB

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-F1.png" width="800"/>
</p>


---

# G – Backup

## G1 – Vault (LRS)
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-G1.png" width="800"/>
</p>


## G2 – Eigene Backup Policy
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-G2.png" width="800"/>
</p>

## G3 – VM-Backup
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-G3-1.png" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-G3-2.png" width="800"/>
</p>

## G4 – Azure Files Backup
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-G4.png" width="800"/>
</p>
## G5 – Verifizieren

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-G5-1.png" width="800"/>
</p>
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-G5-2.png" width="800"/>
</p>
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-G5-3.png" width="800"/>
</p>

---

# H – Monitoring & Kosten

## H1 – Log Analytics + Alert
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-H1-1.png" width="800"/>
</p>
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-H1-2.png" width="800"/>
</p>
- Workspace + VM verbunden  
- alert-cpu-hoch  

## H2 – Budget
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-H2.png" width="800"/>
</p>

---

# I – Security & Governance

## I1 – Defender for Cloud
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-I1-1.png" width="800"/>
</p> 
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-I1-2.png" width="800"/>
</p>
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-I1-3.png" width="800"/>
</p>
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-I1-4.png" width="800"/>
</p>
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-I1-5.png" width="800"/>
</p>
- Secure Score 38%  
- Empfehlungen  
- Empfehlung geöffnet  

## I2 – Policy Tag-Pflicht

<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-I2-1.png" width="800"/>
</p>

---

# J – App Service

## J1 – Web App
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-J1-1.png" width="800"/>
</p>
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-J1-2.png" width="800"/>
</p>
- Web App läuft  
- App Setting UMGEBUNG=Test  

---

# K – Automatisierung

## K1 – Blob per Skript
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-K1.png" width="800"/>
</p>

## K2 – VM-Status Skript
<p align="center">
  <img src="https://github.com/samanehsalahi2-hub/ABSCHLUSSPROJEKT-Microsoft-Azure-/blob/main/Abschlussprojekt-K1.png" width="800"/>
</p>


