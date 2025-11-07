# 🔌 Geliştirilmiş Akıllı Ev Sistemi - Bağlantı Şeması

## 📋 Gerekli Malzemeler

### ESP8266 NodeMCU İçin:
- ESP8266 NodeMCU
- DHT22 Sıcaklık/Nem Sensörü
- PIR Hareket Sensörü
- Yangın Sensörü (Flame Sensor)
- LDR (Işık Sensörü)
- Servo Motor (SG90)
- Röle Modülü
- LED
- Buzzer
- Direnç (10kΩ, 220Ω)

### Arduino Uno İçin:
- Arduino Uno R3
- MFRC522 RFID Okuyucu Modülü
- MQ-2 Gaz Sensörü Modülü
- DC Fan Motor
- L293D Motor Sürücü (veya transistör BC547)
- Direnç (1kΩ)

---

## 🔗 ESP8266 NodeMCU Bağlantıları

### DHT22 Sıcaklık/Nem Sensörü
```
DHT22 VCC    → 3.3V (ESP8266)
DHT22 GND    → GND (ESP8266)
DHT22 DATA   → D2 (GPIO4)
```

### PIR Hareket Sensörü
```
PIR VCC      → 5V (ESP8266 VIN)
PIR GND      → GND (ESP8266)
PIR OUT      → D5 (GPIO14)
```

### Yangın Sensörü (Flame Sensor)
```
FLAME VCC    → 3.3V (ESP8266)
FLAME GND    → GND (ESP8266)
FLAME DO     → D7 (GPIO12)
```

### LDR (Işık Sensörü)
```
LDR bir ucu  → 3.3V (ESP8266)
LDR diğer uç → A0 (ESP8266) ve 10kΩ direnç → GND
```

### Servo Motor
```
SERVO VCC    → 5V (ESP8266 VIN veya harici 5V)
SERVO GND    → GND (ESP8266)
SERVO Signal → D4 (GPIO2)
```

### Röle Modülü
```
RÖLE VCC     → 5V (ESP8266 VIN)
RÖLE GND     → GND (ESP8266)
RÖLE IN      → D0 (GPIO16)
```

### LED
```
LED (+)      → 220Ω direnç → D1 (GPIO5)
LED (-)      → GND (ESP8266)
```

### Buzzer
```
BUZZER (+)   → D8 (GPIO15)
BUZZER (-)   → GND (ESP8266)
```

### Arduino Uno ile Haberleşme
```
ESP8266 TX   → Arduino RX (Pin 0)
ESP8266 RX   → Arduino TX (Pin 1)
ESP8266 GND  → Arduino GND (ORTAK GND ÖNEMLİ!)
```

---

## 🔗 Arduino Uno Bağlantıları

### MFRC522 RFID Okuyucu (SPI Bağlantısı)
```
RFID VCC     → 3.3V (Arduino)
RFID GND     → GND (Arduino)
RFID RST     → Pin 9 (Arduino)
RFID SDA/SS  → Pin 10 (Arduino)
RFID MOSI    → Pin 11 (Arduino)
RFID MISO    → Pin 12 (Arduino)
RFID SCK     → Pin 13 (Arduino)
```

### MQ-2 Gaz Sensörü
```
MQ-2 VCC     → 5V (Arduino)
MQ-2 GND     → GND (Arduino)
MQ-2 AOUT    → A0 (Arduino)
```

### DC Fan Motor (L293D Motor Sürücü ile)
```
L293D Pin 1 (Enable)   → Pin 3 (Arduino PWM)
L293D Pin 2 (Input 1)  → 5V (Arduino)
L293D Pin 3 (Output 1) → Fan (+)
L293D Pin 4-5 (GND)    → GND (Arduino)
L293D Pin 6 (Output 2) → Fan (-)
L293D Pin 7 (Input 2)  → GND (Arduino)
L293D Pin 8 (VCC2)     → Harici 5-12V (Fan gücü)
L293D Pin 16 (VCC1)    → 5V (Arduino)
```

**Alternatif - Transistör BC547 ile (Basit Çözüm):**
```
Arduino Pin 3 → 1kΩ direnç → BC547 Base
BC547 Collector → Fan (-)
BC547 Emitter → GND
Fan (+) → Harici 5-12V
```

### ESP8266 ile Haberleşme
```
Arduino TX (Pin 1)  → ESP8266 RX
Arduino RX (Pin 0)  → ESP8266 TX
Arduino GND         → ESP8266 GND (ORTAK GND!)
```

---

## ⚠️ ÖNEMLİ NOTLAR

### 1. Güç Kaynağı
- **ESP8266**: USB'den beslenmeli (5V) veya harici 5V adaptör
- **Arduino Uno**: USB'den beslenmeli (5V) veya harici 7-12V adaptör
- **Ortak GND**: ESP8266 ve Arduino'nun GND'leri mutlaka birbirine bağlanmalı!

### 2. Voltaj Seviyeleri
- ESP8266 pinleri **3.3V** mantık seviyesinde çalışır
- Arduino Uno pinleri **5V** mantık seviyesinde çalışır
- **Seri haberleşme için**: ESP8266 RX pinine bir voltaj bölücü (1kΩ + 2kΩ direnç) kullanın veya mantık seviyesi çevirici kullanın

### 3. Seri Haberleşme Voltaj Uyumu
```
Arduino TX (5V) → 1kΩ direnç → ESP8266 RX
                ↓
             2kΩ direnç
                ↓
               GND

ESP8266 TX (3.3V) → Arduino RX (Direnç gerekmez, Arduino 3.3V'u okuyabilir)
```

### 4. Fan Motor
- DC motor yüksek akım çeker, Arduino'dan doğrudan bağlamayın
- Mutlaka motor sürücü veya transistör kullanın
- Harici güç kaynağı kullanılmalı (5-12V, motorun özelliklerine göre)

### 5. RFID Modülü
- RFID modülü 3.3V ile çalışır, 5V vermeyın!
- SPI bağlantılarını doğru yapın
- SS pinini (Pin 10) başka amaçla kullanmayın

### 6. Servo Motor
- Servo motor yüksek akım çeker
- Harici 5V güç kaynağı kullanmanız önerilir
- GND'ler ortak olmalı

### 7. Web Arayüz Erişimi
- ESP8266'nın IP adresini seri monitörden okuyun
- Tarayıcıda bu IP adresini yazarak arayüze erişin
- Örnek: http://192.168.1.100

---

## 🎯 Çalışma Mantığı

### Fan Modları:
1. **Manuel Mod (0)**: Web arayüzden açma/kapama
2. **Sıcaklık Modu (1)**: 
   - 28°C altında: Fan kapalı
   - 28-30°C: Düşük hız
   - 30-33°C: Orta hız
   - 33°C+: Yüksek hız
3. **Gaz Sensörü Modu (2)**:
   - 400 altında: Fan kapalı
   - 400-500: Düşük hız
   - 500-600: Orta hız
   - 600+: Yüksek hız

### Veri Akışı:
```
Arduino → (Gaz, RFID, Fan Durumu) → ESP8266
ESP8266 → (Fan Modu, Fan Komutu, Sıcaklık) → Arduino
ESP8266 → (Tüm Veriler) → Web Arayüzü
```

---

## 🔧 Test Adımları

1. **Arduino Testi**: Arduino kodunu yükleyin, seri monitörden veri akışını kontrol edin
2. **ESP8266 Testi**: ESP8266 kodunu yükleyin, WiFi'ye bağlanıp IP almasını bekleyin
3. **Haberleşme Testi**: İki kart arasında veri alışverişini kontrol edin
4. **Web Arayüz Testi**: Tarayıcıdan IP adresine erişin, tüm fonksiyonları test edin
5. **Sensör Testleri**: Her sensörü tek tek test edin
6. **Fan Modları Testi**: Her fan modunu test edin

---

## 📚 Kütüphane Gereksinimleri

### ESP8266 için:
- ESP8266WiFi (Arduino IDE ile gelir)
- ESP8266WebServer (Arduino IDE ile gelir)
- DHT sensor library (Adafruit)
- Servo (Arduino IDE ile gelir)

### Arduino Uno için:
- MFRC522 (RFID kütüphanesi)
- SPI (Arduino IDE ile gelir)

**Kütüphane Kurulumu**: Arduino IDE → Tools → Manage Libraries → Kütüphane adını arayın ve yükleyin
