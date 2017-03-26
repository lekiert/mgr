# Aplikacja e-learningowa wspomagająca naukę języków obcych

## Słowa kluczowe

elearning, rails, angular2, jsonapi

## Streszczenie

Motywacją dla powstania pracy była chęć poznania wydanej wersji frameworka Angular 2 oraz wypróbowania dedykowanych dla niego narzędzi wspomagających proces tworzenia aplikacji. W ramach projektu stworzono e-learningową, składającą się z dwóch części: klienta opartego na frameworku Angular 2 oraz serwera wykonanego przy użyciu Ruby on Rails 5. Jako bazy danych użyto PostgreSQL.

Projekt został stworzony z myślą o tym, aby służyć jako narzędzie dla szkół językowych i innych podmiotów zainteresowanych wykorzystywaniem aplikacji WWW w procesie nauczania. Każda taka jednostka będzie miała możliwość uruchomienia własnej instancji oraz wypełnienia jej treścią. Przygotowano kilka szablonów ćwiczeń, które są grupowane w zestawy testowe. Użytkownicy (uczniowie) mają przypisane do swoich kont kursy składające się takich zestawów. Wyniki rozwiązanych testów są zapamiętywane, dzięki czemu istnieje możliwość śledzenia postępów w nauce.

W części teoretycznej zostały opisane główne założenia przyjęte podczas projektowania aplikacji, wraz z analizą potrzeb użytkowników. Opisano typy kont: administratora, kierownika, nauczyciela, ucznia. Przedstawiono możliwości przypisane każdemu rodzajowi konta. W dalszej części zaprezentowano diagramy obrazujące strukturę bazy danych.

W szczegółach implementacyjnych przedstawiono architekturę i wykorzystane technologie każdej z warstw aplikacji. Opisano biblioteki i narzędzia wspomagające proces wytwarzania aplikacji, umieszczono diagramy klas. Następnie poruszono problematykę testowania aplikacji. Przedstawiono scenariusze testów funkcjonalnych oraz opisano wybrane testy jednostkowe. Uwagę poświęcono również testom manualnym. W ostatniej części podsumowano rezultaty testów.



## Spis treści

1. Wstęp
1. Projekt aplikacji i analiza potrzeb
   1. Wymagania aplikacji
   1. Użytkownicy
   1. Model danych
1. Szczegóły implementacji
   1. API
      1. Architektura
      1. Użyte biblioteki frameworka Ruby on Rails 5
      1. Diagramy klas
   1. Aplikacja kliencka
      1. Architektura
      1. Użyte biblioteki i narzędzia frameworka Angular 2
      1. Diagramy klas
1. Testy automatyczne
   1. Scenariusze
      1. Testy jednostkowe
      1. Testy funkcjonalne
      1. Testy manualne
   1. Rezultaty
1. Podsumowanie

## Bibliografia i linki

* "REST API Design Rulebook", M. Masse, wyd. O'Reilly Media.
* "TypeScript Essentials", Ch. Nance, wyd. Packt Publishing.
* "JSON API By Example", A. Builes. https://leanpub.com/json-api-by-example
* "ng-book2", N. Murray, F. Coury, A. Lerner, C. Taborda. https://www.ng-book.com/2/
* "API on Rails", Abraham Kuri Vargas, http://apionrails.icalialabs.com/
* http://jsonapi-resources.com/
