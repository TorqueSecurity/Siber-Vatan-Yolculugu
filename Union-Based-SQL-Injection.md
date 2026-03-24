Advanced Data Exfiltration: Union-Based SQL Injection
📝 Genel Bakış
Bu laboratuvar, uygulamanın arama (Search) fonksiyonu üzerinden veritabanının tüm şemasını (tablo ve sütun isimleri) dökme ve spesifik kullanıcı verilerini sızdırma sürecini kapsamaktadır.

🛠️ Keşif ve Enumeration Süreci
Veritabanı yapısını çözmek için adım adım şu metodoloji izlenmiştir:

Sütun Sayısının Tespiti: Orijinal sorgunun sonuç kümesiyle eşleşen sütun sayısı ORDER BY ve UNION SELECT denemeleriyle 4 olarak bulunmuştur.

Payload: ' UNION SELECT 1,2,3,4 -- 

Veritabanı Tanımlama: Ekrana yansıyan sütunlar üzerinden sistem fonksiyonları çalıştırılmıştır.

Target DB: ecliptica_cars

Payload: ' UNION SELECT 1,2,3,database() -- 

Tablo Şemasının Çıkartılması: information_schema.tables kullanılarak veritabanındaki kritik tablolar listelenmiştir.

Keşfedilen Tablolar: cars, settings, users

Sütun Analizi: users tablosundaki veri yapısı incelenmiş, hassas verilerin username ve password sütunlarında tutulduğu netleşmiştir.

⚡ Veri Sızdırma (The Final Hit)
Hedef kullanıcı oliverlee için hazırlanan son payload ile parolanın düz metin (plain-text) hali ele geçirilmiştir:

SQL
' UNION SELECT 1, 2, 3, password FROM users WHERE username = 'oliverlee' --
