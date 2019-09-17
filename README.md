# no-name-planner
Jag vill göra ett ordentligt hobby-projekt. Ett webbsystem för att planera musikalproduktioner, bandrep och dylikt.
Systemet har ännu inget namn, vilket är OK under kravsamlingsfas, men namnet borde spikas innan kodprojekt startar, då vissa saker (Visual Studio, databaser osv) kan bli mycket trassel att byta namn på efteråt.
Systemet ska kunna ersätta ett excel-baserat repschema, se exempel i screenshot "excel-schema.png".

Potentiella namn:
* Roperia
* Roperon
* Ropendar

# Kravinsamling
Här samlar jag de krav jag kommer på, och hittar/hör på annat håll.
Systemets fokus bör ligga på att hjälpa arrangörerna. Systemets användare är därmed huvudsakligen regissörer och dylikt. Att andra roller kan nå systemet är en bonus, för att se repschema och registrera sin frånvaro.

<b>En problemställning</b>: Inloggning och användarkonton. Jag vill ha någon nivå av användarkonton för följande krav:
- Systemet måste kunna användas av flera musikaluppsättningar på olika håll utan att påverka varandra. Exempelvis om både WES och Decibel vill nyttja det, ska de kunna leva i olika "bubblor".
- "Vanliga" användare ska kunna rapportera sin egen frånvaro ("jag är utomlands dessa datum") och även se sitt personliga schema.

MEN jag vill undvika en situation där arrangören är beroende av att samtliga deltagare har registrerat ett eget konto. Arrangören måste kunna planera repen utan registrerade användarkonton.
Ska en deltagare kunna använda systemet "anonymt" (utan konto)? Hur hade det funkat med första punkten ovan? Ha projektnamnet i URLen helt enkelt?

<b>Lösningsförslag</b>: Arrangören registrerar ett konto, och skapar ett nytt projekt. Där kan hen ange en fullständig lista med deltagare, varpå deltagarna "finns" och kan användas fullt ut av arrangören. Senare kan deltagarna frivilligt skapa egna konton och säga "Detta är jag" på en av deltagarna.
Genom att helt enkelt inkludera projektets genererade ID i URLen kan en deltagare se rep, material och scener utan inloggning. Att nyttja ett genererat icke-sekventiellt ID istället för projektnamn ger flera fördelar. Dels kan flera arrangörer skapa projekt med samma namn (exempelvis "Terminsavslutning"), och icke-sekventiell generering sänker risken att gå in på någon annans projekt (om ditt projekt har ID 5, finns det sannolikt ett projekt med ID 4). Personligt schema och frånvarohantering fungerar då genom att välja deltagare i en lista.

## Repetition
Systemets kärnfunktion bör vara hantering av "rep". Ett rep innehåller tid och plats, så väl som vilka roller/personer som ska vara med (Exempelvis "Dansare" eller "Stråksektionen") samt instuderingsmaterialet inför repet. Det ska även finnas plats för material efter repet. Exempelvis ett filmklipp från danskoreografin, ljudinspelningar osv.
På "rep"-sidan bör det även visas vilka som har förhinder pga planerad frånvaro.
Det behöver även finnas möjlighet att registrera oplanerad frånvaro. Om Person A aldrig dök upp på repet, eller blev sjuk, ska det gå att registreras efteråt. Detta för att underlätta översiktsvyn.
Då rep ibland kan vara långa - exempelvis heldagsrep - bör man även kunna ange estimerat schema under dagen. Exempelvis om Person A bara deltar i Scen 5, men vi har ett heldagsrep för Scen 1-8, ska inte Person A behöva slösa hela sin dag om hen bara behövdes i en timme.

## Roller och Grupper
Här kopplar man vem som gör vad genom att ge dem Roller. Exempelvis "Ensemble", "Dans", "Melchior (huvudroll)", "Orkester". Dessa roller kan grupperas i grupper. Alternativt bara grupper? Gör det mer skada än nytta med flera steg här, kanske?

## Användare
En användare ska kunna gå in och se sitt personliga schema - baserat på vilka rep hen är registrerad på. Hen ska även kunna rapportera sin planerade frånvaro på sin profil, vilket då kommer synas på repen.

## Scener
Ett perspektiv man ska kunna se i systemet är helhetsbilden av uppsättningen. Exempelvis om man vill titta på materialet från Akt 1 scen 5 så behöver man inte leta upp avsett rep, utan man kan navigera till "Akt 1 scen 5" från helhetsbilden, och därmed se allt material från tidigare rep. Samt frånvaro-status om någon missat att repa just denna scen. Eventuell en "status" på hur välrepad denna scen är - alltså om den behöver mer jobb eller är "färdig".
Bonus: En yta med "övergripande" information om föreställningen i helhet. Exempelvis manus, karaktärsblad, spellistor, videolänkar, rekvisitalistor, scen-modeller osv....

## Icke-funktionella krav
Systemet ska vara någorlunda mobilanpassat. Åtminstone vad gäller läsning. Man ska kunna fråga sig "Vad skulle vi göra nästa rep?" och få svar genom mobilsidan.

# Teknikstack
Detta segment är mer för min egen skull. Jag vill göra detta som en övning, och bör därför välja tekniker efter vad jag vill lära mig.

- Frontend med Vue
- Stil med Vuetify
- Mobilapp med Cordova (?) (https://cordova.apache.org/)
- Backend med .NET Core
- Databas med PostgreSQL
- Docker
- Hostad på Heroku

Notera: Om du vill nyttja Cordova för appar kan det vara sund att hålla frontend och backend helt separerade. Det är bara frontenden jag vill konvertera till app, backenden ska köras på en server oavsett.

# GUI-tankar
Gränssnittet behöver två lägen (menyval?). Visningsläge och adminläge. Jag estimerar att visningsläget huvudsakligen kommer användas från mobiler, medan admin-läget kan prioritera en desktop-experience.
## Visningsläget
Visningsläget är default-sidan för alla som går in på systemet, och har huvudsakligen tre sidor: Rep, Scener och Profil
### Rep-sidan
Repsidan visar by-default nästa rep i fokus. Men man kan skrolla sig till både gamla rep och efterkommande rep (om de har registrerats ännu). Varje rep visar: Tid och plats, vilken scen som repas, med vilka personer, samt länkar till material (Manus, filmklipp (Google Drive/Youtube) osv). Implementeras med en namngiven länk helt enkelt. En länk "manus" kan gå till ett Google Drive dokument.
Listan på rep kan filtreras genom ett filter "Visa bara mina rep", varpå man endast visar de rep som användaren är registrerad på.
### Scener-sidan
På scener-sidan får man en helhetsbild av föreställningen. Den visar en lista med scener (som cards), uppdelade i akter. Varje card visar namnet på scenen, dens "status" och hur många gånger man repat den. Man ska kunna sortera denna lista efter: Kronologisk ordning (ordningen de kommer i musikalen), antal rep (lägsta till högsta) och status (värsta till bästa).
När man klickar sig in på en scen kan man ta del av allt material - instudering, manus, filmklipp från tidigare rep. Man ska kunna nå materialet utan att minnas vilket rep det var ifrån, MEN det bör framgå på något vis vilket rep det var ifrån. Om man exempelvis material 1 säger emot material 2, så behöver man veta vilken information som var nyast, då den sannolikt gäller. 
BONUS: Infon om vilket rep det var ifrån borde vara en länk till avsett rep.

### Profil
Användarens personliga profil. Här rapporterar hen bland annat planerad frånvaro, och kan även se vilka grupper hen blivit tilldelad.
I samband med frånvaron kan hen även se en lista på de rep hen har missat, med länk till avsett rep. Så de kan öva materialet på egen hand. 
NOTE: Just nu kommer jag bara på just "planerad frånvaro" som en feature i Profil-sidan. Om det bara blir det, kanske det går att implementera på annat vis?

## Adminläge
Adminläget är där arrangören går in och planerar nya rep, nya scener, grupperar personer i grupper osv.
