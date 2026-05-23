# Xiaomi Mi 4A Gigabit/Giga Router OpenWRT Kurulum Rehberi
Bu yöntem ile Windows üzerinde Xiaomi Mi Router 4A Gigabit/Giga routerınıza kısa sürede OpenWRT kurabileceksiniz.   
diğer marka ve model routerlarda bu yöntemi denemek cihazı (Brick) eder.
OpenWRT kurulumu cihazınızı garanti dışı bırakacak olup, oluşabilecek tüm sorunlar sizin sorumluluğunuz altında olduğunu belirtmek isteriz. 
Konu ile ilgili hiçbir sorumluluk kabul etmemekteyiz.

##  Dikkat Etmeniz Gerekenler:
- modemin stok sürümü 3.0.x ise bunu 2.28.x olan herhangi bir sürüme düşürmeniz gereklidir.
- Bu yöntem routerın V1 sürümü içindir.
- indirdiğiniz openwrt frimware.bin dosyasının ismini değiştirdikten sonra değiştirdiğiniz isme göre komut yazmanız gerekmektedir. 
- wget komudundaki ip adresini kendindi ip adresinizi yazınız Terminali a.ıp ipconfig yazdıktan sonra ipv4 kısmında yazmaktadır.
# KURULUM
## Router resetleme 
- Routerimizin arkasındaki reset tuşuna basılı tutalım ve routerimizi resetleyelim ardından 192.168.31.1 veya miwifi.com adresine giderek modemimize kurulum yapalım.
## OpenWRT kurulumu için gerekli dosyalarımızı indirelim
- python indirelim
- https://firmware-selector.openwrt.org
- https://github.com/acecilia/OpenWRTInvasion

## Gerekli dosyaları indirdikten sonra OpenWRTİnvasion dosyasını ayıklayalım 
## OpenWRTİnvasion dosyasını açalım ve boş bir kısıma shifte basarak sağ tıklayalım ardından powershell penceresini açalım
### Not:Burada modemimiz internete bağlı olsun ve aşağıdaki komutları yapıştralım
```shell
pip install -r requirements.txt
python remote_command_execution_vulnerability.py
```
- son komutumuzu yapıştırdıkdan sonra bizden routerin ip adresini istiyecektir:192.168.31.1/miwifi.com yazabilirsiniz.
- ardından kurulumda belirlediğimiz şifreyi isteyecektir.
<img width="810" height="452" alt="Ekran görüntüsü 2026-05-23 215138" src="https://github.com/user-attachments/assets/d519d51f-0012-447f-b2a3-4035dbc5d464" />

- Şifreyide yazdıktan sonra bu ekran gelecektir.
### Not:Bu kısımda routerımızın internet ile bağlantısını keselim. (Ana modemden bağlı olan lan kablosunu çıkartalım)
- Bu sayfayı kapatalım.
## openwrt frimware.bin dosyasının adresine gidelim ve boş bir kısıma iki tane terminal penceresi açalım
- ilk terminal penceresinde server açalım.
 ```shell
python -m http.server 8000

```
<img width="805" height="449" alt="Ekran görüntüsü 2026-05-23 220626" src="https://github.com/user-attachments/assets/8d6e7841-0d3f-41e8-9228-a77bb0f10c62" />

- Bu ekran çıktıktan sonra bu pencereyi küçültelim ve diğer terminal penceresine geçelim.

## Routerimize terminalden bağlanalım
- İkinci terminal penceresinden routerimize bağlanalım.

```
telnet 192.168.31.1/miwifi.com
```

* User: `root`
* Password: `root`
## openwrt frimware.bin dosyasını routerimizin tmp dosyasının içine atalım
```
cd /tmp
wget http://Kendi ip adresiniz:8000/openwrt frimware.bin
```
<img width="804" height="447" alt="Ekran görüntüsü 2026-05-23 222953" src="https://github.com/user-attachments/assets/5af9ce51-67b6-4628-9ad3-58a74fce8518" />

- Bu şekilde dosyayı attıktan sonra ls komutunu yapıştırın ve dosyayı atmışmı diye kontrol edelim.

<img width="801" height="446" alt="Ekran görüntüsü 2026-05-23 223204" src="https://github.com/user-attachments/assets/9b002352-d5a3-41e2-8e56-6740f19dcce8" />

- openwrt frimware.bin dosyasının atmış olduk.
## openwrt frimware.bin dosyasını flashlayalım
```
mtd -e OS1 -r write openwrt frimware.bin OS1

```
<img width="805" height="453" alt="Ekran görüntüsü 2026-05-23 223928" src="https://github.com/user-attachments/assets/9be4827b-b3eb-44c9-ae55-d3faa28f3396" />

- Bağlantı koptuktan sonra routerda mavi ışık yanıp sönücektir 192.168.1.1 adresine giderek yazılımın kurulup kurulmadığını öğrenebilirsiniz.

  
  
