# 🌐 Web Uygulama Güvenliği ve Modern Web Mimarisi

Bu doküman, Siber Vatan CTF hazırlık sürecinde öğrendiğim web temelleri ve modern mimari kavramlarını içermektedir.

---

## 1. HTTP Protokolü ve İletişim Temelleri
Web dünyasının ana dili olan HTTP'yi anlamak, sızma testlerinin temelidir.

* **GET vs POST:** GET veriyi URL üzerinden çeker (bilgi toplama için kritiktir), POST ise veriyi gövdede taşınır (şifreler, formlar vb.).
* **HTTPS (Secure):** Veriyi TLS/SSL ile şifreler. Şifrelenmemiş HTTP trafiği, MITM (Aradaki Adam) saldırılarına karşı tamamen açıktır.
* **User-Agent:** İstemcinin tarayıcı ve işletim sistemi bilgisini içerir. Güvenlik duvarlarını (WAF) atlatmak için sıklıkla manipüle edilir.



## 2. Modern Web Mimarisi ve Bileşenler
Web siteleri artık statik değil, dinamik birer uygulama gibi çalışır.

* **API (Application Programming Interface):** Frontend ve Backend arasındaki iletişim köprüsü. Modern saldırıların (IDOR, BOLA) odak noktasıdır.
* **JavaScript & React:** Modern webin motoru. Zafiyet taramalarında `Source Code Analysis` (Kaynak kod analizi) yapılarak gizli API uçları aranır.
* **Load Balancer:** Trafiği yönetir. Pentest sürecinde "Origin IP" tespitini zorlaştıran bir katmandır.
* **WebSocket:** Çift yönlü canlı veri akışı (Chat, Borsa). Klasik HTTP filtrelemelerini aşabilecek potansiyel bir saldırı kanalıdır.



## 3. Veritabanı Sistemleri
* **SQL (Relational):** İlişkisel tablolar. Klasik SQL Injection (SQLi) saldırılarının hedefidir.
* **NoSQL (Document-based):** Esnek yapı (JSON benzeri). NoSQL Injection ve mantıksal sorgu manipülasyonlarına dikkat edilmelidir.

## 4. Güvenlik Stratejisi: Client-Side vs Server-Side
Siber güvenlikteki en temel kural: **İstemci tarafındaki (Client-Side) kontrole asla güvenme!**
* JavaScript ile yapılan fiyat veya yetki kontrolleri, tarayıcı üzerinden kolayca manipüle edilebilir.
* Tüm kritik güvenlik doğrulamaları mutlaka **Server-Side** (Sunucu Tarafı) üzerinde yapılmalıdır.

---
*Bu içerik sürekli güncellenmekte ve yeni öğrenilen zafiyet türleri buraya eklenmektedir.*
