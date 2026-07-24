# 🏗️ Architecture du Lab Blue Team

## Vue d'ensemble

Lab personnel de cybersécurité construit sur **Oracle VirtualBox** sur un PC Windows hôte, orienté **détection et analyse (Blue Team / SOC)**. 

L'objectif est de simuler un environnement d'entreprise réaliste avec :
- Un **SIEM Wazuh** pour la collecte et l'analyse des logs
- Un **Active Directory** pour simuler un réseau d'entreprise Windows
- Des **machines cibles supervisées** avec agents Wazuh
- Une **machine attaquante** (Kali Linux) pour générer des événements de sécurité
- Une **machine volontairement vulnérable** (Metasploitable2) pour la pratique

---

## 🖥️ Machines virtuelles

### Ubuntu 24.04 — Serveur SIEM Wazuh
| Paramètre | Valeur |
|---|---|
| Rôle | Serveur SIEM central |
| OS | Ubuntu 24.04 LTS |
| RAM | 6144 Mo |
| CPU | 7 vCPUs |
| Disque | 40 Go |
| IP Host-Only | 192.168.56.101 |
| Services | Wazuh Indexer (OpenSearch), Wazuh Manager, Wazuh Dashboard |
| Agent Wazuh | ID 000 (local, intégré au manager) |

### Debian 13 — Cible Linux supervisée
| Paramètre | Valeur |
|---|---|
| Rôle | Poste Linux supervisé |
| OS | Debian 13 (Trixie) |
| RAM | 4096 Mo |
| CPU | 6 vCPUs |
| Disque | 30 Go |
| IP Host-Only | 192.168.56.102 |
| Agent Wazuh | ID 001 — debian-lab_siem |
| Vulnérabilités détectées | 120 critiques (CVE 2026) |

### Windows Server 2025 — Contrôleur de domaine
| Paramètre | Valeur |
|---|---|
| Rôle | Contrôleur de domaine Active Directory |
| OS | Windows Server 2025 Standard Evaluation |
| IP réseau AD | 192.168.10.10 |
| IP Host-Only | 192.168.56.103 |
| Domaine | premierAD.com |
| Rôles FSMO | PDC Emulator, RID Master, Infrastructure Master |
| Agent Wazuh | ID 002 — windowsServer_lab_siem |

### Windows 10 Pro — Poste client AD
| Paramètre | Valeur |
|---|---|
| Rôle | Poste client joint au domaine |
| OS | Windows 10 Pro 10.0.19045 |
| IP réseau AD | 192.168.10.11 |
| IP Host-Only | 192.168.56.104 |
| Domaine | premierAD.com |
| DNS | 192.168.10.10 (contrôleur de domaine) |
| Agent Wazuh | ID 003 — windows_client_lab_siem |

### Kali Linux — Machine attaquante
| Paramètre | Valeur |
|---|---|
| Rôle | Simulation d'attaques externes |
| OS | Kali Linux (rolling) |
| IP Host-Only | 192.168.56.102 |
| IP NAT lab-pentest | 10.0.2.6 |
| Agent Wazuh | ❌ Aucun (simule un attaquant externe) |
| Outils | Nmap, Metasploit, Hydra, Netcat, searchsploit |

### Metasploitable2 — Cible vulnérable
| Paramètre | Valeur |
|---|---|
| Rôle | Cible d'entraînement volontairement vulnérable |
| OS | Ubuntu 8.04 |
| IP NAT lab-pentest | 10.0.2.5 |
| Agent Wazuh | ❌ Aucun |
| Services exposés | FTP (vsftpd 2.3.4), SSH, Telnet, Samba 3.0.20, MySQL, VNC... |

### REMnux — Analyse de malware
| Paramètre | Valeur |
|---|---|
| Rôle | Analyse statique
