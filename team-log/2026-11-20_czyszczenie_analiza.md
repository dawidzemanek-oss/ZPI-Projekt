## 2026-11-20 – czyszczenie danych i EDA (`warszawa_mieszkania_full.csv`) - Analityk

### Zakres wykonanych prac

- [x] **Powstanie i cel notebooka**
  - Utworzono notebook `oczyszczenie_analiza_zbioru.ipynb`, który automatyzuje przygotowanie surowego zbioru RCN (`warszawa_mieszkania_full.csv`) do dalszego modelowania oraz przeprowadza analizę eksploracyjną (EDA) warszawskiego rynku mieszkań (2023–2026).

- [x] **Obróbka, standaryzacja i czyszczenie danych**
  - Ujednolicono kodowanie pliku (`utf-8-sig`), przekonwertowano daty (`DOK_DATA`) do formatu `datetime`, a kolumny cenowe, metrażowe, liczbę izb oraz współrzędne na typ liczbowy (`float`).
  - Wyznaczono identyfikator aktu notarialnego (`akt_id`), liczbę lokali w akcie oraz jednostkową cenę lokalu (`cena_lokalu`) i stawkę za metr (`cena_m2`).
  - Oczyszczono zbiór z błędnych rekordów na podstawie 11 reguł kontroli jakości (odfiltrowano m.in. transakcje spoza wolnego rynku, niepełne udziały `!= 1/1`, pakiety wielolokalowe bez rozbitych cen jednostkowych, duplikaty, skrajne metraże/ceny za m² oraz współrzędne poza granicami Warszawy).

- [x] **Wykonane analizy i wizualizacje (EDA)**
  - Porównano rynek pierwotny i wtórny pod kątem liczby i udziału transakcji, rozkładu cen za m² (mediana, średnia, kwartyle Q25/Q75), metrażu, liczby izb oraz odległości od centrum.
  - Wygenerowano wykresy gęstości (KDE) ceny za m², mediany cen w podziale na kategorie metrażu, różnice median (`Pierwotny - Wtórny`) w dzielnicach (min. 50 transakcji) oraz mapę przestrzenną cen za m² w Warszawie z centroidami dzielnic.

- [x] **Napotkane i rozwiązane błędy w danych**
  - `ParserError` – dwie sklejone transakcje w linii 2042 (55 pól zamiast 45) oraz niewidoczny znak BOM w nagłówku `gid` (rozwiązano przez `encoding='utf-8-sig'` i `on_bad_lines='warn'`).
  - `TypeError` / `ValueError` – zapis części wartości liczbowych jako tekst (przecinki dziesiętne) oraz przesunięte kolumny (np. wartość `'True'` w miejscu współrzędnych `longitude`/`latitude`), co wyeliminowano rzutowaniem `pd.to_numeric(..., errors='coerce')` i filtrowaniem zakresu współrzędnych.

### Nowe pliki w repozytorium

- **`dane/warszawa_mieszkania_clean.csv`** – dodano oczyszczony zbiór danych (`df_clean`) wyeksportowany do pliku `.csv`, gotowy do dalszego modelowania i analiz.
- **`notebooks/oczyszczenie_analiza_zbioru.ipynb`** – dodano plik z oczyszczeniem zbioru i analizą danych.
