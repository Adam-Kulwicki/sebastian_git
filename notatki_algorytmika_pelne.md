# Kompleksowe Notatki z Algorytmiki, Struktur Danych i Podstaw Kryptografii

## I. Podstawy Algorytmiki

**1. Czym jest algorytm?**
Algorytm to ściśle określony ciąg instrukcji i operacji, prowadzący do rozwiązania zadanego problemu w skończonym czasie. Jest to przepis na przetworzenie danych wejściowych w pożądane dane wyjściowe.
*Przykład:* Przepis kulinarny lub algorytm Euklidesa do wyznaczania NWD.

**2. Czym jest struktura danych?**
Struktura danych to sposób organizacji, przechowywania i zarządzania danymi w pamięci komputera, który umożliwia ich efektywne modyfikowanie i dostęp do nich. Algorytmy i struktury danych są nierozerwalne – odpowiednia struktura warunkuje wydajność algorytmu.
*Przykład:* Tablica, lista wiązana, drzewo binarne.

**3. Jakie są (4) cechy algorytmu?**
1. **Skończoność:** Algorytm musi zawsze zakończyć się po wykonaniu skończonej liczby kroków.
2. **Określoność (Jednoznaczność):** Każda instrukcja musi być precyzyjna i nie budzić wątpliwości (determinizm).
3. **Efektywność:** Operacje w algorytmie muszą być na tyle podstawowe, by można je było wykonać w skończonym czasie przy użyciu dostępnych zasobów.
4. **Uniwersalność (Ogólność):** Algorytm powinien rozwiązywać całą klasę problemów, a nie tylko jeden konkretny przypadek z góry ustalonymi danymi (np. sortowanie dowolnej tablicy, a nie tylko `[3, 1, 2]`).

**4. W jaki sposób (4) można zapisać algorytm?**
1. **Opis słowny:** Naturalny język, krok po kroku (np. "Weź pierwszą liczbę, porównaj z drugą...").
2. **Pseudokod:** Strukturalny zapis przypominający język programowania, ale niezależny od jego składni.
3. **Schemat blokowy:** Reprezentacja graficzna za pomocą znormalizowanych figur geometrycznych.
4. **Kod źródłowy:** Zapis w konkretnym języku programowania (np. C++, Python).

    ##### Sortowanie Bąbelkowe - Opis słowny

    1. **Start:** Algorytm rozpoczyna przeglądanie od samego początku tablicy (lub listy) elementów.
    2. **Porównywanie sąsiadów:** Wybiera pierwsze dwa sąsiadujące ze sobą elementy i je porównuje.
    3. **Zamiana miejsc (Swap):** Jeśli pierwszy z nich jest większy od drugiego (czyli są w złej kolejności), algorytm zamienia je miejscami. Jeśli są w dobrej kolejności, zostawia je bez zmian.
    4. **Przesunięcie:** Następnie algorytm przesuwa się o jedną pozycję do przodu i porównuje kolejną parę sąsiadów (drugi element z trzecim, potem trzeci z czwartym itd.), powtarzając krok 3.
    5. **Koniec pierwszego przejścia:** Ten proces trwa, aż algorytm dotrze do końca tablicy. Po tym pierwszym pełnym przejściu mamy gwarancję, że **największy element znalazł się na swoim docelowym miejscu** (na samym końcu).
    6. **Kolejne iteracje:** Algorytm wraca na początek i powtarza cały cykl dla pozostałych elementów. Ponieważ ostatni element jest już na swoim miejscu, w każdym kolejnym przejściu algorytm sprawdza o jeden element mniej.
    7. **Warunek zakończenia:** Cały proces powtarza się tak długo, aż podczas jednego pełnego przejścia przez listę **nie zostanie wykonana ani jedna zamiana**. Brak zamian jest dla algorytmu sygnałem, że tablica jest już w pełni posortowana i można zakończyć pracę.

    ##### Sortowanie Bąbelkowe - Schemat Blokowy
    
    ```mermaid
        graph TD
        Start([Start]) --> Wejscie[/"Wczytaj tablicę T o rozmiarze N"/]
        Wejscie --> InicjalizacjaI["i = 0"]
        
        InicjalizacjaI --> PetlaZewnetrzna{"Czy i < N?"}
        
        PetlaZewnetrzna -- Tak --> InicjalizacjaJ["j = 0"]
        PetlaZewnetrzna -- Nie --> Koniec(["Koniec - tablica posortowana"])
        
        InicjalizacjaJ --> PetlaWewnetrzna{"Czy j < N - 1?"}
        
        PetlaWewnetrzna -- Tak --> Porownanie{"Czy T[j] > T[j+1]?"}
        PetlaWewnetrzna -- Nie --> InkrementacjaI["i = i + 1"]
        
        InkrementacjaI --> PetlaZewnetrzna
        
        Porownanie -- Tak --> Zamiana["Zamień T[j] i T[j+1]"]
        Porownanie -- Nie --> InkrementacjaJ["j = j + 1"]
        
        Zamiana --> InkrementacjaJ
        InkrementacjaJ --> PetlaWewnetrzna
    ```

**5. Jak można podzielić struktury danych?**
*   **Liniowe:** Dane ułożone są sekwencyjnie (tablice, listy, stosy, kolejki).
*   **Nieliniowe:** Dane tworzą relacje hierarchiczne lub sieciowe (drzewa, grafy).
*   **Statyczne:** Z góry zdefiniowany rozmiar (tradycyjne tablice w C/C++).
*   **Dynamiczne:** Rozmiar zmienia się w trakcie działania programu (listy wiązane, wektory).

**6. Czym jest analiza algorytmów?**
To proces określania zasobów (czasu procesora oraz pamięci) niezbędnych do wykonania algorytmu w zależności od rozmiaru danych wejściowych (n). Cel to znalezienie asymptotycznej złożoności obliczeniowej, pozwalającej porównywać wydajność niezależnie od sprzętu.

**7. Jakie są podstawowe elementy schematów blokowych?**
*   **Owal:** Początek / Koniec algorytmu.
*   **Równoległobok:** Blok wejścia / wyjścia (np. wczytanie zmiennej, wypisanie wyniku).
*   **Prostokąt:** Blok operacyjny (obliczenia, przypisania, np. `x = x + 1`).
*   **Romb (Decyzyjny):** Instrukcja warunkowa (np. `Czy x > 0?`) – wychodzą z niego co najmniej dwie ścieżki (Tak/Nie).

**8. Wyjaśnij różnicę w podejściu iteracyjnym i rekurencyjnym.**
*   **Iteracja:** Opiera się na pętlach (`for`, `while`). Instrukcje powtarzane są wielokrotnie, a stan kontrolowany jest przez zmienne.
*   **Rekurencja:** Funkcja wywołuje samą siebie z mniejszym rozmiarem problemu, aż do osiągnięcia warunku bazowego (brzegowego). Wymaga użycia stosu wywołań.

**9. Jakie są wady i zalety iteracji i rekurencji?**
*   **Iteracja:**
    *   *Zalety:* Szybsza, mniejsze zużycie pamięci (brak narzutu na ramki stosu), odporna na Stack Overflow.
    *   *Wady:* Kod bywa dłuższy i mniej czytelny dla problemów naturalnie rekurencyjnych (np. przeszukiwanie drzew).
*   **Rekurencja:**
    *   *Zalety:* Czysty, zwięzły kod, idealna do strukturyzacji problemów "dziel i zwyciężaj" (np. QuickSort, algorytmy grafowe).
    *   *Wady:* Narzut pamięciowy (ryzyko przepełnienia stosu), często wyższa złożoność czasowa jeśli nie użyjemy spamiętywania (memoization - np. naiwne Fibonacci).

## II. Systemy Liczbowe i Kodowanie

**10. Czym jest system bitowy (binarny)?**
To pozycyjny system liczbowy o podstawie 2. Do zapisu używa się wyłącznie dwóch cyfr: `0` i `1`. Jest to naturalny język procesorów, ponieważ stany logiczne łatwo reprezentować fizycznie (brak napięcia / jest napięcie).

**11. Jak wykonać konwersję dec2bin (dziesiętny na binarny)?**
Dzielimy liczbę dziesiętną przez 2 z resztą, zapisujemy resztę. Następnie dzielimy wynik z poprzedniego dzielenia ponownie przez 2. Proces powtarzamy aż wynik z dzielenia wyniesie 0. Reszty z dzielenia odczytywane **od końca** (od dołu do góry) dają zapis binarny.
*Przykład (13 dec -> bin):*
13 / 2 = 6, reszta **1**
6 / 2 = 3, reszta **0**
3 / 2 = 1, reszta **1**
1 / 2 = 0, reszta **1**
Wynik: `1101`.

**12. Jak wykonać sprawdzenie działania algorytmu dec2bin?**
Wykonując konwersję odwrotną (bin2dec). Mnożymy każdą cyfrę binarną przez 2^n, gdzie n to waga pozycji (od prawej, zaczynając od 0).
*Przykład 1101:*
1 * 2^3 + 1 * 2^2 + 0 * 2^1 + 1 * 2^0 = 8 + 4 + 0 + 1 = 13.

**13. Czym jest zapis heksadecymalny? Gdzie go spotykamy?**
Zapis szesnastkowy (podstawa 16). Pozwala na znaczne skrócenie zapisu binarnego (4 bity to jedna cyfra hex). Spotykany w: zapisie adresów pamięci, kolorach (np. `#FF0000` w CSS/HTML), kryptografii, czy adresach MAC/IPv6.

**14. Jakie znaki występują w zapisie heksadecymalnym?**
Cyfry od `0` do `9` oraz litery `A` (10), `B` (11), `C` (12), `D` (13), `E` (14), `F` (15).

**15. Jak dokonać konwersji dec2hex?**
Analogicznie do dec2bin, ale dzielimy przez 16.
*Przykład (254 dec -> hex):*
254 / 16 = 15, reszta **14** (czyli **E**)
15 / 16 = 0, reszta **15** (czyli **F**)
Odczytujemy od końca: `FE`.

**16. Czym jest tablica ASCII?**
(American Standard Code for Information Interchange). Siedmiobitowy system kodowania znaków, przypisujący liczbom od 0 do 127 konkretne znaki sterujące, litery angielskiego alfabetu, cyfry i znaki interpunkcyjne. Np. 'A' to 65, 'a' to 97, '0' to 48.

## III. Złożoność i Sortowanie

**17. Na czym polega notacja dużego O?**
Notacja asymptotyczna O(f(n)) określa górne ograniczenie tempa wzrostu czasu (lub pamięci) w stosunku do rozmiaru danych n. Pokazuje najgorszy przypadek działania algorytmu, odrzucając stałe i wyrazy niższego rzędu. Np. dla wielomianu 3n^2 + 5n + 10 złożoność wynosi O(n^2).

**18. Jaka jest podstawowa idea sortowania bąbelkowego (Bubble Sort)?**
Iteracyjne porównywanie i zamienianie miejscami (swap) par sąsiadujących elementów. Największy element w każdym przejściu "wypływa" na koniec tablicy niczym bąbelek powietrza.

**19. Jakie modyfikacje przyspieszają sortowanie bąbelkowe?**
1. **Flaga zmiany (Early exit):** Dodanie zmiennej boolean. Jeśli w całym przejściu nie wykonano ani jednej zamiany, tablica jest już posortowana i przerywamy pętlę.
2. **Skracanie zakresu:** Zapamiętywanie indeksu ostatniej wykonanej zamiany – wszystkie elementy za tym indeksem są już na właściwych pozycjach, więc kolejne przejścia mogą być krótsze.

**20. Idea sortowania przez wstawianie (Insertion Sort)?**
Dzieli tablicę na część posortowaną i nieposortowaną. Pobiera pierwszy element z nieposortowanej części i "wstawia" go w odpowiednie miejsce w części posortowanej, przesuwając większe elementy w prawo. Działa rewelacyjnie dla małych zbiorów lub prawie posortowanych.

**21. Idea sortowania przez wybór (Selection Sort)?**
Znajduje najmniejszy (lub największy) element w nieposortowanej części tablicy i zamienia go z pierwszym elementem nieposortowanym. Następnie zmniejsza rozmiar części nieposortowanej o 1.

**22. Złożoności obliczeniowe poznanych algorytmów (czasowe w najgorszym przypadku):**
*   **Bubble Sort:** O(n^2)
*   **Insertion Sort:** O(n^2) (dla posortowanej: O(n))
*   **Selection Sort:** O(n^2)
*   **Quick Sort:** O(n^2) w najgorszym (np. przy złym wyborze pivota), jednak średnio O(n log n).
*   **Merge Sort:** Zawsze O(n log n) – wymaga jednak dodatkowej pamięci O(n).

**23. Idea sortowania szybkiego (QuickSort)?**
Algorytm "dziel i zwyciężaj". Wybiera się element podziału (pivot). Tablicę dzieli się na dwie mniejsze: elementy mniejsze od pivota lądują po jego lewej stronie, a większe po prawej. Następnie rekurencyjnie wykonuje się to na lewej i prawej podtablicy.

**24. Idea sortowania przez scalanie (MergeSort)?**
Kolejny algorytm "dziel i zwyciężaj". Dzieli tablicę na połowy rekurencyjnie aż do uzyskania tablic 1-elementowych (które z definicji są posortowane). Następnie "scala" mniejsze posortowane tablice w większe posortowane całości, używając dodatkowej pamięci.

**25. Jak przyspieszyć QuickSort i MergeSort?**
*   **QuickSort:** Optymalizacja wyboru pivota (np. mediana z trzech elementów: pierwszego, środkowego i ostatniego). Unika się wtedy najgorszego przypadku O(n^2). Dodatkowo: wykluczenie rekurencji ogonowej, przejście na Insertion Sort dla bardzo małych podtablic (np. < 15 elementów).
*   **MergeSort:** Zastosowanie Insertion Sort dla małych fragmentów. Dodatkowo można uniknąć kopiowania danych do tablicy pomocniczej poprzez cykliczne zamienianie referencji między oryginalną tablicą a buforem operacyjnym.

## IV. Złożone Struktury Danych

**26. Czym jest struktura danych?**
(Ponowione - zob. pkt 2). Sposób logicznej organizacji danych w pamięci wspierający konkretne algorytmy (np. kopiec ułatwia znajdowanie maksimum w czasie O(1)).

**27. Czym jest struktura i jak definiuje się ją w C++?**
Struktura pozwala zgrupać powiązane zmienne (różnych typów) w jeden typ złożony pod wspólną nazwą. W C++ do definicji używa się słowa kluczowego `struct`. Domyślnie wszystkie jej pola są publiczne.

```cpp
    #include <iostream>
    #include <string>

    // 1. Definicja struktury
    struct Osoba {
        std::string imie;
        std::string nazwisko;
        int wiek;
    }; // Pamiętaj o średniku na końcu definicji!

    int main() {
        // 2. Tworzenie obiektu struktury (instancji)
        Osoba pracownik;

        // 3. Przypisywanie wartości do pól struktury za pomocą kropki (.)
        pracownik.imie = "Jan";
        pracownik.nazwisko = "Kowalski";
        pracownik.wiek = 30;

        // 4. Odczytywanie wartości
        std::cout << "Dane pracownika:\n";
        std::cout << "Imię: " << pracownik.imie << "\n";
        std::cout << "Nazwisko: " << pracownik.nazwisko << "\n";
        std::cout << "Wiek: " << pracownik.wiek << " lat\n\n";

        // Opcjonalnie: Szybszy sposób inicjalizacji (dostępny w nowszych wersjach C++)
        Osoba klient = {"Anna", "Nowak", 25};
        std::cout << "Klient: " << klient.imie << " " << klient.nazwisko << "\n";

        return 0;
    }
```

**28. Tablica jako struktura danych – opis, wady, zalety.**
*   **Opis:** Zbiór elementów tego samego typu umieszczonych w ciągłym bloku pamięci.
*   **Zalety:** Dostęp do dowolnego elementu w czasie O(1) dzięki indeksowaniu, minimalny narzut pamięciowy (cache-friendly dla procesora).
*   **Wady:** Z góry określony (statyczny) rozmiar. Bardzo kosztowne (czas O(n)) wstawianie i usuwanie elementów w środku lub na początku tablicy, bo wymaga przesuwania reszty elementów.

**29. Jak dodaje się i usuwa elementy z listy (wiązanej)?**
*   **Dodawanie:** Polega na zaalokowaniu nowego węzła, przypisaniu mu wartości, a następnie przepięciu odpowiednich wskaźników (ang. *pointers*). Nowy węzeł wskazuje na element, który ma być "za nim", a element "przed nim" zmienia swój wskaźnik na nowy węzeł.
*   **Usuwanie:** Polega na "przepięciu" wskaźnika elementu poprzedzającego tak, by pomijał usuwany element i wskazywał na ten następujący po nim. Następnie zwalnia się pamięć usuwanego węzła. Czas samego przepięcia to O(1).

**30. Kolejka vs. Stos vs. Lista:**
*   **Stos (Stack):** Model LIFO (Last In, First Out) – dodajemy (push) i zdejmujemy (pop) tylko z wierzchołka.
*   **Kolejka (Queue):** Model FIFO (First In, First Out) – dodajemy (enqueue) na koniec (tail), usuwamy (dequeue) z początku (head).
*   **Lista:** Dostęp swobodny (iterator) do dowolnego miejsca. Można wstawiać i usuwać w dowolnym punkcie, ale znalezienie i-tego elementu zajmuje czas liniowy O(n).

**31. Realistyczne zastosowania stosu i kolejki:**
*   **Stos:** Cofanie operacji w edytorze tekstów (Ctrl+Z), obsługa wywołań funkcji w procesorze (Call Stack), parsowanie wyrażeń arytmetycznych, nawigacja w przeglądarce (przycisk Wstecz).
*   **Kolejka:** Bufory drukarek (kolejkowanie zadań druku), zarządzanie procesami w systemach operacyjnych, obsługa asynchronicznych requestów webowych, przeszukiwanie BFS grafów.

**32. Czym jest ONP?**
Odwrotna Notacja Polska (Reverse Polish Notation, RPN). Zapis matematyczny, w którym operator znajduje się zawsze po swoich operandach. Eliminuje to konieczność używania nawiasów i uwzględniania priorytetów operatorów. Do jego ewaluacji idealnie nadaje się stos.
*Przykład:* 2 + 3 * 4 zapisane w ONP to `2 3 4 * +`.

**33. Jakie zmiany wprowadza kolejka priorytetowa?**
W zwykłej kolejce elementy wychodzą w kolejności wejścia. W kolejce priorytetowej (często implementowanej na strukturze *kopca*), każdy element ma przypisany "priorytet". Element o najwyższym priorytecie opuszcza kolejkę pierwszy, niezależnie od tego, kiedy do niej trafił (np. karetka na SORze, procesy w systemie czasu rzeczywistego).

**34. Co znaczy, że lista jest dwukierunkowa lub jednokierunkowa?**
*   **Jednokierunkowa (Singly Linked List):** Każdy węzeł posiada wartość oraz wskaźnik tylko na **następny** element. Możemy przechodzić ją tylko do przodu.
*   **Dwukierunkowa (Doubly Linked List):** Każdy węzeł posiada wartość oraz dwa wskaźniki: na element **następny** oraz **poprzedni**. Umożliwia iterację w obu kierunkach kosztem nieco większego zużycia pamięci.

**35. Co wyróżnia strukturę danych zbiór (Set)?**
Zbiór przechowuje unikalne wartości (brak duplikatów). Najczęściej implementowany jako drzewo poszukiwań (C++ `std::set`, O(log n) operacji) lub tablica z haszowaniem (C++ `std::unordered_set`, Python `set`, O(1) amortyzowane operacji). Wykorzystywany do szybkiego sprawdzania przynależności.

**36. Co wyróżnia strukturę danych słownik (Map/Dictionary)?**
Przechowuje pary klucz-wartość (Key-Value). Klucze w słowniku muszą być unikalne. Pozwala na bardzo szybkie (często w czasie O(1)) odszukiwanie danych przypisanych do unikalnego klucza (np. PESEL jako klucz, obiekt pacjenta jako wartość).

**37. Co wyróżnia strukturę danych wektor (Vector / Tablica dynamiczna)?**
Rozwiązuje problem statycznego rozmiaru tablic. Wektor to tablica dynamiczna (np. `std::vector` w C++), która w tle posiada bufor pamięci. Kiedy bufor się zapełni, alokuje nowy (najczęściej 2x większy), kopiuje dane i zwalnia stary. Łączy zalety tablic (odczyt O(1)) z możliwością dynamicznego rozrostu.

## V. Szyfrowanie i Podstawy Kryptografii (Wersja Rozbudowana)

**38. Wymień zastosowania szyfrów.**
Szyfrowanie to fundament dzisiejszego bezpieczeństwa, znajdujący zastosowanie w wielu warstwach technologii:
*   **Poufność komunikacji:** Zabezpieczanie wiadomości w komunikatorach (np. End-to-End Encryption protokołu Signal), e-mailach, czy sieciach wojskowych, aby przechwycona informacja (np. atakiem Man-in-the-Middle) była bezwartościowa dla atakującego.
*   **Bezpieczeństwo w internecie (HTTPS/TLS):** Kryptografia asymetryczna i symetryczna chroni hasła, pakiety sieciowe i dane kart płatniczych przesyłane do serwerów.
*   **Bezpieczeństwo danych w spoczynku:** Algorytmy blokowe stosuje się do szyfrowania całych dysków (np. BitLocker) lub pojedynczych kontenerów z danymi, zabezpieczając systemy plików.
*   **Uwierzytelnianie i podpisy cyfrowe:** Zapewnienie integralności danych i weryfikacja tożsamości – logowanie z użyciem kluczy publicznych SSH, certyfikaty serwerów, algorytmy RSA.

**39. Podaj i opisz 3 główne typy klasycznych szyfrów z przykładami.**
1.  **Szyfry podstawieniowe proste (monoalfabetyczne):** Każdej literze alfabetu jawnego odpowiada zawsze ta sama litera lub znak tajny. Forma znaku zostaje zamieniona, ale znak pozostaje w tym samym miejscu.
    *   *Przykłady:* Szyfr Cezara, Atbasz. Bardzo łatwe do złamania metodą kryptoanalizy częstotlinościowej (np. badanie liczby wystąpień litery 'A' lub 'E' w tekście).
2.  **Szyfry przestawieniowe:** Znaki tekstu jawnego zachowują swoją formę, ale zmieniają ułożenie w pamięci (są tasowane według matematycznego schematu).
    *   *Przykłady:* Szyfr płotkowy, szyfr kolumnowy (macierzowy), anagramy.
3.  **Szyfry podstawieniowe polialfabetyczne:** Najbezpieczniejsza z klasycznych klas. Jedna litera tekstu jawnego jest zastępowana przez wiele różnych znaków szyfrogramu w zależności od jej przesunięcia i klucza. Silnie spłaszcza to statystykę występowania znaków.
    *   *Przykłady:* Szyfr Vigenère'a, niemiecka Enigma.

**40. Wyjaśnij zasadę działania szyfru Cezara.**
Jest to podstawowy szyfr przesuwający. Każdą literę tekstu jawnego zastępujemy literą leżącą o stałą liczbę miejsc dalej w alfabecie. Przesunięcie poza literę 'Z' jest kontrolowane za pomocą arytmetyki modulo (tzw. "zawijanie").
*   **Szyfrowanie:** Przy kluczu $+3$ mamy przesunięcie: $A \to D$, $B \to E$. Zatem słowo "KOT" staje się "NRW".
*   **Deszyfrowanie:** Wykonujemy operację odwrotną, odejmując wartość przesunięcia (szyfrogram $- 3$).
*   *Słabość:* Dla 26-literowego alfabetu istnieje zaledwie 25 wariantów klucza. Atak siłowy (brute-force) na wszystkie kombinacje wymaga minimalnej mocy obliczeniowej.

**41. Wyjaśnij zasadę działania kodu Morse'a.**
Morse to technika kodowania sygnałów, a nie szyfr (z założenia nie ukrywa wiadomości, jedynie tłumaczy ją na inny format przesyłowy).
*   Składa się ze stanów binarnych: sygnałów krótkich (kropka `·`) i sygnałów długich (kreska `-`, która jest trzykrotnie dłuższa od kropki).
*   Synchronizację w transmisji zapewniają precyzyjne odstępy: krótka pauza rozdziela elementy znaku, średnia rozdziela litery, a długa całe słowa.
*   *Przykład:* Litera 'S' to `···`, litera 'O' to `---`.

**42. Wyjaśnij zasadę działania szyfru XOR.**
Opiera się na logicznej bramce XOR (Alternatywa Wykluczająca, symbol $\oplus$). Stanowi absolutny fundament algorytmiki szyfrów blokowych i strumieniowych.
*   Operacja bitowa zwraca `1` tylko, gdy bity wejściowe są różne ($1 \oplus 0 = 1$, $1 \oplus 1 = 0$).
*   **Mechanizm szyfrowania:** Reprezentację binarną tekstu poddaje się operacji logicznej z ciągiem klucza: $Tekst \oplus Klucz = Szyfrogram$.
*   **Samo-odwracalność:** Nie potrzeba osobnej funkcji deszyfrującej. Aby odzyskać tekst, przepuszcza się szyfrogram przez tę samą instrukcję: $Szyfrogram \oplus Klucz = Tekst$. Jeśli klucz składa się z całkowicie losowych wartości o długości komunikatu, algorytm realizuje tzw. wariant z kluczem jednokrotnym (One-Time Pad) i jest uważany za teoretycznie niełamalny.

**43. Wyjaśnij zasadę działania prostego szyfru przestawieniowego.**
Znaki pozostają takie same, ale ich wektor indeksów w ciągu jest transponowany na podstawie geometrii lub prostej reguły. Najłatwiej wyobrazić to sobie jako podzielenie wiadomości na bloki, a następnie zapisywanie znaków naprzemiennie lub zamianę parami indeksu nieparzystego z parzystym. Przykładem antycznym jest spartańska Skytale – rzemień z rzędami tekstu, który stawał się czytelny wyłącznie po nawinięciu na cylinder o ściśle dopasowanym promieniu.

**44. Wyjaśnij zasadę działania szyfru płotkowego (Rail Fence).**
Rozwinięcie szyfru przestawieniowego. Tekst układa się po przekątnych (zygzakiem), wpisując go w wiersze zdefiniowanej dwuwymiarowej tablicy (symulując malowanie szczebelków płotu). Liczba dostępnych wierszy (wysokość) to klucz symetryczny.
*   *Przykład (wysokość = 3, dla słowa "TAJNE"):*
    Wiersz 1: `T . . . E`
    Wiersz 2: `. A . N .`
    Wiersz 3: `. . J . .`
*   Szyfrogram generowany jest poprzez ekstrakcję ciągów znaków rzędami od góry do dołu: `TE AN J` $\to$ `TEANJ`.

**45. Wyjaśnij zasadę działania szyfru ze słowem-kluczem (np. GA-DE-RY-PO-LU-KI). Jakie inne słowa można użyć?**
Technika dwustronnego mapowania harcerskiego bazująca na słowniku. Klucz stanowi zbiór dwuliterowych par (sylab).
*   *Zasada:* Iterując przez wprowadzony ciąg, sprawdzamy każdy znak. Jeżeli znak występuje jako klucz słownika, podmieniamy go na jego przypisaną parę (np. wejście `G` wyrzuca `A`, wejście `A` wyrzuca `G`). Znaków spoza mapy klucza nie modyfikujemy.
*   *Przykłady map:* Elementy w nich muszą zawierać unikalne znaki (brak kolizji).
    *   `PO-LI-TY-KA-RE-NU`
    *   `KO-NI-EC-MA-TU-RY`
    *   `MA-LI-NO-WE-BU-TY`
    *   `KA-CE-MI-NU-TO-WY`

**46. Wyjaśnij zasadę działania szyfru z samogłoskami.**
Rodzina manualnych technik steganograficznych/podstawieniowych stosowanych do podstawowego kamuflażu wyrazów. Logika skupia się wybiórczo na modyfikacji znaków `A, E, I, O, U, Y`.
*   *Wariant cyfrowy:* Tworzy się wektor asocjacyjny dla samogłosek (A=1, E=2, I=3, O=4, U=5, Y=6). Reszta zostaje znakowa. Wyraz "DOM" to "D4M".
*   *Wariant redukcyjny (abjad):* Wszystkie samogłoski zostają wycięte ze strumienia wyjściowego, a przesyłane są tylko spółgłoski (np. "SZYFR" $\to$ "SZFR"). Wiadomość rekonstruowana jest heurystycznie na bazie kontekstu semantycznego.

**47. Wyjaśnij zasadę działania szyfru Atbasz.**
Hebrajski szyfr monoalfabetyczny o charakterze odwróconym (symetryczny). Klucz powstaje przez "złożenie" tradycyjnego alfabetu w jego punkcie środkowym – następuje rzutowanie początkowych indeksów na indeksy końcowe.
Pierwsza litera `A` łączy się z literą `Z`, wartość `B` rzutuje na `Y` itd. Identyczna operacja zarówno zabezpiecza jak i zdejmuje ochronę z pakietu tekstu.

**48. Wyjaśnij zasadę działania szyfru ułamkowego.**
Wymaga zdefiniowania specjalnej macierzy znakowej. Osie kolumn oraz rzędów są indeksowane cyframi (arabskimi lub rzymskimi). Algorytm ukrywa tekst jako ciąg formuł wizualnie przypominających ułamki. Położenie wybranego znaku to licznik i mianownik tego sztucznego ułamka. Kodowanie to trudne do przechwycenia telefonicznie (fonetycznie), używane do bezpiecznej transmisji utrwalanej w brudnopisach z notatkami arytmetycznymi.

**49. Wyjaśnij zasadę działania szyfru Vigenère'a.**
Historycznie przełomowy algorytm wykorzystujący tablicę 26x26, czyli Kwadrat Vigenère'a (gdzie w każdym nowym rzędzie cyklicznie przesuwa się ciąg znaków o pozycję w lewo).
*   Szyfrowanie wykorzystuje słowo uwierzytelniające (np. "TAJNE"), które klonowane jest na całą szerokość kodowanego wejścia.
*   Znak wiadomości wyznacza kolumnę szukania w matrycy, a parujący go znak z replikowanego klucza – właściwy wiersz. Wektor znajdujący się na skrzyżowaniu tworzy szyfrogram.
*   Jeden zarys znaku (np. 'A') potrafi zostać sparsowany na kilka zróżnicowanych elementów wynikowych. Tradycyjna kryptoanaliza używająca rozkładu częstotliwości ulega tutaj całkowitej dezinformacji.

**50. Wyjaśnij zasadę działania szyfru Sanatorium.**
Odłam harcerskich protokołów podstawieniowych bliski mechanizmom "GA-DE-RY-PO-LU-KI". Ponieważ użyte słowo ("SANATORIUM") wykazuje się duplikacją pewnych liter, jak "A" oraz "O", jest to konstrukcja z natury wadliwa do klasycznego parowania sylab. Z reguły rozwiązuje się ten problem, konwertując wyraz w strukturę cyfrowo-literową, rzutując cyfry numeryczne na unikalne znaki znajdujące się w korpusie wyrazu, w celu zachowania integralności translacji.

**51. Opisz szyfr VIC.**
Niezwykle złożony manualny kryptosystem rosyjskiego wywiadu (używany przez agenta "VICTORA" – Reino Häyhänena). Jego trzonem była tzw. straddling checkerboard (szachownica rozdzielająca) operująca na entropii statystycznej – najpopularniejsze znaki języka reprezentowała jedną cyfrą dziesiętną, podczas gdy rzadkie dwiema, niszcząc strukturę długości bloków. Wynik z szachownicy modyfikowano podwójną arytmetyką modułową generowaną na bazie łańcuchów liczb podchodzących pod równania pokrewne do ciągów Fibonacciego i z wyselekcjonowanych dat lub haseł początkowych. Uznany za apogeum szyfrów bez-maszynowych.

**52. Czym jest tablica Polibiusza?**
Najstarszy ze zbadanych dwuwymiarowych systemów znakowych wynaleziony przez starożytnych Greków. Zestaw znaków umieszcza się na kwadratowej przestrzeni (najczęściej 5x5 tablicy wielowymiarowej, ze względów pojemnościowych łącząc np. literę I/J).
*   Zarówno osie poziome, jak i pionowe podlegają etykietowaniu liczbami od 1 do 5.
*   Aby wysłać zakodowaną komórkę tekstu, rzuca się jej pozycję w postaci złączenia indeksu wiersza z indeksem kolumny. Litera lądująca w układzie współrzędnych [1, 4] przesyłana jest jako int "14". Algorytm ten przyczynił się do powstania późniejszych rozwiązań transmisji kablowej i stukowych szyfrów więziennych.

**53. Jakie są cechy dobrego słowa kluczowego w szyfrach typu GA-DE-RY-PO-LU-KI?**
Aby klucz w szyfrze opartym na wzajemnym parowaniu liter był skuteczny, musi spełniać kilka rygorystycznych założeń technicznych i praktycznych:
*   **Unikalność liter (brak powtórzeń):** Żadna litera w całym haśle nie może wystąpić więcej niż jeden raz. Powtórzenia sprawiłyby, że szyfr stałby się niejednoznaczny (jedna litera rzutowałaby na dwie różne).
*   **Parzysta długość:** Klucz musi idealnie dzielić się na pary. Każda litera musi mieć swojego unikalnego partnera.
*   **Wysoka zawartość popularnych znaków:** Ponieważ znaki spoza klucza nie są szyfrowane, dobry klucz powinien zawierać litery najczęściej używane w języku polskim (przede wszystkim samogłoski: A, E, I, O, U, Y), aby zakodować jak największą część wiadomości.
*   **Optymalna długość:** Najlepsze klucze mają od 10 do 14 liter (5 do 7 par). Zbyt krótki klucz (np. 6 liter) zostawia za dużo tekstu jawnego, a zbyt długi trudno ułożyć bez powtarzania liter.
*   **Mnemotechnika (łatwość zapamiętania):** Szyfry tego typu są szyframi pamięciowymi. Klucz powinien być logiczną frazą lub istniejącym słowem (np. `KO-NI-EC-MA-TU-RY`), aby umożliwić jego bezproblemowe odtworzenie w głowie.