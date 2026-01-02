# Wi-Fi Voyageurs — Architecture & Intégration (version anonymisée)

## 1) Contexte & objectif
Un service Wi-Fi voyageurs devait être déployé sur un site à forte criticité (forte affluence, exigences d’image et de continuité de service).  
L’objectif était de **mettre en place une architecture robuste et sécurisée** permettant :
- une **expérience utilisateur stable** (accès Internet / portail captif),
- une **segmentation réseau stricte** (réseaux voyageurs vs internes),
- une **exploitation maintenable** (supervision, procédures, support).

## 2) Portée (scope)
### Inclus
- Cadrage technique (périmètre, dépendances, flux)
- Design d’architecture (réseau, sécurité, intégration)
- Intégration avec les composants existants (réseau, DHCP/DNS, firewall)
- Mise en place des règles de segmentation et des accès
- Mise en exploitation (tests, documentation, support)

### Exclu
- Développement applicatif du portail (si réalisé par un éditeur/tiers)
- Gestion commerciale (tarification, marketing) le cas échéant

### Contraintes
- Disponibilité élevée (pas d’interruption sur les services critiques)
- Sécurité : séparation stricte des environnements
- Exploitation : procédures simples et traçables
- Déploiement progressif (tests puis généralisation)

## 3) Architecture (schéma)
Un schéma anonymisé est à déposer dans `diagram/` (PNG/SVG) : `diagram/diagram.png`.

### Vue logique (description)
- **Zone Accès Wi-Fi** : points d’accès / contrôleur (selon environnement)
- **Zone Captive Portal** : portail/hotspot, API et backoffice (si applicable)
- **Zone Sécurité** : firewall (filtrage, NAT, politiques)
- **Zone Services** : DHCP/DNS, éventuels services d’authentification
- **Zone Observabilité** : logs & supervision (au minimum indicateurs et traces)

### Principes clés
- Segmentation par VLAN / zones (Voyageurs ≠ Interne)
- Flux minimaux nécessaires (principe du moindre privilège)
- Traçabilité : journaux d’accès, événements, incidents

## 4) Mon rôle (ce que j’ai fait)
Rôle principal : **conception & intégration de l’architecture**, avec un focus sur la sécurité et la mise en exploitation.

Responsabilités :
- Analyse des dépendances (réseau, DNS/DHCP, sécurité)
- Proposition d’architecture cible (flux, zones, segmentation)
- Mise en place/validation des configurations (VLAN, règles firewall, NAT, accès)
- Coordination technique avec les parties prenantes (ops/sécurité/éditeur)
- Plan de test (connectivité, segmentation, résilience) et passage en prod
- Documentation opérationnelle (procédures, points de contrôle, runbook)

Décisions techniques (exemples) :
- Séparation stricte “voyageurs / internes” + filtrage des flux
- Standardisation des règles réseau et des points de contrôle
- Mise en place d’un minimum de supervision et d’alerting (disponibilité/erreurs)

## 5) Résultats mesurables
*(à compléter avec tes chiffres réels, même approximatifs mais cohérents)*
- Disponibilité service : **≥ 99%** sur la période d’exploitation (hors maintenances planifiées)
- Réduction des incidents récurrents : **-X%** après standardisation (procédures + contrôles)
- Temps moyen de résolution (MTTR) : **réduit de X à Y** grâce au runbook et aux points de contrôle
- Segmentation validée : **0 passage** non autorisé entre zones (tests de séparation OK)

## 6) Risques & mitigations
- Risque : confusion entre réseaux (voyageurs vs interne)  
  → Mitigation : VLAN/zone dédiés + filtrage strict + tests de séparation
- Risque : dépendances DNS/DHCP (pannes ou mauvaises options)  
  → Mitigation : vérifications, procédure de rollback, tests utilisateurs
- Risque : indisponibilité portail / service tiers  
  → Mitigation : mode dégradé prévu + supervision + plan d’escalade

## 7) Leçons apprises
- Une architecture “simple et cloisonnée” gagne sur une architecture complexe.
- Le passage en production réussit quand les **flux sont documentés** et que les tests sont cadrés.
- La valeur est autant dans la technique que dans l’**exploitation** (runbook, KPI, responsabilités).

## 8) Suite / Roadmap
- Renforcer les KPI : capacité, expérience utilisateur, erreurs portail, latence
- Automatiser davantage : sauvegardes configs, contrôles de conformité, reporting régulier
- Formaliser une revue trimestrielle sécurité/exploitation (changements, incidents, améliorations)
