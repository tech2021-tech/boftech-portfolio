# Wi-Fi Voyageurs — Architecture & Intégration (version anonymisée)

## 1) Contexte & objectif
Déploiement d’un service **Wi-Fi voyageurs** sur un site à forte criticité (continuité de service, exigences de sécurité, support).  
Objectifs :
- offrir une expérience utilisateur stable (accès Wi-Fi / portail captif selon périmètre),
- garantir une **segmentation stricte** entre voyageurs et environnements internes,
- mettre en place une architecture **exploitable** (tests, runbook, points de contrôle).

## 2) Portée (scope)
### Inclus
- cadrage technique (dépendances, flux, contraintes),
- conception de l’architecture cible (zones, redondance, flux),
- intégration réseau (VLAN, trunks/uplinks, services IP selon périmètre),
- intégration sécurité (politiques firewall, filtrage inter-zones, NAT),
- plan de tests (connectivité, segmentation, résilience) + mise en production,
- livrables d’exploitation (procédures, rollback, points de contrôle) + support initial.

### Exclu
- développement applicatif du portail (si pris en charge par un éditeur),
- tarification/monétisation (si hors périmètre).

### Contraintes
- disponibilité : déploiement progressif et sans impact sur les services critiques,
- sécurité : principe du moindre privilège et cloisonnement,
- exploitation : traçabilité, procédures simples, escalade claire.

## 3) Architecture cible (vue logique)
Le design repose sur une architecture redondée :
- **Edge sécurité** : firewall avec **double WAN**, NAT et politiques d’accès,
- **Cœur de réseau** : **2 switches cœur/distribution** en redondance,
- **Contrôle Wi-Fi** : **2 contrôleurs Wi-Fi** en redondance,
- **Services IP** : **2 serveurs DHCP** en redondance,
- **Accès** : **12 switches d’accès** alimentant **56 AP** et la distribution terrain.

> Le schéma détaillé est volontairement anonymisé (pas de noms internes, pas d’IPs réelles).

flowchart LR
  subgraph Edge
    WAN1((WAN 1)) --> FW[Firewall - NAT - Policies];
    WAN2((WAN 2)) --> FW;
  end

  subgraph Core_Distribution
    FW --> CORE1[Core Dist Switch A];
    FW --> CORE2[Core Dist Switch B];
  end

  subgraph Services
    DHCP1[DHCP Server A] --> CORE1;
    DHCP2[DHCP Server B] --> CORE2;
    CTRL1[WiFi Controller A] --> CORE1;
    CTRL2[WiFi Controller B] --> CORE2;
  end

  subgraph Access_WiFi
    CORE1 --> ACCESS[Access Switches x12];
    CORE2 --> ACCESS;
    ACCESS --> APS[APs x56 + Clients];
  end
