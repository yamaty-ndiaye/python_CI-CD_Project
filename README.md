CI/CD Pipeline — Calculatrice Python
Projet de démonstration d'un pipeline CI/CD avec GitHub Actions : tests automatisés, vérification de style de code, et déploiement, le tout containerisé avec Docker.
Architecture
.
├── app/
│   └── calculator.py        # Fonctions métier (addition, soustraction, multiplication, division)
├── tests/
│   └── test_calculator.py   # Tests unitaires (pytest)
├── .github/workflows/
│   └── ci.yml                # Pipeline CI/CD
├── Dockerfile
└── requirements.txt
Stack technique

Python 3.11 — logique métier et tests
pytest + pytest-cov — tests unitaires et couverture de code
flake8 — linting / qualité de code
Docker — containerisation de l'environnement de test
GitHub Actions — orchestration CI/CD

Pipeline CI/CD
Le workflow .github/workflows/ci.yml s'exécute à chaque push et pull request sur main, en 3 étapes séquentielles :

Lint — vérification du style de code avec flake8 sur app/ et tests/.
Test — exécution des tests unitaires avec pytest et mesure de la couverture (pytest-cov), sur une matrice de versions Python (3.10, 3.11, 3.12) pour garantir la compatibilité. Mise en cache des dépendances pip pour accélérer les exécutions.
Deploy — étape de déploiement, déclenchée uniquement sur un push vers main (pas sur les pull requests), après succès des étapes précédentes.

Chaque job dépend du précédent (needs:), garantissant qu'aucun déploiement ne se fait sans tests validés au préalable.
Lancer le projet en local
bash# Installer les dépendances
pip install -r requirements.txt

# Lancer les tests
pytest --cov=app tests/

# Vérifier le style de code
flake8 app/ tests/
Lancer avec Docker
bashdocker build -t calculator-app .
docker run calculator-app
Ce que ce projet démontre

Mise en place d'un pipeline CI/CD complet (lint → test → deploy) avec GitHub Actions
Tests automatisés multi-versions Python avec gestion du cache des dépendances
Containerisation d'une application Python avec Docker
Bonnes pratiques de qualité de code (linting, couverture de tests)

À venir

Remplacement de l'étape de déploiement simulée par un déploiement réel (ex : AWS Lambda, Cloud Run)
Ajout de tests d'intégration