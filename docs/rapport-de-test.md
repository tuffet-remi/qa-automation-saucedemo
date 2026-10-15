# Rapport de test : exécution du 14/10/2026
**Environnement** : Python 3.12.10, pytest 9.1.1, Playwright 1.63.0 (plugin pytest-playwright 0.9.0), Chromium
**Résultat** : 6 réussis, 1 échec attendu (xfail), durée 5.06s
**Anomalie connue** : images identiques pour problem_user, ticket Jira REMI-3
**Conclusion** : 6 tests sur 7 passent. Le 7e détecte un bug connu (REMI-3, sévérité mineure, affichage) à corriger côté application. Aucune autre anomalie détectée.