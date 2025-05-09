# 🍃 MongoDB jako dokumentowa baza danych

## 📌 Wprowadzenie

MongoDB to jedna z najpopularniejszych dokumentowych baz danych typu NoSQL. Została zaprojektowana z myślą o wysokiej dostępności, elastyczności danych i łatwej skalowalności.

---

## 🧾 Dokumentowy model danych

MongoDB przechowuje dane w postaci **dokumentów BSON** (Binary JSON), które przypominają strukturą obiekty JSON, ale oferują dodatkowe typy danych i lepszą wydajność.

### 📄 Przykład dokumentu (JSON):

```json
{
  "_id": "507f191e810c19729de860ea",
  "name": "Anna",
  "email": "anna@example.com",
  "address": {
    "city": "Warsaw",
    "postalCode": "00-001"
  },
  "orders": [
    {"product": "Laptop", "price": 5000},
    {"product": "Mouse", "price": 150}
  ]
}
```

> 💡 **Wskazówka:** BSON wspiera dodatkowe typy jak daty, binaria czy liczby 64-bitowe, których nie znajdziesz w zwykłym JSON.

---

## 🔍 Struktura i kolekcje

* **Baza danych (database)** – kontener na kolekcje
* **Kolekcja (collection)** – zbiór dokumentów (analogiczny do tabeli w SQL)
* **Dokument (document)** – pojedynczy rekord (jak wiersz, ale bardziej elastyczny)

### 📦 Brak schematu:

MongoDB nie wymusza jednolitego schematu dokumentów w kolekcji – każdy dokument może mieć inną strukturę.

> 💡 **Zaleta:** Można łatwo modyfikować dane bez konieczności migracji struktury bazy.

---

## 🛠️ Operacje CRUD

MongoDB udostępnia API dla klasycznych operacji CRUD:

* 🟢 **Create:** `insertOne()`, `insertMany()`
* 🟡 **Read:** `find()`, `findOne()`
* 🔵 **Update:** `updateOne()`, `updateMany()`
* 🔴 **Delete:** `deleteOne()`, `deleteMany()`

```js
// Example query
const user = db.users.findOne({ name: "Anna" });
```

---

## ⚙️ Indeksy i wydajność

MongoDB wspiera wiele typów indeksów:

* indeksy jedno- i wielopolowe,
* indeksy tekstowe,
* geolokalizacyjne,
* indeksy złożone (compound),
* indeksy TTL (czas życia dokumentów).

> 💡 **Wskazówka:** Dobrze dobrany indeks znacząco przyspiesza operacje odczytu.

---

## 📈 Skalowalność i replikacja

MongoDB wspiera poziomą skalowalność przez:

* **Sharding** – podział danych na fragmenty (shardy) według wybranego klucza
* **Replikacja** – tworzenie kopii danych na wielu serwerach (Replica Sets)

> 💡 **Wskazówka:** Replikacja zwiększa dostępność i odporność na awarie.

---

## 📎 Podsumowanie

* MongoDB przechowuje dane w elastycznym formacie BSON/JSON
* Nie wymaga sztywnego schematu
* Oferuje pełne wsparcie dla operacji CRUD i indeksowania
* Umożliwia replikację i sharding dla skalowalności
