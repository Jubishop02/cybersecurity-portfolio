# 🛡️ Lab SIEM - Blue Team

## 🎯 Objectif

Ce lab a pour but de pratiquer les compétences d'un **analyste SOC / Blue Team** dans un environnement simulé proche d'un réseau d'entreprise réel.

Il me permet de :
- Déployer et administrer un **SIEM Wazuh**
- Superviser des machines **Linux et Windows** via des agents
- **Détecter et analyser** des événements de sécurité
- Comprendre les **TTPs des attaquants** pour mieux les détecter
- Pratiquer la **réponse à incident**

---

## 🏗️ Infrastructure

| VM | OS | Rôle |
|---|---|---|
| Ubuntu 24.04 | Ubuntu 24.04 LTS | Serveur SIEM Wazuh |
| Debian 13 | Debian 13 Trixie | Cible Linux supervisée |
| Windows Server 2025 | Windows Server 2025 | Contrôleur de domaine AD |
| Windows 10 Pro | Windows 10 Pro | Poste client AD supervisé |
| Kali Linux | Kali Linux | Simulation d'attaques |
| Metasploitable2 | Ubuntu 8.04 | Cible vulnérable |
| REMnux | REMnux | Analyse de malware |

➡️ [Architecture détaillée](infrastructure/architecture-lab.md)

---

## 🔧 Stack technique

| Outil | Version | Usage |
|---|---|---|
| Wazuh | 4.14.4 | SIEM / XDR |
| OpenSearch | 2.x | Indexation des logs |
| VirtualBox | 7.x | Hyperviseur |
| Active Directory | Windows Server 2025 | Simulation réseau entreprise |

---

## 📁 Contenu

### Infrastructure
- [Architecture du lab](infrastructure/architecture-lab.md)

### Wazuh
- [Installation et configuration](wazuh/installation-configuration.md)
- [Règles de détection](wazuh/regles-detection.md)

### Détection
- [Détection scan Nmap](detection/scan-nmap.md)
- [Détection exploitation vsftpd](detection/exploitation-vsftpd.md)

---

## 📈 Progression

- [x] Déploiement Wazuh all-in-one
- [x] Configuration agents Linux et Windows
- [x] Mise en place Active Directory
- [x] Détection de vulnérabilités (122 CVE critiques identifiées)
- [ ] Règles de détection personnalisées
- [ ] Intégration MITRE ATT&CK
- [ ] Playbooks de réponse à incident
- [ ] Analyse de malware avec REMnux

---

## 🔗 Liens utiles

- [Documentation Wazuh](https://documentation.wazuh.com)
- [MITRE ATT&CK](https://attack.mitre.org)
- [CVE Database](https://cve.mitre.org)
