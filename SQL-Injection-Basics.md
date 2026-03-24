SQL Injection: Authentication Bypass Analysis
📝 Genel Bakış
Bu çalışma, web uygulamalarının kimlik doğrulama (Login) mekanizmalarındaki mantıksal hataların SQL Injection yöntemiyle nasıl manipüle edilebileceğini göstermektedir. Laboratuvar ortamında gerçekleştirilen bu testte, geçerli bir kullanıcı şifresi bilinmeksizin sisteme yetkisiz erişim sağlanmıştır.

🔍 Teknik Analiz (Deep Dive)
Uygulamanın arka planındaki sorgu yapısı şu şekildedir:

SQL
SELECT * FROM users WHERE username = '$user' AND password = '$password'
Saldırgan girdisi ($user) sanitize edilmediği için, girdi alanına enjekte edilen mantıksal operatörler SQL motoru tarafından sorgunun bir parçası olarak yorumlanır.

🚀 Sömürü (Exploitation) Aşamaları
Zafiyet Tespiti: Kullanıcı adı alanına ' (tek tırnak) eklenerek veritabanının SQL Syntax Error döndürdüğü ve girdinin doğrudan sorguya dahil edildiği doğrulandı.

Tautology (Doğrulama) Saldırısı: Giriş paneline şu payload enjekte edildi:

Payload: ' OR 1=1 -- 

Mantıksal Akış: Veritabanı sorguyu şu şekilde çalıştırdı:
SELECT * FROM users WHERE username = '' OR 1=1 -- ' AND password = '...'

1=1 ifadesi her zaman True döndürdüğü için WHERE koşulu sağlandı.

--  ifadesi sorgunun geri kalanını yorum satırı yaparak şifre kontrolünü bypass etti.

🏆 Sonuç
Laboratuvar hedefi olan Sky Raincin kullanıcısına ait e-posta adresi ve profil verileri, herhangi bir kimlik bilgisi olmaksızın başarıyla elde edilmiştir.
