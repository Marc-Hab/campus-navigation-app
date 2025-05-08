# 🧭 Concordia Campus Guide – Backend API

**This repository showcases my work as the backend developer for the Concordia Campus Guide project.**

The project aims to assist Concordia students, faculty, and visitors in navigating campus locations, and this repository specifically focuses on the backend architecture, API endpoints, and database management.

---

## 📌 Overview

This project provides a RESTful API backend for navigating indoor spaces at Concordia University. The system allows users to retrieve campus data, search for rooms and buildings, and compute shortest or accessible paths between points — similar to Google Maps but tailored to indoor campus spaces.

---

## 🔧 What This Project Is

A Django/PostgreSQL backend for a mobile campus navigation app. Inspired by Google Maps, this system enables users to:

* Search for buildings, rooms, and facilities
* Calculate shortest paths between two points on campus
* Locate the nearest amenity (e.g. bathroom, elevator)
* Request accessible routes (for mobility support)

The backend exposes a fully-documented REST API and handles all navigation logic, data modeling, and dynamic pathfinding.

---

## 🛠️ Tech Stack

| Layer     | Tech                             |
| --------- | -------------------------------- |
| Backend   | Django, Django REST Framework    |
| Database  | PostgreSQL                       |
| Dev Tools | Postman, cURL, Docker            |
| Language  | Python                           |

---

## 🔍 Features

### 📊 Data Model

Hierarchical structure:

```
Campus → Buildings → Floors → Rooms → POIs
```

Here’s a high-level ERD of the data model: [`ERD diagram`](./backend/assets/ERD.png)



> 🛠️ Data is stored in CSV files (`floor.csv`, `room.csv`, `poi.csv`) and imported into the database via:

```bash
python manage.py initialize
```

---

### 🧠 Pathfinding

Supports:

* Room-to-room navigation (e.g. H-521 → H-631)
* Finding nearest POI (e.g. closest bathroom or elevator)
* Accessible routing (avoids stairs)

Paths are computed **dynamically** using graph traversal algorithms at request time.

---

### 🔐 API Design

* Clean REST structure (GET, POST, etc.)
* Intuitive endpoint naming
* Consistent JSON responses and error handling

See [`API_DOCUMENTATION.md`](./api/api-documentation.md) for full endpoint details.

---

## 🗃️ Folder Structure

```
campus-navigation-app/
├── backend/              # Django project settings
│   ├── settings.py
│
├── app/                  # Main app: views, models, serializers, urls
│   ├── csv/              # Initialization scripts for database
│   ├── management/       # Custom Django commands
│   ├── migrations/       # Django migrations
│   ├── tests/            # App-specific unit tests
│   ├── views/            # Route definitions
│   ├── models.py
│   ├── serializers.py
│   └── urls.py
│
├── api/ 
│   ├── API_DOCUMENTATION.md  # Full endpoint reference
│
├── manage.py
├── requirements.txt

```
---

## 🚀 Running Locally

### Prerequisites

* Python 3.9+
* PostgreSQL
* [Docker](https://docs.docker.com/get-docker/)

#### **Setup**

```bash
git clone https://github.com/Marc-Hab/campus-navigation-app.git
cd campus-navigation-app
docker-compose up --build
```

#### 🛠️ Apply Migrations & Initialize Data

In a new terminal:

```bash
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py initialize
```

This will:

* Build the Docker image
* Run the Django server inside the container
* Expose the API on [http://localhost:8000/api/](http://localhost:8000/api/)

---

## 🧪 Try It

### Example Requests

```bash
# Get all buildings
curl http://localhost:8000/api/building/all

# Shortest path between two rooms
curl -X POST http://localhost:8000/api/path/rooms \
     -H "Content-Type: application/json" \
     -d '{"room1": "H-521", "room2": "H-631"}'
```

### Postman

Import the included [Postman collection](./postman_collection.json) to explore the API interactively.

---

## ✅ Tests

Run backend tests with:

```bash
docker-compose exec web pytest
```

*(More test coverage can be added for path logic and error cases.)*

---

## 📌 Limitations

* Some advanced features (e.g. cross-building paths) are not implemented.

---
## 🙋‍♂️ About This Repo

This repository focuses exclusively on the **backend**, which was my core responsibility. The frontend was handled by teammates and is not included in this repository.

---

## 📃 License

This project is licensed under the MIT License.
See [`LICENSE`](./LICENSE) for details.

