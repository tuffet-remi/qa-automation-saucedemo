# Plan de test : SauceDemo

## 1. Objectif
Vérifier le comportement de la page de connexion de saucedemo.com (identifiants valides, invalides, champs vides, compte bloqué) et détecter un bug d'affichage connu. Ce projet d'entraînement me permet aussi de pratiquer les outils du métier : automatisation (Playwright, pytest), suivi des anomalies (Jira) et versionnage (GitHub).

## 2. Périmètre
**Testé** : connexion (identifiants valides, invalides, champs vides, compte bloqué), affichage des images produits.
**Non testé** : panier, paiement, tri, performance, accessibilité, sécurité.

## 3. Stratégie
- Tests fonctionnels, cas positifs et négatifs
- Automatisation avec Playwright et pytest (test paramétré pour les champs vides)
- Anomalies documentées dans Jira ; un bug connu est marqué `xfail`

## 4. Environnement et outils
Site saucedemo.com, Python 3.12, Playwright, pytest, Chromium, Jira, GitHub

## 5. Données de test
| Compte | Mot de passe | Usage |
|---|---|---|
| standard_user | secret_sauce | parcours nominal |
| locked_out_user | secret_sauce | compte bloqué |
| problem_user | secret_sauce | bug visuel connu |

## 6. Cas de test
| ID | Cas | Résultat attendu | Test automatisé | Ticket Jira | Statut |
|---|---|---|---|---|---|
| TC01 | Connexion valide | Page Products affichée | test_connexion_reussie | REMI-1 | Passé |
| TC02 | Mauvais mot de passe | Message d'erreur affiché | test_connexion_mauvais_mot_de_passe | REMI-2 | Passé |
| TC03 | Utilisateur bloqué | Message « locked out », pas d'accès aux produits | test_utilisateur_bloque | REMI-4 | Passé |
| TC04 | Champs vides (3 combinaisons) | Message « Username is required » ou « Password is required » | test_connexion_champs_vides | REMI-5 | Passé |
| TC05 | Images produits (problem_user) | Une image différente par produit | test_images_produits_sont_differentes | REMI-3 | Échec attendu (bug connu) |

## 7. Critères d'entrée et de sortie
**Entrée** : site accessible, environnement installé, comptes de test disponibles.
**Sortie** : tous les tests exécutés ; tous passent sauf les bugs connus documentés dans Jira.

## 8. Risques et limites
- Site tiers de démonstration : il peut changer sans préavis
- Sélecteurs dépendants de la structure de la page
- Un seul navigateur (Chromium) par défaut

## 9. Gestion des anomalies
Chaque anomalie est un ticket Jira : étapes de reproduction, résultat attendu, résultat obtenu, sévérité, capture d'écran.