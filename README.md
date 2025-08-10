# STM32 ADC + DMA Örneği

![Potansiyometre Bağlantısı](https://github.com/user-attachments/assets/7465c22f-0b0e-49c8-9eb2-2cf86cc4704e)

Bu proje, **STM32** mikrodenetleyicisi üzerinde **ADC (Analog to Digital Converter)** ile **DMA (Direct Memory Access)** kullanarak **Channel 0** ve dahili **VREFINT** kanalından veri okuma işlemini gerçekleştirir.  
DMA sayesinde ADC verileri kesintisiz olarak bir diziye aktarılır ve LED'ler üzerinden dönüşüm durumları gösterilir.

---

## 📌 Özellikler
- **ADC Channel 0** (PA0 pini üzerinden analog giriş)
- **Dahili VREFINT** ölçümü
- **DMA** ile çift kanal verisinin kesintisiz aktarımı
- **Half Complete** ve **Complete** callback'lerinde LED yakma/söndürme
- **GPIOD Pin 12** ve **Pin 15** LED kontrolü

---

## 🔧 Donanım Bağlantıları
| ADC Kanalı | Pin   | Açıklama                  |
|------------|-------|---------------------------|
| Channel 0  | PA0   | Harici analog giriş pini  |
| VREFINT    | Dahili| MCU'nun dahili referans voltajı |

---

## ⚙️ Çalışma Mantığı
1. `HAL_ADC_Start_DMA()` fonksiyonu ile ADC + DMA başlatılır.
2. DMA, **2 adet veri** (`adcData[0]` ve `adcData[1]`) okur:
   - `adcData[0]` → **Channel 0**
   - `adcData[1]` → **VREFINT**
3. **Half Transfer** tamamlandığında `HAL_ADC_ConvHalfCpltCallback()` çalışır ve **PD12 LED'i yakılır**.
4. **Full Transfer** tamamlandığında `HAL_ADC_ConvCpltCallback()` çalışır ve **PD15 LED'i yakılır**.
5. Ana döngüde (`while(1)`), `flag` kontrol edilerek güncel ADC değerleri değişkenlere atanır.

---
## 🛠️ Geliştirme Ortamı
- **MCU**: STM32F4 Serisi (örnek: STM32F407)
- **IDE**: STM32CubeIDE
- **HAL Kütüphanesi** kullanıldı

---

## 🚀 Kullanım
1. Projeyi **STM32CubeIDE** ile açın.
2. Donanım bağlantılarını tabloya göre yapın.
3. Kodları derleyip karta yükleyin.
4. LED'ler üzerinden ADC veri akışını gözlemleyin.

---

## 📜 Lisans
Bu proje, STM32CubeIDE ile oluşturulmuş örnek bir uygulamadır ve **eğitim amaçlı** kullanılabilir.
