# Dziennik Zmian (Changelog)

Wszystkie zmiany zostały wprowadzone w celu naprawienia niedziałającej aplikacji i doprowadzenia jej do stanu, w którym możliwe było zdiagnozowanie fundamentalnego problemu z zewnętrznym API.

## [2.0.0] - Ostateczna Diagnoza - Lipiec 2025

-   **Zdiagnozowano główną przyczynę problemu:** Ustalono, że adres API `https://info-car.pl/api/word/word-centers/exam-schedule`, z którego korzysta aplikacja, jest już nieaktualny i zwraca stronę HTML zamiast oczekiwanych danych w formacie JSON.
-   **Uodporniono logikę JavaScript:** Zmodyfikowano plik `startSearching.js`, aby poprawnie obsługiwał nieprawidłowe odpowiedzi od serwera (inne niż JSON), co pozwoliło na postawienie ostatecznej diagnozy.
-   **Poprawiono logikę pobierania kategorii:** Usunięto stałą wartość `"B"` i zastąpiono ją dynamicznym pobieraniem kategorii z pliku `.env`.

## [1.1.0] - Poprawki Logiki Skryptów - Lipiec 2025

-   **Naprawiono logikę autoryzacji:** Poprawiono skrypt `getToken.py`, aby zwracał **tylko i wyłącznie czysty token** autoryzacyjny, eliminując błąd `TypeError: is not a legal HTTP header value`.
-   **Dodano szczegółową diagnostykę:** Wprowadzono logowanie błędów w blokach `catch` w pliku `startSearching.js`, co pozwoliło na odkrycie ukrywanych wcześniej błędów `FetchError` i `TypeError`.
-   **Ustabilizowano selektory Selenium:** Zastąpiono niestabilne selektory CSS, zależne od dynamicznie generowanych klas, na rzecz bardziej niezawodnych selektorów **XPath** (np. `//button[contains(text(), 'Wyloguj')]`).
-   **Ulepszono mechanizm przechwytywania tokenu:** Zmieniono logikę z pasywnego przeszukiwania listy żądań na aktywne oczekiwanie za pomocą `driver.wait_for_request()`, co gwarantuje przechwycenie tokenu.

## [1.0.0] - Konfiguracja Środowiska i Zależności - Lipiec 2025

-   **Uruchomiono środowisko Python:** Naprawiono błędy związane z brakiem Pythona w ścieżce systemowej (PATH).
-   **Zainstalowano zależności:** Stworzono plik `requirements.txt` i zainstalowano wszystkie brakujące moduły Pythona: `selenium`, `selenium-wire`, `python-dotenv`, `packaging`, `setuptools`.
-   **Rozwiązano konflikt wersji:** Zidentyfikowano i rozwiązano problem z niekompatybilną wersją biblioteki `blinker`, przypinając ją do stabilnej wersji `1.3`.
-   **Zaktualizowano sterownik przeglądarki:** Naprawiono błąd `SessionNotCreatedException` poprzez aktualizację pliku `utils/chromedriver.exe` do wersji zgodnej z aktualną wersją przeglądarki Google Chrome.
-   **Przeprowadzono wstępną diagnostykę:** Zmodyfikowano skrypty, aby wyłączyć tryb `headless` i umożliwić wizualną obserwację procesu logowania.