# 🔍 Web Uygulamalarında Bilgi Toplama (Information Gathering)

Bu doküman, siber güvenliğin en kritik aşaması olan keşif ve bilgi toplama süreçlerine dair teknik notlarımı ve uygulama örneklerimi içerir.

---

## 🛡️ 1. Pasif Bilgi Toplama (İz Bırakmadan)
Hedef sistemle doğrudan etkileşime girmeden yapılan araştırmalardır.

### **Google Dorking (Google Hacking)**
Google operatörlerini kullanarak hassas verileri filtreleme:
* `site:` : Belirli bir alan adında arama yapar.
* `filetype:` : Belirli dosya uzantılarını (pdf, sql, log) bulur.
* `intitle:` : Sayfa başlığında (Örn: "index of") arama yapar.
* `inurl:` : URL içinde (Örn: "admin") kelime arar.

### **Robots.txt Analizi**
Sitenin kök dizinindeki `robots.txt` dosyası, botların girmesinin yasaklandığı (`Disallow:`) alanları gösterir. Bu alanlar genellikle yönetim panelleri veya yedek klasörleridir.

---

## ⚡ 2. Aktif Bilgi Toplama (Sahada Uygulama)
Hedef sisteme doğrudan istekler göndererek yapılan keşiflerdir.

### **Dizin ve Dosya Taraması (Fuzzing)**
Gözle görülmeyen gizli dizinleri bulmak için `dirb` veya `gobuster` gibi araçlar kullanılır.
* **Örnek Senaryo:** `/promo` veya `/private` gibi dizinlerin tespiti.

### **HTTP Header Analizi**
Sunucunun döndürdüğü yanıt başlıkları incelenerek servis bilgileri ve çerez (cookie) yapıları çözümlenir.
* **Komut:** `curl -I http://[hedef-ip]`

---

## 🏆 Uygulama Notları (Final Sınavı Deneyimi)
Gerçek bir makine üzerinde yapılan testlerde şu sonuçlar elde edilmiştir:
* **Hassas Dizin Tespiti:** `/promo` dizini üzerinden kampanya kodlarına ulaşıldı.
* **Erişim Kısıtlamaları:** `robots.txt` üzerinden botlara kapalı olan ancak saldırganlar için hedef olabilecek dizinler analiz edildi.
