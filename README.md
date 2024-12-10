import random
import numpy as np
import matplotlib.pyplot as plt

# Inisialisasi pemain dengan atribut layangan
players = [
    {"name": "Pemain 1", "tali": 70, "keterampilan": 80, "angin": 60},
    {"name": "Pemain 2", "tali": 80, "keterampilan": 75, "angin": 65},
    {"name": "Pemain 3", "tali": 65, "keterampilan": 85, "angin": 70},
]

# Fungsi untuk menghitung skor setiap pemain
def calculate_score(player):
    base_score = player["tali"] * 0.4 + player["keterampilan"] * 0.5 + player["angin"] * 0.1
    random_factor = random.uniform(0.8, 1.2)  # RNG memengaruhi skor akhir (20% variasi)
    return base_score * random_factor

# Simulasikan pertandingan antar pemain
def simulate_match(player1, player2):
    score1 = calculate_score(player1)
    score2 = calculate_score(player2)
    if score1 > score2:
        return player1["name"]
    elif score2 > score1:
        return player2["name"]
    else:
        return "Seri"

# Lakukan simulasi beberapa ronde
def simulate_tournament(players, rounds=10):
    results = []
    for i in range(rounds):
        p1, p2 = random.sample(players, 2)  # Pilih 2 pemain secara acak
        winner = simulate_match(p1, p2)
        results.append(winner)
    return results

# Jalankan simulasi
results = simulate_tournament(players, rounds=100)

# Hitung frekuensi kemenangan
from collections import Counter

winner_count = Counter(results)

# Visualisasikan hasil
plt.bar(winner_count.keys(), winner_count.values(), color=['blue', 'green', 'red', 'gray'])
plt.title("Distribusi Kemenangan")
plt.xlabel("Pemain")
plt.ylabel("Jumlah Kemenangan")
plt.show()

print("Hasil distribusi kemenangan:", winner_count)
