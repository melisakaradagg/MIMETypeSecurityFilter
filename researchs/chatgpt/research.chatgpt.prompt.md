
# Araştırma Promptu

MIMETypeSecurityFilter hakkında detaylı ve teknik bir güvenlik araştırması yapılması istenmektedir.

Araştırma, web uygulamalarında MIME type doğrulama ve içerik türü filtreleme
mekanizmalarının güvenlik üzerindeki etkilerini kapsamlı şekilde ele almalıdır.

Araştırma kapsamı aşağıdaki başlıkları içermelidir:

1. MIMETypeSecurityFilter teknolojisinin temel çalışma prensipleri  
   - MIME type kavramı ve HTTP içerik türleri  
   - Sunucu ve istemci tarafında MIME doğrulama mekanizmaları  
   - MIME sniffing ve content-type manipulation riskleri  

2. En iyi uygulama yöntemleri (Best Practices) ve endüstri standartları  
   - OWASP önerileri  
   - Secure file upload ve content validation yaklaşımları  
   - Tarayıcı güvenlik başlıkları (X-Content-Type-Options vb.)  

3. Benzer açık kaynak projeler ve alternatif çözümler  
   - MIME type doğrulama kütüphaneleri  
   - Web framework’lerde (Spring, ASP.NET, PHP) yerleşik filtreleme mekanizmaları  
   - WAF (Web Application Firewall) tabanlı çözümler  

4. Kritik yapılandırma dosyaları ve parametreleri  
   - MIME whitelist / blacklist yapılandırmaları  
   - Server-side content inspection ayarları  
   - Dosya uzantısı ve içerik imzası (magic number) kontrolleri  

5. Güvenlik açısından dikkat edilmesi gereken kritik noktalar  
   - MIME type spoofing saldırıları  
   - Zararlı dosya yükleme (malware upload) senaryoları  
   - Cross-Site Scripting (XSS) ve Remote Code Execution (RCE) riskleri  

Çalışmanın teknik seviyesi yüksek olmalı, siber güvenlik bakış açısıyla
derinlemesine ele alınmalı ve OWASP, RFC standartları ve güvenilir
kaynaklar ile desteklenmiş bir Markdown raporu formatında sunulmalıdır.

