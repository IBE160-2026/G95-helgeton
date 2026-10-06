# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G95 – G95-helgeton |
| **Product brief** | `Product Brief WordFlow.pdf` (commit `1866905`). Fila `Wordflow` (uten filendelse, commit `1811862`) har samme innhold som tekst. Vi har vurdert PDF-en som den nyeste versjonen. |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Bør revideres før dere går videre.** Rett punktene markert «Endre» før dere lager PRD og arkitektur.

**Det som er bra:**

1. Godt beskrevet problem med tydelige brukergrupper som har konkrete behov: elever og studenter med dysleksi, flerspråklige elever og voksne som lærer norsk, og lærere som ikke har tid til å lage lyd og ordlister. Eksempelet med studenten som lytter til et økologikapittel på bussen og trykker på «primærprodusent» gjør brukssituasjonen levende.
2. Suksesskriteriene for MVP er konkrete og kan testes: synkronisert markering av ord eller setninger, minst ett bilde knyttet til riktig avsnitt, trykk på ord for forklaring, minst tre kontrollspørsmål per del og at læreren godkjenner KI-forslag før publisering.
3. God holdning til KI: KI-generert innhold er et forslag som læreren må godkjenne, ikke en fasit. Det gir god kvalitetskontroll og godt stoff til refleksjonsrapporten.

**De viktigste endringene:**

1. **Briefen mangler en Scope-del.** Det står ikke hva som er med i første versjon og hva som ikke er det. Kjernefunksjonene (synkronisert opplesning, bilder, trykk for å forstå, kontrollspørsmål og KI-assistert innholdsproduksjon for lærere) er til sammen fem funksjonsområder og to brukerroller. Lag en tydelig «Med i v1» og «Ikke med i v1».
2. **Avklar de tekniske nøkkelvalgene som påvirker omfanget.** Hvor kommer opplesningen fra (nettleserens innebygde tale eller en betalt tale-tjeneste)? Finnes det god norsk stemme? Hvor kommer bildene fra (læreren laster opp, eller KI genererer)? Hvordan kommer et kapittel inn i appen (lim inn tekst, eller last opp PDF)? Svarene avgjør om prosjektet er middels eller vanskelig.
3. **Skill MVP-kriteriene fra de langsiktige effektmålene.** «20 % flere riktige svar», «70 % fullfører kapitlet» og «WCAG 2.1 AA» kan ikke måles eller nås fullt ut i emnet. Behold dem under visjon, og la MVP-kriteriene være det dere tester. Vurder også om «testet med minst 5 testbrukere» er realistisk og nødvendig.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Middels**

**Sammenlignbart med:** 8) Foredragsnotater – sammendrag og quizgenerator (enkel) for kontrollspørsmålene, men synkronisert opplesning, bilder knyttet til avsnitt og to roller med godkjenningsflyt løfter prosjektet til nivået for 2) AI CV- og søknadsassistent (middels).

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | middels | Synkronisering mellom lyd og tekst (markere riktig ord til riktig tid), tempo, hopp tilbake og bytte mellom lesing og lytting uten å miste plassen. |
| Datamodell – antall entiteter og relasjoner mellom dem | middels | Kurs, kapittel, del/avsnitt, begrep, bilde, spørsmål, svar og godkjenningsstatus. |
| Brukere, roller og innlogging | middels | Elev/student og lærer/kursholder med ulike rettigheter (lærer publiserer, elev leser). Innlogging er ikke omtalt. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | middels | Ordforklaringer, kontrollspørsmål med forklaring og forslag til bildeforklaringer. Bildegenerering ville gjort dette høyt. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | middels | LLM-API og eventuelt tale-API. Nettleserens innebygde tale er gratis, men støtten for norsk og for ordmarkering varierer mellom nettlesere. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | middels | Ikke flere brukere samtidig, men tidskritisk synkronisering av lyd og markering i nettleseren. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | middels | Opplasting av bilder og eventuelt lydfiler. PDF-import av kapitler er ikke avklart og ville økt vanskelighetsgraden. |
| Sikkerhet og personvern | lav | Lite personopplysninger. Ved bruk av lærebøker må dere tenke på opphavsrett, og bruke egne eller fritt tilgjengelige tekster til testing. |

**Hva vanskelighetsgraden betyr for dere:**

- _Middels:_ Et godt balansert valg. Pass på at kjerneflyten blir ferdig og stabil før dere legger til mer. For dere betyr det at opplesning med markering og trykk for å forstå på én tekst bør fungere godt før lærerrollen og godkjenningsflyten bygges.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | risiko | Fem funksjonsområder og to roller er mye for én person. Uten Scope er det uklart hva som skal bli ferdig. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | risiko | Briefen er laget utenfor BMAD og mangler Scope og avgrensning. Bruk BMADs product brief-steg til å legge til disse delene før PRD. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | risiko | En webapp passer godt, men synkronisert opplesning med ordmarkering er avhengig av nettleser og stemme. Gjør en liten teknisk test tidlig. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | OK | Dere kan selv høre og se om markeringen følger opplesningen, og vurdere om ordforklaringer og spørsmål er riktige for en kjent tekst. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | OK | MVP-kriteriene er konkrete. Godkjenningsflyten, bildeplassering og antall spørsmål kan testes automatisk. Synkroniseringen må testes manuelt med en testplan. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | risiko | Hvis dere bruker en betalt tale-tjeneste og LLM, trenger sensor nøkler. Nettleserens innebygde tale og en demomodus med ferdig generert innhold gjør appen kjørbar. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | risiko | Ingen plan ennå. Beskriv hvilke tjenester som trengs, og lag en ferdig eksempelleksjon som fungerer uten nøkler. |

**Konklusjon om gjennomførbarhet:**

- **Gjennomførbart med justert omfang.** Se forslagene under.

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. **V1:** læreren limer inn tekst og laster opp bilder til avsnitt, KI foreslår ordforklaringer og kontrollspørsmål som læreren godkjenner, og eleven leser og lytter med markering, trykker på ord og svarer på spørsmål. Bruk nettleserens innebygde tale.
2. **Senere trinn:** PDF-import av kapitler, KI-genererte bilder, uttale av enkeltord, betalt tale med bedre norsk stemme og statistikk over svar.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | «Oppsummering» forklarer tydelig ideen: tekst, lyd og bilder som henger sammen, med KI som lager det som mangler. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Fire tydelige problemer med konkrete brukergrupper. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | OK | Kjernefunksjonene og eksempelet med økologikapitlet beskriver brukeropplevelsen godt. |
| What Makes This Different – er vurderingen ærlig og realistisk? | Juster | Tabellen er god, men nevner ikke eksisterende løsninger som allerede kombinerer tekst og opplesning med markering (for eksempel lese-verktøy i nettlesere og læringsplattformer). Vær ærlig om hva som faktisk er nytt. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | Juster | Fem målgrupper er listet. Velg én primærbruker for v1, for eksempel en student med dysleksi, og la lærerrollen være sekundær. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Juster | MVP-kriteriene er gode. De langsiktige effektmålene kan ikke måles i emnet og bør flyttes til visjon. |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | Endre | Mangler helt. Lag «Med i v1» og «Ikke med i v1». |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Visjonen er tydelig og henger sammen med problemet. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | Endre | Briefen ligger som PDF og som tekstfil uten filendelse. Gjør den om til én Markdown-fil (for eksempel `product-brief.md`) i en planleggingsmappe, slik at endringer kan følges i Git. Sett opp BMAD i repoet. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | Endre | Uten Scope er kjerneflyten uklar. Velg v1 som foreslått over. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | OK | MVP-kriteriene kan bli testtilfeller nesten direkte. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | OK | Universell utforming er selve kjernen i produktet. Det gir et godt grunnlag for designvurderingen. Skisser leservisningen og lærervisningen. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | Juster | Ingen teknologi er valgt. Valget av tale-løsning bør begrunnes tidlig, siden det styrer resten. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | Juster | Planlegg en eksempelleksjon som fungerer uten nøkler, og `.env.example` for LLM. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | Juster | Rydd bort den doble briefen (PDF og fil uten endelse) og legg dokumentasjon i en egen mappe. Bruk egne eller fritt tilgjengelige tekster som testdata. |

## 3. Neste steg for gruppen

1. Lag én `product-brief.md` i en planleggingsmappe, og legg til Scope med «Med i v1» og «Ikke med i v1». Flytt effektmålene til visjon.
2. Gjør en liten teknisk test av nettleserens tale med norsk stemme og ordmarkering, og skriv resultatet inn i briefen som grunnlag for teknologivalget.
3. Sett opp BMAD i repoet og lag PRD ut fra den reviderte briefen.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
