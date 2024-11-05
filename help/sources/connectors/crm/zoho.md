---
keywords: Experience Platform;hem;populära ämnen;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Zoho CRM Source Connector - översikt
description: Lär dig hur du ansluter Zoho CRM till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# [!DNL Zoho CRM]

>[!IMPORTANT]
>
>[!DNL Zoho CRM]-källan kommer att bli inaktuell i slutet av maj 2025. Du kan också använda källan [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md).

Adobe Experience Platform tillåter att data hämtas från externa källor samtidigt som du får möjlighet att strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från ett CRM-system från tredje part. Stöd för CRM-providers omfattar [!DNL Zoho CRM].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Hämta autentiseringsuppgifter för [!DNL Zoho CRM]

Innan du kan hämta data från ditt [!DNL Zoho CRM]-konto till plattformen måste du först hämta dina autentiseringsuppgifter för att autentisera din [!DNL Zoho CRM]-källa. Följ stegen nedan för att hämta klient-ID, klienthemlighet, åtkomsttoken och uppdatera token.

### Registrera ditt program

Det första steget för att hämta autentiseringsuppgifter är att registrera programmet med [[!DNL Zoho CRM] utvecklarkonsolen](https://accounts.zoho.com/). Om du vill registrera ditt program måste du välja klienttyp från: JavaScript, webbaserade, mobila, icke-webbläsarbaserade mobilprogram eller självklient. Ange sedan värden för programnamnet, webbsidans URL och en auktoriserad omdirigerings-URI som [!DNL Zoho CRM] sedan kan använda för att omdirigera dig med en anslagstoken.

En lyckad registrering returnerar ditt klient-ID och din klienthemlighet.

### Skapa en auktoriseringsbegäran

Därefter måste du skapa en [auktoriseringsbegäran](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) med antingen ett webbaserat program eller en självklient. Auktoriseringsbegäran returnerar din anslagstoken, som i sin tur låter dig hämta din åtkomsttoken.

När du skapar en auktoriseringsbegäran måste du fylla i värden för både **scope** och **åtkomsttypen**. Mer information om omfång finns i det här [[!DNL Zoho CRM] dokumentet](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html), medan **åtkomsttypen** alltid ska anges till `offline`.

### Generera åtkomsttoken och uppdatera token

När du har hämtat din anslagstoken kan du generera din [åtkomst- och uppdateringstoken](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) genom att göra en begäran om POST till `{ACCOUNTS_URL}/oauth/v2/token` och samtidigt ange ditt klient-ID, din klienthemlighet, din anslagstoken och omdirigerings-URI. Under det här steget måste du även inkludera `grant_type` som en parameter och ange värdet som `"authorization_code"`.

En lyckad begäran returnerar dina token för åtkomst och uppdatering, som du sedan kan använda för att autentisera.

Detaljerade anvisningar om hur du hämtar dina autentiseringsuppgifter finns i [[!DNL Zoho CRM] autentiseringsguiden](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Anslut [!DNL Zoho CRM] till [!DNL Platform] med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Zoho CRM] till plattformen med API:er eller användargränssnittet:

- [Skapa en  [!DNL Zoho CRM] basanslutning med API:t för Flow Service](../../tutorials/api/create/crm/zoho.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)

## Anslut [!DNL Zoho CRM] till [!DNL Platform] med användargränssnittet

- [Skapa en  [!DNL Zoho CRM] källanslutning i användargränssnittet](../../tutorials/ui/create/crm/zoho.md)
- [Skapa ett dataflöde för en CRM-källanslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)
