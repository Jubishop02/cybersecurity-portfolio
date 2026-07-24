# 🏗️ Architecture du Lab Blue Team

## Vue d'ensemble

Lab personnel de cybersécurité construit sur VirtualBox, orienté **détection et analyse** (Blue Team / SOC). Il combine un SIEM Wazuh, un environnement Active Directory et des machines cibles pour pratiquer la détection d'attaques.

---

## 🖥️ Machines virtuelles

| VM | OS | Rôle | Réseau |
|---|---|---|---|
| Ubuntu24.04 | Ubuntu 24.04 | Serveur SIEM Wazuh | Host-Only 192.168.56.101 |
| debian13 | Debian 13 | Cible Linux supervisée | Host-Only 192.168.56.102 |
| windowsServer | Windows Server 2025 | Contrôleur de domaine AD | AD 192.168.10.10 / Host-Only 192.168.56.103 |
| win10_client01 | Windows 10 Pro | Poste client AD supervisé | AD 192.168.10.11 / Host-Only 192.168.56.104 |
| kali | Kali Linux | Machine de simulation d'attaques | Host-Only + NAT |
| metasploitable2 | Ubuntu 8.04 | Cible volontairement vulnérable | NAT 10.0.2.5 |
| REMnux | REMnux | Analyse de malware | - |

---

## 🌐 Réseaux

| Réseau | Type | Plage IP | Usage |
|---|---|---|---|
| Host-Only | vboxnet0 | 192.168.56.0/24 | Communication agents → SIEM |
| Réseau interne AD | Internal | 192.168.10.0/24 | Domaine Active Directory |
| NAT lab-pentest | NAT | 10.0.2.0/24 | Simulation d'attaques isolée |

---

## 🔍 Supervision Wazuh

| Agent | OS | Statut |
|---|---|---|
| debian-lab_siem | Debian 13 | ✅ Actif |
| windowsServer_lab_siem | Windows Server 2025 | ✅ Actif |
| windows_client_lab_siem | Windows 10 Pro | ✅ Actif |

> ℹ️ Kali et Metasploitable2 n'ont pas d'agent Wazuh — elles jouent le rôle de l'attaquant externe non supervisé.

---

## 🏢 Active Directory

| Paramètre | Valeur |
|---|---|
| Domaine | premierAD.com |
| Contrôleur de domaine | Local_Server_Bishop.premierAD.com |
| Mode | Windows Server 2025 Domain |
| Client joint | win10-client01 |

---

## 📸 Snapshots

Toutes les VMs disposent d'un snapshot **"base-propre-avril-2026"** permettant de restaurer un état stable après les exercices.
