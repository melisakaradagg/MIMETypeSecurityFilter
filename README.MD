# 🛡️ MIME-Guard: File Integrity Enforcer

![Stack](https://img.shields.io/badge/Tech-Python%203.x-blue?style=flat&logo=python)
![Focus](https://img.shields.io/badge/Focus-Input%20Validation-red)
![Standard](https://img.shields.io/badge/Compliance-OWASP%20ASVS-orange)
![License](https://img.shields.io/badge/License-MIT-green)

**MIME-Guard**, web uygulamalarına yönelik dosya yükleme saldırılarını nötralize etmek amacıyla tasarlanmış, binary tabanlı bir içerik doğrulama motorudur.

---

## 🏛️ Mimari Yapı ve Ortam Yönetimi

Proje, sürdürülebilir ve izole bir güvenlik katmanı oluşturmak adına aşağıdaki prensiplerle inşa edilmiştir:

### 📦 Bağımlılık ve İzolasyon Stratejisi
* **Sanal Çalışma Alanı (`venv`):** Proje, sistem kütüphanelerinden bağımsız, kendine ait izole bir `runtime` üzerinde çalıştırılır. Bu sayede versiyon uyuşmazlıklarının önüne geçilir.
* **Paket Standardizasyonu (`requirements.txt`):** Güvenlik motorunun ihtiyaç duyduğu `python-magic` gibi kritik kütüphaneler ve sürümleri bu manifest dosyasında kilitlenmiştir.

### ⚙️ Konfigürasyon ve Güvenlik
* **Çevresel Değişkenler (`.env`):** Uygulama içi sabit kodlama (hard-coding) yerine, güvenlik politikaları ve izin verilen uzantılar dış kaynaklı `.env` dosyasından dinamik olarak çekilir.
* **Repo Hijyeni (`.gitignore`):** Hassas konfigürasyon dosyaları, önbellekler (`__pycache__`) ve yerel ortam dosyalarının versiyon kontrol sistemine karışması engellenmiştir.

---

## 🔧 Kurulum ve Dağıtım (Deployment)

Projeyi geliştirme ortamına almak için terminal üzerinden şu adımları izleyin:

```bash
# 1. Kaynak kodları yerel diske alın
git clone [https://github.com/EfeSidal/MIMETypeSecurityFilter.git](https://github.com/EfeSidal/MIMETypeSecurityFilter.git)
cd MIMETypeSecurityFilter

# 2. İzole Python ortamını oluşturun ve başlatın
python -m venv venv

# Windows Kullanıcıları için:
venv\Scripts\activate
# Linux/macOS Kullanıcıları için:
source venv/bin/activate

# 3. Kütüphaneleri yükleyin ve çevre ayarlarını yapın
pip install -r requirements.txt
cp .env.example .env
import os
from dotenv import load_dotenv
from core.security import ContentValidator

# Çevresel değişkenleri aktif et
load_dotenv()

# Validatör motorunu başlat
validator = ContentValidator(
    whitelist=os.getenv("ALLOWED_EXTENSIONS").split(',')
)

def handle_upload(file_stream):
    # Binary analiz ve imza kontrolü
    scan_result = validator.inspect(file_stream)
    
    if scan_result['is_safe']:
        process_file(file_stream)
        return "200 OK: Dosya temiz."
    else:
        log_incident(scan_result['threat_type'])
        return "406 Not Acceptable: Güvenlik politikası ihlali."
