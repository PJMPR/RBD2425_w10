# 🧰 Przegląd typów baz danych NoSQL

## 📌 Wprowadzenie

Bazy NoSQL nie są jednorodną technologią – w rzeczywistości obejmują wiele modeli danych, z których każdy został zaprojektowany z myślą o określonych przypadkach użycia. Poniżej przedstawiamy przegląd głównych typów.

---

## 🧮 Bazy typu klucz-wartość

### 🔎 Opis:

Najprostszy model, w którym każdemu kluczowi odpowiada jedna wartość.

* 🔑 Klucz – unikalny identyfikator
* 📦 Wartość – dane dowolnego typu (ciąg, liczba, obiekt)

### ✅ Zastosowania:

* Bufory danych
* Sesje użytkownika
* Pamięci podręczne (cache)

### 💼 Przykłady:

* Redis
* Amazon DynamoDB

> 💡 **Wskazówka:** Świetne do odczytów o niskim opóźnieniu i dużej przepustowości.

---

## 📄 Bazy dokumentowe

### 🔎 Opis:

Dane przechowywane w postaci dokumentów, zazwyczaj w formacie JSON, BSON lub XML.

* 📁 Dokument = samodzielna jednostka danych
* 🧩 Brak sztywnego schematu danych

### ✅ Zastosowania:

* Aplikacje webowe i mobilne
* Przechowywanie konfiguracji, logów

### 💼 Przykłady:

* MongoDB
* CouchDB

> 💡 **Wskazówka:** Pozwalają na wygodne modelowanie zagnieżdżonych struktur danych.

---

## 📊 Bazy kolumnowe

### 🔎 Opis:

Zamiast wierszy, dane są przechowywane kolumnami – co pozwala na szybsze operacje analityczne na dużych zbiorach.

### ✅ Zastosowania:

* Hurtownie danych
* Systemy analityczne (OLAP)

### 💼 Przykłady:

* Apache Cassandra
* HBase

> 💡 **Wskazówka:** Bardzo dobrze skalują się poziomo i nadają się do analizy dużych danych.

---

## 🔗 Bazy grafowe

### 🔎 Opis:

Dane reprezentowane jako wierzchołki (obiekty) i krawędzie (relacje między obiektami).

* 🧠 Zoptymalizowane do analizy relacji
* 🔍 Wyszukiwanie ścieżek, połączeń, zależności

### ✅ Zastosowania:

* Sieci społecznościowe
* Systemy rekomendacji
* Analiza oszustw (fraud detection)

### 💼 Przykłady:

* Neo4j
* ArangoDB

> 💡 **Wskazówka:** Umożliwiają wykonywanie złożonych zapytań grafowych w czasie rzeczywistym.

---

## 📎 Podsumowanie

Każdy typ bazy NoSQL ma unikalne właściwości, które czynią go odpowiednim dla innych zastosowań. Wybór odpowiedniego modelu zależy od:

* rodzaju danych,
* sposobu ich przetwarzania,
* wymagań dotyczących skalowalności, spójności i dostępności.

