# /skills — Find den rigtige skill til det du vil

Når brugeren kalder `/skills`, vis dette overblik og anbefal hvad de skal bruge baseret på hvad de er i gang med.

---

## Alle tilgængelige skills

### Koding
| Skill | Hvornår du bruger den |
|---|---|
| `/build` | Du vil bygge noget nyt fra bunden |
| `/debug` | Noget virker ikke og du ved ikke hvorfor |
| `/refactor` | Koden virker, men er rodet eller svær at læse |
| `/explain` | Du forstår ikke hvad en stump kode gør |

### Læring
| Skill | Hvornår du bruger den |
|---|---|
| `/learn [emne]` | Du vil lære noget hurtigt og grundigt |

### Research
| Skill | Hvornår du bruger den |
|---|---|
| `/last30days [emne]` | Du vil vide hvad folk siger om et emne lige nu på sociale medier |

### Skrivning
| Skill | Hvornår du bruger den |
|---|---|
| `/stop-slop` | Din tekst lyder for AI-agtig og du vil have det til at lyde menneskeligt |

### Claude-optimering
| Skill | Hvornår du bruger den |
|---|---|
| `/caveman` | Du vil have kortere svar og spare tokens |
| `/compact` | Samtalen er blevet lang og du vil starte frisk uden at miste kontekst |
| `/compress-pdf` | Du har et langt dokument du vil give Claude uden at bruge for mange tokens |
| `/model-guide` | Du er i tvivl om du skal bruge Haiku, Sonnet eller Opus |

### Marketing (40+ skills)
Skriv `/` og begynd at skrive for at se listen. Eksempler:
- `/copywriting` — skriv salgstekst
- `/page-cro` — optimer en landing page
- `/cold-email` — skriv cold outreach
- `/seo-audit` — analysér SEO
- `/pricing-strategy` — sæt den rigtige pris
- `/launch-strategy` — planlæg et produktlaunch
- `/social-content` — lav indhold til sociale medier

---

## Anbefalinger baseret på situation

Når brugeren beskriver hvad de vil lave, anbefal den bedste kombination. Eksempler:

- "Jeg vil lære at kode" → `/learn programmering` + `/build` når de er klar til at bygge
- "Jeg har en fejl" → `/debug`
- "Jeg vil bygge en app" → `/build` + eventuelt `/caveman` for hurtige svar undervejs
- "Jeg vil skrive en email" → `/copywriting` eller `/cold-email`
- "Hvad sker der inden for AI?" → `/last30days AI`
- "Min tekst lyder robot-agtig" → `/stop-slop`
- "Samtalen er blevet for lang" → `/compact`

---

Beskriv hvad du er i gang med, så anbefaler jeg den bedste skill eller kombination.
