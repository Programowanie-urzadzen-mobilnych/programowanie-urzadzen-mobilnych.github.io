Instrukcja jest tutaj uproszczona i nie tłumaczy wielu rzeczy. W razie problemów pisz na Messengerze

Wszystkie polecenia zakładają że jesteś w CMD w odpowiednim folderze, chyba że napiszę inaczej.

1. `git clone https://github.com/Programowanie-urzadzen-mobilnych/android-app`
2. `cd android-app`
3. `git checkout feature/SR-0`
4. W Android Studio
   1. Importujesz (nie otwierasz) ten folder
   2. File > New > New  Module...
   3. Android Library
   4. Wypełniasz pola
   5. Zamykasz Android Studio, żeby nic nie zepsuło
5. Zmieniasz nazwę folderu z tym modułem, który właśnie założyłeś (zapamiętaj starą nazwę), np.
`ren module module_`. Robimy to, żeby git mógł bez problemu sklonować wszystko do folderu o tej samej nazwie.
6. Na githubie w organizacji "Programowanie urządzeń mobilnych" tworzysz nowe repo, najlepiej o
tej samej nazwie co twój moduł
7. Jako że Android Studio ma własny rozum, najpewniej namieszał trochę w indeksie gita. Trzeba
to naprawić
`git restore --staged .`
8. Dodajemy moduł gita:
`git submodule add https://github.com/Programowanie-urzadzen-mobilnych/[nazwa repo] [nazwa modułu]`
Git pewnie coś będzie narzekać odnośnie LF lub CRLF, można to zignorować
9. `git submodule init`
10. Przekopiuj wszystko z tego folderu któremu zmieniłeś nazwę (`module_`) do folderu
który git właśnie dodał (`module`)
11. `git submodule update --remote --merge`
12. `cd [nazwa modulu]`
13. `git add .`
14. `git commit -m "Created module"` - Jedyny przypadek, gdzie nie dodajemu `SR-[nr]` na początku
15. `git push --set-upstream origin master`
16. `cd ..`
17. `git submodule update --remote --merge`
21. Usuń folder `.idea` oraz plik `Smart River.iml`
18. `git add .`
19. `git commit -m "SR-0 Added submodule [nazwa modułu]`
20. `git push --set-upstream origin master`
22. W Android Studio zaimportuj projekt

Teraz można przetestować w Android Studio. W swoim module zrób jakąś pustą aktywność i dodaj jakiś tekst. W `MainActivity` dodaj odpalanie tej nowej aktywności w `onCreate`: `startActivity(new Intent(this, NazwaAktywnosci.class));`. Najpewniej będzie coś krzyczał że nie ma dependency. `Alt+Enter` powinno załatwić sprawę. Jeśli wszystko działa to usuń to co teraz zrobiłeś, żeby nie zaśmiecać