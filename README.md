# Analyse exploratoire des données : Hotel Booking Demand (R)

Analyse exploratoire complète (AED) de **119 390 réservations hôtelières** de deux hôtels portugais (un hôtel urbain et un hôtel de villégiature, arrivées de juillet 2015 à août 2017). L'objectif est de comprendre les comportements de réservation, d'évaluer la qualité des données et d'identifier les caractéristiques associées aux annulations.

Projet réalisé dans le cadre du cours *Exploration de données* (Sciences des données appliquées, Collège La Cité, 2026), en R Markdown, de façon entièrement reproductible.

## Problématique

> Quelles caractéristiques des réservations (type d'hôtel, délai, tarif, segment de marché, type de dépôt, type de clientèle) sont associées aux annulations, et comment les comportements de réservation diffèrent-ils entre un hôtel urbain et un hôtel de villégiature ?

## Principaux résultats

| Question | Résultat | Méthode |
|:---|:---|:---|
| Annulations selon l'hôtel | City Hotel 41,8 % contre Resort Hotel 27,8 % (association faible, V = 0,14) | Khi-deux, V de Cramer |
| Délai et annulation | Délai médian de 113 jours pour les réservations annulées contre 45 jours pour les autres | Test de Wilcoxon-Mann-Whitney |
| Type de dépôt et annulation | Les réservations non remboursables sont annulées à 99,4 % (association forte, V = 0,48), surtout des groupes et agences hors ligne réservant très tôt | Khi-deux, V de Cramer |
| Segment de marché et annulation | *Groups* le plus annulé (61,1 %), *Complementary* le moins (12,2 %) | Khi-deux, V de Cramer |
| Délai et tarif | Corrélation quasi nulle au global (ρ = 0,013), mais de sens opposés selon l'hôtel (City −0,10, Resort +0,16) | Corrélation de Spearman |
| Tarif selon l'hôtel et la clientèle | Tarif médian plus élevé au City Hotel ; tarifs plus bas pour les groupes et contrats | Wilcoxon, Kruskal-Wallis |

## Démarche

1. **Compréhension métier** : contexte hôtelier, problématique et cinq questions analytiques.
2. **Diagnostic initial** : structure, types, doublons, valeurs manquantes, incohérences.
3. **Analyse univariée numérique** : six variables, statistiques descriptives, histogrammes et boîtes à moustaches.
4. **Analyse univariée catégorielle** : effectifs, fréquences et diagrammes en barres.
5. **Données manquantes** : diagnostic, motifs d'absence, discussion MCAR / MAR / MNAR, comparaison de stratégies avant / après.
6. **Valeurs aberrantes** : méthode de l'écart interquartile (IQR) et examen de chaque cas dans son contexte métier.
7. **Nettoyage et préparation** : journal des opérations, création de 8 nouvelles variables, export du jeu préparé.
8. **Analyse bivariée** : numérique-numérique, numérique-catégorielle et catégorielle-catégorielle, avec tests adaptés.
9. **Synthèse** : résultats, limites, recommandations et nouvelles questions.

## Décisions de nettoyage

- **185 lignes exclues** (0,15 %), toutes des erreurs manifestes : un tarif négatif, un tarif de 5 400, 180 réservations sans aucun occupant, 3 réservations avec 9 ou 10 bébés ou enfants.
- **Doublons conservés** : 31 994 lignes identiques, faute d'identifiant de réservation (elles peuvent correspondre à plusieurs chambres d'un même groupe). Un indicateur `is_duplicate` permet une analyse de sensibilité.
- **Valeurs manquantes** : `agent` et `company` recodés « Aucun » (absence structurelle, sans imputation), `country` recodé « Inconnu », `children` imputé par la médiane (0).
- **Valeurs atypiques réelles conservées** : délais très longs, grands groupes, longs séjours, tarifs nuls.

## Structure du dépôt

```
hotel-booking-eda-r/
│
├── data/
│   ├── hotel_bookings.csv                   # Jeu de données original (intact, 119 390 lignes, 32 variables)
│   └── hotel_bookings_clean.csv             # Jeu préparé (119 205 lignes, 43 variables, aucune valeur manquante)
│
├── Projet_Hotel_Booking_YacineLezoul.Rmd    # Notebook R Markdown : code commenté, analyses et interprétations
├── Projet_Hotel_Booking_YacineLezoul.html   # Rapport généré à partir du Notebook (à télécharger puis ouvrir dans un navigateur)
├── .gitignore                               # Fichiers temporaires de R et RStudio exclus du dépôt
└── README.md                                # Présentation du projet
```

## Reproduire l'analyse

1. Cloner le dépôt et ouvrir `Projet_Hotel_Booking_YacineLezoul.Rmd` dans **RStudio**.
2. Cliquer sur **Knit**. Les packages manquants (`dplyr`, `tidyr`, `ggplot2`, `scales`, `knitr`) s'installent automatiquement.
3. Le rapport HTML et `data/hotel_bookings_clean.csv` sont régénérés. Tous les chemins sont relatifs.

## Outils

R · R Markdown · dplyr · tidyr · ggplot2 · knitr · tests statistiques (Wilcoxon, Kruskal-Wallis, Khi-deux, Spearman)

## Source des données

Antonio, N., de Almeida, A. et Nunes, L. (2019). *Hotel booking demand datasets*. Data in Brief, 22, 41-49. [Article](https://www.sciencedirect.com/science/article/pii/S2352340918315191) · [Jeu de données sur Kaggle](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)

## Auteur

**Yacine Lezoul** · [github.com/lezoul](https://github.com/lezoul)
