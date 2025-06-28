# Flask + MongoDB Atlas CRUD API

A minimal **RESTful API** built with **Flask 3** and **PyMongo 4** that shows how to create, read, update and delete (CRUD) documents in a **MongoDB Atlas** cluster.

---

## ✨ Features

- Python 3.10+ & Flask 3.x
- MongoDB Atlas (free M0 cluster)
- Environment‑variable–based configuration (`python‑dotenv`)
- Simple JSON endpoints — perfect for Postman / cURL testing

---

## 🚀 Quick Start

```bash
# 1️⃣ Clone this repo
$ git clone https://github.com/your‑user/flask-mongo-crud.git
$ cd flask-mongo-crud

# 2️⃣ Create virtual environment
$ python -m venv venv
$ source venv/bin/activate      # Windows: venv\Scripts\activate

# 3️⃣ Install dependencies
$ pip install -r requirements.txt

# 4️⃣ Create the .env file (see next section)

# 5️⃣ Run the server
$ flask run
# http://127.0.0.1:5000/ should show "MongoDB Flask CRUD API is running!"
```

---

## 🛠️ Setting up MongoDB Atlas

1. **Sign in / Create** a free Atlas account at <https://cloud.mongodb.com>.
2. Click **Create** ➜ choose the **M0 Free Tier** cluster.
3. **Select Region** (e.g. AWS / ap‑southeast‑1 → Singapore).
4. In **Database Access** ➜ Add a **database user** (example: `admin` / `strongpassword`).
5. In **Network Access** ➜ Add IP Address `0.0.0.0/0` *(development only)* so your laptop can connect.
6. Once the cluster is built, click **Connect → Drivers → Python**.
7. Copy the **connection string** beginning with `mongodb+srv://…`.
8. **Create a database & collection**:
   - Click **Browse Collections**.
   - Click **Add My Own Data** ➜ Database **`flaskdb`**, Collection **`users`** ➜ *Insert one dummy doc or leave empty*.

> **⚠️ Keep your connection string secret!** It contains your username & password.

---

## 🔑 `.env` file

Create a new `.env` in the project root (**never commit this file!**):

```env
FLASK_ENV=development
FLASK_APP=app.py
MONGO_URI=mongodb+srv://admin:<password>@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority
```

- Replace `<password>` with the real password you set in Atlas.
- Feel free to append `&appName=FlaskMongoCRUD` (optional).

The app uses `client["flaskdb"]` and the `users` collection by default—edit `app.py` if you wish to change these.

---

## 📡 API Endpoints

| Method | Endpoint             | Description              |
|--------|----------------------|--------------------------|
| GET    | `/`                  | Health‑check text        |
| POST   | `/users`             | **Create** a user        |
| GET    | `/users`             | **Read** all users       |
| GET    | `/users/<id>`        | **Read** one user        |
| PUT    | `/users/<id>`        | **Update** a user        |
| DELETE | `/users/<id>`        | **Delete** a user        |

### Example JSON

```json
{
  "name": "Alice",
  "email": "alice@example.com"
}
```

### Testing with Postman

1. **Import** a new request ➜ Method **POST** ➜ URL `http://127.0.0.1:5000/users`.
2. Select Body ➜ **raw** ➜ **JSON** and paste the example JSON above.
3. Click **Send** ➜ Should return `{"_id": "<generated ObjectId>"}` with status `201`.
4. **GET** `http://127.0.0.1:5000/users` ➜ Should list documents.
5. Copy an `_id` and test **PUT** / **DELETE** routes as needed.

> Postman tip: save the _id in an environment variable (`{{userId}}`) for quick chained requests.

---

## 🏗 Project Structure

```
flask-mongo-crud/
├── app.py              # Flask application
├── requirements.txt    # Python dependencies
├── .gitignore          # ignores .env & __pycache__
└── README.md           # (this file)
```

---

## 📦 Deployment

You can deploy to **Render**, **Railway**, **Fly.io**, or any platform that supports Python:

1. Set environment variables (`MONGO_URI`, `FLASK_ENV=production`).
2. Use `gunicorn` in a `Procfile` e.g. `web: gunicorn -b 0.0.0.0:$PORT app:app`.

---

## ⚖️ License

MIT © 2025 Chacharin Lertyosbordin
