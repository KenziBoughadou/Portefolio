# Kenzi Boughadou — Portfolio IA & Data

**Machine learning · Deep learning · NLP appliqué**

Étudiant en **Master 1 MIAS à Centrale Lille et à l’Université de Lille**, je m’intéresse à l’évaluation des modèles et à leurs applications en santé. Ces trois projets personnels relient une question expérimentale, une implémentation lisible et une analyse des résultats, y compris lorsqu’ils contredisent l’amélioration attendue.

**Recherche de stage en IA / Data, en priorité dans la santé : du 22 mars au 31 août 2027.** Alternance M2 envisagée dès septembre 2027, pour douze mois.

[LinkedIn](https://www.linkedin.com/in/kenzi-boughadou-3a4422318/) · [GitHub](https://github.com/KenziBoughadou) · [Contact](mailto:kenzi.boughadou@gmail.com)

## Trois projets, trois questions

| Projet | Question étudiée | Outils principaux |
|---|---|---|
| [PathMNIST Confidence](https://github.com/KenziBoughadou/pathmnist-confidence) | Un modèle plus performant donne-t-il des probabilités plus fiables ? Quand s’abstenir ? | Python, scikit-learn, PyTorch, Streamlit |
| [Fashion-MNIST Study](https://github.com/KenziBoughadou/fashion-mnist-study) | Que change une architecture convolutive face à un réseau dense de capacité proche ? | Python, PyTorch, NumPy, Matplotlib |
| [MediNote](https://github.com/KenziBoughadou/medinote) | Extraire des faits avant de rédiger une note améliore-t-il sa fidélité au dialogue ? | Python, FastAPI, React, TypeScript, API LLM |

Ces travaux couvrent l’apprentissage supervisé, l’entraînement de réseaux neuronaux et l’évaluation d’un modèle de langage déjà entraîné. Les deux projets liés à la santé sont académiques : **aucun usage diagnostique ni validation clinique**.

## PathMNIST Confidence — performance, calibration et abstention

Sur neuf classes d’images histologiques, je compare une **régression logistique**, un **petit CNN entraîné depuis une initialisation aléatoire** et **le même CNN après temperature scaling**.

La validation officielle est séparée en deux partitions stratifiées : sélection du checkpoint et ajustement de la température. Les trois graines CNN sont entraînées et calibrées avant l’évaluation finale sur le test officiel.

**Résultat observé :** le macro-F1 du CNN atteint **0,7077 ± 0,0191**, contre **0,4353** pour la baseline. La température réduit la NLL sur la calibration, mais l’augmente sur le test pour les trois graines. Les erreurs très confiantes persistent ; la calibration n’apporte donc pas une amélioration générale de la fiabilité.

L’analyse comprend NLL, Brier, ECE, diagrammes de fiabilité, erreurs et courbes risque–couverture. **Streamlit explore les prédictions enregistrées**, sans entraînement dans l’application.

**Limites :** baseline non convergée à 300 itérations, trois graines sur une partition fixe, aucune robustesse générale démontrée au changement de centre clinique.

[Code et présentation](https://github.com/KenziBoughadou/pathmnist-confidence) · [Protocole](https://github.com/KenziBoughadou/pathmnist-confidence/blob/main/docs/PROTOCOL.md) · [Résultats complets](https://github.com/KenziBoughadou/pathmnist-confidence/blob/main/results/study/report/README.md)

## Fashion-MNIST Study — comparer MLP et CNN

Je compare un **réseau dense** et un **réseau convolutif**, avec environ 102 000 et 106 000 paramètres, sur dix catégories de vêtements. Chaque modèle est entraîné pendant quinze époques avec trois graines, une partition commune et le même ordre des lots pour une graine donnée.

La boucle PyTorch explicite l’apprentissage, la validation et la sauvegarde du meilleur checkpoint. Les six entraînements précèdent l’évaluation sur le test ; l’étude conserve les erreurs, les courbes et les durées CPU.

**Résultat observé :** le CNN atteint **91,04 ± 0,38 % d’exactitude**, contre **87,89 ± 0,42 %** pour le MLP. Sa durée moyenne d’entraînement est environ **2,75 fois supérieure**. L’amélioration globale ne se retrouve pas dans toutes les classes pour la graine illustrée.

**Limites :** des capacités proches et un budget identique en époques ne rendent pas les architectures ni leur coût équivalents. Le résultat reste propre à ces réglages et à Fashion-MNIST.

[Code et présentation](https://github.com/KenziBoughadou/fashion-mnist-study) · [Six expériences et figures](https://github.com/KenziBoughadou/fashion-mnist-study/blob/main/results/reference/report/README.md) · [Reproductibilité](https://github.com/KenziBoughadou/fashion-mnist-study/blob/main/docs/REPRODUCIBILITY.md)

*Pour les deux études d’images, les valeurs « ± » sont des écarts-types d’échantillon sur trois graines, pas des intervalles de confiance.*

## MediNote — fidélité des résumés et traçabilité des sources

À partir de consultations fictives en français, je compare deux méthodes utilisant le même modèle de langage : **rédaction directe d’une note** et **extraction structurée de faits suivie d’une mise en forme déterministe**.

L’évaluation distingue couverture des faits, omissions, contradictions et soutien des citations. Elle mesure aussi coût et latence. Le test principal porte sur quarante consultations ; les cas de stress restent séparés.

**Résultat observé :** la rédaction directe conserve **95,83 % des faits attendus**, contre **92,50 %** pour la méthode structurée, selon l’évaluation amendée v1.1. Les deux méthodes échouent au critère strict du stress sur les dix paires ; un diagnostic exploratoire détaille les omissions sans remplacer ce résultat.

L’application **React / FastAPI** permet de comparer les notes, de retrouver leurs sources et d’exporter un brouillon. La démonstration utilise des consultations fictives prédéfinies.

**Limites :** corpus artificiel, relecture par l’auteur sans second avis indépendant, règles d’évaluation amendées après observation. Aucun gain de temps clinique n’est établi.

[Code et présentation](https://github.com/KenziBoughadou/medinote) · [Démo en ligne](https://medinote.kbcompany.fr) · [Méthodologie et résultats](https://github.com/KenziBoughadou/medinote/blob/main/docs/HUMAN_REVIEW_RESULTS.md)

## Compétences mises en pratique

| Domaine | Réalisations consultables dans les dépôts |
|---|---|
| Machine learning et deep learning | Prétraitement, régression logistique, MLP, CNN, boucles PyTorch, checkpoints |
| Évaluation expérimentale | Séparation des données, répétitions par graine, analyse des erreurs, calibration et abstention |
| NLP et évaluation de LLM | Extraction structurée, comparaison de pipelines, annotations, bootstrap apparié, coût et latence |
| Développement logiciel | API FastAPI, interfaces React et Streamlit, tests, Git, Docker et CI pour MediNote |
| Reproductibilité | Versions figées, protocoles documentés, prédictions archivées et rapports régénérables |

Les dépôts donnent accès au code, aux résultats détaillés, aux limites et aux commandes de reproduction. Les pistes d’amélioration sont distinguées des expériences effectivement exécutées.

<details>
<summary>Parcours antérieur — projets de cybersécurité</summary>

Mon parcours comprend également une formation en cybersécurité et management. Les projets précédents restent accessibles :

- [Gestionnaire de mots de passe](https://github.com/KenziBoughadou/PasswordManager)
- [Scanner SQL Injection](https://github.com/KenziBoughadou/SQL-Injection-Scanner)
- [Scanner réseau ARP](https://github.com/KenziBoughadou/Network-Scanner)
- [Vérificateur de robustesse des mots de passe](https://github.com/KenziBoughadou/Password-Strength-Checker)
- [Sécurisation du SI d’un établissement hospitalier](https://github.com/KenziBoughadou/Securisation-SI-d-un-etablissement-hospitalier)
- [Projet de sécurisation d’une clinique](https://docs.google.com/document/d/1PHJfkF1azAh7t2jBwTaKjhOJtszHBK0MQ2s4fL786Jo/edit?usp=sharing)

</details>
