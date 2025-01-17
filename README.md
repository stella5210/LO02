# 1. Introduction

## 1.1 Contexte du projet

Ce projet consiste en un jeu de stratégie spatiale développé en Java. Le concept du jeu repose sur la thématique de **"l'Empire Galactique"**, où trois participants s'affrontent pour prendre le contrôle de l'univers à travers l'expansion (**Expand**), l'exploration (**Explore**) et l'anéantissement (**Exterminate**) de vaisseaux spatiaux. L'objectif est de récolter des points en envoyant des vaisseaux, en capturant des secteurs et en exploitant les ressources, le joueur ayant accumulé le plus de points étant déclaré vainqueur.

Dans le cadre de ce projet, notre but était de recréer un environnement de jeu complet, en développant un plateau interactif, des échanges entre les joueurs et un système de score dynamique via l'interface graphique Java (GUI). Le jeu est conçu pour accueillir de **2 à 3 joueurs**, incluant la possibilité de jouer contre des adversaires virtuels (**IA**) capables de prendre des décisions stratégiques élémentaires.

---
## 1.2 Signification du projet

### Amélioration des compétences techniques

Au cours de la conception et du développement de ce projet, nous avons approfondi notre compréhension et notre application des principes fondamentaux de la programmation orientée objet, tels que l'encapsulation, l'héritage et le polymorphisme. En particulier, la conception du plateau hexagonal nous a permis de renforcer notre compréhension et notre manipulation des structures de données complexes. En outre, le projet impliquait le développement de l'interface graphique Java, ce qui nous a permis de maîtriser l'utilisation de la bibliothèque Swing et de créer une interface simple et conviviale, améliorant ainsi nos compétences en développement d'interfaces graphiques.

### Renforcement des compétences en travail d'équipe

Le développement de ce projet a été réalisé en équipe. Grâce à une répartition claire des tâches et une communication active, nous avons pu accomplir chaque étape du projet, de l'analyse des besoins à l'implémentation finale. Ce mode de travail collaboratif a non seulement renforcé notre capacité à travailler ensemble efficacement, mais a également développé notre aptitude à coordonner les tâches et résoudre les conflits, posant ainsi les bases solides pour participer à des projets de développement d'envergure dans l'avenir.

---
# 2. Analyse des exigences

## 2.1 Exigences fonctionnelles

Les principales caractéristiques du jeu sont les suivantes :

1. **Rôles des joueurs et interactions**
   - Le jeu prend en charge 2 à 3 joueurs, avec la possibilité d'intégrer des joueurs virtuels (IA).
   - Les joueurs peuvent choisir la couleur de leurs vaisseaux et les déployer sur le terrain de jeu, avec des tours alternés.
   - À chaque tour, les joueurs doivent définir l'ordre d'exécution des cartes de commande et interagir via l'interface.

2. **Gestion du terrain de jeu et des secteurs**
   - Le jeu utilise un plateau hexagonal pour représenter les régions galactiques, avec des secteurs de niveaux variés (de Level 0 à Level 3).
   - Le secteur central, nommé "Tri-Prime", est un secteur crucial et fixe, servant d'objectif stratégique majeur dans le jeu.

3. **Contrôle des vaisseaux et actions**
   - Les joueurs peuvent utiliser la carte de commande "Expansion" pour déployer des vaisseaux dans les secteurs qu'ils dominent.
   - La carte de commande "Exploration" permet aux joueurs de déplacer leurs vaisseaux dans des secteurs adjacents pour explorer de nouvelles zones.
   - La carte de commande "Extermination" permet aux joueurs de combattre les vaisseaux ennemis et d'essayer de prendre de nouveaux secteurs.

4. **Système de points et but du jeu**
   - L'objectif du jeu est de gagner des points en contrôlant des secteurs et en exploitant des ressources. Les points sont attribués selon le niveau des secteurs contrôlés.
   - À la fin de chaque tour, chaque joueur doit sélectionner un secteur pour le score, et celui qui contrôle le secteur Tri-Prime peut choisir un secteur supplémentaire pour obtenir des points.
   - À la fin de la partie, tous les secteurs seront recalculés et leurs points doublés, le joueur ayant accumulé le plus de points étant désigné vainqueur.
---
## 2.2 Exigences non fonctionnelles

1. **Expérience utilisateur**
   - L'interface du jeu doit être claire et facile à utiliser, affichant de manière évidente le plateau hexagonal, les secteurs contrôlés par les joueurs et les scores en temps réel.
   - Le système doit offrir une réponse instantanée aux actions des joueurs et afficher des messages d'erreur lorsqu'une action incorrecte est effectuée, afin de minimiser les erreurs de manipulation.

2. **Performance du système**
   - Le jeu doit fonctionner sans accroc sur des ordinateurs standards, avec des réponses rapides aux actions des utilisateurs.
   - Les structures de données et les algorithmes doivent être optimisés afin de garantir que les calculs et le traitement des logiques du jeu se fassent dans un délai raisonnable.

3. **Extensibilité et maintenabilité**
   - Le système doit être développé de manière modulaire pour permettre l'ajout facile de nouvelles fonctionnalités dans le futur, comme l'intégration de nouvelles cartes de commande ou des IA plus complexes.
   - La structure du code doit être bien organisée et lisible, facilitant ainsi la maintenance, le débogage et les évolutions futures du système.
 ---
# 3. Conception du système

## 3.1 Architecture générale

L'architecture du jeu est divisée en plusieurs modules principaux :

1. **Module d'interface utilisateur** : Gère l'affichage visuel du jeu et l'interaction avec les joueurs.
   - **GameWindow** : Responsable de la représentation graphique de la fenêtre de jeu, affichant la grille hexagonale et l'interface générale du jeu.
   - **OccupationWindow** : Montre les informations concernant le contrôle de chaque secteur, incluant les joueurs qui en ont la possession et le nombre de vaisseaux présents.
   - **ScoreView** : Affiche les résultats des joueurs et met à jour les scores en temps réel.

2. **Module principal de logique de jeu** : Gère le déroulement du jeu, l'application des règles et les actions des participants.
   - **GameManager** : Le gestionnaire central du jeu, en charge de la gestion des tours, de l'exécution des cartes de commande, du calcul des points et de la gestion de la fin de partie.
   - **Player** et **VirtualPlayer** : Définissent le comportement des joueurs, les joueurs virtuels (IA) ayant des capacités décisionnelles de base permettant des choix tactiques simples.

3. **Module de gestion des données** : En charge de la gestion des données du plateau, des informations relatives à l'occupation des secteurs et des résultats.
   - **Hex** : Représente chaque cellule du plateau de jeu, en gérant les coordonnées et les relations de voisinage, ainsi que d'autres propriétés.
   - **Ship** : Représente les vaisseaux et leur position, leur état et leur comportement de déplacement. Il gère la création, le déplacement et la destruction des vaisseaux.
   - **HexagonView** : Organise la disposition du plateau hexagonal, les niveaux des secteurs, calcule les hexagones voisins et met à jour les informations de contrôle des secteurs.
   - **GameScore** : Gère le calcul et l'affichage des points des joueurs, avec la possibilité de consulter et de mettre à jour les scores pendant chaque tour.
   - **Sector** : Représente un secteur du plateau de jeu, comprenant le niveau du secteur et les informations liées à son contrôle.

4. **Module de gestion des commandes** : Implémente la logique des actions des joueurs via les cartes de commandes.
   - **Command** : Interface définissant les cartes de commande, toutes les actions (Expansion, Exploration, Extermination) doivent implémenter cette interface.
   - **CommandSystem** : En charge de la gestion et de l'exécution des commandes des cartes, assurant le bon déroulement des actions dans le jeu.
   - **Expand**, **Explore** et **Exterminate** : Ces classes définissent respectivement les commandes d'expansion, d'exploration et d'extermination, précisant le comportement et l'effet de chaque commande.

5. **Module stratégique** : Fournit la logique décisionnelle pour les joueurs ou les joueurs virtuels.
   - **Strategy** : Interface permettant aux joueurs ou aux joueurs virtuels de déterminer leur comportement et leurs choix stratégiques.
   - **AggressiveStrategy** et **DefensiveStrategy** : Représentent respectivement les stratégies d'attaque et de défense, utilisées par les joueurs virtuels pour prendre leurs décisions.
 ---
## 3.2 Diagramme de classes et relations (Actuel)
Le diagramme UML des classes présente clairement les différents modules et leurs relations dans l'implémentation actuelle, par exemple :
![UML Diagram](https://raw.githubusercontent.com/stella5210/LO02/main/UML_new.drawio.png)

---
## 3.3 Diagramme de classes précédentes et raisons des modifications
Voici le diagramme des classes de la version précédente du système, avec les raisons des changements appliqués :
![UML Diagram](https://raw.githubusercontent.com/stella5210/LO02/main/UML_old.drawio.png)
- **Modification des classes et des relations** :
- **Raison de la modification** : Cette révision a permis de rendre le code plus modulaire et plus facile à maintenir, en séparant clairement les responsabilités de chaque classe.



---
# 4. Implémentation du code

## 4.1 Structure du jeu

L'architecture du système du jeu se divise en plusieurs modules principaux :

### 1. **GameManager**
  - **Responsabilité :** Le `GameManager` est le contrôleur central du jeu, responsable de la gestion du déroulement des tours, de l'exécution des cartes de commande, du calcul des scores et de la logique de fin de jeu.

### 2. **Player et VirtualPlayer**
  - **Responsabilité :** La classe `Player` représente un joueur du jeu, tandis que la classe `VirtualPlayer` représente un joueur virtuel (IA) avec des capacités de décision de base permettant de faire des choix stratégiques simples.

### 3. **Ship et Hex**
  - **Responsabilité :** La classe `Ship` représente un vaisseau, gérant sa position, son état et ses comportements de déplacement. La classe `Hex` représente un hexagone sur le plateau de jeu, gérant les coordonnées et les relations de voisinage.

### 4. **GameScore et ScoreView**
  - **Responsabilité :** La classe `GameScore` gère le calcul et le stockage des scores des joueurs, tandis que la classe `ScoreView` affiche les scores en temps réel.

### 5. **CommandSystem et Command**
  - **Responsabilité :** Le `CommandSystem` gère l'exécution des commandes des joueurs, tandis que l'interface `Command` définit les différentes commandes du jeu (telles que l'Expansion, l'Exploration et l'Extermination).

---

## 4.2 Classes clés et fonctionnalités

### 1. **GameManager**

- **Responsabilité :** Le `GameManager` est l'élément central qui contrôle le déroulement du jeu, gère les joueurs et les phases de jeu.

- **Méthode clé :**

```java
public void startGame() {
    // Initialise le jeu et commence la phase de placement des vaisseaux
    EventQueue.invokeLater(() -> gameState.gameWindow.setVisible(true));
    EventQueue.invokeLater(() -> gameState.occupationWindow.displayOccupation());
    System.out.println("Ship placement starting");
    // Autres initialisations et placement des vaisseaux des joueurs
}
```
### 2. **Player et VirtualPlayer**
- **Responsabilité :** La classe `Player` est utilisée pour gérer les actions des joueurs, et `VirtualPlayer` est utilisée pour simuler un joueur contrôlé par IA, qui effectue des choix en fonction d'une stratégie simple.

- **Méthode clé :**

```java
public void addShip(Set<String> occupiedSectors) {
    // Le joueur choisit l'emplacement de ses vaisseaux
    Random rand = new Random();
    String selectedSector = availableSectors.get(rand.nextInt(availableSectors.size()));
    // Ajoute un vaisseau au secteur choisi
}

public void chooseCommandOrder() {
    // Le joueur choisit l'ordre d'exécution des cartes de commande
    List<Integer> commands = Arrays.asList(1, 2, 3);
    Collections.shuffle(commands);
    System.out.println("Command order: " + commands);
}
```

### 3. **Ship et Hex**
- **Responsabilité :** La classe Ship gère un vaisseau et son mouvement, tandis que la classe Hex gère la position des hexagones et la relation entre eux.
- **Méthode clé :**

```java
public class Ship {
    private Hex position;

    public void move(Hex target) {
        this.position = target;
        System.out.println("Ship moved to: " + target);
    }
}

public class Hex {
    private int q, r, s;  // Coordonnées de l'hexagone

    public boolean isNeighbor(Hex target) {
        // Vérifie si deux hexagones sont voisins
        return (Math.abs(this.q - target.q) + Math.abs(this.r - target.r) + Math.abs(this.s - target.s)) == 1;
    }
}
```
### 4. **GameScore et ScoreView**
- **Responsabilité :** La classe GameScore calcule et stocke les scores des joueurs, et ScoreView est responsable de l'affichage des scores pendant le jeu.

- **Méthode clé :**
```java
public class GameScore {
    public void calculateRoundScores() {
        // Calcule et met à jour les scores de chaque joueur
    }
}

public class ScoreView {
    public void updateScores() {
        // Met à jour l'affichage des scores
        System.out.println("Updating score view...");
    }
}
```
### 5. **CommandSystem et Command**
- **Responsabilité :** Le CommandSystem gère les commandes effectuées par les joueurs, tandis que l'interface Command définit les types de commandes.

- **Méthode clé :**
```java
public interface Command {
    void execute(Player player);
}

public class CommandSystem {
    public void executeCommand(Player player, Command command) {
        // Exécute la commande choisie par le joueur
        command.execute(player);
    }
}
```
---
## 4.3 Fonctionnalités du jeu

- **Plateau hexagonal** : Utilisation de la classe `Hex` pour représenter un plateau hexagonal, avec des informations sur les niveaux des secteurs et leur état.

- **Système de commandes** : Le joueur choisit parmi différentes commandes pour prendre des actions dans le jeu, chaque commande étant implémentée à travers des classes distinctes qui héritent de l'interface `Command`.

- **Système de points** : Le score est calculé en fonction des secteurs contrôlés par chaque joueur, avec une double comptabilisation des points à la fin du jeu.

---

## 4.4 Conclusion

Ce projet utilise une approche modulaire pour créer un jeu de stratégie basé sur des cartes et des secteurs hexagonaux. Chaque module est responsable d'une partie spécifique du jeu, avec un contrôle centralisé dans la classe `GameManager`. L'utilisation des classes `Player`, `Ship` et `Hex` permet de gérer les interactions entre les joueurs, les vaisseaux et le plateau de jeu. La logique des commandes et des scores est soigneusement intégrée pour créer une expérience de jeu fluide.

---
# 5. Processus de débogage et de test

## 5.1 Tests unitaires

Au cours du développement, nous avons utilisé des tests unitaires pour assurer la précision de chaque module fonctionnel. Voici le processus de test pour quelques modules clés :

### 5.1.1 Classes `Player` et `VirtualPlayer`

- **Objectif** : Tester les actions des joueurs, y compris l'ajout de vaisseaux et la sélection de l'ordre des commandes.
- **Contenu du test** :
  - Tester si le joueur peut correctement choisir et déployer des vaisseaux.
  - Tester si le joueur peut correctement choisir l'ordre des commandes.
  
  Méthodes pertinentes :
  - `addShip(Set<String> occupiedSectors)`
  - `chooseCommandOrder()`

### 5.1.2 Classes `Ship` et `Hex`

- **Objectif** : Tester le mouvement des vaisseaux et la relation d'adjacence des hexagones.
- **Contenu du test** :
  - Tester si un vaisseau peut se déplacer correctement vers la position cible.
  - Tester si deux hexagones sont voisins.
  
  Méthodes pertinentes :
  - `move(Hex target)`
  - `isNeighbor(Hex target)`
---
## 5.2 Tests d'intégration

Les tests d'intégration sont utilisés pour s'assurer que l'interaction entre les différents modules du système se déroule correctement, en particulier lorsque les joueurs effectuent des actions de commande.

### 5.2.1 Classe `GameManager`

- **Objectif** : Tester si le flux du jeu fonctionne correctement.
- **Contenu du test** :
  - Tester si les joueurs peuvent déployer correctement leurs vaisseaux au début du jeu.
  - Tester si les tours du jeu avancent correctement.
  - Tester si le système de points met à jour les scores correctement.
  
  Méthodes pertinentes :
  - `startGame()`
  - `nextTurn()`

### 5.2.2 Classe `CommandSystem`

- **Objectif** : Tester si les commandes sont exécutées correctement dans l'ordre choisi par le joueur.
- **Contenu du test** :
  - Tester si la commande choisie par le joueur est exécutée correctement.
  - Tester l'effet de chaque commande (Expansion, Exploration, Extermination).
  
  Méthodes pertinentes :
  - `executeCommand(Player player, Command command)`
---
## 5.3 Tests de l'interface utilisateur

### 5.3.1 Interface du jeu

- **Objectif** : Tester l'interactivité et la fonctionnalité de l'interface utilisateur.
- **Contenu du test** :
  - Tester si `GameWindow` affiche correctement le plateau de jeu.
  - Tester si `ScoreView` affiche et met à jour les scores correctement.
  
  Méthodes pertinentes :
  - `GameWindow.setVisible(true)`
  - `ScoreView.updateScores()`
---
## 5.4 Tests de performance

### 5.4.1 Performance du jeu

- **Objectif** : Tester si le jeu reste fluide avec plusieurs tours et joueurs.
- **Contenu du test** :
  - Simuler plusieurs tours et joueurs pour s'assurer que le jeu ne présente pas de goulots d'étranglement de performance.
  
  Méthodes pertinentes :
  - `GameManager.startGame()`
---
## 5.5 Gestion des erreurs et débogage

### 5.5.1 Validation des entrées

- **Objectif** : Tester si les entrées des utilisateurs sont correctement validées et traitées.
- **Contenu du test** :
  - Tester si des commandes invalides saisies par l'utilisateur génèrent un message d'erreur approprié.
  
  Méthodes pertinentes :
  - `chooseCommandOrder()`
---
# 6. Limites de l'implémentation

## 6.1 Fonctionnalités non implémentées

Bien que de nombreuses fonctionnalités aient été développées et testées, certaines fonctionnalités n'ont pas été implémentées dans cette version du jeu. Voici les principales limitations :

### 6.1.1 Sauvegarde et Chargement du jeu

- **Problème** : Le jeu ne prend pas en charge la sauvegarde et le chargement de l'état du jeu. Il est donc impossible de sauvegarder la progression du jeu pour la reprendre plus tard.
- **Limitation** : En raison de l'absence de cette fonctionnalité, chaque session de jeu commence à zéro et aucune donnée du jeu précédent ne peut être conservée.

### 6.1.2 Choix stratégique autonome du joueur virtuel

- **Problème** : Les joueurs virtuels (IA) dans le jeu ne choisissent pas de manière autonome des stratégies d'attaque ou de défense. Actuellement, les joueurs virtuels suivent des actions pré-définies sans capacité de décision stratégique en matière d'attaque ou de défense.
- **Limitation** : Bien que les joueurs virtuels soient capables d'effectuer des actions de manière autonome, ces actions ne sont pas basées sur une analyse de la situation de jeu ou des choix stratégiques complexes (telles que des stratégies d'attaque ou de défense élaborées).
---
## 6.2 Conclusion

Ces limitations représentent des aspects qui pourraient être ajoutés dans des versions futures du jeu. L'implémentation de la sauvegarde et du chargement ainsi que des stratégies autonomes pour les joueurs virtuels améliorerait significativement l'expérience de jeu et la flexibilité du système.

---
# 7. Bilan et Perspectives

## 7.1 Bilan

Le projet visait à développer un jeu de stratégie spatial basé sur Java. À travers ce projet, nous avons non seulement créé un jeu avec une interface graphique, mais aussi mis en place l'interaction entre les joueurs, le contrôle des vaisseaux et le système de score. Les principales réalisations du projet sont les suivantes :

- **Logique de jeu centrale** : Nous avons implémenté les contrôles des joueurs, la gestion des tours et l'exécution des cartes de commande.
- **Interface graphique** : À l'aide de la bibliothèque Swing de Java, nous avons conçu les fenêtres du jeu et l'affichage du plateau, permettant aux joueurs de suivre l'avancement du jeu.
- **Système de score** : Le score est calculé en fonction des secteurs contrôlés par les joueurs et des points attribués à chaque phase du jeu.
- **Joueur virtuel** : Nous avons développé une IA simple pour le joueur virtuel, capable d'effectuer des actions de base et de prendre des décisions élémentaires.

Cependant, le projet présente également certaines limites, notamment l'absence de fonctionnalités de sauvegarde et de chargement, ainsi que l'absence de capacité stratégique avancée pour les joueurs virtuels. Malgré cela, nous avons réussi à créer un système de jeu fonctionnel avec une base solide de stratégie.

---
## 7.2 Réflexions

Durant le développement du projet, nous avons rencontré plusieurs défis, le plus important étant de trouver un équilibre entre la complexité et la jouabilité du jeu. Grâce à un développement itératif, nous avons progressivement optimisé le design du jeu, ajusté les règles et l'interface pour garantir une expérience agréable aux joueurs. Par ailleurs, ce projet nous a permis d'approfondir notre compréhension de la programmation orientée objet (POO), notamment en ce qui concerne la conception de classes et la modularité.

Un autre point clé de notre apprentissage a été l'intégration de l'interface graphique pour améliorer l'interactivité et la visualisation du jeu. Bien que nous ayons utilisé la bibliothèque Swing, l'interface finale reste basique, mais elle a servi de fondation solide pour de futures améliorations et extensions.

---
## 7.3 Perspectives

Dans les versions futures, nous envisageons :

- **Ajouter des fonctionnalités de sauvegarde et de chargement** : Cela permettrait aux joueurs de sauvegarder leur progression et de reprendre le jeu plus tard, augmentant ainsi la commodité du jeu.
- **Améliorer l'IA des joueurs virtuels** : Actuellement, les joueurs virtuels n'effectuent que des actions basiques. Nous prévoyons d'introduire des stratégies plus complexes pour rendre l'IA plus intelligente et stimulante.
- **Optimiser l'interface graphique** : Nous comptons améliorer l'interface du jeu, en offrant une expérience utilisateur plus riche et intuitive, comme l'ajout d'animations et de menus interactifs.
- **Interaction directe via le panneau de jeu** : Dans les versions futures, les joueurs pourront interagir directement via le panneau de jeu, en cliquant sur les éléments pour exécuter des actions, afin de rendre l'expérience plus fluide et interactive.
---
## 7.4 Conclusion

Dans l'ensemble, ce projet a été une expérience très enrichissante qui nous a permis de mieux comprendre les divers aspects du développement de jeux, de la conception de l'interface graphique à la logique de jeu complexe, en passant par la création d'IA. Grâce à cette expérience, nous avons non seulement amélioré nos compétences en programmation, mais également renforcé notre capacité à travailler en équipe. Avec l'ajout de nouvelles fonctionnalités à l'avenir, nous sommes convaincus que ce jeu deviendra encore plus complet et stimulant.
