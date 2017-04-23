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

#### Uczeń

Typ ucznia jest kontem użytkownika końcowego aplikacji. Posiada ograniczone uprawnienia, a interfejs wyświetla dane związane z indywidualnymi akcjami i postępami.

- **Uczeń musi mieć możliwość bycia przypisanym do grupy** 
- **Uczeń musi mieć możliwość posiadania przypisanych kursów** 
- **Uczeń musi mieć możliwość rozwiązywania testów w kursach** 
- **Uczeń musi mieć możliwość podglądu własnych akcji**
- **Uczeń musi mieć możliwość podglądu rezultatów sprawdzenia wysłanych odpowiedzi** 

#### Nauczyciel

- **Nauczyciel musi mieć możliwość bycia przypisanym do grupy** 
- **Nauczyciel musi mieć możliwość podglądu rezultatów sprawdzenia wysłanych odpowiedzi przez uczniów grup, do których jest przypisany**
- **Nauczyciel musi mieć możliwość podglądu własnych akcji**  
- ma możliwość podglądu rozwiązań uczniów w swoich grupach

#### Kierownik

- ma dostęp do historii akcji użytkowników

#### Administrator

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