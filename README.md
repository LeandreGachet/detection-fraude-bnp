# Détection de fraude sur données transactionnelles

Prédire si un panier de commerce en ligne est frauduleux, à partir de son seul contenu — articles, prix, quantités — sans aucun historique client.

Challenge de données **BNP Paribas Personal Finance**. Projet individuel de Master 2, soutenu à l'oral.

## La difficulté

92 790 transactions, dont **1,42 % de fraudes**.

Un modèle qui prédirait « personne ne fraude jamais » afficherait 98,58 % de justesse et serait totalement inutile. C'est pourquoi l'évaluation repose sur la **précision moyenne** (aire sous la courbe précision-rappel) et non sur la justesse ni sur l'aire sous la courbe ROC, toutes deux trompeuses sur événement rare.

## Démarche

**Restructuration des données** du format large au format long — une ligne par article au lieu d'une par panier — pour rendre possible l'agrégation par client. Sans cette étape, aucune des variables suivantes n'existe.

**Ingénierie de variables** : nettoyage des descriptions produits, vectorisation des marques et modèles, agrégations financières par panier, et surtout des **indicateurs métiers** construits à partir de l'observation des fraudeurs — cohérence entre un produit et son accessoire, absence de garantie, marques à risque.

**Combinaison de quatre familles de modèles** par moyenne pondérée, les poids reflétant l'apport de chacune : XGBoost en modèle principal, LightGBM pour les motifs asymétriques, CatBoost pour la gestion native des catégories, forêt aléatoire pour réduire la variance.

**Réglage des hyperparamètres** par recherche aléatoire, validation croisée stratifiée, pondération des classes.

## Résultats

| Étape | Précision moyenne |
|---|---|
| Modèle de référence | 0,115 |
| Objectif du challenge | 0,140 |
| Après ingénierie de variables | 0,171 |
| Après combinaison de modèles | 0,191 |
| Après optimisation | **0,201** |

Ce score plaçait le projet **77ᵉ au classement public** du challenge en janvier 2026.

## Contenu

| | |
|---|---|
| `notebooks/notebook.ipynb` | l'ensemble du travail |
| `presentation.pptx` | le support de soutenance |
| `requirements.txt` | les dépendances |

Les données du challenge ne sont pas redistribuées.

---

**Léandre Gachet** — Master Science des données, statistique et économétrie, Université de Rennes
