# Wstęp

Motywacją dla powstania pracy była chęć poznania stabilnej wersji frameworka *Angular 2*, wydanej 15. września 2016 roku, oraz wypróbowania dedykowanych dla niego narzędzi wspomagających proces tworzenia aplikacji. W ramach projektu wykorzystującego tę technologię stworzono aplikację wspomagającą naukę języków obcych. 

W procesie nauki języka obcego zazwyczaj wykorzystuje się podręczniki dostosowane do konkretnej metody nauczania. W przypadku języka angielskiego można w ramach przykładu przytoczyć materiały udostępniane przez wydawnictwo *Pearson* (dawniej *Pearson Longman*), czy *Cambridge University Press*. Ich zawartość i stopień trudności różnią się w zależności od grupy docelowej, jednak ich generalną cechą jest organizacja materiału według przyjętego przez autorów programu nauczania [1]. Zazwyczaj jest to udogodnienie dla lektorów, gdyż nie muszą przygotowywać materiałów do zajęć (lub przygotowują ich mniej). Uczniowie również korzystają z tego, że przy tworzeniu takich podręczników biorą udział profesjonalni metodycy nauczania, zatem mają dostęp do pomocy dydaktycznych wysokiej jakości.

Podręczniki wydawane zarówno w formie papierowej, jak i elektronicznej, składają się z dwóch głównych części: teoretycznej, wprowadzającej osobę uczącą się w nowy materiał, oraz ćwiczeń praktycznych. Te ostatnie zawierają testy służące sprawdzeniu i utrwaleniu zdobytej wiedzy. Ich forma z reguły opiera się na sprawdzonych schematach ćwiczeń, takich jak: wypełnianie luk, parowanie fraz, testy jedno- i wielokrotnego wyboru, krzyżówki. Dodatkowo wykorzystuje się pomoce multimedialne w formie obrazków, zdjęć, nagrań audio i wideo, jak również aplikacje e-learningowe.

Aplikacje takie można podzielić na dwie zasadnicze grupy: dedykowane dla konkretnych podręczników oraz samodzielne oprogramowanie, które zazwyczaj funkcjonuje w formie serwisów webowych. Istniejącymi na rynku rozwiązaniami z tej drugiej grupy są na przykład *busuu* i *Duolingo*. Umożliwiają one rozwiązywanie ćwiczeń oraz zapoznawanie się z przygotowanymi materiałami dydaktycznymi, ponadto zawierają szereg udogodnień, takich jak: spersonalizowane testy, kontrola postępów, konwersacje z *native speakers* (zazwyczaj w formie płatnej), zgrywalizowany proces nauki. 

Warto zwrócić uwagę na fakt, że takie aplikacje i podręczniki zazwyczaj skierowane są do szerokiego grona odbiorców. W wielu przypadkach można taką cechę uznać za zaletę, jednak należy mieć na uwadze, iż istnieją również grupy wymagające materiałów do nauki o bardzo konkretnej tematyce lub sposobie przedstawiania oraz sprawdzania wiedzy. W tym przypadku często korzysta się z autorskich podręczników i programów nauczania, stworzonych pod kątem tych wymagań. Z reguły osoby tworzące takie rozwiązania nie mają środków ani umiejętności, aby stworzyć do swoich materiałów warstwę aplikacji e-learningowej, która wspomagałaby proces dydaktyczny.

## Cel pracy

Celem niniejszej pracy było stworzenie aplikacji, dzięki której podmioty zajmujące się nauczaniem języków obcych przy pomocy autorskich rozwiązań mogłyby skorzystać z możliwości e-learningu. Twórca podręcznika może tworzyć własne testy (zgrupowane w kursy) zawierające ćwiczenia oparte na przygotowanych uprzednio szablonach. Uczniowie mogą rozwiązywać testy z przypisanych im kursów oraz śledzić własne postępy. Każdy podmiot uruchamia własną instancję aplikacji, więc ma możliwość ograniczenia zależności od zewnętrznych usługodawców.

Główną częścią projektu jest aplikacja kliencka napisana we frameworku *Angular 2*. Zawiera ona interfejsy dla wszystkich przyjętych rodzajów kont (administratorów, kierowników, nauczycieli i uczniów) i zawiera większość logiki projektu. Jest skomunikowana z API zgodnym ze standardem JSON API [3]. 

Warstwą API jest aplikacja napisana we frameworku *Ruby on Rails 5*. Został on wybrany ze względu na szybkość wytwarzania gotowego produktu, ponadto posiada on rozszerzenia (*gemy*) wspierające wystawianie końcówek (*endpointów*) zgodnych ze standardem JSON API. Służy on głównie jako interfejs komunikacyjny pomiędzy aplikacją kliencką, a bazą danych, zawiera jednak w niektórych miejscach elementy logiki biznesowej, jak np. weryfikacja poprawności rozwiązań.

## Struktura pracy

W części opisującej założenia projektu przedstawiono podstawowe terminy, które zostały przyjęte w ramach konkretyzacji pojęciowej głównych elementów projektu. Następnie zostały opisane główne założenia przyjęte podczas projektowania aplikacji, wraz z analizą potrzeb użytkowników. Opisano typy kont: administratora, kierownika, nauczyciela, ucznia, wraz z wymaganiami funkcjonalnymi dla każdego rodzaju konta, podano zaimplementowane typy ćwiczeń.

W szczegółach implementacyjnych przedstawiono architekturę i wykorzystane technologie każdej z warstw aplikacji. Opisano biblioteki i narzędzia wspomagające proces wytwarzania aplikacji, umieszczono diagramy klas. Następnie poruszono problematykę testowania aplikacji. Przedstawiono scenariusze testów funkcjonalnych oraz opisano wybrane testy jednostkowe. Uwagę poświęcono również testom manualnym. W ostatniej części podsumowano rezultaty testów.

# Projekt aplikacji i analiza potrzeb

W projekcie aplikacji przedstawione są definicje terminów związanych z aplikacją, wymagania niefunkcjonalne oraz funkcjonalne. Z racji tego, że projekt przewiduje wyodrębnienie czterech typów kont użytkowników, wymagania funkcjonalne zostały pogrupowane według odpowiadających im typów kont.

## Użyte terminy

Poniżej przedstawiono terminy stosowane w aplikacji wraz z ich krótkim wyjaśnieniem:

- **Użytkownik** - konto w aplikacji o przypisanym typie.
- **Uczeń** - typ konta użytkownika końcowego. Zorientowane jest na rozwiązywanie ćwiczeń i podgląd własnych akcji oraz postępów.
- **Nauczyciel** - typ konta lektora. Służy do nadzorowania rezultatów testów rozwiązywanych przez uczniów do przypisanych mu grup.
- **Kierownik** - typ konta przewidziany do podglądu wszystkich akcji użytkowników aplikacji. Przykładem osoby z kontem kierownika jest pracownik szkoły językowej nadzorujący wywiązywanie się z obowiązków przez lektorów.
- **Administrator** - konto o najszerszych uprawnieniach. Osoby z kontem administratora odpowiedzialne są za tworzenie treści dostępnej dla pozostałych kont użytkowników: dodawanie kursów, testów, ćwiczeń, zarządzanie kontami użytkowników.
- **Grupa** - zbiór uczniów oraz przypisanych im nauczycieli oraz kursów.
- **Kurs** - zbiór testów. Organizacja testów zależy od administratora.
- **Test** - zbiór ćwiczeń, z założenia związanych tematyką i stopniem trudności.
- **Ćwiczenie** - jednostka testowa służąca do weryfikacji posiadanej wiedzy oparta o przygotowany szablon.
- **Szablon** - typ ćwiczenia. 

Szersze opisy i definicje każdego z powyższych terminów znajdują się w odpowiadających im sekcjach w niniejszym rozdziale.

## Wymagania aplikacji


### Użytkownicy aplikacji

Do korzystania z aplikacji niezbędne jest posiadanie konta. Konta są zakładane przez Administratora, w aplikacji nie ma przewidzianej możliwości samodzielnej rejestracji, jednak przy spełnieniu założenia prostego i otwartego API, taka funkcja może zostać łatwo zaimplementowana. Każde konto Użytkownika musi mieć przypisany konkretny typ determinujący zarówno stopień uprawnień do wyświetlania, tworzenia, edycji oraz usuwania poszczególnych zasobów, jak i wyświetlany po zalogowaniu interfejs. Krytycznymi dla poprawnego działania aplikacji typami kont są Administrator oraz Uczeń. Typy Nauczyciela oraz Kierownika pełnią funkcję pomocniczą. Przyczyny takiej klasyfikacji dla każdego typu są wymienione w odpowiadających im opisach w dalszej części rozdziału.

#### Wymagania funkcjonalne wspólne dla wszystkich typów kont

**Autentykacja użytkowników**

Użytkownik dokonuje logowania w aplikacji poprzez podanie loginu, będącym przypisanym do jego konta adresem e-mail, oraz hasła. Konto dla Użytkownika jest zakładane przez Administratora aplikacji. Użytkownik powinien mieć dostęp do informacji dotyczących wcześniejszych autentykacji oraz możliwość zmiany swojego hasła. Przyjęto, że wymagane hasło powinno mieć co najmniej 6 znaków.

**Dedykowany interfejs dla każdego typu konta**

Każdy typ użytkownika ma określony cel w aplikacji.


**Scenariusze**

```
Logowanie do aplikacji

Główny scenariusz:

1. Użytkownik wchodzi na stronę główną serwisu.
2. Użytkownik wpisuje e-mail oraz hasło.
3. Po poprawnej autentykacji użytkownik zostaje przekierowany na stronę statystyk lub podsumowania.

Rozszerzenia:

3. A) Użytkownik podał błędne dane logowania.
3. A.1) Zostaje wyświetlony komunikat o błędnych danych.
```

```
Wyświetlenie widoku podsumowania

Główny scenariusz:

1. Zalogowany użytkownik wchodzi na stronę podsumowania.
2. Wyświetlone zostają dane o charakterze powiązanym do typu konta Użytkownika.
3. A) Konto Ucznia zawiera wykres ostatnich rezultatów oraz listę ostatnich swoich akcji.
3. B) Konto Nauczyciela zawiera wykres ostatnich rezultatów uczniów z przypisanych mu grup oraz listę akcji tych uczniów oraz Nauczyciela.
3. C) Konto Administratora oraz Kierownika zawiera wykres ostatnich rezultatów wszystkich Uczniów oraz listę akcji wszystkich Użytkowników.
```

#### Opisy konkretnych typów kont oraz przypisanych im wymagań funkcjonalnych


##### Uczeń

Typ ucznia jest kontem użytkownika końcowego aplikacji. Jego głównym celem jest rozwiązywanie przygotowanych przez Administratora testów. Posiada ograniczone uprawnienia w zakresie dostępu do materiałów oraz możliwości ich edycji. 

**Rozwiązywanie testów z przypisanych kursów**

Ten punkt jest kluczowy dla aplikacji, gdyż ta czynność stanowi o e-learningowym charakterze aplikacji. Aby Uczeń mógł uzyskać dostęp do kursów (testów, oraz również ich podzasobów, czyli ćwiczeń), muszą mu one zostać przypisane bezpośrednio lub pośrednio. Bezpośrednim przypisaniem jest indywidualne przyznanie dostępu Uczniowi do danego kursu, a pośrednim - poprzez grupę, do której należy. Rozwiązywanie testów polega na podaniu odpowiedzi w ćwiczeniach w sposób zgodny z ich szablonami - np. w przypadku testu wielokrotnego wyboru jest to zaznaczenie odpowiedzi, luk - wpisaniu fraz w zaznaczonych miejscach. Uczeń musi mieć również możliwość sprawdzenia wyników rozwiązanego testu (w postaci punktów procentowych) oraz podglądu ewentualnych błędów przesłanych odpowiedzi.

**Przypisanie do grupy**

Grupy użytkowników z założenia odwzorowują grupy zajęciowe w szkołach językowych. Stanowią łącznik pomiędzy konkretnymi, wzajemnie przypisanymi sobie zbiorami Uczniów, Nauczycieli oraz Kursów. Dzięki organizacji uczniów w grupy 


##### Nauczyciel

- **Nauczyciel musi mieć możliwość bycia przypisanym do grupy** 
- **Nauczyciel musi mieć możliwość podglądu rezultatów sprawdzenia wysłanych odpowiedzi przez uczniów grup, do których jest przypisany**
- **Nauczyciel musi mieć możliwość podglądu własnych akcji**  
- ma możliwość podglądu rozwiązań uczniów w swoich grupach

##### Kierownik

- ma dostęp do historii akcji użytkowników

##### Administrator

Konto administratora posiada pełny dostęp do wszystkich funkcji 

### Typy ćwiczeń

#### Luki

#### Pytania wielokrotnego wyboru

#### Parowanie fraz (TODO)

#### Krzyżówki (TODO)


### Wymagania niefunkcjonalne

- **Responsywność** - aplikacja powinna być dostosowana do urządzeń mobilnych.
- **Otwarte źródło** - podmiot wykorzystujący aplikację może wykorzystać publiczne repozytoria w celu udostępnienia swoim klientom własnych instancji.
- **Otwartość na rozszerzenia** - aplikacja nie może ograniczać rozwoju projektu w zakresie tworzenia nowych funkcji i treści (np. szablonów ćwiczeń).
- **Multimedialne załączniki** - niezbędna jest możliwość dodawania do testów ćwiczeń, w których umieszczone są pliki graficzne oraz dźwiękowe.
- **Niezależność** - aplikacja powinna działać poprawnie na popularnych przeglądarkach. Przyjęto, że takimi przeglądarkami są wymienione w oficjalnej dokumentacji frameworka Angular 2 [4].

### Struktura bazy danych



# Szczegóły implementacji


# Testy
# Podsumowanie

[1] http://www.ls.uw.edu.pl/documents/7276721/13367523/6+Lingwistyka+Stosowana+14+Monika+Kusiak-Pisowacka.pdf s. 66-67
[2] http://www.ls.uw.edu.pl/documents/7276721/13367523/6+Lingwistyka+Stosowana+14+Monika+Kusiak-Pisowacka.pdf s. 68
[3] https://angular.io/docs/ts/latest/guide/browser-support.html