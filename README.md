# Choosing a Region for New Oil Wells: Profit and Risk with Bootstrap

A Yandex Practicum project where a machine learning model feeds a business decision. The notebook is written in Russian; this README summarizes it in English.

## Business task

A mining company must choose one of three regions for new wells.
Conditions: 500 points are explored in a region and the 200 best by model prediction are developed; the budget is 10 bn RUB; one unit of product (1,000 barrels) brings 450,000 RUB.
Only regions with a **loss probability below 2.5%** qualify; among them, the one with the highest mean profit wins.

## Data

Geological exploration samples for three regions, 100,000 deposits each: three features and the product volume.

## What I did

1. **Data preparation and EDA**, including a check of linear relationships between features and the target in each region.
2. **Linear regression per region** (75/25 split), compared with a mean baseline and checked with 4-fold cross-validation.
3. **Break-even volume:** 111.1 thousand barrels per well, which is above the average reserves in every region, so good point selection is essential.
4. **Profit function and bootstrap:** 1,000 samples of 500 points, top-200 by prediction; mean profit, 95% confidence interval and loss risk.

## Results

| Region | Model RMSE | Mean profit, bn RUB | 95% CI, bn RUB | Loss risk |
|---|---|---|---|---|
| 1 | 37.76 | 0.40 | [-0.11; 0.90] | 6.0% |
| **2** | **0.89** | **0.45** | **[0.05; 0.83]** | **0.9%** |
| 3 | 40.15 | 0.43 | [-0.07; 0.96] | 5.5% |

**Recommendation: region 2.** It is the only region with a loss risk below 2.5% and it has the highest mean profit. The model is almost exact there (R² ≈ 0.9996), which makes the selection of the best wells reliable.

## Tech stack

Python · pandas · NumPy · scikit-learn · Matplotlib · Seaborn · phik

## How to run

```bash
pip install -r requirements.txt
jupyter notebook oil_well_location.ipynb
```

---

**Кратко по-русски.** Выбор региона для бурения нефтяных скважин (учебный проект Яндекс Практикума): линейная регрессия для каждого региона и бутстреп для оценки прибыли и рисков. Рекомендован регион 2: средняя прибыль 0,45 млрд ₽, риск убытков 0,9% при допустимых 2,5%.
