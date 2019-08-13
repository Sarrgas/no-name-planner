# no-name-planner
Jag vill göra ett ordentligt hobby-projekt. Ett webbsystem för att planera musikalproduktioner, bandrep och dylikt.
Systemet har ännu inget namn, vilket är OK under kravsamlingsfas, men namnet borde spikas innan kodprojekt startar, då vissa saker (Visual Studio, databaser osv) kan bli mycket trassel att byta namn på efteråt.

# Kravinsamling
Här samlar jag de krav jag kommer på, och hittar/hör på annat håll.

## Repetition
Systemets kärnfunktion bör vara hantering av "rep". Ett rep innehåller tid och plats, så väl som vilka roller/personer som ska vara med (Exempelvis "Dansare" eller "Stråksektionen") samt instuderingsmaterialet inför repet. Det ska även finnas plats för material efter repet. Exempelvis ett filmklipp från danskoreografin, ljudinspelningar osv.

## Roller och Grupper
I kopplar man vem som gör vad genom att ge de Roller. Exempelvis "Ensemble", "Dans", "Melchior (huvudroll)", "Orkester". Dessa roller kan grupperas i grupper. Alternativt bara grupper? Gör det mer skada än nytta med flera steg här, kanske?

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
- Behövs en webhost? Nginx?
