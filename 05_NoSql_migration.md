# 📂 Migracja z SQL do MongoDB - Przewodnik projektowania bazy dokumentowej

## 💡 Cel dokumentu

Ten dokument przedstawia zasady oraz dobre praktyki przy projektowaniu bazy danych MongoDB na podstawie relacyjnego modelu SQL. Przeznaczony jest do celów dydaktycznych dla studentów poznających różnice między podejściem relacyjnym a dokumentowym.

---

## 📅 1. Zrozumienie modelu relacyjnego

W relacyjnej bazie danych mamy następujące tabele:

* `customers` - klienci
* `addresses` - adresy klientów
* `products` - produkty
* `inventory` - stany magazynowe
* `orders` - zamówienia
* `order_items` - elementy zamówień

| Tabela        | Relacje                                |
| ------------- | -------------------------------------- |
| `addresses`   | → `customers` (1:1)                    |
| `inventory`   | → `products` (1:1)                     |
| `orders`      | → `customers` (wiele zamówień klienta) |
| `order_items` | → `orders`, `products` (wiele\:wiele)  |

> 💡 **Komentarz:**
> Struktura danych sugeruje wiele zależności 1:1 lub 1\:N, które można efektywnie zamodelować poprzez osadzenie (ang. *embedding*) w MongoDB.

---

## 🛠️ 2. Zasady konwersji do MongoDB

MongoDB nie używa tabel i relacji, ale dokumentów zapisanych w kolekcjach. Przejście z modelu relacyjnego do dokumentowego wymaga decyzji, które dane osadzić (*embed*), a które zreferencjonować (*reference*).

### ✅ **Embed** – czyli osadzanie dokumentów

To wbudowanie jednej struktury danych w inną:

```json
{
  "name": "Brian",
  "address": {
    "city": "Paris",
    "zip": "75001"
  }
}
```

* Zalety: szybki dostęp do danych, brak potrzeby dodatkowych zapytań
* Wady: trudności z aktualizacją powielonych danych

💡 **Kiedy stosować embed:**

* Gdy dane są silnie powiązane i zawsze używane razem
* Gdy dane są niewielkie i niepowtarzalne
* Gdy zależy nam na prostocie i szybkości odczytu

### 🔗 **Reference** – czyli referencje do innego dokumentu

To przechowywanie tylko identyfikatora innego dokumentu:

```json
{
  "name": "Brian",
  "address_id": ObjectId("...")
}
```

* Zalety: brak powielania danych, lepsza spójność przy aktualizacjach
* Wady: potrzeba dodatkowych zapytań (manualne JOINy)

💡 **Kiedy stosować reference:**

* Gdy dane są współdzielone między wieloma dokumentami
* Gdy dane są duże lub często aktualizowane
* Gdy nie zawsze potrzebujemy ich przy pobraniu głównego dokumentu

> 💡 **Komentarz:**\*\*
> Wybór pomiędzy osadzeniem a referencjami zależy od scenariusza odczytu, aktualizacji i rozmiaru dokumentu.

---

## 📁 3. Proponowana struktura dokumentów MongoDB

### `customers`

```json
{
  "_id": ObjectId("..."),
  "first_name": "Brian",
  "last_name": "Miller",
  "email": "brian@example.com",
  "registration_date": "2023-06-19T06:08:48Z",
  "address": {
    "street": "76950 Brenda Village",
    "city": "Patelton",
    "zip_code": "84229",
    "country": "France"
  }
}
```

> 💡 **Uwaga:**
> Adres klienta jest silnie powiązany i unikalny - idealny kandydat do osadzenia.

### `products` + `inventory`

```json
{
  "_id": ObjectId("..."),
  "name": "Wireless Mouse",
  "description": "Ergonomic wireless mouse.",
  "price": 365.90,
  "active": true,
  "inventory": {
    "quantity": 5,
    "last_updated": "2025-05-14T12:00:00Z"
  }
}
```

> 💡 **Wskazówka:**
> Łączymy produkt i magazyn, bo mają relację 1:1 i będą często odczytywane razem.

### `orders`

```json
{
  "_id": ObjectId("..."),
  "customer_id": ObjectId("..."),
  "order_date": "2025-02-28T00:09:03Z",
  "status": "delivered",
  "items": [
    { "product_id": ObjectId("..."), "quantity": 4 },
    { "product_id": ObjectId("..."), "quantity": 2 }
  ]
}
```

> 💡 **Komentarz:**
> `items` są osadzone, ponieważ nie mają znaczenia poza kontekstem zamówienia.

---

## 🔧 4. Najczęstsze problemy i dobre praktyki

| Problem                     | Rozwiązanie                                              |
| --------------------------- | -------------------------------------------------------- |
| Redundancja danych          | Embed tylko dane ściśle powiązane kontekstowo            |
| Trudności z aktualizacją    | W przypadku częstych zmian stosuj referencje             |
| Rosnące rozmiary dokumentów | Dokumenty powinny mieć rozmiar <16MB                     |
| Wydajność zapytań           | Indeksuj kluczowe pola (np. `customer_id`, `order_date`) |

> 💡 **Wskazówka:**
> MongoDB nie ma transakcji między dokumentami (chyba że użyjemy transakcji ACID w kolekcjach w jednej bazie) - warto modelować tak, by unikać ich potrzeby.

---

## 🎯 5. Wzorce modelowania danych

### One-to-One → ✅ Embed

* np. `customers` + `addresses`

### One-to-Many → ✅ Embed lub 🔗 Reference

* np. `orders` + `items` → embed
* np. `orders` + `customer` → reference

### Many-to-Many → 🔗 Reference

* np. `products` w wielu `order_items`

> 💡 **Komentarz:**
> MongoDB pozwala na elastyczne podejście: osadzamy tam, gdzie to logiczne i wydajne, referencjonujemy tam, gdzie wymagane.

---

## 📚 Podsumowanie

Projektowanie bazy MongoDB wymaga myślenia w kategoriach dokumentów i zapytań, a nie tylko struktury danych. Kluczowe pytania to:

* Czy dane są ze sobą logicznie powiązane?
* Czy będą często odczytywane razem?
* Czy dane mogą być współdzielone lub często aktualizowane?

Pamiętaj: **MongoDB to nie SQL bez JOINów** — to zupełnie inny model myślenia.

> 💡 **Zadanie dla studentów:**
> Zaproponuj alternatywny schemat dla `orders`, gdzie każdy produkt ma kopię ceny z momentu zakupu.
