# Plan pozyskiwania danych

Zespół nie wskazał jeszcze ostatecznego tematu. Poniższe źródła obejmują oba rozważane warianty; po wyborze tematu zostawimy w planie tylko właściwe wiersze.

| Źródło / URL / API | Format | Metoda pobrania | Kto odpowiada | Termin próbki |
|---|---|---|---|---|
| Piłka: football-data.co.uk, Premier League 2024/25: https://www.football-data.co.uk/mmz4281/2425/E0.csv | CSV, jeden mecz w wierszu; m.in. data, gospodarz, gość, gole i wynik | Skrypt `scripts/pobierz_pilka.py` pobiera plik przez HTTPS i zapisuje lokalnie w `data/raw/`; bez scrapingu HTML | Dawid Zemanek | 10.11.2026 – wykonano |
| Rower: Otwarte Dane – wartości liczników rowerowych: https://dane.gov.pl/pl/dataset/2274,wartosci-licznikow-rowerowych/resource/32554 | Zasób do pobrania przez stronę/API; format i zakres trzeba potwierdzić dla wybranego miasta | Pobranie zasobu / API po sprawdzeniu metadanych; bez scrapingu | Mateusz Ozga | 13.11.2026 – do wykonania, jeśli wybierzemy temat rowerowy |
| Rower: dane o długości infrastruktury rowerowej dla tego samego miasta i okresu; portal otwartych danych/geoportal wybranego miasta (adres do ustalenia po wyborze miasta) | Do potwierdzenia: CSV lub dane przestrzenne (np. GeoJSON) | Pobranie oficjalnego eksportu/API; nie scrapować, dopóki warunki serwisu nie zostaną sprawdzone | Maksymilian Wrześniewski | 13.11.2026 – do wykonania, jeśli wybierzemy temat rowerowy |

## Wykonane próbne pobranie: piłka nożna

- Źródło: football-data.co.uk, kod ligi `E0` (Premier League), sezon `2425`.
- Adres pliku: https://www.football-data.co.uk/mmz4281/2425/E0.csv
- Pobrano: 10.11.2026, przez skrypt `scripts/pobierz_pilka.py`.
- Wynik próbki: pierwsze 300 rekordów danych zapisane lokalnie jako `data/raw/pilka_2425_E0_sample.csv`.
- Kolumny potrzebne do pytania o przewagę własnego boiska: `Date`, `HomeTeam`, `AwayTeam`, `FTHG`, `FTAG`, `FTR` (nazwy mogą się różnić wielkością liter w zależności od wersji pliku).
- Dane lokalne są ignorowane przez Git. W repozytorium znajduje się skrypt, nie pobrany plik.
- Jest to bezpośrednie pobranie gotowego CSV, a nie scraping strony. Właściciel źródła udostępnia sezonowe pliki CSV na stronie pobierania; przed publikacją wyników należy podać źródło i sprawdzić aktualne warunki ponownego wykorzystania.

## Uwagi do wariantu rowerowego

Źródło liczników jest zidentyfikowane, ale jeszcze nie zweryfikowano, czy dostępny zasób zawiera dane porównywalne dla okresu i miasta, które wybierze zespół. Trzeba też znaleźć długość tras rowerowych dla tych samych jednostek przestrzennych i okresu. Jeśli nie uda się dopasować obu źródeł, ograniczymy analizę do jednego miasta lub wybierzemy temat piłkarski. Nie planujemy scrapingu; jeśli okaże się niezbędny, najpierw sprawdzimy `robots.txt` i warunki użytkowania.
