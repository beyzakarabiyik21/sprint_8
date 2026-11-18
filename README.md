# Kampüs Etkinlikleri

Fakültedeki seminer, atölye, söyleşi ve yarışmaları listeleyen, aranabilen ve yönetilebilen React + TypeScript uygulaması.

Beyza Karabiyik · 2416501003

## Özellikler

- **10 route** (React Router)
- **Context API** (`AppContext`): etkinlik listesi ve kullanıcı bilgisi tüm sayfalarda ortak kullanılır
- **Ekle / güncelle / sil**: Yönetim sayfasından yapılır, silmeden önce onay istenir; değişiklikler ana sayfa, liste ve detay sayfalarına anında yansır (localStorage'a da kaydedilir)
- **Arama ve kategori filtresi**: Etkinlikler sayfasında
- **Form doğrulama**: etkinlik formu, giriş, kayıt ve şifremi unuttum formlarında alan bazlı hata mesajları
- **Mobil uyumlu** görünüm

## Sayfalar

| Route | Sayfa |
| --- | --- |
| `/` | Ana sayfa (yaklaşan 2 etkinlik) |
| `/etkinlikler` | Tüm etkinlikler, arama ve filtre |
| `/etkinlikler/:id` | Etkinlik detayı |
| `/yonetim` | Etkinlik yönetimi (tablo, düzenle, sil) |
| `/yonetim/ekle` | Etkinlik ekle |
| `/yonetim/duzenle/:id` | Etkinlik güncelle |
| `/giris` | Giriş yap |
| `/kayit` | Kayıt ol |
| `/sifremi-unuttum` | Şifremi unuttum |
| `*` | 404 sayfası |

## Klasör yapısı

```
src/
  components/
    events/    EventCard, EventList, EventFilter, EventDetail
    forms/     EventForm, FormField
    layout/    Header, Navigation, Footer, Layout
  context/     AppContext
  data/        events
  pages/       10 sayfa bileşeni
  types/       campus-event
  utils/       filter-events, format-date, validate
```

## Çalıştırma

Proje iki bölümden oluşur. İkisini aynı anda çalıştırmak için iki ayrı terminal açın.

### Backend (Node + Express + MongoDB)

```bash
cd backend
npm install
cp .env.example .env
```

`.env` dosyasındaki `MONGODB_URI` değerini kendi MongoDB Atlas bağlantı adresinizle değiştirin (`<db_password>` yerine şifrenizi yazın, `.net/` sonrasına `kampus` ekleyin). Bu dosya GitHub'a gönderilmez.

```bash
npm run seed   # 6 örnek etkinliği veritabanına yazar
npm run dev    # http://localhost:3000
```

Terminalde `MongoDB bağlandı (Atlas): ...` ve `API: http://localhost:3000` yazılarını görmelisiniz. Kontrol için tarayıcıda `http://localhost:3000/health` adresini açın. Endpoint'ler ve Postman koleksiyonu için [backend/README.md](backend/README.md) dosyasına bakın.

### Frontend (React + TypeScript + Vite)

```bash
cd frontend
npm install
npm run dev    # http://localhost:5173
```

Terminalde yazan adresi (`http://localhost:5173`) tarayıcıda açın.

`frontend/vercel.json`, sayfa yenilendiğinde route'ların Vercel'de 404 vermemesi için tüm istekleri `index.html`'e yönlendirir.
