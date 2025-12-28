# Tarif Rehberi Uygulaması 🍳

## 📋 Proje Açıklaması

Bu proje, kullanıcıların tarif yönetimi yapabileceği kapsamlı bir masaüstü uygulamasıdır. Uygulama, tarif ekleme, güncelleme, silme, filtreleme ve malzeme arama gibi temel işlevleri
kullanıcı dostu bir arayüzle sunmaktadır.

## ✨ Özellikler

### 🍽️ Tarif Yönetimi
- ✅ Yeni tarif ekleme
- ✅ Mevcut tarifleri güncelleme
- ✅ Tarif silme  
- ✅ Tarif detaylarını görüntüleme 

### 🥕 Malzeme Yönetimi
- ✅ Malzeme ekleme ve silme
- ✅ Malzeme arama
- ✅ Malzeme bazlı filtreleme
 
### 🔍 Arama ve Filtreleme
- ✅ Tarif adına göre arama
- ✅ Malzeme bazlı filtreleme
- ✅ Kategori bazlı filtreleme
- ✅ Gelişmiş arama seçenekleri

### 👤 Kullanıcı Deneyimi
- ✅ Kullanıcı dostu arayüz
- ✅ Responsive tasarım
- ✅ Kolay navigasyon
- ✅ Görsel tarif gösterimi

## 🛠️ Kullanılan Teknolojiler

### Backend
- **Java** - Ana programlama dili
- **PostgreSQL** - Veritabanı yönetim sistemi
- **JDBC** - Veritabanı bağlantısı

### Frontend
- **Java Swing** - Grafiksel kullanıcı arayüzü 
- **AWT** - Grafik ve UI bileşenleri

### Geliştirme Araçları
- **IDE** - Java geliştirme ortamı
- **Git** - Versiyon kontrolü
- **Maven/Gradle** - Bağımlılık yönetimi

## 📊 Veritabanı Yapısı

### Tablolar

#### 1. `recipes` - Tarif Bilgileri
```sql
CREATE TABLE recipes (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    instructions TEXT,
    cooking_time INTEGER,
    serving_size INTEGER,
    difficulty_level VARCHAR(50),
    category VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### 2. `ingredients` - Malzeme Bilgileri
```sql
CREATE TABLE ingredients (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL UNIQUE,
    category VARCHAR(100),
    unit VARCHAR(50),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### 3. `recipe_ingredients` - Tarif-Malzeme İlişkisi
```sql
CREATE TABLE recipe_ingredients (
    id SERIAL PRIMARY KEY,
    recipe_id INTEGER REFERENCES recipes(id) ON DELETE CASCADE,
    ingredient_id INTEGER REFERENCES ingredients(id) ON DELETE CASCADE,
    quantity DECIMAL(10,2),
    unit VARCHAR(50),
    UNIQUE(recipe_id, ingredient_id)
);
```

## 🚀 Kurulum ve Çalıştırma

### Gereksinimler
- **Java JDK 11+**
- **PostgreSQL 12+**
- **Maven 3.6+** (opsiyonel)

### Kurulum Adımları

1. **Projeyi klonlayın:**
```bash
git clone https://github.com/yourusername/tarif-rehberi.git
cd tarif-rehberi
```

2. **PostgreSQL veritabanını kurun:**
```sql
-- PostgreSQL'de yeni veritabanı oluşturun
CREATE DATABASE recipe_db;

-- Kullanıcı oluşturun (opsiyonel)
CREATE USER recipe_user WITH PASSWORD 'password123';
GRANT ALL PRIVILEGES ON DATABASE recipe_db TO recipe_user;
```

3. **Veritabanı tablolarını oluşturun:**
```bash
# SQL dosyasını çalıştırın
psql -U recipe_user -d recipe_db -f database/schema.sql
```

4. **Proje ayarlarını yapın:**
```java
// DatabaseConfig.java dosyasında
private static final String DB_URL = "jdbc:postgresql://localhost:5432/recipe_db";
private static final String DB_USER = "recipe_user";
private static final String DB_PASSWORD = "password123";
```

5. **Projeyi derleyin:**
```bash
# Maven kullanıyorsanız
mvn clean compile

# Veya IDE'nizde Build > Build Project
```

6. **Uygulamayı çalıştırın:**
```bash
java -cp target/classes com.recipeapp.Main
```

## 🏗️ Proje Yapısı

```
tarif-rehberi/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   ├── com/
│   │   │   │   └── recipeapp/
│   │   │   │       ├── Main.java
│   │   │   │       ├── gui/
│   │   │   │       │   ├── MainFrame.java
│   │   │   │       │   ├── RecipePanel.java
│   │   │   │       │   ├── IngredientPanel.java
│   │   │   │       │   └── FilterPanel.java
│   │   │   │       ├── model/
│   │   │   │       │   ├── Recipe.java
│   │   │   │       │   ├── Ingredient.java
│   │   │   │       │   └── RecipeIngredient.java
│   │   │   │       ├── dao/
│   │   │   │       │   ├── RecipeDAO.java
│   │   │   │       │   ├── IngredientDAO.java
│   │   │   │       │   └── DatabaseConnection.java
│   │   │   │       └── service/
│   │   │   │           ├── RecipeService.java
│   │   │   │           └── IngredientService.java
│   │   └── resources/
│   │       ├── images/
│   │       └── config/
│   └── test/
├── database/
│   ├── schema.sql
│   └── sample_data.sql
├── docs/
├── pom.xml
└── README.md
```

## 📱 Kullanım Kılavuzu

### Tarif Ekleme
1. Ana menüden "Tarif Ekle" butonuna tıklayın
2. Tarif bilgilerini doldurun (ad, açıklama, talimatlar)
3. Malzemeleri ekleyin
4. "Kaydet" butonuna tıklayın

### Tarif Arama
1. Arama kutusuna tarif adını yazın
2. Filtreleme seçeneklerini kullanın
3. Sonuçları listeden görüntüleyin

### Malzeme Yönetimi
1. "Malzemeler" sekmesine gidin
2. Yeni malzeme ekleyin veya mevcut malzemeleri düzenleyin
3. "Malzeme Sil" ile gereksiz malzemeleri kaldırın

## 🐛 Bilinen Sorunlar ve Çözümler

### 1. Veritabanı Bağlantı Sorunları
**Sorun:** PostgreSQL bağlantısı başarısız  
**Çözüm:** 
- PostgreSQL servisinin çalıştığından emin olun
- Bağlantı parametrelerini kontrol edin
- Firewall ayarlarını kontrol edin

### 2. UI Görüntüleme Problemleri
**Sorun:** Farklı ekran çözünürlüklerinde görüntü bozuklukları  
**Çözüm:** 
- Look and Feel ayarlarını güncelleyin
- Swing bileşenlerinin layout manager'larını optimize edin

### 3. İşlev Çakışmaları
**Sorun:** Aynı anda birden fazla işlem çalıştırıldığında hatalar  
**Çözüm:** 
- SwingUtilities.invokeLater() kullanın
- Thread-safe operasyonlar uygulayın

## 🧪 Test

### Unit Testleri Çalıştırma
```bash
mvn test
```

### Manuel Test Senaryoları
1. **Tarif CRUD İşlemleri**
   - Tarif ekleme, güncelleme, silme
   - Verinin doğru kaydedilmesi

2. **Arama ve Filtreleme**
   - Farklı arama kriterlerini test etme
   - Filtreleme sonuçlarının doğruluğu

3. **UI Responsive Testi**
   - Farklı ekran boyutlarında test
   - Kullanıcı etkileşimlerinin testi

## 🚀 Gelecek Geliştirmeler

- [ ] 📱 Mobil uygulama versiyonu
- [ ] ☁️ Cloud sync özelliği
- [ ] 📊 Beslenme değerleri hesaplama
- [ ] 🖼️ Tarif fotoğrafı ekleme
- [ ] 📋 Alışveriş listesi oluşturma
- [ ] 🔄 Tarif paylaşma özelliği
- [ ] 🌍 Çoklu dil desteği
- [ ] 📈 Popüler tarifler algoritması

## 🤝 Katkıda Bulunma

1. Bu repository'yi fork edin
2. Yeni bir feature branch oluşturun (`git checkout -b feature/amazing-feature`)
3. Değişikliklerinizi commit edin (`git commit -m 'Add some amazing feature'`)
4. Branch'inizi push edin (`git push origin feature/amazing-feature`)
5. Bir Pull Request oluşturun


## 👨‍💻 Geliştirici

**Geliştirici Adı**  
Ümit DANSUK
Bilgisayar Mühendisliği 

## 📞 İletişim

- 📧 Email: umitdansuk@gmail.com


## 📚 Kaynaklar

- [PostgreSQL Resmi Dokümantasyonu](https://www.postgresql.org/docs/)
- [Java Swing Öğreticileri](https://docs.oracle.com/javase/tutorial/uiswing/)
- [Java JDBC ve PostgreSQL](https://www.baeldung.com/java-connect-postgresql)
- [Software Engineering Principles](https://www.pearson.com/us/higher-education/program/Sommerville-Software-Engineering-10th-Edition/PGM187042.html)
- [Stack Overflow](https://stackoverflow.com/)
- [GitHub](https://github.com/)

---
