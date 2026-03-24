Cross-Site Scripting (XSS): Client-Side Security Analysis
📝 Genel Bakış
Web uygulamalarında kullanıcı girdilerinin tarayıcıya yansıtılmadan önce filtrelenmemesi sonucu ortaya çıkan XSS (Reflected, Stored, DOM-based) zafiyetleri üzerine teknik bir çalışmadır.

🧪 Reflected XSS Analizi
Vektör: Arama parametresi veya URL Query String.

Saldırı: Kullanıcının tarayıcısında yetkisiz JavaScript kodu çalıştırmak.

Payload: <script>alert(document.cookie)</script>

Etki: Kullanıcının oturum çerezleri (Session ID) saldırgan tarafından okunabilir hale gelir.

🔒 Stored XSS (Kalıcı Tehdit)
Zararlı kodun sunucu tarafındaki veritabanına (yorumlar, profil bilgileri vb.) kaydedilmesi durumudur.

Risk: Sayfayı ziyaret eden her kurbanın tarayıcısında kod otomatik olarak tetiklenir.

Önleme: Content Security Policy (CSP) kullanımı ve HttpOnly bayraklarının çerezlere tanımlanması kritik önem taşır.
