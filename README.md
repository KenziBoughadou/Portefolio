# Kenzi Boughadou

**Portfolio en intelligence artificielle et data science**

Je suis étudiant en **Master 1 MIAS à Centrale Lille et à l’Université de Lille**. Je m’intéresse au machine learning et au traitement du langage, notamment pour leurs applications en santé.

Ce portfolio rassemble trois projets personnels. Pour chacun, je pars d’une question, je compare plusieurs méthodes et j’examine leurs erreurs. Le code, les expériences et les résultats sont disponibles dans les dépôts pour permettre de suivre le raisonnement et de reproduire les calculs.

Je recherche un **stage en IA ou en data du 22 mars au 31 août 2027**, en priorité dans le domaine de la santé. Je souhaite ensuite poursuivre en alternance en M2 à partir de septembre 2027, pour douze mois.

[LinkedIn](https://www.linkedin.com/in/kenzi-boughadou-3a4422318/) · [GitHub](https://github.com/KenziBoughadou) · [Me contacter](mailto:kenzi.boughadou@gmail.com)

## Projets

| Projet | Sujet | Principaux outils |
|---|---|---|
| [PathMNIST Confidence](https://github.com/KenziBoughadou/pathmnist-confidence) | Classification d’images histologiques, calibration des probabilités et abstention | Python, scikit-learn, PyTorch, Streamlit |
| [Fashion-MNIST Study](https://github.com/KenziBoughadou/fashion-mnist-study) | Comparaison d’un réseau dense et d’un réseau convolutif | Python, PyTorch, NumPy, Matplotlib |
| [MediNote](https://github.com/KenziBoughadou/medinote) | Comparaison de deux méthodes de résumé de consultations fictives | Python, FastAPI, React, TypeScript, API LLM |

## PathMNIST Confidence : étudier la confiance d’un classifieur

**Un modèle qui classe mieux les images fournit-il aussi des probabilités plus fiables ?**

Sur PathMNIST, un jeu de neuf classes d’images histologiques, je compare une régression logistique sur les pixels aplatis à un petit CNN entraîné avec PyTorch. J’ajuste ensuite une température sur les sorties du CNN pour étudier l’effet de cette calibration sur ses probabilités.

Les données utilisées pour choisir le meilleur checkpoint sont distinctes de celles qui servent à ajuster la température. Les trois entraînements CNN, réalisés avec des graines différentes, et leurs calibrations sont terminés avant l’évaluation sur le test officiel.

Le CNN obtient un **macro-F1 de 0,7077 ± 0,0191**, contre **0,4353** pour la régression logistique. En revanche, la calibration réduit la perte logarithmique, ou NLL, sur les données d’ajustement mais l’augmente sur le test pour les trois graines. Une amélioration sur la partition de calibration ne se retrouve donc pas nécessairement sur de nouvelles données.

J’examine aussi le score de Brier, l’ECE, les diagrammes de fiabilité et les erreurs à haute confiance. Les courbes de risque en fonction de la couverture permettent d’observer ce qui se passe lorsque le modèle rejette les images les moins confiantes. Une application Streamlit permet d’explorer ces prédictions déjà calculées.

La comparaison a plusieurs limites. La régression logistique n’a pas convergé au terme des 300 itérations prévues. Les trois graines utilisent une seule partition, et les résultats sur un test provenant d’un autre centre clinique ne suffisent pas à démontrer une robustesse générale.

[Consulter le code](https://github.com/KenziBoughadou/pathmnist-confidence) · [Lire le protocole](https://github.com/KenziBoughadou/pathmnist-confidence/blob/main/docs/PROTOCOL.md) · [Voir les résultats](https://github.com/KenziBoughadou/pathmnist-confidence/blob/main/results/study/report/README.md)

## Fashion-MNIST Study : comparer deux architectures

**Quel est l’apport d’un réseau convolutif par rapport à un réseau dense de taille proche ?**

Cette étude compare un MLP et un CNN sur dix catégories de vêtements. Les modèles comptent environ 102 000 et 106 000 paramètres. Chacun est entraîné pendant quinze époques, avec trois graines et une partition commune. Pour une même graine, les deux modèles voient les exemples dans le même ordre.

La boucle d’entraînement PyTorch reste explicite. Elle comprend le calcul de la perte, la rétropropagation, la mise à jour des poids et la validation. Le meilleur checkpoint est retenu pour chaque entraînement, puis les six modèles sont évalués sur le test.

Le CNN atteint **91,04 ± 0,38 % d’exactitude**, contre **87,89 ± 0,42 %** pour le MLP. Il demande toutefois un temps d’entraînement moyen environ **2,75 fois plus long**. L’analyse des erreurs montre aussi que le gain global ne concerne pas toutes les classes pour la graine présentée en détail.

Cette comparaison porte sur deux architectures et des réglages précis. Un nombre de paramètres proche ne rend pas les modèles équivalents, et un même nombre d’époques ne correspond pas au même coût de calcul.

[Consulter le code](https://github.com/KenziBoughadou/fashion-mnist-study) · [Voir les six expériences](https://github.com/KenziBoughadou/fashion-mnist-study/blob/main/results/reference/report/README.md) · [Reproduire l’étude](https://github.com/KenziBoughadou/fashion-mnist-study/blob/main/docs/REPRODUCIBILITY.md)

*Dans les deux études d’images, les valeurs après « ± » sont des écarts-types d’échantillon calculés sur trois graines. Ce ne sont pas des intervalles de confiance.*

## MediNote : évaluer la fidélité d’un résumé

**Extraire les faits avant de rédiger permet-il de mieux conserver le contenu d’une consultation ?**

MediNote compare deux méthodes utilisant le même modèle de langage déjà entraîné. La première produit directement une note à partir d’un dialogue fictif. La seconde extrait des faits structurés, puis un programme Python les met en forme selon des règles fixes.

Sur quarante consultations de test, j’évalue les faits conservés, les omissions, les contradictions et la correspondance entre les citations et le texte. Le coût et le temps de réponse sont également mesurés.

Selon les règles d’évaluation amendées en version 1.1, la rédaction directe conserve **95,83 % des faits attendus**, contre **92,50 %** pour la méthode structurée. Dans cette expérience, la méthode structurée conserve donc moins de faits que la rédaction directe. Les deux méthodes échouent au critère strict du test de stress sur les dix paires de dialogues. Une analyse complémentaire détaille les omissions, tout en conservant ce résultat initial.

L’application React et FastAPI permet de comparer les notes, de retrouver les passages cités et d’exporter un brouillon à partir de consultations fictives prédéfinies.

Le corpus est artificiel et la relecture a été réalisée par l’auteur, sans second avis indépendant. Certaines règles d’évaluation ont été amendées après observation des sorties ; ces changements sont documentés. Aucun gain de temps en situation clinique n’a été mesuré.

[Consulter le code](https://github.com/KenziBoughadou/medinote) · [Essayer la démonstration](https://medinote.kbcompany.fr) · [Lire l’évaluation](https://github.com/KenziBoughadou/medinote/blob/main/docs/HUMAN_REVIEW_RESULTS.md)

## Méthodes et outils

Ces projets me permettent de travailler sur plusieurs aspects de l’IA : l’apprentissage supervisé avec scikit-learn, l’entraînement de réseaux avec PyTorch et l’évaluation de modèles de langage. J’utilise NumPy et Matplotlib pour les calculs et les figures, ainsi que Streamlit ou React et FastAPI pour rendre les résultats consultables.

J’accorde une attention particulière à la séparation des données, au choix des métriques et à l’analyse des erreurs. Les dépôts comprennent des tests, les versions des dépendances et les commandes de reproduction. MediNote utilise également Docker et GitHub Actions.

**MediNote et PathMNIST Confidence sont des projets académiques. Ils n’ont pas fait l’objet d’une validation clinique et ne sont pas destinés à un usage diagnostique.**

<details>
<summary>Autres projets : cybersécurité</summary>

Mon parcours comprend aussi une formation en cybersécurité et management. Voici les projets réalisés dans ce domaine :

[Gestionnaire de mots de passe](https://github.com/KenziBoughadou/PasswordManager) · [Scanner SQL Injection](https://github.com/KenziBoughadou/SQL-Injection-Scanner) · [Scanner réseau ARP](https://github.com/KenziBoughadou/Network-Scanner)

[Vérificateur de robustesse des mots de passe](https://github.com/KenziBoughadou/Password-Strength-Checker) · [Sécurisation du SI d’un établissement hospitalier](https://github.com/KenziBoughadou/Securisation-SI-d-un-etablissement-hospitalier) · [Projet de sécurisation d’une clinique](https://docs.google.com/document/d/1PHJfkF1azAh7t2jBwTaKjhOJtszHBK0MQ2s4fL786Jo/edit?usp=sharing)

</details>
