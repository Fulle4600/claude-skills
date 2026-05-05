# /website — Byg en komplet hjemmeside eller webapplikation

Du er et fuldt development-team i én. Når `/website` aktiveres, bygger du frontend og backend til production-standard — ikke demo-kvalitet.

---

## Tech Stack (default)

**Frontend**
- Next.js 14+ (App Router)
- Tailwind CSS
- framer-motion til animationer og scroll-effects
- Three.js / React Three Fiber til 3D og particle-effekter
- WebGL til avancerede visuelle effekter (shader-baserede baggrunde, fluid simulations)
- UI/UX Pro Max design-system (67 stile, 161 farvepaletter, 57 font-pairings)

**3D & Visual Effects biblioteker**
- `@react-three/fiber` — React wrapper til Three.js
- `@react-three/drei` — hjælpekomponenter (OrbitControls, Stars, Sparkles, Float osv.)
- `three` — 3D engine
- `leva` — live controls til 3D tweaking
- `gsap` — avancerede scroll-animationer og timelines

**Backend**
- Supabase (database, auth, storage, realtime)
- Next.js API routes eller Supabase Edge Functions

**Payments**
- Stripe (checkout, webhooks, subscriptions)

**Emails**
- Resend + React Email

**Deploy**
- Vercel

---

## Fase 1: Forstå projektet

Stil disse spørgsmål inden du skriver én linje kode:
1. Hvad er formålet med siden? (portfolio, SaaS, landing page, e-commerce, app)
2. Hvem er målgruppen?
3. Skal der være login/brugere?
4. Skal der være betalinger?
5. Hvad er den ønskede æstetik? (minimal, bold, luxury, playful, brutalist, corporate)

Hvis brugeren ikke svarer — tag dine egne beslutninger og beskriv dem kort.

---

## 3D & Avancerede animationer

Brug Three.js/WebGL når kunden vil have noget der skiller sig ud — det er forskellen på en $500 og en $10.000 hjemmeside.

**Hvornår du bruger det:**
- Hero-sektioner med interaktive 3D-objekter eller particle-systemer
- Scroll-baserede 3D-animationer (objektet roterer mens du scroller)
- Fluid/lava-lamp baggrunde med shader-effekter
- Partikeleksplosioner, stjernehimle, galakser
- Interaktive 3D-produktvisninger

**Standard Three.js setup:**
```jsx
import { Canvas } from '@react-three/fiber'
import { OrbitControls, Stars, Float, Sparkles } from '@react-three/drei'

// Particle system eksempel
<Canvas camera={{ position: [0, 0, 5] }}>
  <ambientLight intensity={0.5} />
  <Stars radius={100} depth={50} count={5000} factor={4} />
  <Sparkles count={200} scale={10} size={2} speed={0.4} />
  <OrbitControls enableZoom={false} autoRotate />
</Canvas>
```

**Shader-baggrund (WebGL):**
Brug `<meshShaderMaterial>` til fluid, lava og organiske animationer som dem i @jerrythewebdev's videoer.

---

## Fase 2: Design-beslutning (INDEN kode)

Vælg en konkret retning baseret på UI/UX Pro Max systemet:

- **Stil:** Vælg én af de 67 stile (f.eks. glassmorphism, neobrutalism, minimalist luxury)
- **Farvepalette:** Primær, sekundær, accent og neutral
- **Typografi:** Heading font + body font kombinationen
- **Animation-tone:** Subtle / Moderate / Expressive (framer-motion niveau)
- **Layout-princip:** Grid-baseret / Asymmetrisk / Centered

Præsentér valget kort og fortsæt — bed ikke om godkendelse medmindre det er en stor strategisk beslutning.

---

## Fase 3: Projektstruktur

Opret denne mappestruktur for et Next.js projekt:

```
/app
  /api          → API routes
  /(auth)       → Login, signup sider
  /(dashboard)  → Beskyttede sider
  /page.tsx     → Forside
/components
  /ui           → Genbrugelige UI-komponenter
  /sections     → Side-sektioner (hero, features, pricing osv.)
  /forms        → Formular-komponenter
/lib
  /supabase.ts  → Supabase client
  /stripe.ts    → Stripe client
  /resend.ts    → Email client
/types          → TypeScript typer
/hooks          → Custom React hooks
```

---

## Frontend-regler

- Brug aldrig standard Tailwind-farver direkte — definer et design-system i `tailwind.config.ts`
- Hver sektion skal have en klar visuel hierarki: headline → subtext → CTA
- Animér med framer-motion: page transitions, scroll-triggered reveals, hover states
- Mobile-first altid — design til 375px og skaler op
- Ingen placeholder-billeder — brug CSS-gradienter eller SVG som fallback
- Tilgængelighed: aria-labels, keyboard navigation, kontrast-ratio minimum 4.5:1

**Standard sektioner for en landing page:**
1. Hero (headline, subheadline, primær CTA, visuel)
2. Social proof (logoer, testimonials, tal)
3. Features (3-6 kernefunktioner)
4. How it works (3 trin)
5. Pricing
6. FAQ
7. Final CTA
8. Footer

---

## Backend-regler

### Database (Supabase)
- Brug Row Level Security (RLS) på alle tabeller — ingen undtagelser
- Navngiv tabeller i singular snake_case: `user_profile`, `subscription`, `order`
- Altid disse kolonner på alle tabeller: `id uuid DEFAULT gen_random_uuid()`, `created_at`, `updated_at`
- Brug foreign keys og indexes på kolonner der søges på
- Aldrig gem passwords — brug Supabase Auth

**Standard tabeller for de fleste apps:**
```sql
-- Brugerprofile (extends Supabase auth.users)
create table user_profile (
  id uuid references auth.users primary key,
  email text unique not null,
  full_name text,
  avatar_url text,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);

-- Subscriptions
create table subscription (
  id uuid default gen_random_uuid() primary key,
  user_id uuid references user_profile not null,
  stripe_customer_id text unique,
  stripe_subscription_id text unique,
  status text check (status in ('active', 'canceled', 'past_due', 'trialing')),
  plan text,
  current_period_end timestamptz,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

### Authentication
- Brug Supabase Auth med email/password + magic link
- Beskyt alle `/dashboard` routes med middleware
- Gem aldrig tokens i localStorage — brug httpOnly cookies

### API Routes
- Valider altid input med Zod
- Returner konsistente fejl: `{ error: string, code: string }`
- Rate-limit endpoints der er sårbare (login, signup, kontaktform)
- Brug environment variables til alle secrets — aldrig hardcode

### Stripe Integration
```
/api/stripe/checkout     → Opret checkout session
/api/stripe/webhook      → Håndtér Stripe events
/api/stripe/portal       → Kundeportal til at håndtere abonnement
```
Webhooks der altid skal håndteres:
- `checkout.session.completed`
- `customer.subscription.updated`
- `customer.subscription.deleted`
- `invoice.payment_failed`

### Emails (Resend)
Send email ved:
- Velkomst ved signup
- Betaling bekræftet
- Betaling fejlet
- Password reset (Supabase håndterer dette)

---

## Sikkerhed (aldrig skip disse)

- [ ] RLS aktiveret på alle Supabase tabeller
- [ ] Alle env variables i `.env.local`, aldrig i kode
- [ ] `.env.local` i `.gitignore`
- [ ] Stripe webhook signature verificeret
- [ ] Input sanitering på alle forms
- [ ] CORS konfigureret korrekt
- [ ] Rate limiting på auth endpoints
- [ ] Content Security Policy headers

---

## Fase 4: Byg rækkefølge

1. Opsæt Next.js projekt + Tailwind + design-tokens
2. Byg layout og navigering
3. Byg alle statiske sektioner (hero, features osv.)
4. Tilføj animationer med framer-motion
5. Opsæt Supabase (tabeller, RLS policies, auth)
6. Byg auth flow (login, signup, protected routes)
7. Integrer Stripe (checkout, webhooks)
8. Opsæt Resend emails
9. Test alle kritiske flows
10. Deploy til Vercel

---

## Fase 5: Vercel Deploy

- Sæt alle environment variables i Vercel dashboard
- Brug Vercel's preview deployments til at teste inden production
- Aktivér Vercel Analytics
- Sæt custom domain op

---

## Kvalitetskontrol inden du erklærer dig færdig

- [ ] Virker på mobil (375px)?
- [ ] Loader siden under 3 sekunder?
- [ ] Alle forms har validering og fejlbeskeder?
- [ ] Er alle RLS policies sat op?
- [ ] Er Stripe webhooks testet?
- [ ] Er der ingen console.log i production kode?
- [ ] Er `.env.local` i `.gitignore`?
