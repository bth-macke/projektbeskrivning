# DV1627 Projekt - Snake

Under denna kurs har du lärt dig objektorienterad programmering med C++. I detta projekt kommer du visa dina lärda erfarenheter genom att skapa ett större projekt i C++. Vad du ska skapa är något du säkerligen har bemött tidigare, nämligen spelet *Snake*.

En demoversion av spelet kan du hitta här: https://playsnake.org/ (Skapad av Neave Interactive Ltd.)

För detta projekt får du två val när det gäller att *rita* spelet. Det första alternativet är med biblioteket `ncurses` som erbjuder ett smidigt sätt att rensa terminalen och rita tecken på önskad position. Det andra alternativet är `SFML` (super fast multimedia library) som är ett mycket lättanvänt bibliotek för 2D-spel i C++.

För att alla ska känna att de har en bra grund att börja från ger vi ut en demo-projekt för vardera bibliotek. Dessa demos hjälper dig med:

- rita en markör på önskad position
- inmatning utan att *pausa* spelet
- slumpgenererade tal

Det är inte ett krav att använda dessa demos, men kan hjälpa dig komma igång med ditt projekt. Vi har skapat och testat dessa i både WSL och MacOS. Just installation kan vara lite knepigt, och vill du försöka dig på detta själv ger vi dig de länkar du behöver. Vill du ha stöd hjälper vi dig också: det är bara att köra `make install` och följa anvisningarna i önskat demo! :)

Till skillnad från tidigare examinationsmoment i denna kurs så kommer det inte existera automatiska tester för detta projekt. Istället kommer du ges ett antal kriterier att som du behöver uppfylla baserat på kursmålen, och utöver dessa är du fri att skapa ett spel på den nivån du känner att du är kapabel till. Det projekt du skapar kommer du sedan redovisa inför lärare och en mindre grupp studenter, i vilket du även får se andras arbeten också.

Detta projekt är även betygsättande för denna kurs med betygsskalan A-F. För betyget E (godkänt) ska du skapa ett fungerande spel baserat på kriterier du finner lite längre ner på denna sida. När kriterierna för betyget E är implementerat finns det fyra utmaningar som är värda en poäng styck om de implementeras. En poäng kommer öka ditt betyg med en nivå, givet att kriterierna för betyget E uppfylls. Ordningen på dessa har ingen betydelse, du är fri att välja bland dessa.

------

# Kriterier

**Kodstil:**
- Det får ej existera globala variabler.
- Inga minnesläckor får genereras.
- Inga oväntade programkraschar får uppstå.

**Övrigt:**
- Det är okej att använda standardbibliotekets behållare, exempelvis `std::vector` eller `std::map`.
- Det är okej att använda smarta pekare.

**Spelregler**
- Varje gång ormen äter en matbit ska ormens längd öka och användarens poäng ska ökas.
- Om ormens huvud kommer utanför kartan, eller på samma position som en annan kroppsdel, så är spelet slut.
- En matbit ska skapas på slumpmässig position med jämna intervall. Mat får ej skapas på en position som är utanför kartan, eller på en position som redan är ockuperad av antingen ormen eller en annan matbit.

**För betyget E:**
- All inmatning ska ske genom tangentbord, ej mus.
- Kartan ska bestå av diskreta koordinater. Vardera positition kan alltså nås med ett index för x- respektive y-led.
- Alla objekt som *ritas* i spelet ska vara en barnklass som ärver från en och samma abstrakta basklass. Funktionen som ritar ut objektet på skärmen, som en ruta eller ett tecken, ska överskuggas (override) i barnklassen. Detta gör att olika typer av objekt ritas annorlunda (exempelvis annorlunda färg eller tecken).
- Ormen ska bestå av ett antal objekt som *ritas ut* separat.
- Ormen ska uppdateras med jämna intervall, oavsett om inmatning sker eller ej från användaren.
- Ormens riktning ska gå att styra med hjälp av inmatning (WASD eller/och piltangenter).
- Mat ska skapas på kartan med jämna mellanrum.
- Du ska skapa ett klassdiagram som inkluderar alla klasses du implementerar som tydligt visar deras innehåll (variabler och funktioner) samt relationer mellan dem.
- Angiven kodstil följs
- Angivna spelregler ska följas

**För högre betyg (D-A):**
När du har implementerat kraven för betyget E har du möjlighet att samla poäng för högre betyg. Vardera extraval i listan nertill ger ett poäng var, där ett poäng ökar betyget med en nivå. Om inget extraval implementeras kommer projektet rättas för betyget E. Om exempelvis två extraval implementeras kommer projektet rättas för betyget C. Om exempelvis alla extraval implementeras kommer projektet rättas för betyget A.

- **Meny:** (1 poäng)
	- En meny innan spelet startar
	- När spelet är över återgår programme till menyn
	- Måste styras med piltangenter/WASD
	- Måste implementera minst 3 av följande menyval:
		- Nytt spel
		- Alternativ
		- Highscore (för nuvarande session)
		- Avsluta
		- Credits
- **Modifierare:** (1 poäng)
	- En effekt som påverkar spelet under en kortare tid.
	- Måste implementera minst 3 av följande effekter:
		- Odödlighet
		- Ökad hastighet
		- Bakvänd orm
		- Halvera ormens längd
		- Inverterade kontroller
- **Flerspelarläge:** (1 poäng)
	- Två spelare ska kunna spela spelet i samma fönster
	- Spelare kontrollerar var sin orm med WASD respektive piltangenter
- **Highscore sparas till fil:** (1 poäng)
	- Programmet ska spara de tio högsta poängen med tillhörande namn i en separat textfil.
	- Vid nytt highscore ska programmet fråga efter ett namn att spara poängen med.
	- Top-10 poäng med namn ska visas för spelare före och/eller efter spelet.

------

# Förklaring för högre betyg

## Meny

När programmet startar ska användaren se en meny med alternativ. Det ska alltid finnas ett alternativ som är markerat, och användaren kan ändra alternativ genom att trycka upp/ner eller W/S. När önskat alternativ är markerat ska användaren trycka *enter* för att välja alternativet.

## Modifierare

Under spelets gång ska det skapas modifierare på kartan. Likt matbitar kommer dessa skapas på en slumpmässig koordinat inom kartans ramar som inte redan är ockuperad av mat, orm, eller annan modifierare. När ormens huvud hamnar på samma koordinat som en modifierare ska modifieraren försvinna från kartan och dess effekt ska påbörja sin effekt.

För att detta extraval ska godkännas måste åtminstone tre av följande alternativ implementeras:

**Odödlighet**

Ormen ska under en begränsad tid tillåtas att åka igenom sin egen svans utan att spelet förloras. Det ska även vara möjligt att *teleporteras* från en kant av kartan till motstående kant. Exempelvis kan ormen åka rakt till höger, och de kroppsdelar som åker *utanför* kartans högra sida kommer fortsätta från vänster sida av kartan istället.

**Ökad hastighet**

Ormen ska under en begränsad tid flyttas snabbare genom att korta ner på tiden mellan varje uppdatering. Detta ska göra spelet svårare, då det kräver att användaren måste reagera snabbare. Den ökade hastigheten ska vara tydlig i relation till den ordinarie hastiheten.

**Bakvänd orm**

När denna effekt aktiveras kommer ormen, sett från spelarens ny, att börja åka *baklänges*. Sista kropssdelen på ormen kommer från och med detta ögonblick nu bli ormens huvud, och det ordniarie huvudet kommer nu bli ormens sista kroppsdel istället.

**Halvera ormens längd**

När denna effekt aktiveras kommer ormens hälften av ormens svans att försvinna utan att poäng dras bort för det nuvarande spelet. 

**Inverterade kontroller**

Under en begränsad tid kommer användarens inmatning bli inverterade. Under denna period kommer t.ex. vänsterpil/A styra ormen till höger, och uppåtpil/W kommer styra ormen neråt.

**Flerspelarläge**

När spelet startar ska det finnas två ormar på samma karta, där tanken är att två spelare kan styra var sin orm. Första spelaren styr sin orm mha. WASD, och andra spelaren styr sin orm mha. piltangenter. En spelares orm kommer försvinna om dess huvud krockar med antingen en vägg eller någon kroppsdel från den själv eller den andra ormen. Om en orm försvinner kommer spelet fortsätta fram tills att båda ormarna försvunnit. I detta läge sparas poäng för båda spelarna invidivuellt, så det är möjligt att tävla och jämföra mot varandra.

**Highscore sparas till fil:** 

En textfil ska existera som sparar upp till tio bästa poängen med namn från spelade sessioner. När ett spel är över ska programmet kontrollera om spelets poäng ska sparas. Om poängen ska sparas ska programmet fråga efter användarens namn och spara detta med poängen i *highscore*-filen. Om filen inte innehåller tio *highscores* än, kommer den nya poängen alltid att sparas.

Efter varje spel, oavsett om ett nytt highscore har nåtts eller inte, ska alla sparade *highscores* visas på skärmen tills att användaren ger ett kommando att återgå till ett nytt spel eller stänga av spelet; det viktiga här är att användaren ska ha möjlighet att se vilka *highscores* som existerar. För detta måste alltså existerande *highscores* läsas in.

Ett exempel på en highcore-fil kan vara:
```
210 Joakim
200 Mattias
130 AAA
100 Marcus
30 AAA
```

Highscore-filen ska vara sorterad på poäng, och får högst innehålla tio *highscores*. Namn tillåts att upprepas, exempelvis får två *highscores* ha samma namn.

------

# Demo och installation

Till alla demos medföljer det en `makefile` samt källkod. Att använda denna källkod kommer ej ses som plagiat. Det är fritt att använda och modifiera den som du vill.

Medföljande `makefile` kan användas för att installera allt som behövs för vardera bibliotek. Det är inget krav att använda `make` i ditt projekt, men vill du simplifiera din kompilering och länkning har vi lagt in kommenterar som gör det lättare för dig att modifiera filen där det behövs. Mycket är automatiserat, exempelvis kommer alla source-filer i mappen `src/` att kompileras, och alla dessa kommer automatiskt ha tillgång till alla header-filer i `include/`.

Alla demos tillåter dig att köra `make install` som kommer installera vad som tillåts genom `make` och ger utskrifter för det du måste installera på egen hand. Just `ncurses` är i många fall förinstallerat, och kör du MacOS kommer detta med xcode. `SFML` däremot kräver lite mer förberedelser som du kan läsa om nedan.

Efter installation kan du köra `make clean all` för att kompilera på nytt, och `make run` för att exekvera programmet (går att kombinera med `make clean all run`). `makefile` Är skapad att först kompilera alla källfiler till objektfiler, sedan länka dessa till en exekverbar fil.

**SFML för WSL** 

Om du vill installera `SFML` till WSL på egen hand: (kom ihåg att integrera med X11, ex. `Xming`, för att skapa fönster)
https://www.sfml-dev.org/tutorials/2.5/start-linux.php

SFML skapar ett eget fönster för rendering, men eftersom WSL inte har direkt tillgång att göra detta i Windows används `Xming`. I demot medföljer installationsfil och instruktioner för `Xming`, det är bara att köra `make install` i terminalen och följa de instruktioner som ges.

Notera att programmet `Xming` behöver startas inför varje session, vilket är lätt att glömma och man funderar på varför ens projekt inte går att köra. Du måste även beskriva för WSL att `Xming` ska användas inför varje session, vilket du gör med kommandot `export DISPLAY=:0`. Allt detta nämns i demot.

**SFML för MacOS**

Om du vill installera `SFML` till MacOS på egen hand: (Skippa sektionen *Create your first SFML program*, detta sköter vi med make)
https://www.sfml-dev.org/tutorials/2.5/start-osx.php

Kör `make install`, `make` kommer följa instruktionerna i länken ovan och placera rätt filer i rätt mappar. När du sen försöker länka programmet under `make clea all` kommer din dator varna för att någon sfml-lib inte är skapad av en känd utvecklare; TA INTE BORT FILERNA. SFML är både gammalt och pålitligt. Vad du behöver göra är att ge tillåtelse för alla *libbar* att användas. Detta kan du göra genom att följa listan nedan.

Kan behöva göras innan varje session: (Uppdaterar om jag hittar en lättare lösning)
- Systeminställningar
	- Säkerhet och integritet
		- (Tab) Integritet
			- (Vänster spalt) Klicka på 'Utvecklarverktyg'
			- (Nere vänster) 'Klicka på låset om du vill göra ändringar'
			- (Höger ruta) Klicka på 'Terminal'
				- Skriv in lösenord och godkänn

------

# Komma igång

Rekommenderade steg att komma igång med ditt projekt:

1. Ladda ner och inspektera demo för `ncurses` och `SFML`. Välj den du känner ger dig en rimlig utmaning för den tid du är given. Sök gärna upp fler exempel för vardera bibliotek, samt dokumentation för det bibliotek du vill använda.

2. Skapa ett basprojekt som låter dig rita en ruta/symbol på önskad koordinat, låt oss kalla detta ditt *scenobjekt*.

3. Skapa funktionalitet att flytta på ditt scenobjekt up/ner/höger/vänster med antingen piltangenter eller WASD.

4. Uttöka din *spel-loop* att flytta på ditt scenobjekt med jämna mellanrum, exempelvis varje `0.5` sekunder, även när användaren inte gör någon inmatning. Låt scenobjetet förflytta sig i den senaste angivna riktningen från användaren.

5. Skapa en 'svans' av mer scenobjekt som följer ditt ursprungliga scenobjekt.

	- Ta fram papper och penna och designa ett klassdiagram för vad du i nuläget tror behöver existera i detta projekt, och relationer mellan dessa. Exempelvis ska det existera en abstrakt basklass för allt som ska ritas i spelet, hur ser detta ut i ett klassdiagram? Vad ska ärva från denna basklass? Hur ska din orm vara implementerad? Ha som mål att skapa en orm med godtycklig längd

	- Testa din design i kod. Fungerar det som du tänkt? Behöver någonting modifieras i ditt klassdiagram?

6. Du har nu kommit igång och är på god väg åt rätt riktning. Lycka till! :)

# Examination

Projeket ska lämnas in som en `.zip`-fil i CodeGrade innan deadline. Bedömning sker för det projekt som lämnas in, vilket förväntas vara samma som sedan redovisas.
