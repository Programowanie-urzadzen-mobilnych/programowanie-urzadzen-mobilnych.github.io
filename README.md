# ZenHub
[link](https://app.zenhub.com/workspaces/smart-river-5e6290ba0815ca1065d21c9f/board?repos=245463746)
# GitFlow
Skrócony opis Git Flow który u nas by działał:

Każdy branch wychodzi z mastera nazywa się jako `feature/SR-[numer zadania z
zenhub]` lub `fix/SR-[numer zadania]`. Przykład: `feature/SR-4`.

Commity zaczynają się od `SR-[numer zadania]`. Przykład:
`SR-4 Dodano kilka śmieci`

Branche są mergowane tylko po review. Poszczególne moduły wymagają review od pozostałych osób z tego modułu, główny projekt wymaga review od co najmniej jednej osoby ze wszystkich modułów

Zakaz pushowania bezpośrednio do mastera (na GitHubie można ustawić).

Wyjątkiem są hotfixy, które nie wymagają review. Branch może być hotfixem tylko jeśli postał <24h od następnego pokazu
