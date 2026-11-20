# Gasnący Płomień

Gra 2D w stylu soulslike, z widokiem z boku jak w Castlevanii, w mrocznej, sakralnej stylistyce pixel-art. Ma sześć krain, sześciu bossów, ogniska i dusze. Muzyka jest generowana na żywo w przeglądarce (metal z chórem przy bossach i gotycki ambient w krainach). Gra działa po polsku i po angielsku.

## Wersje

| Wersja | Gdzie | Jak |
|---|---|---|
| **www** | `web/index.html` | Otwórz plik w przeglądarce albo włącz GitHub Pages (niżej). |
| **telefon – aplikacja na Androida (APK)** | budowana automatycznie przez GitHub Actions | Zakładka **Actions → Android APK →** ostatnie uruchomienie → plik `gasnacy-plomien-apk`. |
| **telefon – „aplikacja” z przeglądarki** | GitHub Pages | Otwórz stronę na telefonie → menu przeglądarki → **Dodaj do ekranu głównego**. Działa też na iPhonie i offline. |

### GitHub Pages (granie w przeglądarce pod stałym adresem)
1. **Settings → Pages → Build and deployment → Source: GitHub Actions**.
2. Każdy push do `main` publikuje grę pod adresem `https://<twoj-login>.github.io/<nazwa-repo>/`.

### APK na Androida
- Każdy push do `main` buduje plik APK. Pobierzesz go w **Actions** jako artefakt, który jest dostępny przez 90 dni.
- Tag `v*`, na przykład `git tag v0.2.0 && git push --tags`, dodatkowo tworzy **Release** z plikiem APK do pobrania.
- Na telefonie zezwól na instalację z nieznanych źródeł, a potem otwórz plik APK.
- To wersja *debug*, odpowiednia do testów i do dzielenia się ze znajomymi. Do Google Play potrzebna jest podpisana wersja *release* (AAB) i konto deweloperskie Google Play, które jest płatne jednorazowo.

### Budowanie lokalne (opcjonalnie)
Potrzebujesz Node.js 20, JDK 17 i Android Studio.
```bash
npm install
npm run android:init   # tworzy folder android/ i ustawia orientację poziomą oraz pełny ekran
npm run android:apk    # APK: android/app/build/outputs/apk/debug/app-debug.apk
npm run android:open   # albo otwórz projekt w Android Studio
```
Po każdej zmianie w `web/index.html` uruchom `npm run android:sync`.

### iPhone (App Store)
Capacitor obsługuje też iOS (`npx cap add ios`). Wymaga to jednak komputera Mac z Xcode i płatnego konta Apple Developer, a tych rzeczy nie da się zbudować automatycznie bez dodatkowej konfiguracji. Do tego czasu na iPhonie najprościej grać przez Pages i opcję „Dodaj do ekranu głównego”.

## Sterowanie
- **Klawiatura:**
  - A/D – ruch, Spacja – skok, ↓+Spacja – zeskok z platformy;
  - J – cios, K – ciężki cios;
  - L lub Shift – przewrót;
  - E – Flakon Żaru;
  - F – interakcja;
  - Esc – pauza i ustawienia;
  - 1–6 na ekranie tytułowym – skok do wybranej krainy.
- **Pad:** RB – cios, RT – ciężki cios, A – skok, B – przewrót, X – flakon, Y – interakcja, Start – pauza.
- **Dotyk:** przyciski na ekranie, które pojawiają się automatycznie na telefonie.

## Ustawienia
Język (PL/EN), rozdzielczość renderowania, skalowanie obrazu, pełny ekran, cząsteczki, poświata, kontury postaci, wstrząsy, winieta, licznik FPS, głośność muzyki i efektów, sterowanie dotykowe i przezroczystość przycisków.

## Muzyka
Muzykę generuje kod gry przez Web Audio: chór, organy, dzwony, przesterowane gitary i perkusję. Nie ma w niej żadnych nagrań ani utworów cudzych autorów, więc nie wymaga licencji. Każda kraina ma własny motyw, każdy boss własny riff, a w drugiej fazie walki muzyka przyspiesza.

## Struktura
```
web/                 gra (index.html), manifest, service worker, ikony
assets/              ikona i ekran startowy dla aplikacji
scripts/             dostosowanie projektu Androida
capacitor.config.json
.github/workflows/   automatyczne budowanie APK i publikacja na Pages
```
