# 🛡️ Cybersecurity Portfolio

## 👋 À propos

Gendarme depuis 16 ans avec une expérience opérationnelle en unités d'intervention (PSPG, PSIG, Peloton Autoroutier, PIGM), actuellement en reconversion professionnelle vers la **cybersécurité**.

Mon parcours en sécurité physique et gestion de crise me donne une compréhension unique des enjeux de sécurité, que j'applique désormais au monde numérique.

---

## 🎯 Objectif professionnel

Analyste SOC / Pentester Junior | Recherche CDI à partir de Mars 2027

---

## 🔐 Compétences techniques

### Systèmes & Réseaux

- Linux (administration, scripts Bash)
- Windows (Active Directory, GPO)
- Protocoles réseau (TCP/IP, DNS, DHCP)

### SIEM & analyse de logs

- Wazuh (déploiement, configuration, dashboard, gestion d'agents)
- Splunk (SPL : `stats`, `dc()`, filtrage, corrélation)
- Sysmon (configuration de détection communautaire)

### Outils de pentesting

- Nmap, Gobuster, Burp Suite
- Metasploit Framework
- Wireshark
- Kali Linux

### Programmation

- Python (scripts d'automatisation)
- Bash scripting

### Méthodologies

- OWASP Top 10
- Kill Chain
- MITRE ATT&CK

---

## 🖥️ Labs pratiques

### SOC Home Lab — Wazuh SIEM + Sysmon (Active Directory simulé)

**Architecture montée sous VMware Workstation :**
- 1x manager Wazuh (Debian 12) — déploiement all-in-one (indexer + server + dashboard)
- 1x contrôleur de domaine Windows Server 2019 (Active Directory)
- 2x postes clients Windows 11
- 1x machine Kali Linux (poste attaquant)
- Réseau isolé dédié (192.168.96.0/24), séparé du réseau NAT utilisé uniquement pour les mises à jour système

**Mise en œuvre :**
- Installation et configuration du SIEM Wazuh (manager, indexer, dashboard) sur Debian
- Déploiement d'agents Wazuh sur l'ensemble des postes Windows du lab
- Installation de Sysmon (configuration communautaire Neo23x0/SwiftOnSecurity) pour une visibilité fine sur la création de processus, l'accès mémoire inter-processus et les modifications de registre
- Intégration du canal d'événements Sysmon dans la configuration des agents Wazuh (`ossec.conf`)
- Analyse de logs bruts (firewall, VPN, IDS) via Splunk : détection de scans de reconnaissance (ping sweep horizontal, scan de ports vertical), corrélation SPL
- Investigation d'alertes de sévérité élevée dans le dashboard Wazuh, avec vérification manuelle des faux positifs (ex : accès légitime à `lsass.exe` par Windows Defender vs technique de vol de credentials)
- Résolution de problématiques réseau concrètes : segmentation NAT/réseau isolé, configuration DHCP/IP statique, dépannage de connectivité inter-VM

**Compétences démontrées :**
- Déploiement et administration d'un SIEM open source de bout en bout
- Détection basée sur les logs et cartographie MITRE ATT&CK
- Administration Linux (Debian) et Windows Server / Active Directory
- Analyse de logs réseau (firewall, VPN, IDS) et requêtage SPL (Splunk)
- Diagnostic réseau (VMware networking, DHCP, NAT, VLAN isolé)

---

## 📜 Certifications

### ✅ Obtenues

- 🎓 **TryHackMe — Pre Security** (par examen) — mars 2026
- 🎓 **TryHackMe — Cyber Security 101** (45h) — décembre 2025
- 🎓 **ANSSI SecNumacadémie** — MOOC SSI complet (88-90%) — janvier 2026
- 🎓 **ANSSI / Club EBIOS** — Introduction EBIOS Risk Manager — janvier 2026
- 🎓 **Cisco Networking Academy** — Introduction to Cybersecurity — janvier 2026
- 🎓 **IBM SkillsBuild** — Cybersecurity Fundamentals — janvier 2026

### 🎯 En cours / Objectifs

- 🔄 **CompTIA Security+** (objectif 2027)
- ⏳ **TryHackMe SOC Level 1** (en cours)
- ⏳ **Blue Team Labs Online** (objectif 2027)

---


## 📊 Profils

- 🎮 **TryHackMe** : [Jubishop02](https://tryhackme.com/p/Jubishop)
- 💼 LinkedIn : <https://www.linkedin.com/in/julien-g-a000b399/>

---

## 🚀 Parcours d'apprentissage

### Actuellement en cours

- ✅ TryHackMe Jr Penetration Tester Path
- ✅ HackTheBox Academy - Penetration Tester Path
- ⏳ Préparation CompTIA Security+

### Objectifs 2026-2027

- Obtenir Security+ (Q2 2026)
- Obtenir PNPT (Q3 2026)
- 30+ writeups de machines HTB/THM
- Portfolio de 5+ scripts Python

---

## 💪 Atouts professionnels

**De la gendarmerie à la cybersécurité** :

- ✅ **Rigueur opérationnelle** : Respect strict des procédures (ISO 27001, ANSSI)
- ✅ **Gestion de crise** : 16 ans d'intervention en situations à haut risque
- ✅ **Analyse de menace** : Évaluation rapide et prise de décision sous pression
- ✅ **Travail en équipe** : Coordination d'opérations complexes
- ✅ **Habilitation Défense** : Possibilité d'obtenir clearance pour missions sensibles

---

## 📫 Contact

- 📧 Email : [<gazeaux.julien@gmail.com>]
- 💼 LinkedIn : <https://www.linkedin.com/in/julien-g-a000b399/>
- 🐙 GitHub : Vous êtes déjà ici !

---

## 📝 Notes

*Ce portfolio est en construction active. Nouveaux writeups et projets ajoutés régulièrement.*

*Dernière mise à jour : Septembre 2026*

---

**"De la protection physique à la protection numérique - même mission, nouveaux outils."**
