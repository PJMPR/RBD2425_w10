# ⚙️ Instalacja i podstawowe operacje w MongoDB

## 📌 Wprowadzenie

Poniższy dokument przeprowadzi Cię przez proces instalacji MongoDB oraz pokaże przykładowe operacje CRUD w środowisku lokalnym.

---

## 🛠️ Instalacja MongoDB

### 🖥️ Windows

1. Pobierz instalator z [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)
2. Uruchom instalator i wybierz "Complete Installation"
3. Zaznacz opcję uruchamiania MongoDB jako serwis (rekomendowane)

### 🐧 Linux (Ubuntu)

```bash
sudo apt update
sudo apt install -y mongodb
sudo systemctl enable mongodb
sudo systemctl start mongodb
```

### 🍏 macOS (Homebrew)

```bash
brew tap mongodb/brew
brew install mongodb-community@7.0
brew services start mongodb-community@7.0
```

---

## 🚀 Uruchomienie i dostęp do bazy

Po zainstalowaniu:

* Serwer MongoDB nasłuchuje na porcie `27017`
* Możesz połączyć się przez terminal:

```bash
mongosh
```

* Lub przez GUI: **MongoDB Compass** ([pobierz tutaj](https://www.mongodb.com/try/download/compass))

---

## 🧰 Podstawowe narzędzia MongoDB

### 💻 mongosh

Nowoczesny shell do komunikacji z MongoDB, pozwala na wykonywanie zapytań i administrowanie bazą danych z poziomu terminala.

```bash
mongosh
```

### 🖼️ MongoDB Compass

GRAFICZNE narzędzie do przeglądania danych, tworzenia zapytań i analizowania indeksów. Idealne dla początkujących oraz do szybkiego prototypowania.

### ☁️ MongoDB Atlas

Chmurowa usługa MongoDB – pozwala tworzyć, zarządzać i skalować bazy danych bez konieczności lokalnej instalacji. Oferuje GUI, backupy, monitoring i dostęp do API.

> 💡 **Wskazówka:** MongoDB Atlas to świetna opcja do nauki i pracy zespołowej z bazą danych bez potrzeby konfigurowania serwera lokalnego.

### 🧩 JetBrains Rider (z DataGrip)

Rider umożliwia integrację z MongoDB poprzez wbudowane narzędzie DataGrip lub dedykowane wtyczki. Pozwala na eksplorację dokumentów, zapytań i edycję danych w przyjaznym interfejsie.

> 💡 **Wskazówka:** Przydatne dla programistów pracujących w środowiskach .NET i pełnej integracji z kodem aplikacji.

### 🐳 Obrazy Dockerowe

MongoDB jest dostępne jako oficjalny obraz Docker. Można go łatwo uruchomić bez instalacji lokalnej:

```bash
docker run -d -p 27017:27017 --name mongodb mongo
```

Dodanie wolumenów i konfiguracji:

```bash
docker run -d \
  -p 27017:27017 \
  -v ~/mongo-data:/data/db \
  --name mongodb \
  mongo
```

> 💡 **Wskazówka:** Docker to świetna opcja do testowania, szybkiego prototypowania i pracy w izolowanym środowisku.

---

## 📦 Przykładowe operacje CRUD

### 1️⃣ Insert

```js
// Create a document
use mydb;
db.users.insertOne({ name: "Alice", age: 30 });
db.users.insertMany([
  { name: "Bob", age: 25 },
  { name: "Charlie", age: 35 }
]);
```

### 2️⃣ Read

```js
// Find one document
const user = db.users.findOne({ name: "Alice" });

// Find all users older than 30
db.users.find({ age: { $gt: 30 } });
```

### 3️⃣ Update

```js
// Update one document
db.users.updateOne(
  { name: "Alice" },
  { $set: { age: 31 } }
);
```

### 4️⃣ Delete

```js
// Delete one document
db.users.deleteOne({ name: "Charlie" });
```

---

## 📎 Podsumowanie

* Instalacja MongoDB różni się w zależności od systemu operacyjnego
* Narzędzia CLI i GUI umożliwiają zarządzanie bazą
* CRUD operacje w MongoDB są proste i czytelne, nawet bez definiowania schematu
