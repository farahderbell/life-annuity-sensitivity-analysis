# 📊 Actuarial Life Annuity — VAP & Sensitivity Analysis

## 📌 Présentation du projet

Ce projet d'**Actuariat Vie** porte sur l'étude de l'influence du **taux d'intérêt** sur la **Valeur Actuelle Probable (VAP)** d'une rente viagère.

L'objectif est de construire une démarche actuarielle complète permettant de passer des **données de mortalité** à l'**évaluation financière d'une rente**, puis d'étudier la sensibilité de cette valorisation aux hypothèses financières et démographiques.

L'étude porte sur un portefeuille d'assurés suédois ayant souscrit un contrat en **2018 à l'âge de 75 ans**. La cohorte étudiée correspond donc aux individus nés en :

$$2018 - 75 = 1943$$

L'analyse consiste ainsi à suivre la **cohorte 1943** à partir de l'âge de 75 ans afin d'estimer la mortalité, construire les probabilités de survie et calculer la VAP d'une rente.

---

## 🎯 Problématique

> **Comment les variations du taux d'intérêt et de la mortalité influencent-elles la valeur actuelle probable d'une rente viagère ?**

L'évaluation d'une rente viagère repose principalement sur deux dimensions :

* 🧬 **Dimension démographique** : la mortalité et la probabilité de survie des assurés ;
* 💰 **Dimension financière** : le taux d'intérêt utilisé pour actualiser les paiements futurs.

Plus un assuré vit longtemps, plus la durée probable de versement de la rente augmente.

À l'inverse, un taux d'intérêt plus élevé réduit la valeur actuelle des paiements futurs, tandis qu'un taux plus faible augmente cette valeur.

---

# 📚 1. Fondements théoriques

## 1.1 Cohorte

Une **cohorte** désigne un groupe d'individus partageant une même caractéristique temporelle, généralement une année de naissance.

Dans cette étude :

```text
Année de souscription = 2018
Âge à la souscription = 75 ans

Cohorte = 2018 - 75
        = 1943
```

La cohorte est ensuite suivie au cours du temps :

| Année | Âge | Cohorte |
| ----: | --: | ------: |
|  2018 |  75 |    1943 |
|  2019 |  76 |    1943 |
|  2020 |  77 |    1943 |
|   ... | ... |    1943 |

Cette approche permet de suivre **la même génération** au fur et à mesure qu'elle vieillit, ce qui est particulièrement pertinent pour l'étude d'une rente viagère.

---

## 1.2 Taux central de mortalité

Le taux central de mortalité mesure l'intensité des décès au sein d'une population exposée au risque.

Pour un âge $x$, on considère :

* $D_x$ : nombre de décès observés ;
* $E_x$ : exposition au risque ;
* $m_x$ : taux central de mortalité.

L'estimateur est :

$$\hat{m}_x = \frac{D_x}{E_x}$$

Par exemple, pour 200 décès et une exposition de 10 000 personnes :

$$\hat{m}_x = \frac{200}{10\,000} = 0{,}02$$

soit un taux de mortalité estimé de **2 %**.

---

## 1.3 Estimation par maximum de vraisemblance

L'estimation des taux de mortalité repose sur l'hypothèse :

$$D_x \sim \mathcal{P}\left(E_x \, m_x\right)$$

où le nombre de décès suit une **loi de Poisson** de paramètre $E_x \, m_x$.

La maximisation de la vraisemblance conduit à :

$$\boxed{\hat{m}_x = \frac{D_x}{E_x}}$$

Ainsi, le taux central utilisé dans l'étude correspond bien à l'**estimateur du maximum de vraisemblance** sous l'hypothèse de Poisson.

---

## 1.4 Intervalle de confiance à 90 %

L'estimation d'un taux de mortalité comporte une incertitude statistique.

Sous l'hypothèse de Poisson, l'erreur standard est approximée par :

$$\mathrm{SE}\left(\hat{m}_x\right) = \sqrt{\frac{\hat{m}_x}{E_x}}$$

Pour un niveau de confiance de 90 %, le quantile utilisé est :

$$z_{0{,}95} = 1{,}645$$

L'intervalle de confiance est alors :

$$\mathrm{IC}_{90\%} = \left[\, \hat{m}_x - z_{0{,}95} \cdot \mathrm{SE}\left(\hat{m}_x\right) \; ; \; \hat{m}_x + z_{0{,}95} \cdot \mathrm{SE}\left(\hat{m}_x\right) \,\right]$$

Un intervalle étroit indique une estimation relativement précise, tandis qu'un intervalle plus large traduit une incertitude statistique plus importante.

---

# 💰 2. Valeur actuelle et rente viagère

## 2.1 Actualisation

Un paiement futur n'a pas la même valeur qu'un paiement immédiat.

Avec un taux d'intérêt annuel $i$, le facteur d'actualisation est :

$$v = \frac{1}{1+i}$$

La valeur actuelle d'un paiement de montant 1 effectué dans $k$ années est :

$$v^{k} = (1+i)^{-k}$$

Ainsi :

$$i \uparrow \quad \Longrightarrow \quad v \downarrow \quad \Longrightarrow \quad \text{valeur actuelle} \downarrow$$

---

## 2.2 Valeur Actuelle Probable (VAP)

La VAP combine :

1. la valeur actuelle des paiements futurs ;
2. la probabilité que ces paiements soient effectivement versés.

Pour une rente viagère à termes anticipés :

$$\boxed{\ \ddot{a}_x = \sum_{k=0}^{+\infty} v^{k} \, {}_{k}p_{x} \ }$$

où :

* $v^{k}$ est le facteur d'actualisation ;
* ${}_{k}p_{x}$ est la probabilité qu'un assuré âgé de $x$ ans survive encore $k$ années.

La VAP dépend donc simultanément :

* du **taux d'intérêt** ;
* de la **mortalité**.

Une hausse du taux d'intérêt réduit la VAP, tandis qu'une diminution de la mortalité augmente les probabilités de survie et donc la VAP.

---

## 2.3 Rente viagère

Une rente viagère est versée tant que l'assuré est vivant.

Pour une rente à termes anticipés, le premier paiement est effectué immédiatement :

$$\ddot{a}_x = \sum_{k=0}^{+\infty} v^{k} \, {}_{k}p_{x}$$

La durée des paiements n'est donc pas connue à l'avance : elle dépend de la durée de vie de l'assuré.

---

## 2.4 Rente temporaire de 15 ans

Une rente temporaire fonctionne selon le même principe, mais les paiements sont limités à une durée maximale de 15 ans :

$$\ddot{a}_{x:\overline{15|}} = \sum_{k=0}^{14} v^{k} \, {}_{k}p_{x}$$

On a généralement :

$$\ddot{a}_{x} > \ddot{a}_{x:\overline{15|}}$$

car la rente viagère peut continuer à être versée au-delà de 15 ans si l'assuré est toujours vivant.

---

# 🗃️ 3. Données

## Human Mortality Database

Les données utilisées proviennent de la **Human Mortality Database (HMD)**.

La base fournit notamment :

* les années d'observation ;
* les âges ;
* les décès observés ;
* les expositions au risque ;
* les taux de mortalité.

L'étude utilise les données de **Suède**.

---

# 🔬 4. Méthodologie

L'analyse suit le processus actuariel suivant :

```text
                 Données HMD
                      │
                      ▼
              Données de mortalité
                      │
                      ▼
              Extraction cohorte 1943
                      │
                      ▼
          Estimation des taux m̂x
                      │
                      ▼
        Intervalles de confiance 90 %
                      │
                      ▼
       Probabilités de décès qx
                      │
                      ▼
       Probabilités de survie px
                      │
                      ▼
             Probabilités kpx
                      │
                      ▼
                  VAP
                      │
             ┌────────┴────────┐
             ▼                 ▼
      Sensibilité au       Sensibilité à
      taux d'intérêt       la mortalité
             │                 │
             └────────┬────────┘
                      ▼
             Analyse comparative
```

---

## 4.1 Téléchargement des données

Les données de mortalité suédoises sont récupérées depuis la HMD.

Les informations nécessaires à l'étude sont ensuite sélectionnées afin de construire la trajectoire de mortalité de la cohorte 1943.

---

## 4.2 Extraction de la cohorte 1943

La cohorte est extraite selon la condition :

$$\text{année} - \text{âge} = 1943$$

Ainsi :

$$2018 - 75 = 1943 \qquad 2019 - 76 = 1943 \qquad 2020 - 77 = 1943$$

Cette méthode permet de suivre la même génération au cours du temps.

---

## 4.3 Estimation des taux de mortalité

Pour chaque âge de la cohorte :

$$\hat{m}_x = \frac{D_x}{E_x}$$

Le tableau construit contient notamment :

* l'âge ;
* l'année ;
* le nombre de décès ;
* l'exposition au risque ;
* le taux de mortalité estimé ;
* l'erreur standard ;
* les bornes de l'intervalle de confiance à 90 %.

---

## 4.4 Transformation en probabilités de décès et de survie

Les taux centraux sont transformés en probabilités annuelles de décès sous l'hypothèse d'une **force de mortalité constante sur l'année** :

$$\boxed{\ q_x = 1 - e^{-m_x} \ }$$

La probabilité de survie est :

$$\boxed{\ p_x = 1 - q_x = e^{-m_x} \ }$$

Les probabilités de survie cumulées sont ensuite obtenues par :

$${}_{k}p_{x} = \prod_{j=0}^{k-1} p_{x+j}$$

Ces probabilités constituent l'un des éléments essentiels au calcul de la VAP.

---

# 📈 5. Résultats

## 5.1 Taux de mortalité estimés

L'analyse des taux de mortalité de la cohorte 1943 à partir de 75 ans montre une **augmentation progressive du taux de mortalité avec l'âge**.

Cette évolution est cohérente avec le vieillissement : le risque de décès augmente lorsque l'âge avance.

Aux âges élevés, l'augmentation devient progressivement plus importante.

### Intervalles de confiance

Les intervalles de confiance à 90 % permettent d'évaluer l'incertitude statistique associée aux estimations.

Dans l'analyse, les bandes restent relativement proches de la courbe centrale, ce qui indique des estimations relativement stables sur la période étudiée.

D'un point de vue actuariel, cette estimation est importante car une erreur dans la mortalité peut directement modifier l'estimation des engagements futurs d'une rente.

---

## 5.2 Log-taux historiques de mortalité

L'étude utilise également le logarithme des taux de mortalité :

$$\ln\left(\mu_x\right)$$

Cette transformation permet de mieux visualiser la structure de la mortalité.

Le graphique obtenu montre une croissance relativement régulière du log-taux avec l'âge, ce qui est cohérent avec les modèles classiques de mortalité.

La forme observée est notamment proche de la loi de **Gompertz** :

$$\mu(x) = B \, e^{c x}$$

et donc :

$$\ln\left(\mu(x)\right) = \ln(B) + c x$$

Cette relation explique pourquoi le log-taux présente approximativement un comportement linéaire avec l'âge.

---

# 💶 6. Influence du taux d'intérêt sur la VAP

L'analyse de sensibilité consiste à faire varier le taux d'intérêt et à observer l'évolution de la VAP.

La relation observée est **décroissante** :

$$\boxed{\ i \uparrow \ \Longrightarrow \ \mathrm{VAP} \downarrow \ }$$

Cette relation découle directement du facteur d'actualisation :

$$v = (1+i)^{-1}$$

Lorsque $i$ augmente, $v$ diminue et les paiements futurs ont une valeur actuelle plus faible.

L'analyse montre également que la relation n'est pas parfaitement linéaire. La VAP est particulièrement sensible aux faibles niveaux de taux, ce qui est important dans l'évaluation des engagements d'assurance à long terme.

---

# 🧬 7. Influence des variations de mortalité

Plusieurs scénarios de mortalité sont étudiés afin d'analyser le **risque de longévité**.

Lorsque la mortalité diminue :

$$\text{mortalité} \downarrow \ \Longrightarrow \ \text{survie} \uparrow \ \Longrightarrow \ \text{durée des paiements} \uparrow \ \Longrightarrow \ \mathrm{VAP} \uparrow$$

Inversement :

$$\text{mortalité} \uparrow \ \Longrightarrow \ \mathrm{VAP} \downarrow$$

Cette relation correspond directement au fonctionnement d'une rente viagère.

Le **risque de longévité** correspond ainsi au risque que les assurés vivent plus longtemps que prévu, entraînant une durée de paiement plus importante.

---

# ⚖️ 8. Analyse comparative

La VAP dépend de deux grandes familles d'hypothèses :

| Dimension        | Variable         | Effet sur la VAP |
| ---------------- | ---------------- | ---------------- |
| 💰 Financière    | Taux d'intérêt ↑ | VAP ↓            |
| 💰 Financière    | Taux d'intérêt ↓ | VAP ↑            |
| 🧬 Démographique | Mortalité ↑      | VAP ↓            |
| 🧬 Démographique | Mortalité ↓      | VAP ↑            |

Les hypothèses financières agissent principalement sur la **valeur des flux**, tandis que les hypothèses démographiques influencent leur **durée probable**.

Dans le cadre de cette étude, l'effet du taux d'intérêt apparaît plus marqué que celui des chocs de mortalité considérés. Cependant, cela ne signifie pas que le risque de mortalité est négligeable : sur des produits de très longue durée, son influence peut devenir beaucoup plus importante.

---

# 📌 9. Principaux enseignements

Le projet met en évidence plusieurs résultats actuariels :

### 1. La mortalité augmente avec l'âge

Les taux de mortalité estimés pour la cohorte 1943 augmentent progressivement à partir de 75 ans.

### 2. La mortalité présente un comportement proche de Gompertz

Le log-taux de mortalité présente une évolution approximativement linéaire avec l'âge.

### 3. La VAP diminue lorsque le taux d'intérêt augmente

Un taux d'intérêt plus élevé réduit la valeur actuelle des paiements futurs.

### 4. Une amélioration de la mortalité augmente la VAP

Une mortalité plus faible signifie une durée de vie plus importante et donc des paiements de rente potentiellement plus longs.

### 5. Les hypothèses financières et démographiques sont complémentaires

L'évaluation actuarielle d'une rente nécessite de considérer simultanément :

* les probabilités de survie ;
* le taux d'intérêt ;
* la durée probable des paiements.

---

# 🏁 10. Conclusion

Ce projet a permis de construire une démarche complète d'évaluation actuarielle d'une rente viagère, depuis les données de mortalité jusqu'à l'analyse de sensibilité de la valeur actuelle probable.

La démarche repose sur :

```text
Données de mortalité
        ↓
Cohorte 1943
        ↓
Maximum de vraisemblance
        ↓
Taux de mortalité
        ↓
IC à 90 %
        ↓
Probabilités de décès
        ↓
Probabilités de survie
        ↓
Valeur Actuelle Probable
        ↓
Analyse de sensibilité
```

Les résultats montrent notamment qu'une **augmentation du taux d'intérêt réduit la VAP**, tandis qu'une **amélioration de la mortalité augmente la VAP**.

L'étude souligne ainsi l'importance, en actuariat vie, de combiner correctement les **hypothèses démographiques** et les **hypothèses financières** pour évaluer les engagements futurs d'un assureur.

---

# 🛠️ Technologies et outils

* **R**
* **Human Mortality Database (HMD)**
* `demography`
* `StMoMo`
* `lifecontingencies`
* Analyse statistique
* Mathématiques actuarielles
* Analyse de sensibilité

---

# 📚 Références

1. **Human Mortality Database (HMD)**
2. **Cours d'Actuariat Vie — ESPRIT / Université du Mans**
3. **R Core Team**

---

