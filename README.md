# 🐍 Git + GitHub w PyCharm – ściąga krok po kroku (GUI)

Ta sama instrukcja co wersja z VS Code i terminalem, tylko **klikana w PyCharmie**. Prawie wszystko robisz przyciskami, a terminal jest potrzebny sporadycznie.

> 💡 Nazwy menu mogą się minimalnie różnić zależnie od wersji PyCharma (nowy interfejs vs klasyczny). Jeśli czegoś nie widzisz, użyj wyszukiwarki akcji: **Shift Shift** i wpisz nazwę (np. *Push*).

## 📑 Spis treści

1. [Setup środowiska](#i-setup-środowiska)
2. [Praca na plikach (commit, push)](#ii-praca-na-plikach)
3. [Branche i Pull Requesty](#iii-branche-i-pull-requesty-praca-w-dwie-osoby)
4. [Konflikty](#iv-konflikty-conflict)
5. [Codzienny start](#v-codzienny-start)
6. [Dołączanie do istniejącego projektu](#vi-dołączanie-do-istniejącego-projektu-dla-drugiej-osoby)
7. [Skróty klawiszowe](#vii-skróty-klawiszowe)

---

# I. Setup środowiska

## 1. Instalacja

- Utwórz konto na GitHubie na maila uczelni: https://github.com/
- Zainstaluj:
  - **PyCharm** (wersja Community wystarczy): https://www.jetbrains.com/pycharm/download/
  - **Git:** https://git-scm.com/ (PyCharm sam wykryje, gdzie jest zainstalowany; jeśli nie, wskaż ścieżkę w *Settings → Version Control → Git*)
  - **Python:** https://www.python.org/downloads/

## 2. Konfiguracja Gita

Jeśli przy pierwszym commicie PyCharm zapyta o imię i mail, wpisz swoje dane (te same, co na GitHubie). Możesz też ustawić je raz w terminalu:

```bash
git config --global user.name "Twoje Imię"
git config --global user.email "twoj@email.com"
```

## 3. Logowanie do GitHuba w PyCharmie

1. Otwórz ustawienia:
   - 🪟 **Windows / Linux:** `File → Settings` (`Ctrl+Alt+S`)
   - 🍎 **Mac:** `PyCharm → Settings` (`Cmd+,`)
2. Przejdź do **Version Control → GitHub**.
3. Kliknij **+** → **Log In via GitHub** i zaloguj się w przeglądarce.
4. Zatwierdź. Twoje konto powinno pojawić się na liście.

## 4. Tworzenie projektu i środowiska wirtualnego

1. Na ekranie startowym kliknij **New Project** (albo `File → New Project`).
2. Ustaw:
   - **Location** – folder projektu i jego nazwa,
   - **Interpreter type: Project venv** (albo *Virtualenv*) – PyCharm sam utworzy środowisko `.venv` w folderze projektu,
   - jeśli jest opcja **Create Git repository**, zaznacz ją (inaczej zrobisz to w następnym punkcie).
3. Kliknij **Create**.
4. Sprawdź, że w terminalu PyCharma (`Alt+F12`, Mac: `Option+F12`) po lewej stronie widać `(.venv)`.

## 5. Plik `.gitignore`

1. W drzewie projektu kliknij prawym na główny folder → **New → File** → nazwij `.gitignore`.
2. Wpisz do niego:

   ```text
   .venv/
   __pycache__/
   .idea/
   .DS_Store
   ```

   `.idea/` to ustawienia PyCharma, które są lokalne i nie powinny trafiać do repo. `.DS_Store` to śmieci z macOS.

> Jeśli PyCharm pyta *"Add file to Git?"*, kliknij **Add**.

## 6. Utworzenie repo lokalnie i na GitHubie

1. Jeśli nie zrobiłeś tego przy tworzeniu projektu: menu **Git → Create Git Repository** (w starszych wersjach: `VCS → Enable Version Control Integration → Git`) i wybierz folder projektu.
2. Zrób pierwszy commit (patrz [II.1](#1-pierwszy-commit)), bo bez commita nie da się wrzucić projektu na GitHuba.
3. Wrzuć projekt na GitHuba: menu **Git → GitHub → Share Project on GitHub**.
4. W oknie wpisz **nazwę repo**, zdecyduj, czy ma być **Private** czy publiczne, i kliknij **Share**.
5. Zaznacz pliki do pierwszego wrzucenia, jeśli o to zapyta, i potwierdź.
6. Wejdź na GitHuba w przeglądarce i sprawdź, czy repo się pojawiło.
7. W ustawieniach repo (**Settings → Collaborators**) dodaj drugą osobę.

---

# II. Praca na plikach

## 1. Pierwszy commit

W PyCharmie zamiast `git add` + `git commit` używasz okna **Commit**.

1. Otwórz okno **Commit**:
   - 🪟 **Windows / Linux:** `Alt+0` albo `Ctrl+K`
   - 🍎 **Mac:** `Cmd+0` albo `Cmd+K`
2. Zaznacz checkboxami pliki, które chcesz wrzucić do commita (to odpowiednik `git add`).
3. Wpisz **opis commita** (np. `init`).
4. Kliknij:
   - **Commit** – zapisuje wersję tylko lokalnie,
   - **Commit and Push…** – zapisuje i od razu wrzuca na GitHuba.

> Pliki nieśledzone przez Gita (nowe) trafiają do sekcji **Unversioned Files**. Zaznacz je, żeby zostały dodane.

## 2. Push

- Menu **Git → Push…** (`Ctrl+Shift+K`, Mac: `Cmd+Shift+K`).
- W oknie zobaczysz listę commitów do wysłania. Kliknij **Push**.
- ✅ Sprawdź na GitHubie w przeglądarce, czy zmiany się pokazały.

## 3. Sprawdzanie stanu (odpowiednik `git status`)

- Okno **Commit** pokazuje zmienione pliki.
- Okno **Git** (`Alt+9`, Mac: `Cmd+9`) pokazuje historię commitów (**Log**) i branche.
- Aktualny branch widać w **widżecie brancha** na górze okna PyCharma (nazwa typu `main`).

---

# III. Branche i Pull Requesty (praca w dwie osoby)

Żebyście nie nadpisali sobie nawzajem kodu, pracujcie na osobnych gałęziach (*branches*).

## Krok 1. Pobierz aktualny stan

- `Git → Update Project…` (`Ctrl+T`, Mac: `Cmd+T`).
- Wybierz **Merge** (zamiast *Rebase*) i kliknij **OK**.

## Krok 2. Utwórz własnego brancha

1. Kliknij **widżet brancha** u góry (np. `main`).
2. Wybierz **New Branch…**.
3. Wpisz nazwę brancha i kliknij **Create**. PyCharm od razu na niego przełączy.

## Krok 3. Pracuj i commituj

Zmień coś w kodzie, a potem zrób commit jak w [II.1](#1-pierwszy-commit).

## Krok 4. Wrzuć brancha na GitHuba

- `Git → Push…` (`Ctrl+Shift+K` / `Cmd+Shift+K`) → **Push**.

## Krok 5. Pull Request

1. Po pushu PyCharm pokaże powiadomienie **Create Pull Request** – kliknij je.
   Jeśli zniknęło: otwórz repo na GitHubie w przeglądarce i kliknij zielony **Compare & pull request**.
2. Opisz zmiany i kliknij **Create pull request**.
3. Zatwierdź: **Merge pull request** (na GitHubie albo w oknie **Pull Requests** w PyCharmie).

## Krok 6. Wróć na `main` i pobierz zmiany

1. Kliknij widżet brancha → `main` → **Checkout**.
2. Zrób `Git → Update Project…` (`Ctrl+T` / `Cmd+T`).

## Krok 7 (opcjonalnie). Usuń niepotrzebnego brancha

Widżet brancha → najedź na nazwę brancha → **Delete**.

> 💡 Przed każdym nowym branchem wracaj na `main` i rób *Update Project*, żeby zaczynać od aktualnego kodu.

---

# IV. Konflikty (Conflict)

Konflikt pojawia się, gdy Wy albo ktoś z pary edytowaliście tę samą linię w pliku. PyCharm pokaże wtedy okno **Conflicts** z listą plików.

1. Wybierz plik i kliknij **Merge…**
2. Otworzy się edytor z trzema kolumnami:
   - **lewa** – Twoja wersja,
   - **prawa** – wersja z drugiego brancha,
   - **środkowa** – wynik końcowy.
3. Dla każdej zmiany kliknij strzałkę `>>` lub `<<`, żeby wybrać wersję (albo edytuj środek ręcznie). Szybkie opcje: **Accept Left** / **Accept Right**.
4. Kliknij **Apply**.
5. Zrób commit z opisem `fix: resolve merge conflict` i **Push**.

> 💡 Najczęściej konflikt pojawia się na pull requeście, bo `main` poszedł do przodu. Wtedy na swoim branchu zrób *Update Project* (Merge), rozwiąż konflikt jak wyżej i zrób Push. PR odświeży się sam.

---

# V. Codzienny start

1. Otwórz projekt w PyCharmie (**File → Open Recent** albo ekran startowy).
2. **Środowisko `.venv` aktywuje się samo** w terminalu PyCharma, bo interpreter jest przypisany do projektu. Upewnij się tylko, że widzisz `(.venv)`.
3. Upewnij się, że jesteś na `main` (widżet brancha u góry). Jeśli nie, kliknij go i wybierz `main` → **Checkout**.
4. Pobierz najnowszy stan: `Git → Update Project…` (`Ctrl+T` / `Cmd+T`).

---

# VI. Dołączanie do istniejącego projektu (dla drugiej osoby)

Ta sekcja jest dla osoby, która **nie zakłada** repo, tylko dołącza do projektu kolegi/koleżanki. Zamiast tworzyć repo, **klonujesz** gotowe.

## 1. Jednorazowy setup

1. Zrób punkty **I.1 – I.3** (instalacja, konfiguracja Gita, logowanie do GitHuba w PyCharmie).
2. Zaakceptuj zaproszenie do repo (mail albo powiadomienia na GitHubie). Bez tego nie wrzucisz zmian.

## 2. Pobranie projektu

1. Na ekranie startowym kliknij **Clone Repository** (albo `Git → Clone…`).
2. Wybierz **GitHub** po lewej, znajdź repo na liście (albo wklej link HTTPS w zakładce *Repository URL*).
3. Wybierz folder docelowy i kliknij **Clone**.
4. Zaufaj projektowi (**Trust Project**).

## 3. Własne środowisko wirtualne

Folder `.venv` **nie jest** w repo (jest w `.gitignore`), więc każdy tworzy swój:

1. PyCharm zwykle pokaże baner **Configure Python interpreter** (albo użyj ustawień: `Settings → Python → Interpreter → Add Interpreter → Add Local Interpreter`).
2. Wybierz **Virtualenv → New**, lokalizacja `.venv` w folderze projektu, i kliknij **OK**.
3. Jeśli w projekcie jest plik `requirements.txt`, PyCharm zaproponuje jego instalację. Jeśli nie, wpisz w terminalu:

   ```bash
   pip install -r requirements.txt
   ```

## 4. Praca na własnym branchu

Nigdy nie pracuj bezpośrednio na `main`. Schemat jest ten sam, co w sekcji [III](#iii-branche-i-pull-requesty-praca-w-dwie-osoby):

1. *Update Project* na `main`.
2. Widżet brancha → **New Branch…**
3. Zmiany → **Commit** → **Push**.
4. **Create Pull Request** → merge robi osoba, która pilnuje `main` (albo Wy razem po sprawdzeniu zmian).

---

# VII. Skróty klawiszowe

| Akcja | 🪟 Windows / Linux | 🍎 Mac |
|---|---|---|
| Okno **Commit** / commit | `Alt+0` / `Ctrl+K` | `Cmd+0` / `Cmd+K` |
| **Push** | `Ctrl+Shift+K` | `Cmd+Shift+K` |
| **Update Project** (pull) | `Ctrl+T` | `Cmd+T` |
| Okno **Git** (historia, branche) | `Alt+9` | `Cmd+9` |
| Terminal | `Alt+F12` | `Option+F12` |
| Ustawienia | `Ctrl+Alt+S` | `Cmd+,` |
| Wyszukaj akcję | `Shift Shift` | `Shift Shift` |

---

## 🔁 Odpowiedniki: terminal vs PyCharm

| Terminal | PyCharm (GUI) |
|---|---|
| `git status` | okno **Commit** (`Alt+0` / `Cmd+0`) |
| `git add .` + `git commit -m "..."` | zaznacz pliki + opis w oknie **Commit** → **Commit** |
| `git push` | `Git → Push…` |
| `git pull origin main` | `Git → Update Project…` |
| `git checkout -b nazwa` | widżet brancha → **New Branch…** |
| `git checkout main` | widżet brancha → `main` → **Checkout** |
| `git clone ...` | **Clone Repository** |
| `git branch -d nazwa` | widżet brancha → **Delete** |
| rozwiązywanie konfliktu ręcznie | okno **Merge…** z trzema kolumnami |
