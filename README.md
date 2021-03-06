# Playbook
Codestyle, konvensjoner etc for Rubynor.

## Versjonskontroll
- Bruk feature branches. Branchnavnet skal være i kebab-case (`my-super-branch`, ikke `my_super_branch`). Navnet skal beskrive klart hva endringen består i.
- Commits skal fortrinnsvis gjøre én ting.
- Bruk meningsfulle commit messages. Husk at commit messages er en hjelp til folk som leser koden og forsøker å forstå hvorfor ting er gjort. Gode eksempler: `Bugfix: Representanten hopper til nederst i listen når de oppdateres`, `Tabeller for møter`, `Gjør login-knappen mer synlig i menyen`. Dårlige eksempler: `Fikset en bug`, `WIP: prøver å fikse representanter`


## Sjekkliste før man lager en pull request
- *Les over diffen på Github før du lager PR-en og se om du finner noen feil*
- Er det utkommentert kode her? I så fall - fjern.
- Er det print statements og annet debug her? I så fall - fjern.
- Dersom det er migrations:
  - Har de fornuftige navn?  
  - Vil de fungere uten å måtte resette databasen?
  - Har du oppdatert seed data? 
  - Har du migrert eksisterende data? (Eksempel: Om du legger til en constraint om at alle `Meetings` må ha en `status`, må du i migrasjonen sørge for at alle de nåværende møtene også får en `status`)
  - Har nye felter fornuftige default-verdier? Spesielt: Har boolean-felter en default-verdi?
- Dekker pull requesten en og bare en endring? Hvis ikke, vurder å splitte opp PR-en i flere.
- Har du innført nye n+1 queries?
- Er det indexer på alle databasefelter du slår opp data på?
- Har du addet alle filene?
- Har du fjernet autogenererte filer (spesielt fra `rails generate`)?
- Har du brukt variabler, metodeparametre, gems, imports etc tidligere som du har glemt å fjerne?
- Kjører testene?
- Har du skrevet nye tester for endringene du har gjort?
- Har du testet at det virker lokalt på din egen maskin?
- Har du tenkt på alle edge cases?
- Er branchen rebaset mot siste master?
- Har du ved et uhell innført noen ting ved en merge/rebase som ikke skulle vært der?

## Sjekkliste etter at man har laget en pull request
- Klager Semaphore på noe?
- Klager Code Climate på noe?
- Virker review-appen?

## Når PRen er klar til review
- Legg kortet i "review"-kolonnen i Trello
- Gi beskjed på Slack om at det er en PR klar til review
- Få feedback fra minst en reviewer. Rett feil, spør om det er noe du lurer på.
- Gi beskjed når du er klar til ny review
- Fortsett med denne sirkelen til en reviewer gir deg tommel opp for merge
- Merge inn i master - gjør gjerne en rebase for å merge sammen småfikser
- Slett branchen når den er merget
- Sjekk at staging fungerer, siden master automatisk deployerer til staging
- Flytt kortet til 'done'-kolonnen i Trello

## Sjekkliste hvis man har promotet staging til produksjon
- Har du kjørt `rails db:migrate` om det er databaseendringer?
- Har du sjekket at det virker? Om det er to eller flere "brukertyper", sjekk med alle
- Har du lagt til noe som krever setup på Heroku? Eksempelvis første deploy som tar i bruk epost - da må sendgrid eller lignende settes opp

## Styleguide

### Rails
Følg https://github.com/thoughtbot/guides/tree/master/style/rails

### Ruby
Følg https://github.com/thoughtbot/guides/tree/master/style/ruby


## Verktøy

### Trello
* Backlog (planlagte oppgaver)
* Doing (Hva du jobber på akkurat nå)
* Review (oppgaver som er i PR-review)
* I produksjon siden sist
* Done

#### Konvensjoner
* Husk å assigne deg selv til en oppgave når du setter i gang med den (og ikke lenge før)
* Før du tar en ny oppgave - vær HELT sikker på at du ikke kommer videre med den/de du jobber på allerede, og at det du holder på med er helt ferdig, i følge denne guiden
* Når det er du som har programmert oppgaven, er det ditt ansvar å sørge for at den havner hele veien i produksjon - det inkluderer å mase om folk ikke gir deg code review og faktisk pushe ting til staging- og produksjonsmiljø (og teste at det virker når det ER i disse miljøene)
