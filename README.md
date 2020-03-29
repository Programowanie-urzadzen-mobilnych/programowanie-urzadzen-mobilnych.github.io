- [ZenHub](#zenhub)
- [GitFlow](#gitflow)
- [Dodawanie tasków do ZenHuba](#dodawanie-task%c3%b3w-do-zenhuba)
- [Instrukcja pracy](#instrukcja-pracy)
  - [Dodawanie nowego modułu](#dodawanie-nowego-modu%c5%82u)
  - [Przed pierwszym odpaleniem Android Studio](#przed-pierwszym-odpaleniem-android-studio)
  - [Przed **każdym** zaczęciem pracy w Android Studio](#przed-ka%c5%bcdym-zacz%c4%99ciem-pracy-w-android-studio)
  - [Tworzenie brancha](#tworzenie-brancha)
  - [Wysyłanie kodu na GitHuba](#wysy%c5%82anie-kodu-na-githuba)
  - [Pull Request, Review i Mergowanie](#pull-request-review-i-mergowanie)

# ZenHub
[link](https://app.zenhub.com/workspaces/smart-river-5e6290ba0815ca1065d21c9f/board?repos=245463746)

Pamiętajcie żeby przesuwać taski do odpowiednich kolumn w zależności od stanu.

Króki opis kolumn:
- New Issues - wszystko domyślnie trafia tam.
- Backlog - Taski, które tzeba zrobić w pierwszej kolejności. Radziłbym, żeby były tu maks 2
taski od każdej drużyny.
- In Progress - ktoś pracuje nad tym zadaniem.
- Review/QA - Zadanie jest w zasadzie zrobione i czeka na review, lub poprawiane są błędy
znalezione w review.
- Done - Zadanie jest zrobione, ale nie może być zamknięte bo czeka na inne zadanie
- Closed - Zadanie jest zamknięte. Może być zamknięte bo jest skończone, albo zostało odrzucone
(np. nie starczy na to czasu)

# GitFlow
Skrócony opis Git Flow który u nas by działał:

Każdy branch wychodzi z mastera i nazywa się jako `feature/SR-[numer zadania z
zenhub]` lub `fix/SR-[numer zadania]`. Przykład: `feature/SR-4`.

Sidenote: branche powinny teoretycznie wychodzić z developa, który jest co jakiś czas łączony
z masterem, żeby master zawsze był stabilny, ale nie mamy czasu na takie zabawy

Commity zaczynają się od `SR-[numer zadania]`. Przykład:
`SR-4 Added some garbage`

Branche są mergowane tylko po review. Poszczególne moduły wymagają review od pozostałych osób z tego modułu, główny projekt wymaga review od co najmniej jednej osoby ze wszystkich modułów

Zakaz pushowania bezpośrednio do mastera (na GitHubie można ustawić).

Wyjątkiem są hotfixy, które nie wymagają review. Branch może być hotfixem tylko jeśli powstał <24h od następnego pokazu

# Dodawanie tasków do ZenHuba
W zenhubie każdy może dodawać taski. Widać kto dodał, więc bez trolowania.

Dodajcie jakiś skrócony tytuł i w opisie podawajcie konretne informacje. W polu
`Labels` z prawej dodajcie label `feature` lub `bug`, ewentualnie `documentation`.
Oznaczajcie też do którego modułu jest ten task. 

Jeżeli zadanie składa się z kilku elementów to zamiast klikać `Submit new issue` klikajcie `Create an Epic` i tam dodawajcie zadania.

W przypadku gdy zadanie jest częścią epika, do nazywania branchy i do commitów używajcie numeru epika, a nie podzadania

# Instrukcja pracy
## Dodawanie nowego modułu
Dodawanie nowego modułu jest trochę skomplikowane, na szczęście to robi tylko jedna osoba
z drużyny i tylko raz. [tutaj](nowy-modul.md) jest instrukcja jak to zrobić. W razie problemów kontaktujcie się ze mną na Messengerze

## Przed pierwszym odpaleniem Android Studio
Zanim będzie można coś zrobić trzeba sklonować główne repo i kazać gitowi pobrać
wszystkie moduły. W sumie to jest proste i trzeba tylko przekleić odpowiednie komendy
w CMD. Zakładam tutaj że każdy ma gita zainstalowanego, jak nie to odsyłam do wujka Google

1.  odpalić CMD i wejść do folderu gdzie ma być projekt (poleceniem `cd`)
2.  Wpisać lub wkleić `git clone https://github.com/Programowanie-urzadzen-mobilnych/android-app`
3. `cd android-app`
4. `git submodule init`
5. `git submodule update`

## Przed **każdym** zaczęciem pracy w Android Studio
Zawsze trzeba się upewnić, że pobrane są najnowsze wersje modułów. Nie zgłaszajcie błędów
innym drużynom jeśli nie jesteście pewni że macie najnowsze

1. Odpalić CMD i wejść do folderu z projektem
2. `git pull`
3. Możliwe że android studio coś namiesza. Wtedy trzeba `git add . && git reset --hard`
4. `git submodule update --remote --merge`

Od tego momentu pracujecie w **swoim** module, nie w głównym folderze projektu.

## Tworzenie brancha
Upewnijcie się że jesteście na aktualnym masterze i tworzycie brancha
1. CMD -> folder projektu
2. `cd [twój moduł]`, np. `cd data-store`
3. `git checkout master`
4. `git pull`
5. `git checkout -b [feature lub fix]/SR-[numer taska]`

## Wysyłanie kodu na GitHuba
Każde zmiany w kodzie trzeba zakomitować i wypchnąć na Githuba. Debaty jak często 
komitować (miliard komitów na godzinę czy jeden tylko jeden na sam koniec) trwają od 20 lat,
ale generalnie polecam robić komit na koniec każdego dnia pracy, czyli np. coś porobiłem
ale więcej mi się nie chce i idę grać w lola, to zakomitować i wypchnąć żeby nie zginęło.

W CMD w folderze modułu
1. `git add .` - mówi gitowi na któe pliki ma patrzeć (`.` oznacza wszystko w tym folderze i podfolderach)
2. `git commit -m "SR-[nr zadania] Krótka wiadomość co się zrobiło"` - robi nowego komita. `-m`
mówi jaka jest wiadomość tego komita.
3. `git push` - wypycha wszystko na githuba do konkretnego brancha

Pierwszy `git push` na nowym branchu może nie zadziałać. Git wyświetla tam jakie polecenie
trzeba wpisać żeby zadziałało.

## Pull Request, Review i Mergowanie
Żeby połączyć branche w jednego mastera, trzeba zrobić tzw. Pull Request (PR w skrócie).
Robi się to z poziomu repozytorium modułu na Githubie przyciskiem `New pull request`.
Potem w polu `compare` trzeba wybrać brancha, uzupełnić tytuł i opis (jeśli trzeba).
Po prawej kliknąć na `Reviewers` i dodać pozostałe osoby ze swojej drużyny, a następnie 
kliknąć `assign yourself` trochę niżej. 