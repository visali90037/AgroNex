 # AgroNex: Integrated Soil Analytics and Precision Crop Management

> Soil sensors and drone imagery, analysed together by deep learning, give farmers one simple report in their own language.

---

## Overview

Indian soils have been cultivated for generations with little replenishment, and excess fertilizer can create micronutrient imbalance that harms crops. Plant diseases add yearly losses of 15–20% in major crops. Soil testing and crop monitoring are usually separate, costly and technical, so problems are found late.

**AgroNex** joins the two. In-field soil sensors measure the condition of the soil, an autonomous drone photographs the crop, and deep-learning models combine both to detect disease and weeds, check nutrient balance, and predict growth and harvest time. The farmer gets charts, alerts and remedies in a mobile app, in a regional language.

## Key features

- **Soil + crop in one report:** moisture, NPK, temperature and humidity readings analysed together with drone images of the same field.
- **Disease, weed and growth detection:** CNN-based image analysis.
- **Nutrient advice:** checks whether soil nutrients are balanced and suggests corrections.
- **Growth and harvest prediction** from soil and image data.
- **Automatic irrigation:** the soil unit switches a mini pump when moisture is too low.
- **Farmer-friendly:** the drone is switched on in the field; no technical steps are needed. The app supports regional languages.

## How it works

```mermaid
flowchart TD
    A[Drone captures geotagged crop images] --> B[Pre-processing: OpenCV, scikit-image]
    C[ESP32 soil node: moisture, NPK, temperature, humidity] --> D[Cloud: MySQL on AWS]
    B --> E[CNN analysis: disease, weeds, growth stage]
    D --> F[Soil analysis: nutrient balance]
    E --> G[Data fusion and report generation]
    F --> G
    G --> H[Mobile app: charts, alerts, remedies in regional language]
    C -->|moisture low| I[Relay + mini pump]
```

1. Soil sensors send readings to the cloud through the ESP32.
2. The drone surveys the field and captures geotagged images.
3. Images are pre-processed (morphological, Gaussian and wavelet methods) and analysed by CNN models.
4. The server combines image results with soil data and generates the report.
5. The app shows the report, alerts, remedies and growth forecast.

## Tech stack

| Area | Technologies |
|---|---|
| Image processing | OpenCV, scikit-image, Pillow, NumPy (morphological, Gaussian, wavelet) |
| Deep learning | TensorFlow, Keras; CNN with transfer learning; GAN for synthetic training images |
| Embedded / IoT | ESP32, Arduino IDE, MQTT over Wi-Fi |
| Data / cloud | MySQL, AWS |
| Hardware | Autonomous drone with camera and GPS; soil moisture, NPK and DHT11 sensors; relay and mini pump; 20×4 LCD |
| App | Mobile application with charts, alerts and regional-language support |

## Prototype hardware (soil monitoring unit)

| Component | Cost (₹) |
|---|---|
| ESP32 | 750 |
| DHT11 sensor | 100 |
| Mini water pump | 200 |
| RS485 to TTL converter | 75 |
| SPDT relay | 40 |
| 20×4 LCD | 500 |
| Soil moisture sensor | 500 |
| Soil NPK sensor | 5,000 |
| **Total** | **7,165** |

The drone components are budgeted at about ₹39,550, giving a prototype cost of about **₹46,715**. The full project is estimated at ₹5.5 lakh over about 180 days.

## Project status

- [x] Concept and idea submission
- [x] Soil-sensor node built and under testing (ESP32, moisture sensor, LCD)
- [ ] Drone platform: field-survey flights and image capture
- [ ] CNN models for disease and weed detection
- [ ] Cloud pipeline and data fusion
- [ ] Mobile app with regional-language support
- [ ] Field testing

## Repository structure

> Update this to match your actual folders.

```
AgroNex/
├── firmware/        # ESP32 code (Arduino IDE)
├── ml/              # Image processing and CNN training notebooks
├── backend/         # Cloud services and database
├── app/             # Mobile application
├── docs/            # Concept document, slides, diagrams
└── images/          # Prototype photos
```

## Getting started

```bash
# Clone the repository
git clone https://github.com/visali90037/AgroNex.git
cd AgroNex

# ML environment
pip install tensorflow keras opencv-python scikit-image pillow numpy
```

For the firmware, open the sketch in `firmware/` with the Arduino IDE, select your ESP32 board, set your Wi-Fi and MQTT details, and upload.

## Risks and planned mitigation

| Risk | Mitigation |
|---|---|
| Wind affects drone control and flight path | Fly in suitable weather; GPS path correction |
| Weak signal in bad weather | Buffer data on the node and upload when signal returns |
| Poor light gives low-quality images | Gaussian and wavelet enhancement; repeat capture |
| Limited disease images for training | Transfer learning, GAN images, build a field dataset over time |

## Future scope

- Voice and WhatsApp alerts in local languages
- LoRa and solar-powered sensor nodes for remote fields
- TinyML on the ESP32 and edge AI on the drone
- Spot spraying of only the affected patches
- Multispectral (NDVI) imaging for early stress detection

## Team

**Team AgroNex**

| Name | Role |
|---|---|
| _Add member_ | _Role_ |

**Mentor:** Dr. Pachhaiammal Priya M

## References

1. Gheorghe C., Deac T.A., Filip N. (2019). *Image Processing Techniques Used in Soil Moisture Analysis.* DOI: 10.35633/INMATEH-58-16
2. Goap A., Sharma D., Shukla A.K., Krishna C.R. (2018). *An IoT based smart irrigation management system using Machine Learning and open source technologies.*
3. Kansal K., Gupta T., Singh A., Majumdar R. (2019). *Image Processing of Vegetables and Predicting Disease.* ISSN: 2278-3075
4. Kurtulmus E., Arslan B., Kurtulmus F. (2022). *Deep learning for proximal soil sensor development towards smart irrigation.*
5. Hafeez A., Husain M.A., Singh S.P., Chauhan A., Khan M.T., Soni S.K. (2022). *Implementation of drone technology for farm monitoring and pesticide spraying.*
