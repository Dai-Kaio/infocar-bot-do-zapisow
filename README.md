# Bot do Rezerwacji Egzaminów na Prawo Jazdy (Info-Car)

Jest to zautomatyzowany skrypt do wyszukiwania i rezerwacji terminów egzaminów na prawo jazdy w serwisie info-car.pl. Aplikacja działa w pętli, sprawdzając co kilka sekund dostępność terminów zgodnie z preferencjami ustawionymi przez użytkownika.

## UWAGA: Status Projektu (Lipiec 2025)

**Projekt w obecnej formie jest NIEFUNKCJONALNY.**

W wyniku przeprowadzonej analizy i debugowania ustalono, że kluczowy adres API, z którego program pobierał harmonogramy egzaminów, jest już nieaktualny. Serwis info-car.pl zmienił swoją strukturę, w wyniku czego serwer zamiast danych w formacie JSON zwraca stronę HTML.

**`https://info-car.pl/api/word/word-centers/exam-schedule` -> ZWRACA HTML ZAMIAST JSON**

Repozytorium to stanowi archiwum w pełni zdebugowanej i naprawionej wersji aplikacji, która jest gotowa do działania, gdyby tylko adres API został w niej zaktualizowany.

## Jak aplikacja działa (teoretycznie)

1.  **Automatyczna autoryzacja:** Skrypt Pythona (`getToken.py`) uruchamia w tle przeglądarkę, loguje się na Twoje konto i przechwytuje token autoryzacyjny.
2.  **Pętla wyszukiwania:** Główny skrypt JavaScript w nieskończonej pętli odpytuje API info-car o dostępne terminy egzaminów.
3.  **Filtrowanie:** Wyniki są filtrowane na podstawie Twoich preferencji (kategoria, WORD, zakres dat, godziny) ustawionych w pliku `.env`.
4.  **Automatyczna rezerwacja:** Po znalezieniu pasującego terminu, program automatycznie go dla Ciebie rezerwuje.
5.  **Powiadomienie:** Po udanej rezerwacji w konsoli pojawia się stosowna informacja. Użytkownik musi ręcznie zalogować się na stronę i opłacić rezerwację w ciągu ok. 40 minut.

## Instalacja i Uruchomienie

Poniższa instrukcja zawiera wszystkie kroki, które doprowadziły do pomyślnego uruchomienia i zdiagnozowania aplikacji.

### Wymagania wstępne:
*   **Node.js:** [Pobierz i zainstaluj](https://nodejs.org/en)
*   **Python:** [Pobierz i zainstaluj](https://www.python.org/downloads/) (podczas instalacji **koniecznie zaznacz opcję "Add Python to PATH"**).
*   **Google Chrome:** Zainstalowana aktualna wersja przeglądarki.

### Kroki instalacji:

1.  **Pobierz repozytorium:** Sklonuj lub pobierz pliki projektu jako ZIP.

2.  **Zainstaluj zależności Pythona:**
    Otwórz wiersz poleceń (CMD) w głównym folderze projektu i wykonaj komendę. Zainstaluje ona wszystkie wymagane biblioteki Pythona z pliku `requirements.txt`.
    ```bash
    pip install -r requirements.txt
    ```

3.  **Zaktualizuj ChromeDriver:**
    *   Sprawdź swoją wersję Google Chrome (w przeglądarce przejdź do `chrome://settings/help`).
    *   Wejdź na stronę [ChromeDriver for Testing](https://googlechromelabs.github.io/chrome-for-testing/).
    *   Pobierz sterownik pasujący do Twojej wersji przeglądarki (plik `chromedriver-win64.zip`).
    *   Wypakuj archiwum i skopiuj plik `chromedriver.exe`.
    *   Wklej i zamień istniejący plik w folderze `utils/`.

4.  **Skonfiguruj plik `.env`:**
    *   W głównym folderze projektu stwórz plik o nazwie `.env`.
    *   Wypełnij go swoimi danymi, używając poniższego szablonu.
    *   **Aby znaleźć swoje `WORDID`**, otwórz plik `data/words.json` i odszukaj numer `id` dla swojego miasta.

    **Szablon `.env`:**
    ```
    EMAIL="twoj_email@do.infocar.pl"
    PASSWORD="twoje_haslo"
    CATEGORY="B"
    FIRST_NAME="TwojeImie"
    LAST_NAME="TwojeNazwisko"
    PESEL="TwojPesel"
    PHONE_NUMBER="TwojNumerTelefonu"
    PKK_NUMBER="TwojNumerPKK"
    WORDID="45"
    DATE_FROM="2025-07-20"
    DATE_TO="2025-08-31"
    PREFERRED_HOURS="8,9,10,11,12"
    ```

5.  **Uruchom aplikację:**
    *   Do pierwszego uruchomienia i zbudowania zależności użyj pliku `build.bat`.
    *   Do każdego kolejnego uruchomienia używaj pliku `start.bat`.