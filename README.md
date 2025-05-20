# Cybersecurity-Projects
# Projekt 01: Zabezpieczenie systemu Linux

## 📌 Opis projektu

Ten projekt koncentruje się na podstawowych krokach zabezpieczania systemu Linux. Obejmuje aktualizacje systemu, zarządzanie użytkownikami i grupami, oraz monitorowanie usług.

## 🎯 Cel projektu

- Zrozumienie podstawowych mechanizmów bezpieczeństwa w systemie Linux.
- Praktyczne zastosowanie poleceń związanych z zarządzaniem systemem.
- Przygotowanie środowiska do dalszych projektów z zakresu cyberbezpieczeństwa.

## 🛠️ Środowisko

- **System operacyjny:** Ubuntu 22.04 LTS
- **Użytkownik:** adam
- **Uprawnienia:** sudo

## 🧪 Wykonane kroki

1. **Aktualizacja systemu:**
   - `sudo apt update`
   - `sudo apt upgrade`
2. **Przegląd użytkowników i grup:**
   - `cat /etc/passwd`
   - `cat /etc/group`
3. **Sprawdzenie aktywnych usług:**
   - `systemctl list-units --type=service --state=running`
4. **Monitorowanie połączeń sieciowych:**
   - `ss -tuln`
5. **Sprawdzenie statusu SSH:**
   - `sudo systemctl status ssh`

## 📸 Zrzuty ekranu


## 📚 Wnioski

- Poznałem podstawowe polecenia związane z aktualizacją i monitorowaniem systemu Linux.
- Zrozumiałem strukturę plików `/etc/passwd` i `/etc/group`.
- Nauczyłem się identyfikować aktywne usługi i połączenia sieciowe.

## 📁 Dodatkowe materiały

- Szczegółowe notatki i wyjaśnienia znajdują się w katalogu `docs/`.
- Przykładowe pliki konfiguracyjne i dane testowe w katalogu `examples/`.

## 📄 Licencja

Ten projekt jest udostępniony na licencji MIT. Szczegóły w pliku `LICENSE`.
