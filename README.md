# 📊 Espérance de Vie Trading - ATR

> Indicateur TradingView Pine Script pour calculer votre espérance de vie en trading basée sur l'ATR et optimiser votre gestion du risque.

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Pine Script](https://img.shields.io/badge/Pine%20Script-v5-green)
![License](https://img.shields.io/badge/license-MIT-yellow)

## 🎯 Présentation

**Espérance de Vie Trading** est un indicateur avancé qui vous aide à répondre à une question cruciale : **"Combien de temps puis-je tenir en position avant d'atteindre mon drawdown maximum ?"**

En utilisant l'**ATR (Average True Range)** comme mesure de volatilité, cet outil calcule en temps réel votre espérance de vie en minutes, votre target optimale, et le ratio entre votre TP et votre espérance de vie.

## ✨ Fonctionnalités

- 📈 **Calcul dynamique de l'ATR** sur n'importe quel timeframe (1min, 5min, 15min, etc.)
- ⏱️ **Espérance de vie en minutes** basée sur votre capital et la volatilité du marché
- 🎯 **Target TP automatique** calculée depuis l'ATR (par défaut ATR/2)
- 💰 **Gain potentiel** estimé en dollars
- 📊 **Ratio TP/Vie** avec code couleur pour évaluer la qualité du setup
- 🌍 **Compatible avec tous les actifs** (Futures, Forex, Crypto, Actions)

## 🖼️ Aperçu

L'indicateur affiche un tableau en temps réel avec :

| Métrique | Description |
|----------|-------------|
| **ATR** | Volatilité moyenne actuelle |
| **Target TP** | Objectif de take profit dynamique |
| **Gain potentiel** | Profit estimé si TP atteint |
| **Espérance de vie** | Durée avant d'atteindre le DD Max |
| **Temps pour TP** | Temps estimé pour atteindre le TP |
| **Ratio TP/Vie** | Proportion de l'espérance utilisée |
| **DD Max** | Drawdown maximum tolérable |

### Code couleur du Ratio TP/Vie

- 🟢 **< 50%** : Excellent setup, beaucoup de marge
- 🟠 **50-80%** : Acceptable mais risqué
- 🔴 **> 80%** : Défavorable, peu de marge d'erreur

## 🚀 Installation

1. Ouvrez TradingView
2. Créez un nouvel indicateur Pine Script
3. Copiez-collez le code depuis `Esperance_Vie_ATR_Modified.pine`
4. Enregistrez et ajoutez l'indicateur à votre graphique

## ⚙️ Configuration

### Paramètres principaux

```
Capital ($) : 2000          // Votre capital disponible
Valeur par point ($) : 20   // Valeur d'un point pour l'actif tradé
Nombre de contrats : 1      // Taille de position
Période ATR : 14            // Période pour le calcul de l'ATR
Timeframe ATR : 5           // Timeframe des bougies (1, 5, 15, 30, 60)
Diviseur de risque : 10     // Ajustement conservateur (1 = pas d'ajustement)
Diviseur ATR pour TP : 2    // Target = ATR/2 (ajustable)
```

### Adaptation par actif

| Actif | Valeur par point | Remarques |
|-------|------------------|-----------|
| **NQ (Nasdaq)** | $20 | 1 point = $20 |
| **ES (S&P 500)** | $50 | 1 point = $50 |
| **Forex EUR/USD** | Variable | Dépend du lot size |
| **Crypto BTC** | 1 | Utiliser % du capital |

## 📖 Comment l'utiliser

### 1. Calculer votre espérance de vie

L'indicateur divise votre DD Max par l'ATR actuel pour déterminer combien de périodes (bougies) vous pouvez survivre :

```
Espérance (périodes) = DD Max / ATR
Espérance ajustée = Espérance / Diviseur de risque
Espérance (minutes) = Espérance ajustée × Timeframe
```

### 2. Évaluer la qualité du setup

Regardez le **Ratio TP/Vie** :

- ✅ **Ratio < 30%** : Setup optimal, prenez le trade !
- ⚠️ **Ratio 50-80%** : Acceptable mais surveillez
- 🚫 **Ratio > 80%** : Évitez, trop risqué

## 💡 Exemples pratiques

### Exemple 1 : Setup optimal

```
ATR : 11 pts
DD Max : 100 pts
Espérance de vie : 45 min
Temps pour TP : 10 min
Ratio TP/Vie : 22% 🟢
```

**Interprétation** : Excellent ! Vous avez 45 minutes de marge et votre TP ne demande que 22% de ce temps.

### Exemple 2 : Setup défavorable

```
ATR : 39 pts
DD Max : 100 pts
Espérance de vie : 2.5 min
Temps pour TP : 0.5 min
Ratio TP/Vie : 20% 🟢
```

**Interprétation** : Bien que le ratio soit bon, l'espérance de vie est trop courte (2.5 min). Marché trop volatil pour votre capital.

## 🔧 Personnalisation

### Modifier le diviseur de risque

- **Diviseur = 1** : Mode agressif, espérance de vie réelle
- **Diviseur = 10** : Mode conservateur (recommandé)
- **Diviseur = 20** : Mode ultra-conservateur

### Ajuster la target

- **TP = ATR/2** : Équilibré (par défaut)
- **TP = ATR/3** : Conservateur, TP plus proche
- **TP = ATR** : Agressif, TP plus lointain

## 📝 Formules mathématiques

```
DD Max (points) = Capital / (Valeur_par_point × Contrats)

Espérance_brute = DD_Max / ATR

Espérance_ajustée = Espérance_brute / Diviseur_risque

Target_TP = ATR / Diviseur_TP

Temps_TP = Target_TP / ATR

Ratio = Temps_TP / Espérance_ajustée × 100
```

## 🎓 Concepts clés

### ATR (Average True Range)

L'ATR mesure la volatilité moyenne d'un actif sur une période donnée. Un ATR élevé = marché volatil, un ATR faible = marché calme.

### Espérance de vie

Concept unique qui répond à : "Si je prends une position et que le marché va constamment contre moi avec la volatilité actuelle, combien de temps avant d'atteindre mon stop loss maximum ?"

### Ratio TP/Vie

Indicateur de qualité du setup : plus le ratio est faible, plus vous avez de marge d'erreur pour atteindre votre TP avant d'atteindre votre DD Max.

## ⚠️ Avertissements

- Cet indicateur est un **outil d'aide à la décision**, pas un système de trading complet
- Les performances passées ne garantissent pas les résultats futurs
- Ajustez toujours les paramètres selon votre profil de risque
- Ne tradez jamais avec de l'argent que vous ne pouvez pas vous permettre de perdre

## 🙏 Remerciements

Merci à la communauté TradingView pour l'inspiration et le partage de connaissances.

---

**⚡ Bon trading et gérez votre risque intelligemment ! ⚡**
