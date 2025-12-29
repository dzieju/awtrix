# AWTRIX Blueprint - GUI Interface Overview

This document describes the graphical user interface that users will see when creating an automation using this blueprint in Home Assistant.

## Blueprint Selection Screen

When users go to create a new automation, they will see:

**Name:** Awtrix – Wyświetlanie danych z czujnika

**Description:** Publikuje wartość encji czujnika do AWtrix przez MQTT z konfigurowalną ikoną, liczbą powtórzeń, czcionką i opcjami tekstu (wielkie litery / brak przewijania).

## Configuration Interface

After selecting the blueprint, users will see a form with the following fields:

### 1. Czujnik źródłowy (Source Sensor)
- **Type:** Entity Dropdown
- **Description:** Wybierz encję czujnika (np. temperatury, wilgotności)
- **Interface:** Searchable dropdown showing all sensors in Home Assistant
- **Example:** `sensor.bedroom_temperature`

### 2. Temat MQTT (MQTT Topic)
- **Type:** Text Input
- **Description:** Temat MQTT dla Twojego urządzenia AWtrix (np. awtrix_664dc4/custom/sypialnia)
- **Interface:** Single-line text box
- **Example:** `awtrix_664dc4/custom/sypialnia`

### 3. ID ikony (Icon ID)
- **Type:** Text Input
- **Default Value:** "1447"
- **Description:** Numer ikony AWtrix (np. 1447)
- **Interface:** Single-line text box
- **Example:** `1447` or `a7890`

### 4. pushIcon
- **Type:** Slider
- **Default Value:** 2
- **Range:** 0 to 2
- **Description:** Wartość pushIcon (0 = nie nadpisuj, 2 = nadpisz)
- **Interface:** Horizontal slider with markers at 0, 1, and 2

### 5. Liczba powtórzeń (Repeat Count)
- **Type:** Number Input
- **Default Value:** 1
- **Range:** 1 to 10
- **Description:** Ile razy ma się wyświetlić komunikat
- **Interface:** Number box with +/- buttons

### 6. Wielkie litery (Uppercase)
- **Type:** Toggle Switch
- **Default Value:** ON (true)
- **Description:** Czy tekst ma być pisany wielkimi literami
- **Interface:** Toggle switch (ON/OFF)

### 7. Bez przewijania (No Scroll)
- **Type:** Toggle Switch
- **Default Value:** OFF (false)
- **Description:** Czy tekst ma być statyczny (bez przewijania)
- **Interface:** Toggle switch (ON/OFF)

### 8. ID czcionki (Font ID)
- **Type:** Number Input
- **Default Value:** 0
- **Range:** 0 to 5
- **Description:** Numer czcionki AWtrix (np. 0 = domyślna)
- **Interface:** Number box with +/- buttons

## Example Configuration

Here's what a completed configuration might look like:

```
Czujnik źródłowy: sensor.bedroom_temperature
Temat MQTT: awtrix_664dc4/custom/sypialnia
ID ikony: 1447
pushIcon: ●━━ (2)
Liczba powtórzeń: 1
Wielkie litery: ✓ ON
Bez przewijania: ✗ OFF
ID czcionki: 0
```

## Generated Automation Behavior

When configured and saved, the automation will:

1. **Trigger:** Activate whenever the selected sensor value changes
2. **Action:** Publish an MQTT message to the specified topic with the following JSON payload:
   ```json
   {
     "text": "23°C",
     "icon": "1447",
     "pushIcon": 2,
     "repeat": 1,
     "noScroll": false,
     "uppercase": true,
     "font": 0
   }
   ```
3. **Mode:** Restart (if the sensor changes rapidly, restart the automation)

## Advantages of GUI Configuration

✅ **No YAML Knowledge Required** - Users configure everything through dropdown menus, sliders, and toggles

✅ **Validation** - Home Assistant validates inputs automatically (entity must exist, numbers within range, etc.)

✅ **Easy Updates** - Users can modify configuration anytime through the same GUI

✅ **Reusable** - Create multiple automations for different sensors/rooms using the same blueprint

✅ **Error Prevention** - No syntax errors from manual YAML editing

✅ **Visual Feedback** - Clear labels and descriptions guide users through configuration
