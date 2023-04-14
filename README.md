# TP2 - Industrialisation du Logiciel

Projet GitHub : https://github.com/seba-chappuis/idl-tp2

Projet  GitLab : https://gitlab-etu.ing.he-arc.ch/sebastie.chappuis3/idl-tp2

## Exercice 1

> Quelles étapes (steps) sont réalisées par cette action ?

- Mise en place de Python 3.10
- Installation des dépendances
- Utilisation du linter flake8
- Test avec pytest

> Une étape est définie au minimum par 2 éléments, lesquels sont-ils et à quoi servent-ils ?

- `name` : nom de l'étape
- `run` : commande à exécuter pour l'étape en question

> La première étape contient le mot-clé `with`, a quoi sert-il ?

À indiquer des paramètres supplémentaires pour l'étape en question, par exemple `python-version` pour spécifier la version de Python à utiliser.

## Exercice 2

> Sur l’onglet Summary d’une analyse de code, SonarCloud fournit 4 indicateurs.
> Quels sont-ils et quelles sont leurs utilités ?

- `Reliability` : fiabilité du code : nombre de bugs présents dans le code
- `Security` : sécurité du code : nombre de failles pouvant potentiellement être exploitées
- `Maintainability` : maintenabilité du code : nombre de "code smells" présents dans le code, c'est-à-dire du code qui est confus, difficile à lire, etc.
- `Security Review` : indique le code qui doit être évalué manuellement car il peut potentiellement poser un problème de sécurité

> À quoi sert l’indicateur Quality Gate ?

Un indicateur permettant de déterminer si le projet est prêt pour la production ou non suivant de nombreux critères.

> Quelle est la différence entre les sections New code et Overall Code dans l’onglet Summary ?

- La section "New code" indique les les résultats de la dernière analyse de code
- La section "Overall Code" indique les résultats de toutes les analyses de code

> Y a-t-il des Code Smells ? Si oui, combien et pour quelle(s) raisons(s) ?

Oui, trois code smells : deux sont un paramètre de fonction non utilisé (`deferred`) et un correspondant à deux fonctions identiques (`spend_cash` et `spend_money`).

> Y a-t-il des Security Hotspots ? Si oui, combien et pour quelle(s) raison(s) ?

Oui, une, avec le message suivant sur la ligne `FROM python:3.9` de `/Dockerfile` : "The python image runs with root as the default user. Make sure it is safe here."

## Exercice 3

> Que fait le job pytest ?

Le job `pytest` exécute les tests unitaires avec `pytest`.

> Que fait le job image-creation ?

Le job `image-creation` construit l'image Docker du projet.

> Que fait le job package-creation ?

Le job `package-creation` construit le package du projet.

> Les jobs s’exécutent-ils dans le même ordre que défini dans le fichier ? Sinon, pourquoi ?

Tous les jobs d'un même stage s'exécutent en parallèle. Si le stage d'un job n'est pas défini, il appartient au stage `test`.

Par défaut, les stages (dans l'ordre de leur exécution) sont : `build`, `test` et `deploy`.

Dans notre cas, le job `image-creation` appartient au stage `build` et est exécuté en premier, et les jobs `pytest` et `package-creation` appartiennent au stage `test` et sont exécutés en parallèle après le stage `build`.

> Le stage 2 génère une image Docker. Où est-elle stockée et comment pouvez-vous la retrouver ?

L'image Docker est accessible depuis l'onglet `Packages & Registries` de GitLab.

> Le stage 3 génère un wheel Python. Où est-il stocké et comment pouvez-vous le retrouver ?

Le wheel Python est stocké dans le dossier `/dist` à la racine du projet GitLab dans un fichier `.whl`.
