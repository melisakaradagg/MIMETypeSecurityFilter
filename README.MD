# 🛡️ MIMEType Content Security Filter

![Language](https://img.shields.io/badge/Language-Java%20%7C%20Python-blue?logo=secure)
![Security Standard](https://img.shields.io/badge/Security-NIST%20%7C%20OWASP-black)
![Category](https://img.shields.io/badge/Category-AppSec%20%7C%20Content%20Safety-orange)
![License](https://img.shields.io/badge/License-MIT-green)

**MIMETypeSecurityFilter**, web uygulamalarına yüklenen veya sunulan dosyaların içerik türlerini (MIME) derinlemesine analiz eden, "Content Sniffing" saldırılarını ve kötü niyetli dosya yürütme girişimlerini engelleyen gelişmiş bir güvenlik filtresidir.

---

## 📑 İçindekiler

- [Proje Hakkında](#-proje-hakkında)
- [Temel Güvenlik Fonksiyonları](#-temel-güvenlik-fonksiyonları)
- [Teknik Metodoloji](#-teknik-metodoloji)
- [Kurulum ve Entegrasyon](#-kurulum-ve-entegrasyon)
- [Örnek Senaryo](#-örnek-senaryo)
- [Yasal Uyarı](#-yasal-uyarı)

---

## Proje Hakkında

Modern web saldırılarında, saldırganlar genellikle dosya uzantılarını manipüle ederek sistemlere sızmaya çalışırlar (Örn: `.jpg` görünümlü bir `.php` shell dosyası). 

Bu filtre, sadece dosya uzantısına veya tarayıcıdan gelen `Content-Type` header bilgisine güvenmek yerine, dosyanın **binary (ikili) yapısını** inceleyerek gerçek kimliğini doğrular. Proje, kurumsal düzeydeki uygulamalarda **Unrestricted File Upload** zafiyetini minimize etmek için tasarlanmıştır.

---

## Temel Güvenlik Fonksiyonları

Proje, dosya güvenliği üzerinde 3 ana katmanda koruma sağlar:

### 1. Magic Bytes (Signature) Doğrulaması
Dosyanın ilk baytlarını analiz ederek gerçek türünü belirler.
- **Header Eşleşmesi:** Gelen HTTP header bilgisi ile dosya imzasının (Magic Numbers) tutarlılığını kontrol eder.
- **Sahtecilik Tespiti:** Resim dosyası gibi görünüp içinde executable (çalıştırılabilir) kod barındıran dosyaları anında bloklar.



### 2. Content Sniffing Koruması
Tarayıcıların MIME türlerini tahmin etme (sniffing) özelliğini devre dışı bırakır.
- **X-Content-Type-Options:** Tüm yanıtlara `nosniff` parametresini otomatik olarak enjekte eder.
- **MIME Confusion:** Tarayıcının bir metin dosyasını script olarak yorumlamasından kaynaklanan XSS risklerini ortadan kaldırır.

### 3.Uzantı ve Metadata Temizliği
- **Whitelist Kontrolü:** Sadece izin verilen güvenli uzantıların sisteme girmesine izin verir.
- **Null Byte Injection:** Dosya isimlerindeki `%00` (Null Byte) gibi bypass tekniklerini temizler.

---

## Teknik Metodoloji

Bu filtre, analizlerini gerçekleştirirken aşağıdaki endüstri standartlarını referans alır:

| Teknik | Açıklama |
| :--- | :--- |
| **Deep Packet Inspection** | Dosya içeriğinin byte bazlı taranarak zararlı patternlerin (desenlerin) bulunması. |
| **OWASP File Upload** | OWASP'ın dosya yükleme güvenliği için önerdiği "MIME Validation" pratikleri. |
| **Entropy Check** | Dosya içindeki verinin rastgeleliğini ölçerek gizlenmiş (obfuscated) kod tespiti. |

---

## Kurulum

Projeyi mevcut middleware yapınıza entegre etmek için:

```bash
# Projeyi klonlayın
git clone [https://github.com/EfeSidal/MIMETypeSecurityFilter.git](https://github.com/EfeSidal/MIMETypeSecurityFilter.git)

# Bağımlılıkları kontrol edin
cd MIMETypeSecurityFilter
pip install -r requirements.txt

from security_filter import MIMETypeFilter

# Filtreyi tanımla
mimetype_filter = MIMETypeFilter(allowed_types=['image/jpeg', 'image/png', 'application/pdf'])

# Yüklenen dosyayı doğrula
is_secure = mimetype_filter.validate(request.files['upload_file'])

Developed by <b>MelisaKaradağ</b> for Safer Content Delivery 

Öğrenci Numarası: 2420191031
