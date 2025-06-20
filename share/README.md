# Dossier `share`

Ce répertoire est **public** et contient uniquement des ressources pouvant être partagées sans risque (pas de données sensibles ni propriétaires).

## Règles de contribution

1. **Aucune information sensible** : pas de données personnelles identifiables (PII), secrets, clés ou mots de passe.
2. **Transparence** : pas de contenu mensonger, trompeur ou abusif.
3. **Organisation stricte** : respecter l'arborescence décrite ci-dessous ; un fichier doit avoir une place claire.
4. **Qualité de code** : pour tout code Python, respecter :
   * Python ≥ 3.8 avec *type hints* ;
   * Conventions PEP 8 ;
   * Docstrings Google/NumPy ;
   * Pydantic pour la validation et exceptions explicites ;
   * Logging structuré.
5. **Documentation** : chaque fichier doit commencer par un en-tête mentionnant : titre, auteur, date, objectif.
6. **Jeux de données** : toujours fournir un `dataset_card.md` décrivant source, schéma, licence.
7. **Notebooks** : doivent être exécutables de bout en bout et accompagnés d'un export HTML dans `demos/`.
8. **Historique** : chaque changement significatif doit être ajouté au `CHANGELOG.md`.

## Arborescence standard

```
share/
├── docs/                # Guides, articles, présentations
│   ├── architecture/    # Diagrammes, décisions d'architecture
│   ├── api/             # Spécifications OpenAPI / Swagger
│   └── how_to/          # Tutoriels, pas-à-pas
├── datasets/            # Extraits de données non sensibles
├── notebooks/           # Notebooks Jupyter
├── demos/               # Applications ou scripts de démonstration
├── media/               # Images, vidéos, slides
├── reference/           # Articles académiques, livres blancs
├── LICENSE.md           # Licence du contenu partagé
└── README.md            # (ce fichier)
```

Merci de contribuer de façon responsable ! 🍀