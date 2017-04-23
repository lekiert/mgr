# Aplikacja e-learningowa wspomagająca naukę języków obcych

## Słowa kluczowe

e-learning, Ruby on Rails wersja 5, Angular wersja 2, JSON API, REST, TypeScript

## Streszczenie

W ramach projektu stworzono aplikację e-learningową, składającą się z dwóch części: klienta opartego na frameworku Angular 2 oraz serwera wykonanego przy użyciu Ruby on Rails 5. Jako bazy danych użyto PostgreSQL.

Projekt został stworzony z myślą o tym, aby służyć jako narzędzie dla szkół językowych i innych podmiotów zainteresowanych wykorzystywaniem aplikacji WWW w procesie nauczania. Każda taka jednostka będzie miała możliwość uruchomienia własnej instancji oraz wypełnienia jej treścią. Przygotowano kilka szablonów ćwiczeń, które są grupowane w zestawy testowe. Użytkownicy (uczniowie) mają przypisane do swoich kont kursy składające się takich zestawów. Wyniki rozwiązanych testów są zapamiętywane, dzięki czemu istnieje możliwość śledzenia postępów w nauce.

W części teoretycznej zostały opisane główne założenia przyjęte podczas projektowania aplikacji, wraz z analizą potrzeb użytkowników. Opisano typy kont: administratora, kierownika, nauczyciela, ucznia. Przedstawiono możliwości przypisane każdemu rodzajowi konta. W dalszej części zaprezentowano diagramy obrazujące strukturę bazy danych.

W szczegółach implementacyjnych przedstawiono architekturę i wykorzystane technologie każdej z warstw aplikacji. Opisano biblioteki i narzędzia wspomagające proces wytwarzania aplikacji, umieszczono diagramy klas. Następnie poruszono problematykę testowania aplikacji. Przedstawiono scenariusze testów funkcjonalnych oraz opisano wybrane testy jednostkowe. Uwagę poświęcono również testom manualnym. W ostatniej części podsumowano rezultaty testów.


## Spis treści

1. Wstęp
    1. Cel pracy
    1. Struktura pracy
1. Projekt aplikacji i analiza potrzeb
   1. Użyte terminy
   1. Wymagania aplikacji
   1. Użytkownicy
      1. Uczeń
      1. Nauczyciel
      1. Kierownik
      1. Administrator
   1. Struktura bazy danych
1. Szczegóły implementacji
   1. API
      1. Architektura
      1. Użyte biblioteki frameworka Ruby on Rails 5
      1. Diagramy klas
   1. Aplikacja kliencka
      1. Architektura
      1. Użyte biblioteki i narzędzia frameworka Angular 2
      1. Diagramy klas
1. Testy
   1. Scenariusze
      1. Testy jednostkowe
      1. Testy funkcjonalne
      1. Testy manualne
   1. Rezultaty
1. Podsumowanie

## Bibliografia i linki

* M. Masse, „REST API Design Rulebook”, wyd. O'Reilly Media.
* Ch. Nance, „TypeScript Essentials”, wyd. Packt Publishing.
* A. Builes. „JSON API By Example”, https://leanpub.com/json-api-by-example
* N. Murray, F. Coury, A. Lerner, C. Taborda, „ng-book2”, https://www.ng-book.com/2/
* Abraham Kuri Vargas, „API on Rails”, http://apionrails.icalialabs.com/
* http://jsonapi-resources.com/
* http://www.ls.uw.edu.pl/documents/7276721/13367523/6+Lingwistyka+Stosowana+14+Monika+Kusiak-Pisowacka.pdf
* https://angular.io/docs/ts/latest/guide/browser-support.html
