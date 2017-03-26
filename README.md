# Aplikacja e-learningowa wspomagająca naukę języków obcych

## Słowa kluczowe

elearning, rails, angular2, jsonapi

## Streszczenie

Celem niniejszej pracy jest stworzenie aplikacji, która będzie mogła pełnić funkcję pomocniczą podczas nauczania języków obcych. Każdy zainteresowany podmiot będzie miał możliwość uruchomienia swojej instancji oraz wypełnienia jej własną treścią, dzięki czemu uczniowie będą mogli w dogodnym dla siebie miejscu i czasie rozwiązywać testy sprawdzające ich postępy, a osoby prowadzące kurs otrzymają wgląd do efektów pracy swoich podopiecznych.

W części teoretycznej zostaną opisane główne założenia przyjęte podczas projektowania aplikacji, wraz z analizą potrzeb użytkowników. Opisane będzie przyjęte podejście do rozwiązań konkretnych problemów z nimi związanych, możliwości aplikacji, takie jak: uprawnienia kont, typy ćwiczeń, metody kontroli postępów, jak również perspektywy dalszej rozbudowy o kolejne funkcje. 

Projekt został podzielony na dwie warstwy, które zostaną wykonane w dwóch różnych technologiach. Użytkownicy aplikacji będą korzystali z frontendowego klienta stworzonego we frameworku Angular 2, którzy będzie komunikował się z API obsługiwanego przez Ruby on Rails 5. Standardem przyjętym w interakcji jest specyfikacja JSON API. Wymienione technologie zostaną w niniejszej pracy opisane, przedstawione będą zalety ich wykorzystania oraz szczegóły implementacji. 

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
   1. Rezultaty
1. Podsumowanie

** TODO: rozwinac punkty **

## Bibliografia i linki

* "JSON API By Example", Adolfo Builes. https://leanpub.com/json-api-by-example
* "ng-book2", N. Murray, F. Coury, A. Lerner, C. Taborda. https://www.ng-book.com/2/
* "API on Rails", Abraham Kuri Vargas, http://apionrails.icalialabs.com/
* http://jsonapi-resources.com/
