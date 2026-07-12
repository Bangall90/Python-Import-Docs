# 📦 Python Import Docs

Kumpulan dokumentasi *import* Python yang sering dipakai, mencakup **standard library** dan **library populer pihak ketiga**. Setiap entri berisi penjelasan singkat fungsi modul dan contoh kode yang bisa langsung dicoba.

## Daftar Isi

- [1. Standard Library](#1-standard-library)
  - [1.1 File & Direktori](#11-file--direktori)
  - [1.2 Serialisasi Data](#12-serialisasi-data)
  - [1.3 Tanggal & Waktu](#13-tanggal--waktu)
  - [1.4 Matematika & Angka Acak](#14-matematika--angka-acak)
  - [1.5 Teks & Regex](#15-teks--regex)
  - [1.6 Struktur Data & Fungsional](#16-struktur-data--fungsional)
  - [1.7 Sistem & Proses](#17-sistem--proses)
  - [1.8 Jaringan](#18-jaringan)
  - [1.9 Konkurensi](#19-konkurensi)
  - [1.10 Logging & Debugging](#110-logging--debugging)
  - [1.11 Lain-lain yang Berguna](#111-lain-lain-yang-berguna)
  - [1.12 Database](#112-database)
- [2. Library Populer (Pihak Ketiga)](#2-library-populer-pihak-ketiga)
  - [2.1 Data Science](#21-data-science)
  - [2.2 Web Development](#22-web-development)
  - [2.3 Web Scraping & HTTP](#23-web-scraping--http)
  - [2.4 Database & ORM](#24-database--orm)
  - [2.5 Testing](#25-testing)
  - [2.6 Utilitas & Validasi](#26-utilitas--validasi)
  - [2.7 Machine Learning](#27-machine-learning)
  - [2.8 Image Processing](#28-image-processing)
  - [2.9 Data App & Dashboard](#29-data-app--dashboard)
  - [2.10 Excel / Spreadsheet](#210-excel--spreadsheet)

---

## 1. Standard Library

### 1.1 File & Direktori

#### `os`
Interaksi dengan sistem operasi: variabel lingkungan, path, direktori, proses.

```python
import os

os.mkdir("data")                      # buat folder
print(os.getcwd())                    # direktori kerja saat ini
print(os.listdir("."))                # daftar isi direktori
print(os.environ.get("HOME"))         # baca environment variable
```

#### `pathlib`
Cara modern berorientasi objek untuk memanipulasi path file, alternatif `os.path`.

```python
from pathlib import Path

p = Path("data") / "file.txt"
p.parent.mkdir(exist_ok=True)
p.write_text("halo dunia")
print(p.exists(), p.suffix, p.stem)
```

#### `shutil`
Operasi file tingkat tinggi: copy, move, hapus folder, kompres.

```python
import shutil

shutil.copy("source.txt", "backup.txt")
shutil.move("backup.txt", "archive/backup.txt")
shutil.make_archive("output", "zip", "data")
```

#### `glob`
Mencari file berdasarkan pola wildcard.

```python
import glob

for file in glob.glob("*.py"):
    print(file)
```

### 1.2 Serialisasi Data

#### `json`
Membaca dan menulis data format JSON.

```python
import json

data = {"nama": "Budi", "umur": 25}
json_str = json.dumps(data, indent=2)   # dict -> json string
parsed = json.loads(json_str)           # json string -> dict

with open("data.json", "w") as f:
    json.dump(data, f)
```

#### `csv`
Membaca dan menulis file CSV.

```python
import csv

with open("data.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["nama", "umur"])
    writer.writerow(["Budi", 25])

with open("data.csv") as f:
    for row in csv.reader(f):
        print(row)
```

#### `pickle`
Serialisasi objek Python ke bentuk biner (khusus antar-Python, bukan lintas bahasa).

```python
import pickle

data = {"a": 1, "b": [1, 2, 3]}
with open("data.pkl", "wb") as f:
    pickle.dump(data, f)

with open("data.pkl", "rb") as f:
    loaded = pickle.load(f)
```

### 1.3 Tanggal & Waktu

#### `datetime`
Manipulasi tanggal, waktu, dan durasi (timedelta).

```python
from datetime import datetime, timedelta

now = datetime.now()
besok = now + timedelta(days=1)
print(now.strftime("%d-%m-%Y %H:%M:%S"))
```

#### `time`
Fungsi terkait waktu tingkat rendah, termasuk delay eksekusi.

```python
import time

start = time.time()
time.sleep(1)          # jeda 1 detik
print("Durasi:", time.time() - start)
```

### 1.4 Matematika & Angka Acak

#### `math`
Fungsi matematika dasar: akar, trigonometri, logaritma, konstanta.

```python
import math

print(math.sqrt(16))     # 4.0
print(math.pi)            # 3.14159...
print(math.factorial(5))  # 120
```

#### `random`
Menghasilkan angka/pilihan acak.

```python
import random

print(random.randint(1, 10))          # angka acak 1-10
print(random.choice(["a", "b", "c"])) # pilih 1 elemen acak
lst = [1, 2, 3, 4]
random.shuffle(lst)                   # acak urutan list
```

#### `statistics`
Perhitungan statistik dasar seperti mean, median, standar deviasi.

```python
import statistics

data = [1, 2, 3, 4, 5]
print(statistics.mean(data))    # 3
print(statistics.stdev(data))   # 1.58...
```

### 1.5 Teks & Regex

#### `re`
Regular expression untuk pencarian dan manipulasi pola teks.

```python
import re

text = "Kontak: budi@email.com"
match = re.search(r"[\w.]+@[\w.]+", text)
if match:
    print(match.group())   # budi@email.com

# ganti semua angka dengan '#'
print(re.sub(r"\d", "#", "Order 12345"))
```

#### `string`
Konstanta dan utilitas terkait string (huruf, angka, tanda baca).

```python
import string

print(string.ascii_lowercase)  # abcdefghijklmnopqrstuvwxyz
print(string.digits)           # 0123456789
```

### 1.6 Struktur Data & Fungsional

#### `collections`
Struktur data tambahan: `Counter`, `defaultdict`, `namedtuple`, `deque`.

```python
from collections import Counter, defaultdict, namedtuple

# hitung frekuensi elemen
print(Counter(["a", "b", "a", "c", "a"]))  # Counter({'a': 3, 'b': 1, 'c': 1})

# dict dengan nilai default otomatis
dd = defaultdict(list)
dd["buah"].append("apel")

# tuple dengan nama field
Point = namedtuple("Point", ["x", "y"])
p = Point(1, 2)
```

#### `itertools`
Fungsi untuk membuat iterator efisien (kombinasi, permutasi, perulangan tak hingga).

```python
import itertools

print(list(itertools.combinations([1, 2, 3], 2)))  # [(1,2),(1,3),(2,3)]
print(list(itertools.permutations([1, 2], 2)))      # [(1,2),(2,1)]

for i in itertools.count(start=1):
    if i > 3:
        break
    print(i)
```

#### `functools`
Alat pemrograman fungsional: caching, decorator, reduce.

```python
from functools import lru_cache, reduce

@lru_cache(maxsize=None)
def fib(n):
    return n if n < 2 else fib(n - 1) + fib(n - 2)

total = reduce(lambda a, b: a + b, [1, 2, 3, 4])  # 10
```

### 1.7 Sistem & Proses

#### `sys`
Interaksi dengan interpreter Python: argumen CLI, path, exit.

```python
import sys

print(sys.argv)          # daftar argumen command line
print(sys.version)       # versi Python
sys.exit(0)               # keluar dari program
```

#### `subprocess`
Menjalankan perintah/program eksternal dari dalam Python.

```python
import subprocess

result = subprocess.run(["echo", "halo"], capture_output=True, text=True)
print(result.stdout)
```

#### `argparse`
Membuat antarmuka command-line dengan parsing argumen otomatis.

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--nama", required=True)
args = parser.parse_args()
print(f"Halo, {args.nama}")
```

### 1.8 Jaringan

#### `urllib`
Modul bawaan untuk membuka URL dan melakukan request HTTP dasar.

```python
from urllib.request import urlopen

with urlopen("https://example.com") as response:
    html = response.read().decode()
```

#### `socket`
Komunikasi jaringan tingkat rendah (TCP/UDP).

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("example.com", 80))
s.close()
```

### 1.9 Konkurensi

#### `threading`
Menjalankan beberapa thread untuk tugas I/O-bound secara paralel.

```python
import threading

def tugas():
    print("berjalan di thread lain")

t = threading.Thread(target=tugas)
t.start()
t.join()
```

#### `multiprocessing`
Menjalankan proses paralel untuk tugas CPU-bound (memanfaatkan banyak core).

```python
from multiprocessing import Process

def kerja():
    print("proses terpisah")

p = Process(target=kerja)
p.start()
p.join()
```

#### `asyncio`
Pemrograman asinkron menggunakan `async`/`await` untuk I/O non-blocking.

```python
import asyncio

async def main():
    print("mulai")
    await asyncio.sleep(1)
    print("selesai")

asyncio.run(main())
```

### 1.10 Logging & Debugging

#### `logging`
Framework standar untuk mencatat log aplikasi (lebih baik daripada `print`).

```python
import logging

logging.basicConfig(level=logging.INFO)
logging.info("Aplikasi dimulai")
logging.warning("Ini peringatan")
logging.error("Terjadi kesalahan")
```

#### `traceback`
Menampilkan/mengolah informasi error (stack trace) secara terprogram.

```python
import traceback

try:
    1 / 0
except ZeroDivisionError:
    traceback.print_exc()
```

### 1.11 Lain-lain yang Berguna

#### `typing`
Anotasi tipe untuk kode yang lebih jelas dan bisa dicek statis (mis. dengan mypy).

```python
from typing import List, Dict, Optional

def cari(nama: str, data: List[Dict[str, str]]) -> Optional[str]:
    for item in data:
        if item.get("nama") == nama:
            return item["nama"]
    return None
```

#### `dataclasses`
Membuat class untuk menyimpan data dengan boilerplate minimal.

```python
from dataclasses import dataclass

@dataclass
class Produk:
    nama: str
    harga: float
    stok: int = 0

p = Produk("Buku", 50000)
print(p)   # Produk(nama='Buku', harga=50000, stok=0)
```

#### `enum`
Membuat konstanta bernama (enumerasi) yang aman secara tipe.

```python
from enum import Enum

class Status(Enum):
    AKTIF = 1
    NONAKTIF = 2

print(Status.AKTIF)        # Status.AKTIF
print(Status.AKTIF.value)  # 1
```

#### `copy`
Menyalin objek secara shallow atau deep copy.

```python
import copy

original = {"list": [1, 2, 3]}
salinan = copy.deepcopy(original)
salinan["list"].append(4)
print(original["list"])   # tidak berubah: [1, 2, 3]
```

---

### 1.12 DataBase

#### `sqlite3`
Database ringan berbasis file, bawaan Python (standard library) — tidak perlu install server terpisah.

```python
import sqlite3

# 1. KONEKSI — membuka (atau membuat baru) file database
conn = sqlite3.connect("data.db")
cursor = conn.cursor()

# 2. MENU UTAMA — operasi dasar ke database (CRUD)

# Membuat tabel
cursor.execute("""
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY,
        nama TEXT,
        umur INTEGER
    )
""")

# Menambah data (Create)
cursor.execute("INSERT INTO users (nama, umur) VALUES (?, ?)", ("Budi", 25))
cursor.execute("INSERT INTO users (nama, umur) VALUES (?, ?)", ("Ani", 30))

# Membaca data (Read)
cursor.execute("SELECT * FROM users")
print(cursor.fetchall())

# Mengubah data (Update)
cursor.execute("UPDATE users SET umur = ? WHERE nama = ?", (26, "Budi"))

# Menghapus data (Delete)
cursor.execute("DELETE FROM users WHERE nama = ?", ("Ani",))

# 3. SIMPAN — commit() wajib dipanggil supaya perubahan benar-benar tersimpan ke file
conn.commit()

# Tutup koneksi setelah selesai
conn.close()
```

**Keterangan bagian:**
- **Koneksi:** `sqlite3.connect("data.db")` — membuka file database, otomatis dibuat kalau belum ada.
- **Simpan:** `conn.commit()` — tanpa ini, semua INSERT/UPDATE/DELETE tidak akan tersimpan permanen ke file.
- **Menu utama:** `cursor.execute(...)` — tempat semua perintah SQL (CREATE, INSERT, SELECT, UPDATE, DELETE) dijalankan.

## 2. Library Populer (Pihak Ketiga)

> Perlu instalasi lewat `pip install <nama_library>` sebelum digunakan.

### 2.1 Data Science

#### `numpy`
Komputasi numerik dengan array multidimensi yang efisien.

**Install:** `pip install numpy`

```python
import numpy as np

arr = np.array([1, 2, 3, 4])
print(arr.mean())          # 2.5
print(arr * 2)              # [2 4 6 8]
matrix = np.zeros((2, 3))   # matriks 2x3 berisi nol
```

#### `pandas`
Analisis dan manipulasi data tabular (DataFrame), mirip spreadsheet.

**Install:** `pip install pandas`

```python
import pandas as pd

df = pd.DataFrame({"nama": ["Ani", "Budi"], "umur": [25, 30]})
print(df.head())
print(df[df["umur"] > 26])          # filter baris
df.to_csv("output.csv", index=False)
```

#### `matplotlib`
Membuat grafik dan visualisasi data.

**Install:** `pip install matplotlib`

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3], [4, 5, 6])
plt.xlabel("X")
plt.ylabel("Y")
plt.savefig("grafik.png")
```

### 2.2 Web Development

#### `flask`
Micro web framework untuk membuat API atau aplikasi web sederhana.

**Install:** `pip install flask`

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/")
def home():
    return jsonify({"pesan": "Halo dari Flask"})

if __name__ == "__main__":
    app.run(debug=True)
```

#### `django`
Framework web full-stack "batteries-included": ORM, admin panel, auth, routing — semua sudah tersedia.
 
**Install:** `pip install django`
 
```python
# models.py — mendefinisikan tabel database sebagai class Python
from django.db import models
 
class Produk(models.Model):
    nama = models.CharField(max_length=100)
    harga = models.DecimalField(max_digits=10, decimal_places=2)
    stok = models.IntegerField(default=0)
 
    def __str__(self):
        return self.nama
 
# views.py — menangani request dan mengembalikan response
from django.http import JsonResponse
 
def daftar_produk(request):
    return JsonResponse({"pesan": "Halo dari Django"})
 
# Setup project baru:   django-admin startproject myproject
# Jalankan server:       python manage.py runserver
```

#### `fastapi`
Framework web modern berbasis type hints, cepat, dan otomatis membuat dokumentasi API.

**Install:** `pip install fastapi uvicorn`

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/produk/{item_id}")
def baca_produk(item_id: int):
    return {"item_id": item_id}

# jalankan dengan: uvicorn nama_file:app --reload
```

### 2.3 Web Scraping & HTTP

#### `requests`
Library HTTP yang sederhana untuk memanggil API atau mengambil halaman web.

**Install:** `pip install requests`

```python
import requests

response = requests.get("https://api.github.com")
print(response.status_code)
print(response.json())
```

#### `beautifulsoup4` (`bs4`)
Parsing dan ekstraksi data dari HTML/XML.

**Install:** `pip install beautifulsoup4`

```python
from bs4 import BeautifulSoup
import requests

html = requests.get("https://example.com").text
soup = BeautifulSoup(html, "html.parser")
print(soup.title.text)
print([a["href"] for a in soup.find_all("a")])
```

### 2.4 Database & ORM

#### `sqlalchemy`
ORM (Object-Relational Mapping) untuk berinteraksi dengan database SQL memakai objek Python.

**Install:** `pip install sqlalchemy`

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.orm import declarative_base, Session

Base = declarative_base()

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    nama = Column(String)

engine = create_engine("sqlite:///app.db")
Base.metadata.create_all(engine)

with Session(engine) as session:
    session.add(User(nama="Budi"))
    session.commit()
```

### 2.5 Testing

#### `pytest`
Framework testing yang ringkas dan populer di ekosistem Python.

**Install:** `pip install pytest`

```python
# file: test_math.py
def tambah(a, b):
    return a + b

def test_tambah():
    assert tambah(2, 3) == 5

# jalankan dengan: pytest test_math.py
```

### 2.6 Utilitas & Validasi

#### `pydantic`
Validasi data dan pengaturan (settings) berbasis type hints, sering dipakai bersama FastAPI.

**Install:** `pip install pydantic`

```python
from pydantic import BaseModel

class Produk(BaseModel):
    nama: str
    harga: float

p = Produk(nama="Buku", harga="50000")   # otomatis dikonversi ke float
print(p.harga, type(p.harga))
```

#### `python-dotenv`
Memuat variabel lingkungan dari file `.env` ke dalam aplikasi.

**Install:** `pip install python-dotenv`

```python
from dotenv import load_dotenv
import os

load_dotenv()   # membaca file .env
api_key = os.getenv("API_KEY")
```

#### `tqdm`
Menampilkan progress bar untuk loop atau proses panjang.

**Install:** `pip install tqdm`

```python
from tqdm import tqdm
import time

for i in tqdm(range(100)):
    time.sleep(0.01)
```

### 2.7 Machine Learning

#### `scikit-learn`
Library machine learning klasik: klasifikasi, regresi, clustering, evaluasi model.

**Install:** `pip install scikit-learn`

```python
from sklearn.linear_model import LinearRegression
import numpy as np

X = np.array([[1], [2], [3], [4]])
y = np.array([2, 4, 6, 8])

model = LinearRegression()
model.fit(X, y)
print(model.predict([[5]]))   # prediksi mendekati 10
```

#### `torch` (PyTorch)
Framework deep learning untuk membangun dan melatih neural network, mendukung komputasi GPU.
 
**Install:** `pip install torch`
 
```python
import torch
 
# Tensor: struktur data utama di PyTorch, mirip array numpy tapi bisa jalan di GPU
x = torch.tensor([1.0, 2.0, 3.0])
y = torch.tensor([4.0, 5.0, 6.0])
print(x + y)                        # tensor([5., 7., 9.])
 
# Cek ketersediaan GPU (CUDA)
print("GPU tersedia:", torch.cuda.is_available())
 
# Layer neural network sederhana
model = torch.nn.Linear(in_features=3, out_features=1)
output = model(x)
print("Output layer:", output)
```

### 2.8 Image Processing

#### `Pillow` (`PIL`)
Membuka, memanipulasi, dan menyimpan berbagai format gambar.

**Install:** `pip install pillow`

```python
from PIL import Image

img = Image.open("foto.jpg")
img_resize = img.resize((200, 200))
img_resize.save("foto_kecil.jpg")
print(img.size, img.format)
```

---

### 2.9 Data App & Dashboard
 
#### `streamlit`
Membuat aplikasi web interaktif (dashboard, alat visualisasi data) hanya dengan kode Python, tanpa perlu HTML/CSS/JS.
 
**Install:** `pip install streamlit`
 
```python
import streamlit as st
 
st.title("Dashboard Sederhana")
 
nama = st.text_input("Masukkan nama kamu")
if nama:
    st.write(f"Halo, {nama}!")
 
angka = st.slider("Pilih angka", 0, 100, 50)
st.write("Angka terpilih:", angka)
 
# jalankan dengan: streamlit run nama_file.py
```

### 2.10 Excel / Spreadsheet

#### `openpyxl`
Membaca dan menulis file Excel (`.xlsx`) langsung dari Python — bikin, edit, atau baca spreadsheet tanpa buka Excel.

**Install:** `pip install openpyxl`

```python
from openpyxl import Workbook, load_workbook

# Membuat file Excel baru
wb = Workbook()
ws = wb.active
ws.title = "Data"

ws.append(["Nama", "Umur", "Kota"])
ws.append(["Budi", 25, "Jakarta"])
ws.append(["Ani", 30, "Bandung"])

wb.save("data.xlsx")

# Membaca file Excel yang sudah ada
wb2 = load_workbook("data.xlsx")
ws2 = wb2.active

for row in ws2.iter_rows(values_only=True):
    print(row)
```


## Cara Menggunakan Repo Ini

1. Gunakan Ctrl+F / daftar isi di atas untuk mencari modul yang dibutuhkan.
2. Setiap contoh kode bisa langsung dicopy dan dijalankan (pastikan library pihak ketiga sudah di-`pip install` terlebih dahulu).
3. Tambahkan entri baru dengan mengikuti format: **nama modul** → penjelasan singkat → contoh kode.

## 📄 License

This project is licensed under the **MIT License**.

You are free to use, copy, modify, merge, publish, distribute, sublicense, and even use this software for commercial purposes, provided that the original copyright notice and this permission notice are included in all copies or substantial portions of the software.

This project is provided **"as is"**, without any warranty of any kind. See the `LICENSE` file for more details.
