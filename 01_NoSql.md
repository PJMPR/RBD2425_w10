# 🗃️ Bazy danych NoSQL vs Relacyjne

## 📌 Wprowadzenie

W świecie baz danych istnieją dwa główne paradygmaty przechowywania i zarządzania danymi:

* **Relacyjne bazy danych (RDBMS)**
* **Bazy danych NoSQL**

Każde z tych rozwiązań ma swoje zalety, ograniczenia oraz typowe scenariusze użycia.

---

## 🧱 Relacyjne bazy danych (RDBMS)

Relacyjne bazy danych opierają się na modelu relacyjnym, zaproponowanym przez Edgara F. Codd'a w 1970 roku. Dane są przechowywane w **tabelach**, a relacje między nimi są definiowane za pomocą **kluczy głównych i obcych**.

### ✅ Cechy charakterystyczne:

* 📐 Ścisła struktura danych (schemat)
* 🔐 Spójność danych (ACID)
* 🔄 SQL jako język zapytań
* 🔗 Relacje między tabelami

  > 💡 **Ciekawostka: Co to jest ACID?**
  > ACID to zestaw właściwości zapewniających wiarygodność operacji w relacyjnych bazach danych:
  >
  > * **A** (Atomicity) – atomowość: operacje są wykonywane w całości albo wcale,
  > * **C** (Consistency) – spójność: baza przechodzi ze stanu poprawnego do kolejnego poprawnego,
  > * **I** (Isolation) – izolacja: równoległe transakcje nie wpływają na siebie,
  > * **D** (Durability) – trwałość: raz zatwierdzone zmiany są trwałe, nawet przy awarii.

### 📊 Przykład:

Tabela `Użytkownicy`:

| id | imię | email                                       |
| -- | ---- | ------------------------------------------- |
| 1  | Anna | [anna@example.com](mailto:anna@example.com) |
| 2  | Jan  | [jan@example.com](mailto:jan@example.com)   |

Tabela `Zamówienia`:

| id | id\_użytkownika | data       |
| -- | --------------- | ---------- |
| 1  | 1               | 2024-05-01 |
| 2  | 2               | 2024-05-02 |

---

## 🧬 Bazy danych NoSQL

Bazy danych NoSQL ("Not Only SQL") to grupa systemów bazodanowych zaprojektowanych z myślą o skalowalności, elastyczności i szybkości działania w przypadku nowoczesnych aplikacji.

### 🧰 Rodzaje baz NoSQL:

| Typ              | Opis                                           | Przykłady               |
| ---------------- | ---------------------------------------------- | ----------------------- |
| 🔖 Dokumentowe   | Dane przechowywane jako dokumenty (np. JSON)   | MongoDB, CouchDB        |
| 📚 Kolumnowe     | Dane w kolumnach, zoptymalizowane do analityki | Apache Cassandra, HBase |
| 🔗 Grafowe       | Dane jako wierzchołki i krawędzie (relacje)    | Neo4j, ArangoDB         |
| 🧮 Klucz-wartość | Najprostszy model: para klucz-wartość          | Redis, DynamoDB         |

### ✅ Cechy charakterystyczne:

* 🧩 Brak sztywnego schematu
* ⚡ Wysoka wydajność i skalowalność
* 📡 Często stosowane w aplikacjach webowych i big data
* 📉 Słabsze gwarancje spójności (BASE zamiast ACID)

  > 💡 **Ciekawostka: Co to jest BASE?**
  >
  > BASE to model spójności stosowany w bazach NoSQL jako alternatywa dla ACID:
  >
  > * **BA** (Basically Available) – system zawsze odpowiada, nawet jeśli dane są częściowo niedostępne,
  > * **S** (Soft state) – stan systemu może się zmieniać w czasie (nawet bez nowych danych),
  > * **E** (Eventually consistent) – dane osiągną spójność po pewnym czasie, nie natychmiast.
  >
  > Ten model pozwala na wyższą dostępność i lepszą skalowalność kosztem natychmiastowej spójności.

---

## ⚖️ Porównanie RDBMS vs NoSQL

| Cecha             | RDBMS              | NoSQL                           |
| ----------------- | ------------------ | ------------------------------- |
| 📐 Schemat danych | Ścisły             | Elastyczny                      |
| 🔗 Relacje        | Obsługiwane        | Ograniczone lub brak            |
| 🔐 Spójność       | ACID               | BASE                            |
| ⚡ Skalowalność    | Pionowa (scale-up) | Pozioma (scale-out)             |
| 💬 Język zapytań  | SQL                | Różne, często zapytania natywne |
| 📊 Typowe użycie  | Finanse, ERP, CRM  | Social media, IoT, Big Data     |

📊 Skalowanie

| Cecha                | Skalowanie pionowe       | Skalowanie poziome        |
| -------------------- | ------------------------ | ------------------------- |
| Sposób działania     | Zwiększanie mocy serwera | Dodawanie nowych serwerów |
| Koszt początkowy     | Niższy                   | Wyższy                    |
| Skalowalność         | Ograniczona              | Bardzo dobra              |
| Złożoność techniczna | Niska                    | Wysoka                    |
| Ryzyko awarii        | Wyższe                   | Niższe (rozproszenie)     |

---

## 🧠 Kiedy wybrać które rozwiązanie?

| Scenariusz                             | Lepszy wybór |
| -------------------------------------- | ------------ |
| Aplikacje transakcyjne                 | RDBMS        |
| Duże zbiory niestrukturalnych danych   | NoSQL        |
| Analiza relacji między danymi          | NoSQL (graf) |
| Raportowanie i analizy finansowe       | RDBMS        |
| Aplikacje webowe o zmiennej strukturze | NoSQL        |

---

## 📎 Podsumowanie

* RDBMS to sprawdzony wybór dla systemów wymagających silnej spójności danych.
* NoSQL oferuje większą elastyczność i skalowalność, co czyni go idealnym dla nowoczesnych aplikacji i dużych zbiorów danych.
* Wybór technologii zależy od konkretnych wymagań projektu – często stosuje się podejście hybrydowe.

---
