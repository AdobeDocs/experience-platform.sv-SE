---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Felsökningsguide för Privacy Service
description: Det här dokumentet innehåller svar på vanliga frågor om Privacy Service samt information om vanliga fel i API:t.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# [!DNL Privacy Service] felsökningsguide

Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful-API och användargränssnitt som hjälper företag att hantera förfrågningar om kunddata. Med [!DNL Privacy Service]kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata, vilket underlättar automatiserad efterlevnad av organisatoriska och juridiska sekretessbestämmelser.

Det här dokumentet innehåller svar på vanliga frågor om [!DNL Privacy Service]samt information om vanliga fel i API:t.

## Vad är skillnaden mellan en användare och ett användar-ID när sekretessförfrågningar görs i API:t? {#user-ids}

JSON-nyttolasten för begäran måste innehålla en `users` en array som innehåller specifik information för varje användare som sekretessbegäran gäller för. Varje objekt i `users` arrayen är ett objekt som representerar en viss användare, som identifieras av dess `key` värde.

Varje användarobjekt (eller `key`) innehåller en egen `userIDs` array. Den här arrayen visar specifika ID-värden **för en viss användare**.

Titta på följande exempel `users` array:

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

Arrayen innehåller två objekt, som representerar enskilda användare som identifieras av deras `key` värden (&quot;DavidSmith&quot; och&quot;user12345&quot;). &quot;DavidSmith&quot; har bara ett angivet ID (deras e-postadress), medan &quot;user12345&quot; har två (deras e-postadress och ECID).

Mer information om att tillhandahålla information om användaridentitet finns i handboken om [identitetsdata för sekretessförfrågningar](identity-data.md).


## Kan jag använda [!DNL Privacy Service] för att rensa data som av misstag har skickats till [!DNL Platform]?

Adobe stöder inte användning av [!DNL Privacy Service] för att radera data som av misstag har skickats till en produkt. [!DNL Privacy Service] är utformat för att hjälpa dig att uppfylla dina skyldigheter för den registrerade (eller konsumenten) att få tillgång till eller ta bort uppgifter. All annan användning av Privacy Service för datarensning eller underhåll stöds inte eller tillåts inte.

Begäran om sekretess är tidskänslig och har fyllts i med avseende på tillämplig integritetslagstiftning. inlämning av ansökningar som inte är registrerade eller behandlade som ger tillgång till eller tar bort uppgifter påverkar alla [!DNL Privacy Service] kunder och möjlighet att [!DNL Privacy Service] stödja lämpliga rättsliga tidslinjer. Det finns nu en hög överföringsgräns per dag för att förhindra missbruk av tjänsten.

Kontakta kontoteamet på Adobe för att koordinera och vidta åtgärder för att ta bort eventuella PII- eller dataproblem.

## Hur får jag information om status för min sekretessförfrågan eller mitt jobb?

Du kan hämta information om ett visst jobb genom att använda [!DNL Privacy Service] API eller användargränssnitt.

### Använda API:et

Så här hämtar du status för ett visst jobb med [!DNL Privacy Service] API, gör en begäran till roten (`GET /`) slutpunkt, med jobbets ID i sökvägen för begäran. Mer information finns i avsnittet om [kontrollera status för ett jobb](api/privacy-jobs.md#check-the-status-of-a-job) i [!DNL Privacy Service] API-guide.

### Använda gränssnittet

Alla aktiva jobbbegäranden visas i listan i **[!UICONTROL Job Requests]** widgeten på [!DNL Privacy Service] Kontrollpanel för användargränssnitt. Statusen för varje jobbförfrågan visas under **[!UICONTROL Status]** kolumn. Mer information om hur du visar jobbförfrågningar i användargränssnittet finns i [Användarhandbok för Privacy Service](ui/user-guide.md).

## Hur hämtar jag resultaten från mina slutförda sekretessjobb?

The [!DNL Privacy Service] API och användargränssnitt innehåller båda metoder för att hämta resultaten av slutförda jobb i ZIP-format.

### Använda API:et

Gör en begäran till roten (`GET /`) i [!DNL Privacy Service] API, med ID:t för jobbet vars resultat du vill hämta i sökvägen för begäran. Om jobbets status är klar innehåller API:t en `downloadURL` i svarstexten. Det här attributet innehåller en URL som du kan klistra in i webbläsarens adressfält för att hämta ZIP-filen.

Mer information finns i avsnittet om [söka efter ett jobb med dess ID](api/privacy-jobs.md#check-the-status-of-a-job) i [!DNL Privacy Service] API-guide.

### Använda gränssnittet

På [!DNL Privacy Service] Kontrollpanelen för användargränssnittet hittar du det jobb du vill hämta från **Jobbförfrågningar** widget. Välj ID för jobbet för att öppna sidan Jobbinformation. Välj **Ladda ned** i det övre högra hörnet för att ladda ned ZIP-filen. Se [Användarhandbok för Privacy Service](ui/user-guide.md) för mer detaljerade steg.

## Vanliga felmeddelanden {#common-error-messages}

I följande tabell beskrivs några vanliga fel i [!DNL Privacy Service], med beskrivningar som hjälper till att lösa deras respektive problem.

| Felmeddelande | Beskrivning |
| --- | --- |
| Användar-ID:n hittades inte. | Vissa användar-ID:n som angavs i begäran kunde inte hittas och hoppades över. Kontrollera att du använder rätt namnutrymme(n) och ID-värden i nyttolasten för begäran. Visa dokumentet på [tillhandahålla identitetsdata](./identity-data.md) om du vill ha en mer detaljerad förklaring. |
| Ogiltigt namnutrymme | Ett angivet ID-namnområde för ett användar-ID var ogiltigt. Se avsnittet om [standardidentitetsnamnutrymmen](./api/appendix.md#standard-namespaces) i [!DNL Privacy Service] API-guide för en lista över godkända namnutrymmen. Om du använder ett anpassat namnutrymme kontrollerar du att du anger ID:n `type` egenskapen &quot;custom&quot;. |
| Delvis slutförd | Jobbet slutfördes, men vissa data var inte tillämpliga för den angivna begäran och hoppades över. |
| Data har inte det format som krävs. | Ett eller flera av datavärdena för det angivna programmet var felaktigt formaterade. Mer information finns i jobbinformationen. |
| IMS-organisationen har inte etablerats. | Det här meddelandet visas när din organisation inte har etablerats för [!DNL Privacy Service]. Kontakta administratören om du vill ha mer information. |
| Åtkomst och behörigheter krävs. | Åtkomst och behörigheter krävs för att kunna använda [!DNL Privacy Service]. Kontakta administratören för att få åtkomst. |
| Ett problem uppstod vid överföring och arkivering av åtkomstdata. | När det här felet inträffar överför du åtkomstdata igen och försöker igen. |
| Arbetsbelastningen har överskridits för den aktuella dokumenthastighetsgränsen. | När det här felet inträffar ska du minska överföringshastigheten och försöka igen. |
| För många förfrågningar<br>(HTTP 429-fel) | Om dina överföringsmönster överskrider den övervakade gränsen för tillåtna datatypsjobb får du ett HTTP 429-fel som svar på fortsatt trafik från din organisation. Privacy Service är avsedd för behandling av den registrerades förfrågningar om integritet. Den ska inte användas för datarensning. Om du får HTTP 429-fel implementeras begränsnings- och begärandebegränsningar för att skydda Adobe mot missbruk som kan äventyra regelefterlevnad.<br>Alternativa metoder för att minimera dina data tillhandahålls av [ange förfallotidsplaner för datauppsättning](../hygiene/ui/dataset-expiration.md) och använder [radera post, funktion](../hygiene/ui/record-delete.md). Mer information om hur du använder funktionerna finns i respektive dokumentation. |
