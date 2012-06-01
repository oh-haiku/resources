# Project reflections - OH-HAIKU

Detta är en project reflections-rapport för projektet OH-HAIKU av grupp 51, inom ramarna för kursen Software Engineering Project vid Chalmers tekniska högskola.

## 1. Skillnader mellan individuell programmering och arbete i grupp
Grupparbete ställer större krav på dokumentation och planering. Om tydliga gränssnitt mellan moduler inte har definierats så riskerar gruppen att implementera inkompatibla produkter. Detta skedde dock inte vårt fall, men gruppmedlemmar har erfarenhet av tidigare incidenter.

Ledarskap är också ett problem. Den som jobbar ensam vet att ingen annan kan lösa de problem som han eller hon lämnar efter sig.
Den svenska Jantelagen gör dock att ingen gärna tar en tydlig ledarposition i en grup. Detta fungerar inte längden. 
Utan tydligt ledarskap faller uppgifter mellan stolarna och gruppen förlorar sin fokus.

Grupparbete kan dock leda till högre effektivitet om det sköts på rätt sätt. I vår grupp uppnåddes goda resultat både på kodsidan och vad gäller det grafiska gränssnittet, mycket på grund av att kommunikationen var god och man därmed kunde utnyttja gruppmedlemmarnas individuella styrkor.
Att teamets informationsflöde dessutom präglades av issue-hantering hos Github och Google Groups ledde till att alla i teamet uppdaterades samtidigt. Som nämns nedan har fysiska möten använts i mindre utsträckning vilket har lett till att inofficiella kommunikationskanaler såsom mun-till-mun mellan gruppmedlemmar, som kan orsaka dubbelarbete, har eliminerats.


## 2. Metoder som användes för att skapa dokumenten
Projektets första dokument skapades i gemensamma Google Documents-dokument. På detta sätt kunde alla kollaborera i realtid.
Formatet är dock inte lämpligt för längre bruk i detta sammanhang, då versionshanteringsfunktionaliteten är begränsad.
Därför gick gruppen över till Markdown-dokument.

## 3. SE-metodernas lämplighet
De SE-metoder som användes inom projektet fungerade väldigt bra. Exempel på dessa är versionshantering med Git, code hosting och issue-hantering hos Github samt kommunikation via Google Groups och IRC-kanal. 

Av praktiska skäl kunde gruppmedlemmarna inte träffas oftare än några enstaka gånger i veckan. Istället sköttes kommunikation och kollaborering med de tidigare nämnda verktygen. Detta fungerade över förväntan. Särskilt under den sista hektiska utvecklingsveckan var effektiviteten inom gruppen mycket hög trots avsaknaden av fysiska möten. Issue-hanteringen såg till att inga uppgifter föll mellan stolarna. Då en gruppmedlem pushade kod och samtidigt var medveten om att den inte var fullständigt korrekt, skapades samtidigt en issue. Detta för att signalera till övriga i teamet att framgång gjorts men koden inte är fullständig ännu. På detta sätt uppnåddes en hög effektivitet och minimalt med dubbelarbete. 

De SE-tekniker som fungerade mindre väl var de som helt enkelt aldrig implementerades ordentligt. 
Projektet använde sig inte av någon tydlig arbetsmodell, som vattenfall eller SCRUM, utan använde sig av mer intuitiva arbetsmetoder. 
Ett visst mått av SCRUM-liknande arbete skedde mot slutet, då vi jobbade mot våra två releaser på ett iterativt sätt och issue-hanteringen fick motsvara en SCRUM-backlog.
Eventuellt hade projektet kunnat må bra av att belägga handledaren med en tydlig Product Owner-roll.

## 4. Kodtäckning
Kodtäckningen på de två modellklasserna är nästan 100-procentig. Vi hade långt gående planer på att uppnå hög kodtäckning även vad gäller våra Activities. I praktiken gick inte detta, beroende på buggar i Android SDK:t.


Se respektive release i [huvudrepositoriet](https://github.com/oh-haiku/oh-haiku) för kodtäckningsrapporter.

## 5. Allmänna kommentarer
Att skriva tester för att tydligt definiera applikationens beteende är ett bra sätt att gediget planera sitt arbete. Formatet som testerna skulle uttryckas i var dock inte riktigt expressivt, tyckte vi i gruppen. Ibland stod formalia i vägen för en lämplig beskrivning av testbeteendet.

### Användarfunktionalitet som kvarstår

- Dela Haiku via SMS och e-post
- Se hur en Haiku har delats i BrowseSavedHaikus-vyn
- Realtidsvisnings av stavelseantal i HaikuComposition-vyn
- Texterna i applikationen bör lokaliseras. Just nu är informationen i appen på engelska, men haikualgoritmen är svensk.

### Tekniska frågor som kvarstår

#### Haikualgoritm
Haikualgoritmen bör skrivas om så att den kan skilja vokalkluster i sammansatta ord från diftonger.

En engelsk Haiku-algoritm bör också definieras

#### Databasmigrering

En viktig fråga som ännu är olöst är migrering av databasen. Om objektmodellen förändras bör även databasen förändras. I ORM:et som vi använder finns dock inga inbyggda funktioner för smidiga migreringar. Den naiva lösningen är att läsa in hela databasen i minnet, radera databasen och bygga upp den igen enligt den nya objektmodellen, och sedan återinföra informationen.
Att deserialisera databasen blir dock svårt, eftersom objektmodellen har förändrats. Detta leder till att deserialiseringen kan misslyckas.

I ORM:et finns dock en möjlighet att definiera databasversioner. Ett callback körs när databasen uppgraderas. I detta callback kan vi kontrollera den gamla och kommande databasversionen. På detta sätt vore det möjligt att definiera handskrivna migrationsmetoder som är anpassade för migrationer mellan olika databasversioner. I dessa kunde t.ex. rå SQL-kod exekveras som sköter migreringen på bästa sätt. Detta kan mycket väl vara den mest framtidssäkra metoden.

#### Activity-byten i samband med Twitterauktorisering
Vid Twitterauktorisering sker just nu ett klumpigt byte till huvud-activityn. Detta borde skötas så att back-stacken inte störs, vilket är konsekvensen för närvarande.