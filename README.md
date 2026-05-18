# Hva trenger man dette prosjektet til?

JasperReports tilbyr en måte å tilgjengeliggjøre fonter på. Dett kalles "Font extentions".
Dette er et alternativ til å tilgjengeliggjøre fonter på OS nivå eller på JVM nivå.




## Hvilke fonter finnes
### Mulish 
https://fonts.google.com/specimen/Mulish

I forhold til Arial så har denne en tanke større linjehøyde slik at man i mange tilfeller må gå ned en skriftstørrelse
dersom det er kritisk at designet er det samme som før ved overgang fra Arial.
Mulish Bold er også vesentlig bredere enn Arial og har dermed ulik linjebrekking.


### Fira Sans
https://fonts.google.com/specimen/Fira+Sans

Denne ligner Mulish og Arial og har samme linjehøyde som Arial. Denne er funnet til å være drop-in kompatibel med Arial
samtidig som den ligner veldig på Mulish. 

Disse fontene er lisensiert under SIL Open Font License (OFL). Se /src/main/resources/no/kartverket/fonts for detaljer

# Publisering
Pakken ble tidligere publisert til Nexus. Gamle versjoner av pakken er migrert til GitHub Packages.

Nye pakker publiseres til [GitHub Packages](https://github.com/orgs/kartverket/packages?repo_name=matrikkel-jasperreports-fonts) via [build-push.yml](.github/workflows/build-publish.yml) workflowen.
Ved hver push til `master` så vil det bygges og publiseres en ny versjon av pakkene.


## Versjonering
Pakken har versjonsnummer som er av formatet `[Major version].[Date].[SHA]`
Versjonsnummeret oppdateres ved hver publisering.

`[Major version]` oppdateres ved breaking changes og kan endres i [build-push.yml](.github/workflows/build-publish.yml) workflowen.
