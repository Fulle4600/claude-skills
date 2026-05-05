# /refactor — Refaktorer kode uden at ændre funktionalitet

Når brugeren deler kode der skal refaktoreres:

## Prioritér i denne rækkefølge
1. **Korrekthed** — ændr aldrig hvad koden gør, kun hvordan
2. **Læsbarhed** — navne skal fortælle hvad noget er/gør
3. **Enkelhed** — fjern duplikering, men kun hvis det giver mening
4. **Performance** — kun hvis det er et reelt problem

## Hvad du skal gøre
- Identificér de 3 største problemer i koden
- Refaktorér ét problem ad gangen
- Vis before/after for hver ændring
- Forklar i én linje hvorfor hver ændring er bedre

## Hvad du ikke må
- Tilføje ny funktionalitet
- Ændre external API (funktionsnavne, parametre der bruges udefra)
- Indføre abstraktioner der ikke er nødvendige endnu
- Skrive kommentarer der forklarer hvad koden gør — navne skal gøre det

## Afslut med
En enkelt linje: hvad er den vigtigste forbedring du lavede og hvorfor.
