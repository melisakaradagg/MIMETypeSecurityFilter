# 🛡️ MIMEType Content Security Filter

![Language](https://img.shields.io/badge/Language-Java%20%7C%20Python-blue?logo=secure)
![Security Standard](https://img.shields.io/badge/Standard-OWASP-black)
![Category](https://img.shields.io/badge/Category-SecOps%20%7C%20AppSec-red)
![License](https://img.shields.io/badge/License-MIT-green)

**MIMETypeSecurityFilter**, web uygulamalarında dosya yükleme güvenliğini sağlamak için geliştirilmiş, içerik türlerini (MIME) derinlemesine analiz eden bir güvenlik katmanıdır.

---

## 📑 İçindekiler

- [Proje Hakkında](#-proje-hakkında)
- [Özellikler ve Analiz Yetenekleri](#-özellikler-ve-analiz-yetenekleri)
- [Teknik Metodoloji](#-teknik-metodoloji)
- [Kurulum](#-kurulum)
- [Kullanım](#-kullanım)
- [Yasal Uyarı](#-yasal-uyarı)

---

## 🎯 Proje Hakkında

Bu proje, dosya uzantısı manipülasyonu ve "Content Sniffing" saldırılarına karşı koruma sağlar. Sadece `Content-Type` header bilgisine güvenmek yerine, dosyanın **Magic Bytes** yapısını kontrol ederek gerçek içeriği doğrular ve yetkisiz dosya yürütme girişimlerini engeller.

---

## 🚀 Özellikler ve Analiz Yetenekleri

### 1. 🔍 Magic Bytes Analizi
Dosyaların binary imzalarını kontrol ederek sahte uzantıları tespit eder.
- **Header Doğrulama:** Gönderilen tür ile gerçek veri yapısı arasındaki tutarlılığı ölçer.
- **Kötü Niyetli Kod Engelleme:** Resim dosyası içine gizlenmiş scriptleri (PHP, JS vb.) bloke eder.

### 2. 🛡️ Tarayıcı Güvenliği (No-Sniff)
- **X-Content-Type-Options:** Yanıtlara eklenen `nosniff` parametresi ile tarayıcıların dosyayı yanlış yorumlamasını önler.

### 3. 📂 Güvenli Liste (Whitelist)
- Sadece önceden tanımlanmış güvenli MIME türlerinin (JPEG, PNG, PDF vb.) sisteme girişine izin verir.

---

## 🛠️ Teknik Metodoloji

| Standart / Teknik | Açıklama |
| :--- | :--- |
| **OWASP File Upload** | Küresel güvenlik standartlarına uygun dosya doğrulama süreçleri. |
| **Magic Numbers** | Dosya türlerini belirlemek için kullanılan benzersiz byte imzaları. |
| **Integrity Check** | Dosya bütünlüğünün ve güvenliğinin uçtan uca kontrolü. |

---

## 📥 Kurulum

Projeyi yerel makinenize klonlayın ve gerekli bağımlılıkları yükleyin.

```bash
# Repoyu klonlayın
git clone [https://github.com/EfeSidal/MIMETypeSecurityFilter.git](https://github.com/EfeSidal/MIMETypeSecurityFilter.git)

# Proje dizinine girin
cd MIMETypeSecurityFilter

# Gerekli kütüphaneleri yükleyin
pip install -r requirements.txt
from security_filter import MIMETypeFilter

# Filtreyi tanımla (Sadece güvenli dosya türleri)
mimetype_filter = MIMETypeFilter(allowed_types=['image/jpeg', 'image/png', 'application/pdf'])

# Yüklenen dosyayı doğrula
is_secure = mimetype_filter.validate(request.files['upload_file'])

if not is_secure:
    return "Güvenlik İhlali: Geçersiz Dosya İçeriği!", 403

Developed by Melisa Karadağ

Öğrenci Numarası: 2420191031
