# Adli Bilişim/Forensics Notları

## Adli Bilişim Süreçleri

- Olayı anlama

- Ortamı Korumaya Alma

- Delil Tespiti

- Delillerin Toplanması

- İnceleme ve Analiz

- Raporlama

- Sunum

## İmaj alma

- FTKImager - En yaygın imaj alma programı

En çok kullanılan image türleri Raw ve E01.

Raw veya E01 ile sıkıştırdığınızda hash değeri değişmez.

- DC3DD 

`dc3dd if=\\.\D: of=c:\Users\user\Desktop\dc3dd hash=md5 log=usb_log.txt`

- TD2 - Imaj alma donanımı

## İmaj Dosyasını Canlandırma

- VboxManage

Alınan imajı sanal makinede çalıştırmak için convert etmemiz gerekiyor

`VboxManage.exe convertdd training_image_window.raw yeni_imaj.vdi --format VDI`

## Artifact 

Kullanıcının bıraktığı izler/ipucular.

- Jump List  

`%appdata%\Roaming\Microsoft\Windows\Recent\AutomaticDestinations`

JumpListsView kullanarak son açılan dosyalar hakkında bilgi alabiliriz. 

- Thumbnail dosyaları

`%appdata%\Local\Microsoft\Windows\Explorer`

- Thumbcache Viewer

Thumbnailleri görüntülememizi sağlar.

- Prefetch Dosyaları

En çok kullandığınız dosyalar. "pf" uzantili dosyalar.

- WinPrefetchView

"pf" uzantılı dosyaları incelememizi sağlar.

`WinPrefetch.exe /shtml output.html`

- BMC tools master

Ekranın cache e alınan sslerini "tile" şeklinde çıkarır. 

`python bmc-tools.py -s ./ -d ./ciktilar` 

- Browsing Hisrory View

Browser History lerinii incelememizi sağlar

- Amcache Parser

Bir zararlı çalıştırılmış ve buna dair kanıt bulunamıyorsa, AMCACHE.hve dosyasına bakılabilir. Amcache Parser sayesinde içerisine bakabiliriz.

`AmcacheParser.exe -f C:\Windows\appcompat\Programs\Amcache.hve -csv ./`

## RAM

- Volatility

Memory Forensic için ideal bir araç.

Memory incelemesine başlarken ilk önce profil bilgisini elde etmemiz gerekiyor.

`volatility -f memdump.mem imageinfo`

Process Listesi için

`volatility.exe -f memdump.mem --profile=PROFILISMI pslist`

DLL Listesi

`volatility.exe -f memdump.mem --profile=PROFILISMI dlllist`

Malware Araması (Kesin bilgi vermez)

`volatility.exe -f memdump.mem --profile=PROFILISMI malfind`

Dosyayı elde etmek için

`volatility.exe -f memdump.mem --profile=PROFILISMI procdump --dump-dir ./ -p <PIDDEGERI>`

Register dosyalarını görmek için

`volatility.exe -f memdump.mem --profile=PROFILISMI hivelist`

NTLM Hashleri elde etmek için 

`volatility.exe -f memdump.mem --profile=PROFILISMI hashdump -y 0x89a1c008 -s 0x8c3349c8`

SAM dosyasını kopyalamak için

`reg save hklm\SAM C:\Users\user\Desktop\SAM`

## EXIF

- Exiftool

Dosyaların metadatalarını görmemizi sağlar.

## Diğer

- Search Everything Programı

Security loglarını incelemek için

`EvtxECmd.exe -f Security.ectx --csv ./`

- LinkParser

Link dosyalarından bilgi elde etmemize yarar. Dosyanın oluşturulduğu bilgisayarın MAC adresine kadar biilgiler verir. 







