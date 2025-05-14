# 🧾 Definiowanie schematu dokumentu w MongoDB

## 📌 Co to jest walidacja schematu?

MongoDB pozwala na definiowanie schematu dokumentu dla kolekcji przy użyciu składni `$jsonSchema`. Dzięki temu można określić:

* które pola są wymagane,
* jakie typy danych są akceptowane,
* ograniczenia takie jak długość, zakres, wzorzec (np. email).

---

## 🛠️ Tworzenie kolekcji ze schematem

```js
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "email"],
      properties: {
        name: {
          bsonType: "string",
          description: "Imię użytkownika (wymagane)"
        },
        email: {
          bsonType: "string",
          pattern: "^.+@.+$",
          description: "Adres email (wymagany, poprawny format)"
        },
        age: {
          bsonType: "int",
          minimum: 0,
          maximum: 120,
          description: "Wiek (opcjonalny, liczba całkowita)"
        }
      }
    }
  },
  validationAction: "error" // lub "warn"
})
```

---

## 🔎 `required`: Pola wymagane

```json
"required": ["name", "email"]
```

Pola wymienione w tej tablicy **muszą** być obecne w każdym dokumencie.

---

## 🔐 `bsonType`: Typ danych

Możliwe wartości:

* `string`, `int`, `bool`, `date`, `array`, `object`, `null`, itp.

```json
"bsonType": "string"
```

---

## 🎯 Walidacja typu i zakresu

Można dodać dodatkowe ograniczenia:

```json
"age": {
  "bsonType": "int",
  "minimum": 0,
  "maximum": 120
}
```

---

## 🧪 `validationAction`: Co się dzieje przy błędzie?

| Wartość               | Efekt                                                 |
| --------------------- | ----------------------------------------------------- |
| `"error"` (domyślnie) | Odrzuca dokument niezgodny ze schematem               |
| `"warn"`              | Akceptuje dokument, ale zapisuje ostrzeżenie w logach |

---

## 📅 Jak sprawdzić schemat kolekcji?

```js
db.getCollectionInfos({ name: "users" })
```

Lub przez MongoDB Compass: zakładka **Validation** w szczegółach kolekcji.

---

## 📚 Praktyczne zastosowania

* Zapewnienie spójności danych (np. `email`, `wiek`),
* Walidacja danych wejściowych aplikacji,
* Wymuszanie obowiązkowych pól (np. `createdAt`, `status`).

> 💡 **Wskazówka:** Używaj schematów walidacji szczególnie w projektach zespołowych lub zewnętrznych API, gdzie kontrola nad strukturą danych jest kluczowa.
