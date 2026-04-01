Andrii Khomenko | IAD | 3 rok | Case Study

# **Analiza możliwości predykcji dziennego kierunku zmian ceny złota na** **podstawie danych rynkowych i makroekonomicznych z wykorzystaniem** **metod klasyfikacji**


**1.** **Business Understanding**

1.0. Tło problemu i kontekst biznesowy


Złoto od wielu lat postrzegane jest jako tzw. _bezpieczna przystań_ (safe haven), czyli
aktywo chroniące wartość kapitału w okresach podwyższonej niepewności
gospodarczej, inflacji, niestabilności rynków finansowych oraz napięć
geopolitycznych. Jego ograniczona podaż, globalna akceptowalność oraz
historyczna rola w systemie finansowym sprawiają, że zachowanie cen złota często
różni się od zachowania rynków akcji czy innych instrumentów finansowych.


W praktyce inwestycyjnej analiza zależności pomiędzy rynkiem złota a innymi
instrumentami, takimi jak indeksy giełdowe czy surowce energetyczne, stanowi
istotny element podejmowania decyzji inwestycyjnych. Umiejętność przewidywania
krótkoterminowego kierunku zmian ceny złota może wspierać inwestorów oraz
analityków finansowych w zarządzaniu portfelem oraz ocenie bieżącej sytuacji
rynkowej.


1.1. Cel analizy


Głównym celem niniejszego case study jest **zbadanie możliwości przewidywania**
**kierunku dziennej zmiany ceny złota na podstawie wybranych wskaźników**
**rynkowych**, takich jak indeks giełdowy S&P 500, ceny ropy naftowej oraz palladu.


Analiza ma charakter eksploracyjno-predykcyjny i koncentruje się na ocenie, czy
informacje pochodzące z innych rynków finansowych mogą dostarczać sygnałów
pozwalających klasyfikować dni jako wzrostowe lub spadkowe dla rynku złota.


1.2. Definicja problemu analitycznego


Problem analityczny został sformułowany jako **zadanie klasyfikacji nadzorowanej** .
Zmienną decyzyjną jest kierunek dziennej zmiany ceny złota, przyjmujący dwie
możliwe klasy:


     - **UP**      - cena złota wzrosła w porównaniu do poprzedniego dnia,

     - **DOWN**      - cena złota spadła lub pozostała bez zmian.


Taki sposób definicji zmiennej decyzyjnej umożliwia uproszczenie problemu
predykcyjnego oraz zwiększa interpretowalność wyników, co jest szczególnie istotne
w kontekście zastosowanych algorytmów eksploracji danych.


1.3. Uzasadnienie wyboru podejścia klasyfikacyjnego


Pomimo faktu, że ceny instrumentów finansowych mają charakter ciągły, w
niniejszym projekcie zdecydowano się na podejście klasyfikacyjne zamiast
regresyjnego. Decyzja ta została podjęta z następujących powodów:


  - wylosowany algorytm **OneR** jest algorytmem klasyfikacyjnym **,**

  - klasyfikacja kierunku zmiany ceny jest często bardziej użyteczna decyzyjnie
niż dokładna predykcja wartości,

  - binarny podział na dni wzrostowe i spadkowe pozwala na łatwiejszą
interpretację wyników oraz porównanie modeli.

1.4. Interesariusze i potencjalne zastosowanie wyników


Potencjalnymi odbiorcami wyników analizy mogą być:


  - inwestorzy indywidualni,

  - analitycy rynków finansowych,

  - osoby zajmujące się zarządzaniem ryzykiem.


Uzyskane modele mogą stanowić narzędzie wspomagające krótkoterminową ocenę
sytuacji rynkowej, a także punkt wyjścia do dalszych, bardziej zaawansowanych
analiz predykcyjnych.


1.5. Kryteria sukcesu projektu


Za sukces projektu uznaje się:


  - poprawne sformułowanie problemu klasyfikacyjnego,

  - zbudowanie i ocenę dwóch modeli klasyfikacyjnych (OneR oraz Random
Forest),

  - przejrzystą interpretację wyników,

  - porównanie modeli pod kątem skuteczności i interpretowalności.


**2.** **Data Understanding**

2.0. Źródło i charakterystyka zbioru danych


W analizie wykorzystano zbiór danych _financial_regression.csv_, zawierający **szereg**
**czasowy danych finansowych** z okresu od **2010 do 2024 roku** . Każda obserwacja
odpowiada jednemu punktowi czasowemu i opisana jest za pomocą zestawu
zmiennych dotyczących rynków kapitałowych oraz surowców.


Zbiór danych obejmuje **47 kolumn**, w tym:


    - jedną zmienną czasową ( _date_ ),

    - zestawy zmiennych opisujących **indeks giełdowy S&P 500**,

    - zestawy zmiennych opisujących **indeks NASDAQ**,

    - zestawy zmiennych opisujących **rynek złota (Gold)**,

    - zestawy zmiennych opisujących **rynek palladu (Palladium)** .


Dla każdego z wymienionych instrumentów dostępne są dane typu **OHLCV**, czyli:


    - cena otwarcia ( _open_ ),

    - cena maksymalna ( _high_ ),

    - cena minimalna ( _low_ ),

    - cena zamknięcia ( _close_ ),

    - wolumen obrotu ( _volume_ ).

2.1. Opis zmiennych i ich znaczenia ekonomiczne
2.1.1. Zmienna czasowa

        - date – data obserwacji; zmienna pełni rolę indeksu czasowego,
umożliwiając analizę dynamiki zmian w czasie oraz synchronizację
danych pochodzących z różnych rynków finansowych.
2.1.2. Zmienne dotyczące rynków finansowych i surowców – dane dzienne


Do tej grupy należą zmienne opisujące **indeksy giełdowe oraz rynki surowców**
**i metali**, które mają **charakter danych dziennych** . Dla wszystkich tych
instrumentów dostępny jest analogiczny zestaw zmiennych typu **OHLCV**, co
zapewnia spójność struktury danych.


**Instrumenty objęte danymi dziennymi:**


        - indeks giełdowy **S&P 500**

        - indeks giełdowy **NASDAQ**

        - **srebro (silver)**


      - **ropa naftowa (oil)**

      - **platyna (Platinum)**

      - **pallad (palladium)**

      - **złoto (gold)**


**Zakres dostępnych zmiennych:**


Dla każdego z powyższych instrumentów dostępne są następujące kolumny:


      - *.open – cena otwarcia,

      - *.high – najwyższa cena w danym dniu,

      - *.low – najniższa cena w danym dniu

      - *.close – cena zamknięcia,

      - *.volume – wolumen obrotu,

      - *.high.low – różnica pomiędzy ceną maksymalną i minimalną, będąca
miarą dziennej zmienności.


**Znaczenie ekonomiczne:**


      - **cena zamknięcia (close)** stanowi podstawową miarę kierunku
zmian rynku i jest najczęściej wykorzystywana w analizach
finansowych,

      - **zakres cenowy (high.low)** odzwierciedla poziom zmienności i
niepewności rynkowej w danym dniu,

      - **wolumen (volume)** jest przybliżeniem aktywności inwestorów oraz
płynności rynku.


W niniejszym projekcie szczególną rolę odgrywają zmienne dotyczące rynku złota,
które stanowią podstawę do konstrukcji zmiennej decyzyjnej w dalszych etapach
analizy.


2.1.3. Zmienne makroekonomiczne – dane miesięczne


**us_rates_%**


      - zmienna opisująca **stopy procentowe w Stanach Zjednoczonych**
(wyrażone w procentach),

      - dane mają charakter **miesięczny**,

      - stopy procentowe są jednym z kluczowych instrumentów polityki
monetarnej i mają istotny wpływ na rynki finansowe, w tym na rynek
złota, który często reaguje odwrotnie do zmian stóp procentowych.


**CPI**

    - **Consumer Price Index**     - wskaźnik cen towarów i usług
konsumpcyjnych,

    - Dane raportowane w **ujęciu miesięcznym**,

    - CPI jest podstawową miarą inflacji i odzwierciedla zmiany siły
nabywczej pieniądza,

    - Wzrost inflacji często zwiększa zainteresowanie złotem jako
zabezpieczeniem wartości kapitału.
2.1.4. Zmienne walutowe – dane dzienne


**usd_chf**


    - kurs wymiany dolara amerykańskiego względem franka
szwajcarskiego,

    - dane o **częstotliwości dziennej**,

    - frank szwajcarski, podobnie jak złoto, bywa postrzegany jako
bezpieczna przystań, co może prowadzić do interesujących
zależności pomiędzy tymi aktywami.


**eur_usd**


    - kurs wymiany euro względem dolara amerykańskiego,

    - dane o **częstotliwości dziennej**,

    - para walutowa EUR/USD jest jedną z najważniejszych na rynku Forex
i często odzwierciedla globalne nastroje makroekonomiczne oraz
politykę monetarną.
2.1.5. Zmienna makroekonomiczna – dane kwartalne


**GDP**


    - **Gross Domestic Product**     - produkt krajowy brutto,

    - dane raportowane w **ujęciu kwartalnym**,

    - PKB jest miarą ogólnej kondycji gospodarki i poziomu aktywności
ekonomicznej,

    - Zmiany PKB mogą pośrednio wpływać na rynki finansowe oraz popyt
na surowce i metale szlachetne.
2.1.6. Podsumowanie charakterystyki zmiennych


Zbiór danych łączy w jednym zestawie:


    - dane dzienne (rynki finansowe, surowce, waluty),


        - dane miesięczne (stopy procentowe, inflacja),

        - dane kwartalne (PKB).


Takie połączenie zmiennych o różnej częstotliwości obserwacji stanowi
istotne wyzwanie analityczne i wymaga odpowiednich decyzji na etapie
przygotowania danych, które zostaną szczegółowo omówione w kolejnym
etapie.


**3.** **Data Preparation**

3.0. Wstępna eksploracja danych (EDA)


Przed przystąpieniem do imputacji i przygotowania danych wykonano krótką analizę
eksploracyjną, w szczególności w zakresie wartości odstających oraz zmienności
cen. Zastosowano wykresy pudełkowe (boxplot) dla wybranych instrumentów (m.in.
złoto, S&P500, ropa, srebro, platyna i pallad) oraz wykres czasowy ceny złota z
oznaczeniem obserwacji odstających według reguły IQR (1.5×IQR). Dodatkowo
przeanalizowano dzienne stopy zwrotu złota, aby ocenić poziom zmienności
szeregu.


Wyniki wskazują, że w danych występują obserwacje odstające, jednak są one
charakterystyczne dla danych finansowych i odpowiadają okresom zwiększonej
zmienności rynkowej. Z tego powodu nie usuwano tych obserwacji, ponieważ
mogłoby to prowadzić do utraty informacji o ekstremalnych zdarzeniach, które w
praktyce są istotne dla rynku.


Rys. 1. Boxploty cen zamknięcia wybranych instrumentów


Rys. 2. Wartości odstające ceny złota w czasie


Rys. 3. Dzienne stopy zwrotu ceny złota


3.1. Wybór docelowej częstotliwości czasowej danych


Zbiór danych zawiera zmienne raportowane z różną częstotliwością czasową:
dzienną, miesięczną oraz kwartalną. Przed rozpoczęciem modelowania konieczne
było podjęcie decyzji dotyczącej **ujednolicenia osi czasu**, aby wszystkie obserwacje
mogły zostać wykorzystywane w jednym modelu klasyfikacyjnym.


W niniejszej analizie jako **docelową częstotliwość danych przyjęto częstotliwość**
**dzienną** .


Decyzja ta została podjęta z następujących powodów:


   - zmienna decyzyjna (kierunek zmiany ceny złota) oparta jest na **dziennych**
**notowaniach**,

   - większość zmiennych objaśniających (rynki akcji, surowce, metale, kursy
walut) ma charakter dzienny,

   - agregacja danych dziennych do danych miesięcznych lub kwartalnych
prowadziłaby do znacznej utraty informacji oraz zmniejszenia liczby
obserwacji.


Dane miesięczne i kwartalne zostały zatem dostosowane do częstotliwości dziennej
w kolejnych etapach przygotowania danych.


Rys. 4. Wizualizacja braków danych (missingness plot) dla wybranych zmiennych w czasie.


Rysunek 4. jednoznacznie wskazuje, że zmienne dzienne posiadają obserwacje
niemal dla każdego dnia roboczego, natomiast zmienne makroekonomiczne
charakteryzują się długimi okresami braku danych, co potwierdza ich niższą
częstotliwość raportowania. Obserwacja ta uzasadnia konieczność ujednolicenia
danych do wspólnej osi czasowej.


3.2. Dostosowanie danych miesięcznych i kwartalnych do częstotliwości dziennej


W zbiorze danych występują zmienne makroekonomiczne raportowane rzadziej niż
dane rynkowe:


   - us_rates_% oraz CPI – dane **miesięczne**,

   - GDP – dane **kwartalne** .


Aby umożliwić ich wykorzystanie w modelach klasyfikacyjnych opartych na danych
dziennych, zastosowano metodę **forward-fill** (przenoszenie ostatniej znanej
wartości). Polega ona na przypisaniu ostatniej dostępnej obserwacji do kolejnych dni
aż do momentu publikacji nowej wartości.


Takie podejście jest uzasadnione ekonomicznie, ponieważ wskaźniki
makroekonomiczne zmieniają się stosunkowo wolno, a w praktyce rynkowej do
momentu ogłoszenia nowej wartości wykorzystywana jest ostatnia znana
obserwacja. Dzięki temu możliwe było ujednolicenie danych do wspólnej osi
czasowej bez sztucznego „zgadywania” brakujących wartości.


Warto zaznaczyć, że forward-fill **nie uzupełnia braków na początku szeregu**
**czasowego**, ponieważ nie istnieje wcześniejsza obserwacja, którą można przenieść.
Z tego powodu początkowe wiersze bez wartości makroekonomicznych zostały
usunięte z dalszej analizy, aby zachować spójność danych.


3.3. Podsumowanie braków po imputacji i decyzja o usunięciu NA


Po zastosowaniu forward-fill obliczono łączny udział braków danych w zbiorze.
Wyniósł on około **4.47%**, co jest relatywnie niską wartością. Ponieważ pozostałe
braki danych pojawiały się najczęściej w całych wierszach (brakowało wielu
zmiennych jednocześnie), podjęto decyzję o usunięciu obserwacji z wartościami NA
zamiast dalszej imputacji. Takie podejście upraszcza proces przygotowania danych
i ogranicza ryzyko wprowadzenia sztucznych wartości.


3.4. Konstrukcja zmiennej decyzyjnej oraz przygotowanie zbioru danych do
modelowania


Celem analizy było zbudowanie modelu klasyfikacyjnego przewidującego dzienny
kierunek zmiany ceny złota. W związku z tym konieczne było zdefiniowanie zmiennej
decyzyjnej o charakterze binarnym oraz przygotowanie odpowiedniego zbioru cech
wejściowych.


Zmienna decyzyjna **gold_direction** została skonstruowana na podstawie dziennej
zmiany ceny zamknięcia złota. Dla każdej obserwacji obliczono różnicę pomiędzy
ceną zamknięcia danego dnia a ceną z dnia poprzedniego. Na tej podstawie przyjęto
następujące klasy:


  - **UP**   - cena złota wzrosła w porównaniu do dnia poprzedniego,

  - **DOWN**   - cena złota spadła lub pozostała bez zmian.


Takie podejście pozwala sprowadzić problem do klasyfikacji binarnej i jest często
stosowane w analizach krótkoterminowych danych finansowych. Pierwsza


obserwacja szeregu czasowego, dla której nie można obliczyć zmiany względem
poprzedniego dnia, została usunięta z dalszej analizy.


Rys. 5. Rozkład klas zmiennej gold_direction


Po zdefiniowaniu zmiennej decyzyjnej przygotowano zbiór cech wejściowych. Do
dalszej analizy wybrano wyłącznie zmienne numeryczne, z wyłączeniem zmiennych
bezpośrednio związanych z konstrukcją zmiennej decyzyjnej (takich jak bezwzględna
cena złota oraz dzienna różnica cen), aby uniknąć tzw. _data leakage_ . Następnie
przeanalizowano wzajemne korelacje pomiędzy cechami i usunięto zmienne
charakteryzujące się bardzo wysoką korelacją (powyżej 0.95), co pozwoliło
ograniczyć redundancję informacji w zbiorze danych.


Ostateczny zbiór danych do modelowania składał się ze zmiennej decyzyjnej,
zestawu wybranych cech numerycznych oraz zmiennej czasowej date,
wykorzystywanej wyłącznie do zachowania kolejności chronologicznej obserwacji.


Ze względu na szeregowy charakter danych finansowych, podział danych na zbiory
treningowy i testowy został wykonany z zachowaniem kolejności czasowej, bez
losowego próbkowania. Cztery ostatnie obserwacje zostały wydzielone jako zbiór
predykcyjny, służący wyłącznie do demonstracji działania modeli na najbardziej
aktualnych danych. Pozostałe obserwacje podzielono w proporcji 80%–20% na zbiór
treningowy oraz zbiór walidacyjny (testowy).


Tak przygotowany zbiór danych stanowił podstawę do dalszego etapu modelowania
i ewaluacji algorytmów klasyfikacyjnych.


**4.** **Modelowanie**


W niniejszym rozdziale przedstawiono proces budowy oraz oceny modeli
klasyfikacyjnych wykorzystanych do predykcji dziennego kierunku zmiany ceny złota.
Zastosowano dwa algorytmy o różnym stopniu złożoności: prosty model regułowy
OneR oraz bardziej zaawansowany model zespołowy Random Forest.


4.0. Zastosowane algorytmy: OneR oraz Random Forest


Algorytm **OneR (One Rule)** jest prostym modelem klasyfikacyjnym opartym na
pojedynczej regule decyzyjnej. Wybiera on jedną zmienną objaśniającą, która
najlepiej rozdziela klasy decyzyjne, a następnie buduje regułę przypisującą klasę na
podstawie wartości tej zmiennej. Ze względu na swoją prostotę OneR został
wykorzystany jako **model bazowy**, umożliwiający ocenę minimalnego poziomu
skuteczności predykcji.


Model **Random Forest** jest algorytmem zespołowym opartym na wielu drzewach
decyzyjnych trenowanych na losowych podpróbkach danych oraz losowych
podzbiorach cech. Takie podejście pozwala na modelowanie złożonych,
nieliniowych zależności pomiędzy zmiennymi oraz ogranicza ryzyko przeuczenia.
Random Forest jest często stosowany w analizach finansowych ze względu na swoją
stabilność i odporność na szum w danych.


4.1. Uzasadnienie wyboru algorytmu Random Forest


Wybór algorytmu Random Forest jako głównego modelu predykcyjnego był
uzasadniony kilkoma czynnikami. Po pierwsze, analizowany problem charakteryzuje
się dużą zmiennością i potencjalnie nieliniowymi zależnościami pomiędzy
zmiennymi rynkowymi i makroekonomicznymi, które trudno uchwycić za pomocą
prostych reguł decyzyjnych. Po drugie, Random Forest umożliwia jednoczesne
wykorzystanie wielu cech, co jest istotne w kontekście wielowymiarowego
charakteru danych finansowych.


Dodatkową zaletą Random Forest jest możliwość oceny ważności cech, co pozwala
na interpretację wpływu poszczególnych zmiennych na decyzje modelu. Algorytm
ten posiada również wbudowany mechanizm walidacji (out-of-bag error), który
umożliwia ocenę jakości modelu bez konieczności stosowania dodatkowych
zbiorów walidacyjnych.


4.2. Trening i wyniki modelu OneR


Model OneR został wytrenowany na zbiorze treningowym z wykorzystaniem
wszystkich dostępnych cech wejściowych, przy czym algorytm automatycznie
wybrał jedną zmienną, na podstawie której skonstruował prostą regułę decyzyjną.
Następnie model został oceniony na zbiorze walidacyjnym przy użyciu
standardowych miar jakości klasyfikacji.


Uzyskane wyniki wskazują, że skuteczność modelu OneR jest ograniczona. Choć w
porównaniu do losowego zgadywania model osiąga umiarkowane wartości miar
jakości, to jego wyniki pozostają wyraźnie słabsze niż w przypadku bardziej
zaawansowanego algorytmu Random Forest. OneR charakteryzuje się stosunkowo
wysoką czułością (Recall), co oznacza skłonność do częstego przewidywania klasy
UP, jednak odbywa się to kosztem obniżonej precyzji (Precision).


W konsekwencji miara F1-score osiąga jedynie umiarkowany poziom, co potwierdza,
że model oparty na pojedynczej regule nie jest w stanie uchwycić złożonych
zależności występujących w danych finansowych. Z tego względu algorytm OneR
należy traktować przede wszystkim jako model bazowy i punkt odniesienia dla
bardziej złożonych metod klasyfikacyjnych.


4.3. Trening i wyniki modelu Random Forest


Model Random Forest został wytrenowany na zbiorze treningowym z wykorzystaniem
wyselekcjonowanego zbioru cech. W trakcie treningu przeanalizowano wpływ liczby
drzew decyzyjnych na jakość modelu, wykorzystując błąd out-of-bag (OOB).
Zaobserwowano, że po przekroczeniu pewnej liczby drzew dalsze zwiększanie ich
liczby nie prowadzi do istotnej poprawy jakości modelu, co pozwoliło na wybór liczby
drzew zapewniającej stabilność predykcji.


Rys. 6. Wartości błędu OOB dla różnej liczby drzew


Model Random Forest osiągnął istotnie lepsze wyniki niż algorytm OneR we
wszystkich zastosowanych miarach jakości. W szczególności uzyskano wyższy wynik
F1-score, co wskazuje na lepsze zbalansowanie pomiędzy precyzją i czułością.


Rys. 7. Ważność cech dla modelu Random Forest


Dodatkowa analiza ważności cech pozwoliła wskazać zmienne, które miały
największy wpływ na decyzje modelu, co zwiększa interpretowalność uzyskanych
wyników. Random Forest nie wykazywał problemu z nowymi, wcześniej
nieobserwowanymi wartościami cech i lepiej generalizował na zbiorze walidacyjnym
oraz predykcyjnym.


**5.** **Ewaluacja modeli**


Celem etapu ewaluacji było porównanie jakości modeli klasyfikacyjnych OneR oraz
Random Forest oraz ocena ich przydatności w zadaniu predykcji dziennego kierunku
zmiany ceny złota. Modele zostały ocenione na zbiorze walidacyjnym z
wykorzystaniem standardowych miar jakości klasyfikacji: Accuracy, Precision,
Recall oraz F1-score.


Rys. 8. Ewaluacja modeli


Model **OneR** osiągnął umiarkowaną skuteczność klasyfikacji. Accuracy na poziomie
około 0.49 wskazuje na wyniki zbliżone do losowego zgadywania, jednak pozostałe
miary sugerują, że model posiada ograniczoną zdolność rozróżniania klas. Wartość
Recall (0.67) oznacza, że algorytm stosunkowo często poprawnie identyfikował dni
wzrostowe ceny złota, jednak odbywało się to kosztem umiarkowanej precyzji
(Precision ≈ 0.51). W rezultacie miara F1-score na poziomie 0.58 potwierdza, że
model oparty na pojedynczej regule decyzyjnej nie jest w stanie w pełni uchwycić
złożonych zależności występujących w danych finansowych. OneR może być zatem
traktowany głównie jako model bazowy i punkt odniesienia dla bardziej
zaawansowanych algorytmów.


Model **Random Forest** uzyskał lepsze wyniki we wszystkich analizowanych miarach
jakości. Accuracy na poziomie około 0.51 jest nieznacznie wyższa niż w przypadku
modelu OneR, jednak istotniejsze różnice widoczne są w pozostałych metrykach.
Bardzo wysoka wartość Recall (0.91) wskazuje, że model skutecznie identyfikował
dni, w których cena złota rosła. Jednocześnie Precision na poziomie około 0.51
sugeruje umiarkowaną liczbę fałszywych alarmów, co jest typowe dla
krótkoterminowych predykcji na rynkach finansowych. Kluczową miarą pozostaje
F1-score, który osiągnął wartość około 0.66, wskazując na lepsze zbalansowanie
pomiędzy precyzją i czułością niż w przypadku modelu OneR.


Uzyskane wyniki potwierdzają przewagę algorytmu Random Forest nad prostym
modelem OneR, choć należy podkreślić, że poprawa jakości predykcji ma charakter
umiarkowany. Wskazuje to na wysoką losowość oraz trudność krótkoterminowego
przewidywania kierunku zmian cen na rynku finansowym. W tym kontekście
osiągnięte wartości miar jakości należy uznać za realistyczne i zgodne z charakterem
analizowanego problemu.


**6.** **Wnioski końcowe**


Celem niniejszego projektu była analiza możliwości predykcji dziennego kierunku
zmiany ceny złota na podstawie danych rynkowych oraz makroekonomicznych, z
wykorzystaniem algorytmów klasyfikacyjnych OneR oraz Random Forest.
Przeprowadzone eksperymenty pokazują, że zadanie to jest trudne i obarczone
wysokim poziomem niepewności, co jest charakterystyczne dla krótkoterminowych
prognoz na rynkach finansowych.


Model OneR, oparty na pojedynczej regule decyzyjnej, okazał się modelem o
ograniczonej skuteczności. Choć w niektórych przypadkach był w stanie poprawnie
identyfikować kierunek zmian ceny złota, jego uproszczona struktura nie pozwalała
na uchwycenie złożonych i nieliniowych zależności występujących w danych
finansowych. W rezultacie model ten może pełnić jedynie rolę punktu odniesienia dla
bardziej zaawansowanych algorytmów.


Zastosowanie algorytmu Random Forest pozwoliło na uzyskanie wyraźnie lepszych
wyników. Model ten, dzięki wykorzystaniu wielu drzew decyzyjnych oraz losowego
doboru cech, był w stanie skuteczniej uchwycić zależności pomiędzy zmiennymi
objaśniającymi a zmienną decyzyjną. Pomimo tego, uzyskana skuteczność predykcji
pozostaje umiarkowana, co potwierdza, że krótkoterminowy kierunek zmian cen
złota jest trudny do jednoznacznego przewidzenia nawet przy użyciu bardziej
złożonych metod.


Wyniki analizy sugerują również, że rozpatrywany zbiór danych może być lepiej
dostosowany do zadań regresyjnych, takich jak prognozowanie wielkości zmian cen
lub stóp zwrotu, zamiast binarnej klasyfikacji kierunku zmian. Informacja ilościowa
zawarta w danych rynkowych może w większym stopniu ujawniać się w modelach
regresyjnych niż w prostym podziale na klasy UP i DOWN.


Podsumowując, projekt potwierdza zasadność stosowania bardziej
zaawansowanych algorytmów, takich jak Random Forest, w analizie danych
finansowych, jednocześnie wskazując na naturalne ograniczenia predykcji
krótkoterminowej. Uzyskane rezultaty są spójne z charakterem rynków finansowych
i mogą stanowić punkt wyjścia do dalszych badań, w szczególności z
wykorzystaniem modeli regresyjnych lub metod analizy szeregów czasowych.


