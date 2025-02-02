# GrowBox
Node-RED Flow to Control a hydroponic grow box

---

### **Projektbeschreibung**
Das Node-RED-Projekt automatisiert die Steuerung und Überwachung einer Growbox mit einem hydroponischen Ebbe-Flut-System. Die angeschlossenen Geräte wie Wasserpumpen, Lüfter und Beleuchtung werden über ZigBee-Steckdosen gesteuert. Zwei ESP32-Boards erfassen Klimadaten (Temperatur, Luftfeuchtigkeit, Lichtstärke) sowie Parameter der Nährlösung (Temperatur, Füllstand, EC-Wert). Node-RED dient als zentrale Plattform für Steuerung, Visualisierung und Datenlogging.

---

### **Funktionen**
#### **1. Steuerung der Geräte über ZigBee-Steckdosen**
- Alle Geräte (z. B. Wasserpumpe, Lüfter, Beleuchtung) sind an ZigBee-fähige Steckdosen angeschlossen.
- Node-RED kommuniziert über ein ZigBee-Gateway (Deconz oder ein anderes kompatibles System) mit den Steckdosen.
- Geräte können basierend auf Zeitplänen oder Sensordaten automatisch ein- und ausgeschaltet werden.
  - **Beispiel:** Die Wasserpumpe wird in definierten Intervallen aktiviert, um das Ebbe-Flut-System zu betreiben.

#### **2. Klimadatenüberwachung**
- Die ESP32-Boards messen Temperatur und Luftfeuchtigkeit in der Growbox und senden die Daten per MQTT oder HTTP an Node-RED.
- Node-RED visualisiert die Klimadaten in einem Dashboard und ermöglicht die Konfiguration von Schwellwerten.
  - **Beispiel:** Bei zu hoher Temperatur oder zu hoher Luftfeuchtigkeit wird der Lüfter über eine ZigBee-Steckdose aktiviert.

#### **3. Nährlösungsmanagement**
- Sensoren messen den Füllstand, die Temperatur und die elektrische Leitfähigkeit (EC) der Nährlösung.
- Die Werte werden in Echtzeit an Node-RED übertragen und im Dashboard angezeigt.
  - **Beispiel:** Bei Überschreiten einer vorgegebenen Temperatur wird davon ausgegangen, das sich zu wenig Nährlösung im Tank befindet. Die Heizung wird ausgeschaltet. Diese Funktion kann abgeschaltet werden um z.B. bei der Anzucht eine Heizmatte mit eigener Regelung an der Heizungssteckdose zu betreiben.

#### **4. Benutzeroberfläche**
- Node-RED bietet ein übersichtliches Dashboard zur Steuerung und Überwachung:
  - Anzeige von Klimadaten, Gerätezuständen und Nährstoffüberwachung. Grafische Darstellung mit vpdchart.
  - Manuelle Steuerung der ZigBee-Steckdosen (z. B. zum Testen von Geräten).
  - Anpassung von Zeitplänen für Beleuchtung, Bewässerung und Lüftung.

#### **5. Automatisierung & Alarme**
- Automatische Steuerung basierend auf Sensordaten:
  - Aktivierung des Lüfters bei hoher Luftfeuchtigkeit.
  - Anpassung der Beleuchtungsdauer je nach Wachstumsphase.
  - Regelmäßige Aktivierung der Pumpe für das Ebbe-Flut-System.
- Pushover Alarme bei kritischen Werten sind geplant.

#### **6. Datenlogging**
- Alle Messwerte (Temperatur, Luftfeuchtigkeit, pH-Wert, EC-Wert) können im Verlauf angesegen werden.
- Eine Langzeitspeicherung in einer InfluxDB ist geplant um langfristig das Pflanzenwachstum zu optimieren.

---

### **Hardwareanforderungen**
1. **ZigBee-Komponenten**:
   - ZigBee-Steckdosen und USB-Schalter zur Steuerung von Pumpen, Lüftern und Beleuchtung.
   - Ein ZigBee-Gateway (z. B. Deconz, Zigbee2MQTT mit einem CC2531-Stick oder Sonoff Zigbee Bridge).
2. **ESP32-Mikrocontroller**:
   - Für die Messung von Klimawerten und Tanküberwachung mit installiertem Tasmota.
3. **Sensoren**:
   - BME280 für Temperatur und Luftfeuchtigkeit, BH1750 für die Lichtstärke.
   - konduktive Füllstandsmessung, wasserdichter DS18B20  und EC-Sensor für die Nährlösung.
4. **Server für Node-RED**:
   - Raspberry Pi oder ein anderer Server mit installiertem Node-RED.
   - Node-RED Erweiterungen
5. **Growbox**:
   - einen ausreichend hohen Schrank um einen Tank, den Ebbe-Flut-Tisch und die Elektroinstallation aufzunehmen.
---

### **Vorteile des Systems**
- **Flexibilität:** Geräte können kabellos über ZigBee gesteuert werden.
- **Energieeffizienz:** Automatische Steuerung reduziert unnötigen Energieverbrauch.
- **Präzision:** Sensordaten ermöglichen eine optimale Anpassung an die Bedürfnisse der Pflanzen.
- **Benutzerfreundlichkeit:** Intuitive Bedienung über das Node-RED-Dashboard.
- **Skalierbarkeit:** Das System kann leicht um weitere Sensoren oder Geräte erweitert werden.

---

Dieses Projekt kombiniert moderne IoT-Technologien wie ZigBee mit hydroponischer Präzision, um eine effiziente und benutzerfreundliche Lösung für den Betrieb einer Growbox zu schaffen!

### **Project Description**  
The Node-RED project automates the control and monitoring of a grow box equipped with a hydroponic ebb and flow system. Connected devices such as water pumps, fans, and lighting are controlled via ZigBee smart plugs. Two ESP32 boards collect climate data (temperature, humidity, light intensity) as well as nutrient solution parameters (temperature, level, EC value). Node-RED serves as the central platform for control, visualization, and data logging.

---

### **Features**  

#### **1. Device Control via ZigBee Smart Plugs**  
- All devices (e.g., water pump, fan, lighting) are connected to ZigBee-enabled smart plugs.  
- Node-RED communicates with the plugs via a ZigBee gateway (e.g., Deconz or another compatible system).  
- Devices can be automatically switched on and off based on schedules or sensor data.  
  - **Example:** The water pump is activated at defined intervals to operate the ebb and flow system.  

#### **2. Climate Monitoring**  
- The ESP32 boards measure temperature and humidity inside the grow box and send the data to Node-RED via MQTT or HTTP.  
- Node-RED visualizes the climate data in a dashboard and allows configuration of thresholds.  
  - **Example:** If the temperature or humidity exceeds a set threshold, the fan is activated via a ZigBee smart plug.  

#### **3. Nutrient Solution Management**  
- Sensors measure the level, temperature, and electrical conductivity (EC) of the nutrient solution.  
- The values are transmitted to Node-RED in real time and displayed on the dashboard.  
  - **Example:** If the temperature exceeds a predefined value, it is assumed that there is insufficient nutrient solution in the tank. The heater is turned off. This function can be disabled to allow a heat mat with its own controller to operate on the heater's smart plug during seedling propagation.  

#### **4. User Interface**  
- Node-RED provides an intuitive dashboard for control and monitoring:  
  - Display of climate data, device statuses, and nutrient monitoring with graphical representation using vpdchart.  
  - Manual control of ZigBee smart plugs (e.g., for testing devices).  
  - Adjustment of schedules for lighting, irrigation, and ventilation.  

#### **5. Automation & Alerts**  
- Automatic control based on sensor data:  
  - Fan activation when humidity is high.  
  - Adjustment of lighting duration depending on growth phase.  
  - Regular activation of the pump for the ebb and flow system.  
- Pushover alerts for critical values are planned.  

#### **6. Data Logging**  
- All measured values (temperature, humidity, pH value, EC value) can be viewed over time.  
- Long-term storage in an InfluxDB is planned to optimize plant growth over time.

---

### **Hardware Requirements**  

1. **ZigBee Components**:  
   - ZigBee smart plugs and USB switches for controlling pumps, fans, and lighting.  
   - A ZigBee gateway (e.g., Deconz, Zigbee2MQTT with a CC2531 stick, or Sonoff Zigbee Bridge).  

2. **ESP32 Microcontrollers**:  
   - For measuring climate values and tank monitoring. Tasmota for connection via WiFi.

3. **Sensors**:  
   - BME280 for temperature and humidity; BH1750 for light intensity.
   - Conductive level sensor, waterproof DS18B20, and EC sensor for nutrient solution monitoring.

4. **Server for Node-RED**:  
   - Raspberry Pi or another server running Node-RED.
   - Node-RED extensions.

5. **Grow Box**:  
   - A sufficiently tall cabinet to house a tank, ebb-and-flow table, and electrical installation.

---

### **System Advantages**  

- **Flexibility:** Devices can be wirelessly controlled via ZigBee.  
- **Energy Efficiency:** Automated controls reduce unnecessary energy consumption.  
- **Precision:** Sensor data allows optimal adjustments to plant needs.  
- **User-Friendliness:** Intuitive operation through the Node-RED dashboard.  
- **Scalability:** The system can be easily expanded with additional sensors or devices.

---

This project combines modern IoT technologies like ZigBee with hydroponic precision to create an efficient and user-friendly solution for operating a grow box!

Quellen

