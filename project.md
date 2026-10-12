# Môj slovník — project.md

> **Local by default — tvoje slová, tvoje dáta.**

---

## 1. Aký problém riešim (jednou vetou)

Slová, na ktoré pri učení narazím (cudzie jazyky, latinčina, odborné pojmy), sa mi strácajú v zošitoch a rôznych appkách, a nemám jedno súkromné miesto, kde si ich rýchlo uložím, prepojím medzi viacerými jazykmi a precvičím.

---

## 2. Kto sú moji useri

**MVP: ja sám** – jeden používateľ, ktorý sa učí viac jazykov naraz a k tomu odborné pojmy (napr. chémia, latinčina).

Čo od appky potrebujem:
- uložiť slovo za pár sekúnd, hneď keď ho stretnem, a doplniť ho až neskôr,
- mať pri jednom slove viac jazykov naraz (SK, EN, DE, ES, JP…),
- precvičovať si slová ako zo zošita (zakryť preklad a vybaviť si ho),
- nemusieť si zakladať účet, mať dáta u seba a appku používať aj offline.

**Neskôr (po MVP):** študenti (jazyky + školské predmety) a ľudia, čo sa učia viac jazykov naraz. Kvôli nim sa v MVP nič nerobí, ale dátový model by ich nemal zablokovať.

---

## 3. Ako chcem problém vyriešiť (MVP)

Offline webová appka (PWA), ktorú si nainštalujem na Android z prehliadača. Má tri časti:

### 3.1 Quick Add + Inbox
- Na každej obrazovke je tlačidlo **+ Pridať slovo**: jedno textové pole a uložiť.
- Slovo bez prekladov skončí v **Inboxe** („čaká na spracovanie“).
- V Inboxe slovo otvorím a doplním ho. Keď má aspoň 2 jazykové verzie, presunie sa do slovníka.

### 3.2 Slovník (karta slova)
Jedno slovo = jedna **karta** (koncept), ktorá obsahuje:
- **jazykové verzie**: jazyk + zápis (napr. `de: Apfel`, `ja: りんご / ringo`),
- **tagy** (ovocie, chémia, kov…),
- **poznámku** (voľný text).

Ďalej:
- Zoznam kariet s vyhľadávaním (podľa textu) a filtrom (podľa jazyka a tagu).
- **Režim zošita:** preklady na karte sú zakryté a odkryjem ich ťuknutím.
- Jazyky si definujem sám (aj „Latinčina“ alebo „Chémia – značky“), nie sú to iba moderné jazyky.

### 3.3 Precvičovanie
- **Klasický režim:** vyberiem zdrojový a cieľový jazyk (napr. SK → DE). Dostanem slovo a napíšem preklad.
- **Multilanguage Thinking:** appka pri každej otázke náhodne vyberie dvojicu jazykov, ktoré karta má (napr. DE → EN, ES → JA).
- **Kontrola odpovede:** porovnám ju po normalizácii (orezanie medzier, malé/veľké písmená). Pri japončine uznám kanu aj romaji.
- **Záznam pokusov:** uloží sa každá odpoveď (správna/nesprávna + čo som napísal), napr. `Apfell ❌ → Apfel ✅`.
- Na konci kola vidím jednoduchý výsledok: X/Y správne a zoznam chýb.
- Výber slov je zatiaľ náhodný, voliteľne podľa tagu alebo jazyka.

### 3.4 Dáta
- Všetko sa ukladá lokálne v zariadení (IndexedDB). Nie je tu žiadny server ani účet.
- **Export/import do JSON súboru** slúži ako záloha, aby som o dáta neprišiel pri zmazaní prehliadača alebo pri výmene mobilu.

### Kedy je MVP hotové
- [ ] Vložím slovo cez Quick Add za menej ako 5 sekúnd.
- [ ] Spracujem slovo z Inboxu (jazyky, tagy, poznámka).
- [ ] Nájdem kartu podľa textu, jazyka alebo tagu.
- [ ] Odohrám kolo v klasickom aj multilanguage režime a vidím svoje chyby.
- [ ] Appka funguje v režime lietadlo a je nainštalovaná na ploche Androidu.
- [ ] Exportujem dáta a vrátim ich späť importom.
- [ ] Sám ju 2 týždne reálne používam pri učení.

---

## 4. Čo v MVP nebude (non-goals) a prečo

| Nebude v MVP | Prečo |
|---|---|
| **Používateľské účty, cloud, synchronizácia** | Odporuje to princípu „local by default“, potrebovalo by to server, autentifikáciu a riešenie GDPR. Pre jedného používateľa na jednom zariadení to stačí nahradiť exportom/importom. |
| **Spaced repetition (SRS algoritmus)** | Najprv potrebujem dáta o pokusoch, ktoré MVP už zbiera. SRS sa potom dá doplniť nad existujúcu tabuľku pokusov bez prerábania. |
| **Daily úlohy a jazykové postavy** | Je to motivačná vrstva. Má zmysel až vtedy, keď funguje jadro (ukladanie + precvičovanie). Grafiku a návrh postáv netreba na overenie nápadu. |
| **Your Growth – grafy a štatistiky** | V MVP stačí výsledok kola. Grafy prídu, keď bude dosť histórie, ktorú sa oplatí zobrazovať. |
| **Výslovnosť (prehrávanie, nahrávanie, hodnotenie)** | Audio a rozpoznávanie reči sú technicky náročné a často vyžadujú online služby. Poznámka na karte zatiaľ postačí aj na prepis výslovnosti. |
| **Streaky, achievementy, odznaky, pripomienky** | Gamifikácia nerieši hlavný problém. Notifikácie pri PWA navyše fungujú obmedzene. |
| **Automatický preklad / slovníkové API** | Appka nie je prekladač. Ide o *moju* slovnú zásobu, ktorú si vypĺňam sám. Navyše by to vyžadovalo internet. |
| **Tolerancia preklepov (fuzzy matching), hlasové odpovede** | V MVP platí presná zhoda po normalizácii. Kým nevidím reálne chyby, nevieme, aká tolerancia je správna. |
| **OCR / pridanie slova fotoaparátom** | Je to zložité a Quick Add rieši rovnakú potrebu jednoduchšie. |
| **Šifrovanie databázy, PIN, biometria** | Dáta sú lokálne v mojom zariadení, takže pre jedného používateľa je riziko nízke. Pridá sa pred zverejnením appky pre iných. |
| **Natívna appka v Google Play / iOS** | PWA sa dá nainštalovať na Android bez publikovania. Na Google Play sa dá neskôr zabaliť (Capacitor) bez prepisovania kódu. |
| **Viac používateľov / zdieľanie slovníkov** | MVP je pre mňa. Zdieľanie by vyžadovalo server. |

---

## 5. Aké technológie potrebujem

Výber je spravený tak, aby išiel dobre pri vývoji s pomocou AI: populárne technológie s množstvom príkladov, jeden jazyk na všetko, žiadny backend.

| Oblasť | Technológia | Prečo |
|---|---|---|
| Jazyk | **TypeScript** | Typy zachytia veľa chýb, ktoré urobím ja aj AI. Typy navyše slúžia ako „dokumentácia“ dátového modelu. |
| UI framework | **React** | Najrozšírenejší, AI ho pozná najlepšie a dá sa neskôr zabaliť do mobilnej appky. |
| Build nástroj | **Vite** | Jednoduchý a rýchly štart (`npm create vite@latest`). |
| Štýly | **Tailwind CSS** | Štýlovanie priamo v komponentoch, bez samostatných CSS súborov. |
| Lokálna databáza | **IndexedDB cez Dexie.js** | Databáza priamo v prehliadači, funguje offline a zvládne aj tisíce slov. Dexie je jednoduché API nad IndexedDB, `useLiveQuery` automaticky obnoví UI po zmene dát. |
| Offline + inštalácia | **vite-plugin-pwa** (Workbox) | Vygeneruje service worker a manifest, aby appka fungovala bez internetu a dala sa „Pridať na plochu“. |
| Navigácia | **React Router** | Obrazovky Inbox / Slovník / Karta / Precvičovanie. |
| Testy | **Vitest** | Testy pre logiku: kontrolu odpovedí, výber jazykových dvojíc, import/export. Pri kóde od AI sú dôležité, aby som vedel, že funguje. |
| Verzionovanie | **Git + GitHub** | História zmien, pri každej AI úprave sa dá vrátiť späť. |
| Hosting | **GitHub Pages / Netlify / Vercel** (zadarmo) | Iba statické súbory, dáta zostávajú v zariadení. Na inštaláciu PWA je potrebné HTTPS. |
| Editor | **VS Code** + AI asistent | |

**Neskôr (nie v MVP):** Capacitor (Google Play), Web Speech API (výslovnosť), Chart.js/Recharts (Growth grafy), knižnica `wanakana` (prevod kana ↔ romaji).

### Návrh dátového modelu (Dexie)

```ts
Language { id, name, code?, flag? }              // "Nemčina", "de", 🇩🇪 – aj vlastné, napr. "Latinčina"
Card     { id, status: 'inbox' | 'active', note?, tags: string[], createdAt, updatedAt }
Term     { id, cardId, languageId, text, altText? } // altText napr. romaji "ringo"
Attempt  { id, cardId, fromLanguageId, toLanguageId, answer, correct: boolean, createdAt }
```

Pri Quick Add vznikne `Card` so stavom `inbox` a s jedným `Term` bez jazyka. Tabuľka `Attempt` je základ pre neskoršie spaced repetition aj Growth štatistiky.

---

## Otvorené otázky (nechávam na neskôr)
- Uzná sa pri slove s viacerými významami (napr. EN „bank“) ktorýkoľvek z nich? V MVP: jedna karta = jeden význam.
- Majú sa pri kontrole odpovede ignorovať diakritika a nemecké „ß/ss“? V MVP nie.
