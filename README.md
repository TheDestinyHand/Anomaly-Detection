# ✈️ Turbofan Engine Remaining Useful Life (RUL) Prediction

Analisi esplorativa, feature engineering e modellazione predittiva per la stima della vita residua utile (RUL) di motori aeronautici basata sul dataset **NASA C-MAPSS (FD001)**.

---

## 📋 Panoramica del Progetto
La manutenzione predittiva nel settore aerospaziale richiede modelli capaci di stimare con precisione il momento in cui un componente critico subirà un guasto strutturale. Questo repository contiene una pipeline end-to-end sviluppata in **R e R Markdown**, che parte dall'analisi della telemetria dei sensori fino all'addestramento di un modello di **Random Forest** e alla valutazione tramite metriche di costo industriali (NASA Score).

---

## 📊 Principali Fasi della Pipeline
1. **Caricamento e Pulizia dei Dati:** Gestione del dataset multivariato `train_FD001.txt` (26 colonne: ID motore, cicli temporali, 3 parametri operativi e 21 sensori fisici).
2. **Feature Engineering (RUL Target):** Calcolo del Remaining Useful Life come differenza tra il ciclo massimo di vita di ciascun motore e il ciclo corrente, applicando un limite superiore (*cap*) a 125 cicli in accordo con la letteratura scientifica.
3. **Analisi Esplorativa (EDA):** Visualizzazione dei trend di degrado sui singoli sensori (es. *Sensor 14* e *Sensor 2*).
4. **Rimozione Varianza Quasi-Zero:** Esclusione delle feature non informative per ottimizzare la stabilità computazionale.
5. **Modellazione Predittiva:** Addestramento di un modello di **Random Forest** con suddivisione train/validation a livello di singolo motore (*EngineID*) per prevenire data leakage.
6. **Valutazione e Diagnostica:** 
   * Calcolo dell'**RMSE** sul set di validazione.
   * Implementazione della **funzione di score asimmetrico ufficiale NASA (PHM08)** per penalizzare i ritardi diagnostici.
   * **Analisi dei Residui** per identificare il bias e l'accuratezza in prossimità del guasto imminente.

---

## 📈 Risultati Chiave
* **Feature Importance:** I sensori *Sensor21*, *Sensor8*, *Sensor9* e *Sensor4* risultano i predittori principali, contribuendo per oltre il 15% all'incremento dell'errore in caso di permutazione (%IncMSE).
* **Performance:** Il modello raggiunge un **RMSE di 19.09 cicli** sul set di validazione, dimostrando un'elevata precisione soprattutto nelle fasi terminali, dove il RUL si avvicina a zero (guasto imminente).

---

## 🛠️ Tecnologie Utilizzate
* **Linguaggio:** R
* **Librerie Principali:** `tidyverse` (dplyr, ggplot2, tidyr, readr), `caret`, `randomForest`, `knitr`
* **Output Formats:** HTML / PDF (tramite R Markdown)

---

