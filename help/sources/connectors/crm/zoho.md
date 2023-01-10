---
keywords: Experience Platform;hem;populära ämnen;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Zoho CRM Source Connector - översikt
description: Lär dig hur du ansluter Zoho CRM till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från ett CRM-system från tredje part. Stöd för CRM-leverantörer innefattar [!DNL Zoho CRM].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Hämta autentiseringsuppgifter för [!DNL Zoho CRM]

Innan du kan hämta data från [!DNL Zoho CRM] konto till Platform måste du först hämta dina autentiseringsuppgifter för att autentisera [!DNL Zoho CRM] källa. Följ stegen nedan för att hämta ditt klient-ID, din klienthemlighet, din åtkomsttoken och din uppdateringstoken.

### Registrera ditt program

Det första steget i att hämta inloggningsuppgifterna är att registrera programmet med [[!DNL Zoho CRM] utvecklarkonsol](https://accounts.zoho.com/). Om du vill registrera programmet måste du välja klienttyp: JavaScript, webbaserade, mobila, icke-webbläsarbaserade mobilprogram eller självklient. Ange sedan värden för programnamnet, webbsidans URL och en auktoriserad omdirigerings-URI som [!DNL Zoho CRM] Du kan sedan använda för att omdirigera dig med en anslagstoken.

En lyckad registrering returnerar ditt klient-ID och din klienthemlighet.

### Skapa en auktoriseringsbegäran

Sedan måste du skapa en [auktoriseringsförfrågan](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) med antingen ett webbaserat program eller en självklient. Auktoriseringsbegäran returnerar din anslagstoken, som i sin tur låter dig hämta din åtkomsttoken.

När du skapar en auktoriseringsbegäran måste du fylla i värden för båda **scope** och **åtkomsttyp**. Se detta [[!DNL Zoho CRM] dokument](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) för mer information om omfång, medan **åtkomsttyp** ska alltid anges till `offline`.

### Generera åtkomsttoken och uppdatera token

När du har hämtat din anslagstoken kan du generera [komma åt och uppdatera token](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) genom att göra en POST-förfrågan till `{ACCOUNTS_URL}/oauth/v2/token` samtidigt som ditt klient-ID, din klienthemlighet, din anslagstoken och omdirigerings-URI tillhandahålls. Under det här steget måste du även inkludera `grant_type` som en parameter och ange värdet som `"authorization_code"`.

En lyckad begäran returnerar dina token för åtkomst och uppdatering, som du sedan kan använda för att autentisera.

Detaljerade anvisningar om hur du hämtar dina inloggningsuppgifter finns i [[!DNL Zoho CRM] autentiseringsguide](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Anslut [!DNL Zoho CRM] till [!DNL Platform] använda API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Zoho CRM] till Plattform med API:er eller användargränssnittet:

- [Skapa en [!DNL Zoho CRM] basanslutning med API:t för Flow Service](../../tutorials/api/create/crm/zoho.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)

## Anslut [!DNL Zoho CRM] till [!DNL Platform] med användargränssnittet

- [Skapa en [!DNL Zoho CRM] källanslutning i användargränssnittet](../../tutorials/ui/create/crm/zoho.md)
- [Skapa ett dataflöde för en CRM-källanslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)
