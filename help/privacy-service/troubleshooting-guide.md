---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Frågor och svar om sekretessservice
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 7e2e36e13cffdb625b7960ff060f8158773c0fe3

---


# Frågor och svar om sekretessservice

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform Privacy Service.

Integritetstjänsten tillhandahåller ett RESTful API och användargränssnitt som hjälper företag att hantera förfrågningar om kunddata. Med Integritetstjänsten kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata, vilket underlättar automatiserad efterlevnad av organisatoriska och juridiska sekretessbestämmelser.

## Kan jag använda integritetstjänsten för att rensa upp data som av misstag skickats till plattformen?

Adobe stöder inte användning av Integritetstjänst för att radera data som av misstag har skickats till en produkt. Integritetstjänsten är utformad för att hjälpa dig att uppfylla dina skyldigheter när det gäller att få tillgång till eller radera information för registrerade (eller konsumenter). Dessa förfrågningar är tidskänsliga och har slutförts med avseende på tillämplig integritetslagstiftning. Inlämning av förfrågningar som inte är förfrågningar om tillgång till eller radering av registrerade personer/konsumenter påverkar alla kunder inom integritetstjänsten och möjligheten för integritetstjänsten att ge stöd för lämpliga rättsliga tidsramar.

Kontakta din kontoansvarige (CDM) för att koordinera och göra en insats för att ta bort eventuella PII- eller dataproblem.

## Hur får jag information om status för min sekretessförfrågan eller mitt jobb?

Du kan hämta information om ett visst jobb genom att använda sekretesstjänstens API eller användargränssnittet.

### Använda API

Om du vill hämta statusen för ett visst jobb med hjälp av sekretesstjänstens API, gör du en begäran till rotslutpunkten (`GET /`) med hjälp av jobbets ID i sökvägen för begäran. Mer information finns i avsnittet om [att kontrollera statusen för ett jobb](api/privacy-jobs.md#check-the-status-of-a-job) i utvecklarhandboken för Integritetstjänst.

### Använda gränssnittet

Alla aktiva jobbförfrågningar visas i widgeten **Jobbförfrågningar** på kontrollpanelen för sekretesstjänster. Statusen för varje jobbförfrågan visas under **statuskolumnen** . Mer information om hur du visar jobbförfrågningar i användargränssnittet finns i användarhandboken [för](ui/user-guide.md)sekretesstjänsten.

## Hur hämtar jag resultaten från mina slutförda sekretessjobb?

Sekretesstjänstens API och användargränssnittet innehåller båda metoder för att hämta resultaten av slutförda jobb i ZIP-format.

### Använda API

Gör en begäran till rotslutpunkten (`GET /`) i sekretesstjänstens API, med ID:t för det jobb vars resultat du vill hämta i sökvägen för begäran. Om jobbets status är slutförd inkluderar API:t ett `downloadURL` -attribut i svarstexten. Det här attributet innehåller en URL som du kan klistra in i webbläsarens adressfält för att hämta ZIP-filen.

Mer information finns i avsnittet om hur du [söker efter ett jobb med hjälp av dess ID](api/privacy-jobs.md#check-the-status-of-a-job) i utvecklarhandboken för Integritetstjänst.

### Använda gränssnittet

På kontrollpanelen för sekretesstjänster hittar du det jobb som du vill hämta från **widgeten** Jobbförfrågningar. Klicka på ID:t för jobbet för att öppna sidan _Jobbinformation_ . Hämta ZIP-filen genom att klicka på **Hämta** i det övre högra hörnet. Mer information finns i användarhandboken [för](ui/user-guide.md) Integritetstjänst.