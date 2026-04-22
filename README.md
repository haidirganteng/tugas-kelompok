# tugas-kelompok
# Inisialisasi
antrian = deque()
riwayat = []

def tambah_pelanggan():
    nama = input("Masukkan nama pelanggan: ")
    jenis = input("Jenis (VIP/Biasa): ").lower()

    data = {"nama": nama, "jenis": jenis}

    if jenis == "vip":
        antrian.appendleft(data)
        print(f"{nama} (VIP) masuk ke depan antrian.")
    else:
        antrian.append(data)
        print(f"{nama} (Biasa) masuk ke belakang antrian.")

    riwayat.append(data)


def undo():
    if not riwayat:
        print("Tidak ada data untuk di-undo.")
        return

    terakhir = riwayat.pop()

    try:
        antrian.remove(terakhir)
        print(f"Pesanan {terakhir['nama']} dibatalkan.")
    except ValueError:
        print("Data tidak ditemukan di antrian.")


def proses_dapur():
    if not antrian:
        print("Antrian kosong.")
        return

    pelanggan = antrian.popleft()
    print(f"Memproses pesanan: {pelanggan['nama']} ({pelanggan['jenis']})...")
    print(f"Pesanan {pelanggan['nama']} selesai!")


def tampilkan_antrian():
    if not antrian:
        print("Antrian kosong.")
        return

    print("\nDaftar Antrian:")
    for i, p in enumerate(antrian, start=1):
        print(f"{i}. {p['nama']} ({p['jenis']})")
    print()


# Program utama
while True:
    print("\n=== SISTEM LAYANAN RESTORAN ===")
    print("1. Tambah Pelanggan")
    print("2. Undo (Batalkan terakhir)")
    print("3. Proses Dapur")
    print("4. Lihat Antrian")
    print("5. Keluar")

    pilihan = input("Pilih menu: ")

    if pilihan == "1":
        tambah_pelanggan()
    elif pilihan == "2":
        undo()
    elif pilihan == "3":
        proses_dapur()
    elif pilihan == "4":
        tampilkan_antrian()
    elif pilihan == "5":
        print("Program selesai.")
        break
    else:
        print("Pilihan tidak valid.")
