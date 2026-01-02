# Checklist — Publication GitHub (Public) sans risque

Avant de rendre un projet PUBLIC, vérifier :

## À supprimer / anonymiser (obligatoire)
- IPs publiques/privées réelles (remplacer par 10.0.0.0/24 “exemple”)
- Noms d’hôtes, identifiants, emails internes, numéros de contrat
- Captures montrant des identités, noms de sites sensibles, tickets, logs bruts
- Secrets : mots de passe, clés API, tokens, certificats, config VPN
- Détails de sécurité exploitables (règles IPS/IDS complètes, ACL détaillées)

## À garder (valeur recruteur)
- Schéma d’architecture **anonymisé**
- “Mon rôle” et “décisions”
- Résultats mesurables (avant/après)
- Méthode : MCO/MCS, procédures, KPIs, tests
- Leçons apprises & améliorations

## Règle
Si une information peut aider un attaquant plus qu’un recruteur : **tu l’enlèves**.
