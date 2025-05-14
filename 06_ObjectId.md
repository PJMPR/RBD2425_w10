# 🆔 ObjectId w MongoDB – co to jest i jak działa?

## 🔍 Czym jest `ObjectId`?

W MongoDB każde dodawane do kolekcji dokumenty mają unikalny identyfikator w polu `_id`. Domyślnym typem tego identyfikatora jest **`ObjectId`**, który wygląda np. tak:

```json
"_id": ObjectId("64e4b9e1f843f534a5cf8c2f")
```

## ⚙️ Jak powstaje `ObjectId`?

`ObjectId` to 12-bajtowy identyfikator binarny, który zawiera:

* 🕒 **4 bajty**: znacznik czasu (sekundy od 1.01.1970 UTC),
* 🖥️ **5 bajtów**: identyfikator hosta i procesu,
* 🔢 **3 bajty**: licznik unikalności.

Dzięki temu każdy `ObjectId` jest:

* **unikalny** — nawet w różnych instancjach bazy,
* **posortowany czasowo** — można po nim sortować dokumenty chronologicznie.

---

## ✅ Czy muszę go podawać ręcznie?

**Nie musisz.**

MongoDB **automatycznie** generuje pole `_id: ObjectId(...)` jeśli go nie podasz przy dodawaniu dokumentu:

```js
// to wystarczy:
db.users.insertOne({ name: "Anna" });
```

Jeśli podasz własne `_id`, musi on być **unikalny** w obrębie kolekcji:

```js
// możesz też podać jawnie swój identyfikator:
db.users.insertOne({ _id: "anna123", name: "Anna" });
```

---

## 📌 Kiedy warto podać `_id` samodzielnie?

* Gdy migrujesz dane z innego systemu,
* Gdy integrujesz MongoDB z aplikacją zewnętrzną,
* Gdy potrzebujesz własnego schematu identyfikatorów (np. `email`, `slug`).

> 💡 **Wskazówka:** Jeśli sam podajesz `_id`, zadbaj o jego unikalność. MongoDB nie pozwoli na dodanie dwóch dokumentów z tym samym `_id`.

---

## 🔬 Jak odczytać czas z `ObjectId`?

W shellu MongoDB możesz wydobyć czas utworzenia:

```js
ObjectId("64e4b9e1f843f534a5cf8c2f").getTimestamp()
// → ISODate("2023-08-22T14:11:13Z")
```

To przydatne np. do sortowania lub debugowania.

---

## 🧠 Podsumowanie

| Cecha              | Wartość                               |
| ------------------ | ------------------------------------- |
| Domyślny typ `_id` | `ObjectId`                            |
| Automatyczne?      | ✅ Tak, generowane przez MongoDB       |
| Unikalność         | ✅ Gwarantowana globalnie              |
| Chronologia        | ✅ Można sortować po czasie utworzenia |
| Można nadpisać?    | ✅ Tak, ale wymaga jawnego `_id`       |
