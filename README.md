# Awtrix – Wyświetlanie danych z czujnika

Blueprint dla Home Assistant do automatycznego wyświetlania danych z czujników na urządzeniu AWtrix przez MQTT.

## Opis

Ten blueprint umożliwia łatwe tworzenie automatyzacji, która publikuje wartości z czujników Home Assistant (np. temperatura, wilgotność) do urządzenia AWtrix za pomocą protokołu MQTT. Blueprint oferuje pełną konfigurację GUI bez konieczności ręcznego pisania YAML.

## Funkcje

- 📊 **Wyświetlanie danych z czujników** - automatyczna publikacja wartości czujnika
- 🎨 **Konfigurowalna ikona** - wybór ikony AWtrix do wyświetlenia
- 🔄 **Liczba powtórzeń** - kontrola, ile razy komunikat ma się wyświetlić
- 🔤 **Opcje formatowania tekstu** - wielkie litery, przewijanie
- 🎭 **Wybór czcionki** - różne style czcionek AWtrix
- ⚙️ **Proste GUI** - wszystkie opcje dostępne przez interfejs graficzny

## Instalacja

1. Skopiuj plik `dzieju.yaml` do folderu `blueprints/automation` w katalogu konfiguracyjnym Home Assistant
2. W Home Assistant przejdź do: **Ustawienia** → **Automatyzacje i sceny** → **Blueprinty**
3. Kliknij **Importuj Blueprint** i wybierz skopiowany plik

Alternatywnie, możesz zaimportować blueprint bezpośrednio przez URL:
```
https://github.com/dzieju/awtrix/blob/main/dzieju.yaml
```

## Użycie

1. Przejdź do **Ustawienia** → **Automatyzacje i sceny**
2. Kliknij **Utwórz automatyzację** → **Użyj blueprintu**
3. Wybierz "Awtrix – Wyświetlanie danych z czujnika"
4. Skonfiguruj poniższe opcje:

### Parametry konfiguracji

#### Czujnik źródłowy
Wybierz encję czujnika, którego wartość chcesz wyświetlić na AWtrix (np. `sensor.temperature_bedroom`).

#### Temat MQTT
Temat MQTT dla Twojego urządzenia AWtrix. Format: `awtrix_[ID]/custom/[nazwa]`
Przykład: `awtrix_664dc4/custom/sypialnia`

#### ID ikony
Numer ikony AWtrix do wyświetlenia. Domyślnie: `1447`
Możesz znaleźć dostępne ikony na: https://developer.lametric.com/icons

#### pushIcon
Wartość pushIcon określa sposób wyświetlania ikony:
- `0` = nie nadpisuj bieżącej ikony
- `2` = nadpisz bieżącą ikonę (domyślnie)

#### Liczba powtórzeń
Ile razy komunikat ma się wyświetlić na AWtrix. Zakres: 1-10, domyślnie: 1

#### Wielkie litery
Czy tekst ma być pisany wielkimi literami. Domyślnie: włączone

#### Bez przewijania
Czy tekst ma być statyczny (bez przewijania). Domyślnie: wyłączone

#### ID czcionki
Numer czcionki AWtrix:
- `0` = czcionka domyślna
- `1-5` = inne dostępne czcionki

## Przykład działania

Po skonfigurowaniu automatyzacji:
1. Każda zmiana wartości czujnika uruchamia automatyzację
2. Aktualna wartość czujnika (np. "23°C") jest publikowana do AWtrix przez MQTT
3. AWtrix wyświetla wartość z wybraną ikoną i konfiguracją

## Format wiadomości MQTT

Blueprint generuje JSON payload w formacie:
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

## Wymagania

- Home Assistant z zainstalowaną integracją MQTT
- Skonfigurowane urządzenie AWtrix
- Działające połączenie MQTT między Home Assistant a AWtrix

## Rozwiązywanie problemów

### Automatyzacja się nie uruchamia
- Sprawdź, czy czujnik faktycznie zmienia wartość
- Zweryfikuj poprawność tematu MQTT
- Upewnij się, że połączenie MQTT działa

### AWtrix nie wyświetla danych
- Sprawdź logi MQTT w Home Assistant
- Zweryfikuj format tematu MQTT dla Twojego urządzenia
- Upewnij się, że AWtrix jest połączony z brokerem MQTT

### Nieprawidłowe formatowanie tekstu
- Sprawdź ustawienia czcionki i opcje tekstu
- Zweryfikuj, czy wartość czujnika jest prawidłowa

## Licencja

MIT

## Autor

Grzegorz Ciekot (dzieju)
