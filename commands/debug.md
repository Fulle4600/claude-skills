# /debug — Systematisk debugging

Når brugeren deler en fejl eller et bug, følg denne proces:

## Trin 1: Forstå fejlen
- Hvad er den præcise fejlbesked?
- Hvornår sker den? Altid eller kun i bestemte situationer?
- Hvad var den seneste ændring inden fejlen opstod?

## Trin 2: Isolér problemet
- Find den mindste mulige reproduktion af fejlen
- Identificér præcist hvilken linje/funktion der fejler
- Tjek om det er et data-problem, logik-problem eller miljø-problem

## Trin 3: Hypoteser
- List 3 mulige årsager fra mest til mindst sandsynlig
- For hver hypotese: hvad ville bevise eller modbevise den?

## Trin 4: Fix
- Rets kun det der er ødelagt — intet andet
- Forklar i én sætning hvad root cause var
- Hvis fix introducerer ny risiko, nævn det

## Regler
- Gæt aldrig — bed om mere info hvis noget er uklart
- Vis altid den færdige kode, ikke bare beskrivelsen af ændringen
- Tjek om samme bug kan eksistere andre steder i koden
