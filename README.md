# Technical Design Document (TDD)

## Table of Contents
1. [Introduction](#1-introduction)
2. [Gameplay](#2-gameplay)
3. [Interface Utilisateur (UI/UX)](#3-interface-utilisateur)
4. [Architecture Technique](#4-architecture-technique)
5. [Plan de Développement](#5-plan-de-developpement)
6. [Ressources et Références](#6-ressoures-et-références)
7. [Nomenclature](#7-nomenclature)
8. [UML](#8-uml)
9. [Optionnel](#9-optionnel)

## 1. Introduction

### 1.1 Nom du projet
**Nom du jeu** : _Portal Dash_  
**Équipe** : _GTech3: Gathelier Axel, Enzo Mirabella, Romain Ponsignon, David De Oliveira, Axel Picou_  
**Date de création** : _18-02-2025_  
**Version du document** : _1.1.0_  

### 1.2 Objectif du projet
Résumé du concept du jeu : _Un endless runner en 2.5D où le joueur traverse des portails changeant à la fois l'environnement et le gameplay, passant d'un surf dans la neige façon Alto, à un vol inspiré de Geometry Dash dans un monde futuriste spatial, puis à une course sur des voies ferrées façon Little Big Planet dans une mine._

### 1.3 Plateformes et technologies
- **Plateformes cibles** : _Android_  
- **Moteur de jeu** : Unreal Engine _5.4_  
- **Langages de programmation** : blueprint
- **Gestion de version** : GitHub _https://github.com/GamingCampus-MillieBourgois-24-25/grand-projet-commun-portal-dash_  

---

## 2. Gameplay

### 2.1 Mécaniques de base
- **Type de jeu** : Runner infini
- **Déplacement** : Automatique vers la droite
- **Contrôles** : _Swipe haut/bas, tap_  
- **Obstacles et dangers** : _Differents obstacles en fonction de la thématique du monde/portail_
- **Collectibles** : _Pièce dispersé dans les mondes_
- **Pièce** : _Servent à acheter des boosts à utiliser en début de game ou les améliorer_

### 2.2 Système de portails
- **Fréquence d’apparition** : _Les portails apparaîtront après temps donné dans le level._  
- **Effets visuels et sonores associés** : fondu au noir + son de traversé du portail_  
- **Conséquences sur le gameplay** : _Impact sur la difficulté due au changement de gameplay répété, modification de la mécanique de gameplay_
  - **Portail du niveau de la neige :** Passage à un gameplay de surf. Le joueur glisse sur une pente et doit appuyer sur son écran pour sauter et esquiver les différents obstacles. Plus le joueur appuis longtemps, plus il saute haut (dans la limite du raisonable/ valeur de hauteur max à attribuer plus tard).
  - **Portail du niveau de la mine/western:** Passage à un gameplay de choix (le joueur a le choix de plusieur voie a certains point de la carte)
  - **Portail du niveau futuriste :** Passage à un gameplay type vaisseau Geometry Dash

### 2.3 Power-ups et objets spéciaux
- **Types de power-ups** : Un power-up commun pour chaque monde "bouclier", ainsi que 2 power-up par niveau 
  - Western:
    - Lasso "Aimant qui attire les pièces";
    - TNT "Détruit obstacle activation automatiquement";
     
  -  Neige:
      -  Planneur "S'active en saut";
      -  Vin chaud "x2 en pièce";
  -  Futuriste:
      -  Laser "Détruit les obstacles, activation automatique";
      -  Dash "Wrap sur une distance prédéfinie tant mètres";


- **Durée d’effet** : _En fonction du temps en seconde_  
- **Méthode d’obtention** : _Collectable dans les niveaux_  

### 2.4 Système de Score et Progression
- Calcul du score : Le score se calcule par la distance parcourue dans la game. La métrique utilisée est le mètre.
- Système de missions : Il y a des objectifs de base qui dès qu’ils sont complétés, des nouveaux apparaîtront. Il y a également des missions hebdomadaires qui sont bien plus longues à réaliser, et ces quêtes se réinitialisent toutes les semaines.

- système de mise à niveau des power-ups pour prolonger leur durée ou renforcer leurs effets.  
---

## 3. Interface Utilisateur (UI/UX)

### 3.1 Éléments du HUD
- **Affichage du score** : _En haut à gauche; Score qui s'incrémente en temps réel_  
- **Affichage des power-ups actifs** : _Icônes rondes; Timers visuels sur l'icône (icône affiche le timer sous forme de la perte de couleur de l'asset en fonction du temps et dans le sens de temps)_  
- **Boutons et interactions in-game** : _Bouton pause en haut à droite sous forme d'icône; Interactions avec le jeu en appuyant partout autre que sur le bouton pause_

### 3.2 Menus et navigation
- **Écran titre** : _Bouton regarder une pub pour un bonus; Bouton pour aller dans les paramètres; Bouton invisible au milieu de l'ecran pour lancer la partie (comme Subway Surfer); Affichage des objectifs en cours en bas au milieu de l’écran_  
- **Paramètres** : _Volume (Musique, Bruitage); graphismes (Low, Medium, High)_
- **Pause** : _Accès aux paramètres; Affichage des objectifs en cours_

---

## 4. Architecture Technique

### 4.1 Organisation du projet Unreal Engine
- **Structure des scènes** : _Scene Menu Principale, Scene Jeu, Scene Ecran de Chargement_  
- **Système de génération du niveau** : _Chunk pré-générer placé de façon aléatoire_  
- **Gestion des assets** : _Les chunks hors affichage sont Destroy_  
- **Système de gestion des portails** : _Post Process avec shake de la camera + fondu au noir + FX_
- **Sytème de sauvegarde** : _Unreal Engine Blueprint_

### 4.2 Performances et optimisation
- **Techniques utilisées** : _Profilage (Permet de checker les performance)_  
- **Ciblage FPS** : _adaptatif_  

---

## 5. Plan de Développement

### 5.1 Roadmap
- **Phase 1 : Prototype de chaque gameplay des portails** (1semaine)  
- **Phase 2 : Ajustement des prototypes et ajouts des gameplay secondaires** (1semaine)  
- **Phase 3 : Ajout de l’UI et des feedbacks** (2jour)  
- **Phase 4 : Optimisation et tests** (2jour)  
- **Phase 5 : Release** (_25-04-2025_)  

### 5.2 Répartition des tâches
- **Développeurs** : _Gathelier Axel, David De Oliveira, Axel Picou, Enzo Mirabella, Romain Ponsignon_  
- **Graphistes/UI** : _Axel Picou, Enzo Mirabella_  
- **Sound Design** : _Romain Ponsignon, Gathelier Axel_  
- **Testeurs** : _Gathelier Axel, Gaming Campus_  

---

## 6. Ressources et Références

- **Dépôt GitHub** : _https://github.com/GamingCampus-MillieBourgois-24-25/grand-projet-commun-portal-dash_
- **Recherche Unreal** :
  - Timeline (équivalent à DoTween) : https://dev.epicgames.com/documentation/en-us/unreal-engine/timelines-in-unreal-engine / https://www.youtube.com/watch?v=UlcK7MSP75w
  - In-Game Ads (équivalent à Unity Ads) : https://www.fab.com/listings/f8aabb9a-7c96-4f79-97ff-04bcc146e595
  - Charger un Level de manière asynchrone (pour les écran de chargement) : https://www.fab.com/listings/f8aabb9a-7c96-4f79-97ff-04bcc146e595
  - Force Feedback (retour haptique) : https://www.youtube.com/watch?v=aKNYdT-rR8U
  - Système de Sauvegarde: https://www.youtube.com/watch?v=6CP8BhrOdgU / https://dev.epicgames.com/documentation/en-us/unreal-engine/saving-and-loading-your-game-in-unreal-engine
  - Tuto Unreal Engine Post-Process : https://www.youtube.com/@UnrealCG / https://www.youtube.com/watch?v=ezRd6t7ZNHE&t=30s
  - Recuperer temps IRL (Date Time) : https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/Math/DateTime / https://dynomega.com/unreal-engine/blueprints/ue5-simple-time-of-day-system/time-of-day-bp
  - Base de donnée (DataTables) : https://dev.epicgames.com/documentation/en-us/unreal-engine/data-driven-gameplay-elements?application_version=4.27


---

## 7. Nomenclature

### 7.1 Généralités
- Utiliser **PascalCase** pour tous les noms.
- Préfixer chaque asset en fonction de son type pour faciliter l’organisation.
- Éviter les abréviations trop courtes ou non standardisées.
- Utiliser des noms explicites et descriptifs.

### 7.2 Préfixes des assets

| Type d’Asset            | Préfixe  | Exemple                        |
|-------------------------|---------|--------------------------------|
| Blueprint (objet)       | BP_     | `BP_PlayerCharacter`          |
| Blueprint (interface)   | BPI_    | `BPI_Interactable`            |
| Blueprint (fonction utilitaire) | BPF_ | `BPF_MathLibrary`       |
| Matériau                | M_      | `M_PlayerSkin`                |
| Matériau Instance       | MI_     | `MI_PlayerSkinRed`            |
| Texture                | T_      | `T_UI_HealthBar`              |
| Static Mesh            | SM_     | `SM_RockBig`                  |
| Skeletal Mesh          | SK_     | `SK_PlayerCharacter`          |
| Animation Blueprint    | ABP_    | `ABP_Player`                  |
| Séquence d’animation   | ANIM_   | `ANIM_Run`                    |
| Son                   | S_      | `S_Explosion`                 |
| Effet Sonore          | SFX_    | `SFX_PortalOpen`              |
| Musique               | MX_     | `MX_BackgroundTheme`          |
| Particule             | P_      | `P_Explosion`                 |
| Widget                | W_      | `W_MainMenu`                  |
| Niveau (Map)          | LVL_    | `LVL_MainMenu`                |

### 7.3 Blueprints spécifiques
- Les **Blueprints d’acteurs** doivent suivre la structure : `BP_[Nom]`
- Les **Blueprints composants** : `BPC_[Nom]`
- Les **Blueprints de contrôleur** : `BP_Controller_[Nom]`
- Les **Blueprints de GameMode** : `BP_GM_[Nom]`
- Les **Blueprints de HUD** : `BP_HUD_[Nom]`

### 7.4 Variables
- **Booleans** : Préfixe `b` (ex: `bIsJumping`, `bHasPowerUp`)
- **Integers** : `i` (ex: `iScore`, `iHealth`)
- **Floats** : `f` (ex: `fSpeed`, `fJumpHeight`)
- **Vectors** : `v` (ex: `vPlayerPosition`)
- **Textures** : `Tex_` (ex: `Tex_IconPlayer`)
- **Audio** : `Aud_` (ex: `Aud_PortalSound`)
- **Références d’acteurs** : `Ref_` (ex: `Ref_PlayerCharacter`)

### 7.5 Fonctions et événements
- Les fonctions commencent par un verbe pour indiquer l’action : `CalculateScore`, `SpawnEnemy`, `PlaySoundEffect`
- Les événements commencent par `On` : `OnPlayerDeath`, `OnPortalEnter`
- Les macros sont préfixées par `MACRO_` : `MACRO_CalculateDistance`
- Les interfaces sont préfixées par `I_` : `I_Interactable`

### 7.6 Dossiers du projet Unreal
La structure des dossiers doit être claire pour organiser les assets.

### 7.7 Commit

Description de l'action réalisée (Add:, Fix: ...) + description de ce qui a été ajouté ou modifié (EX: Add: class Player). Ajouter en description du commit quels fichiers on été Modifier/Supprimer/Déplacer/Ajouter.

---

## 8 UML

### 8.1 Diagramme général

![uml behaviour drawio](https://github.com/user-attachments/assets/1f15430d-22bb-4507-a641-df3f197d90d9)

### 8.1 Diagramme récupération de coin

![Diagramme coin drawio](https://github.com/user-attachments/assets/b56f4441-6f00-41af-85ba-94440b5217a0)


---

## 9. Features Optionnelles  

Cette section regroupe les améliorations et ajouts envisageables si le projet est terminé en avance ou repris ultérieurement.  

### 9.1 Boutique  
Ajout d’une boutique permettant d’acheter des **skins** et des **power-ups** à l’aide de la monnaie du jeu ou de la monnaie payante.  

### 9.2 Tutoriel  
Mise en place d’un **tutoriel interactif** pour expliquer les mécaniques du jeu aux nouveaux joueurs.  

### 9.3 Fonctionnalités Multijoueur  
- **Leaderboard** : Classement des joueurs en fonction de leurs scores.  
- **Événements communautaires** : Challenges et événements limités dans le temps.  
- **Éditeur de niveaux** : Outil permettant aux joueurs de créer et partager leurs propres niveaux.  
