# Elaltıntaş — Modüler Su Deposu Hesaplama Sistemi

Web tabanlı depo hesaplama, teklif oluşturma ve kullanıcı yönetim sistemi.

---

## Özellikler

- JWT ile güvenli kullanıcı girişi
- Anlık depo hacim, ağırlık, civata, conta hesaplama
- Teklif oluşturma ve listeleme
- Birim fiyat yönetimi (admin paneli)
- Kullanıcı yönetimi (admin paneli)
- SQLite veritabanı (veri kalıcılığı)

---

## Yerel Kurulum (Geliştirme)

### 1. Gereksinimler
- Python 3.11+
- pip

### 2. Bağımlılıkları yükle
```bash
cd backend
pip install -r requirements.txt
```

### 3. Uygulamayı başlat
```bash
cd backend
uvicorn main:app --reload --port 8000
```

### 4. Tarayıcıda aç
```
http://localhost:8000
```

### Varsayılan giriş
- **Kullanıcı adı:** admin
- **Şifre:** admin123

> ⚠️ İlk girişten sonra admin şifresini değiştirmeyi unutmayın!

---

## Railway'e Deploy (Ücretsiz Hosting)

### 1. GitHub'a yükle
```bash
git init
git add .
git commit -m "ilk commit"
git remote add origin https://github.com/KULLANICI/depo-app.git
git push -u origin main
```

### 2. Railway'de proje oluştur
1. [railway.app](https://railway.app) adresine git
2. "New Project" → "Deploy from GitHub repo"
3. Bu repoyu seç
4. Otomatik deploy başlar (~2 dakika)

### 3. Ortam değişkeni ekle (önemli!)
Railway dashboard → Variables → ekle:
```
SECRET_KEY = guclu-rastgele-bir-sifre-buraya-yaz-2024
```

### 4. URL al
Railway sana `https://depo-xxx.up.railway.app` gibi bir URL verir.
Bu URL'den her yerden erişebilirsin.

---

## Proje Yapısı

```
depo_app/
├── backend/
│   ├── main.py          ← FastAPI uygulaması (API + auth + DB)
│   └── requirements.txt ← Python bağımlılıkları
├── frontend/
│   └── index.html       ← Tek sayfalık web arayüzü
├── railway.toml         ← Railway deploy ayarları
├── nixpacks.toml        ← Build ayarları
├── Procfile             ← Başlatma komutu
└── .gitignore
```

---

## API Endpointleri

| Method | Endpoint | Açıklama |
|--------|----------|----------|
| POST | /api/token | Giriş (JWT al) |
| GET | /api/fiyatlar | Birim fiyatları listele |
| PUT | /api/fiyatlar | Birim fiyatları güncelle (admin) |
| POST | /api/hesapla | Depo hesapla + kaydet |
| GET | /api/teklifler | Teklifleri listele |
| POST | /api/teklifler | Yeni teklif oluştur |
| GET | /api/teklifler/{id} | Teklif detayı |
| PUT | /api/teklifler/{id}/durum | Durum güncelle (admin) |
| GET | /api/kullanicilar | Kullanıcıları listele (admin) |
| POST | /api/kullanici | Kullanıcı ekle (admin) |
| GET | /api/istatistik | Genel istatistik (admin) |

Tüm endpointler (token hariç) `Authorization: Bearer <token>` header gerektirir.

---

## Sonraki Geliştirmeler (Yapılabilir)

- [ ] PDF teklif çıktısı (WeasyPrint veya ReportLab)
- [ ] Üretim formu PDF
- [ ] Gergi-kulak hesaplama modülü
- [ ] Sac kalınlığı lookup tablosu
- [ ] E-posta ile teklif gönderme
- [ ] PostgreSQL'e geçiş (büyük ölçek için)
