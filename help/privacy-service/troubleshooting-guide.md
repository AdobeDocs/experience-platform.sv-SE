---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vanliga frågor om Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# [!DNL Privacy Service] felsökningsguide

Adobe Experience Platform [!DNL Privacy Service] tillhandahåller ett RESTful API och användargränssnitt som hjälper företag att hantera förfrågningar om kunddata. Med [!DNL Privacy Service]kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata, vilket underlättar automatiserad efterlevnad av organisatoriska och juridiska sekretessbestämmelser.

Det här dokumentet innehåller svar på vanliga frågor om [!DNL Privacy Service]samt information om vanliga fel i API:t.

## Vad är skillnaden mellan en användare och ett användar-ID när sekretessförfrågningar görs i API:t? {#user-ids}

För att kunna göra ett nytt sekretessjobb i API:t måste JSON-nyttolasten för begäran innehålla en `users` array som listar specifik information för varje användare som sekretessbegäran gäller för. Varje objekt i arrayen är ett objekt som representerar en viss användare, som identifieras av dess `users` `key` värde.

Varje användarobjekt (eller `key`) innehåller i sin tur en egen `userIDs` array. Den här arrayen visar specifika ID-värden **för en viss användare**.

Titta på följande `users` exempelarray:

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

Mer information om att tillhandahålla information om användaridentitet finns i guiden om [identitetsdata för sekretessförfrågningar](identity-data.md).


## Kan jag använda [!DNL Privacy Service] för att rensa data som av misstag har skickats till [!DNL Platform]?

Adobe stöder inte användning [!DNL Privacy Service] för att radera data som av misstag skickats till en produkt. [!DNL Privacy Service] är utformat för att hjälpa dig att uppfylla dina skyldigheter för den registrerade (eller konsumenten) att få tillgång till eller ta bort uppgifter. Dessa förfrågningar är tidskänsliga och har slutförts med avseende på tillämplig integritetslagstiftning. Inlämning av förfrågningar som inte är förfrågningar om tillgång eller radering för registrerade/konsumenter påverkar alla [!DNL Privacy Service] kunder och möjligheten [!DNL Privacy Service] att ge stöd för lämpliga rättsliga tidsramar.

Kontakta din kontoansvarige (CDM) för att koordinera och göra en insats för att ta bort eventuella PII- eller dataproblem.

## Hur får jag information om status för min sekretessförfrågan eller mitt jobb?

Du kan hämta information om ett visst jobb genom att använda [!DNL Privacy Service] API:t eller användargränssnittet.

### Använda API

Om du vill hämta statusen för ett visst jobb med [!DNL Privacy Service] API:t gör du en begäran till rotslutpunkten (`GET /`) med hjälp av jobbets ID i sökvägen för begäran. Mer information finns i avsnittet om [att kontrollera statusen för ett jobb](api/privacy-jobs.md#check-the-status-of-a-job) i [!DNL Privacy Service] utvecklarhandboken.

### Använda gränssnittet

Alla aktiva jobbbegäranden visas i widgeten på **[!UICONTROL Job Requests]** kontrollpanelen för [!DNL Privacy Service] användargränssnitt. Statusen för varje jobbförfrågan visas under **[!UICONTROL Status]** kolumnen. Mer information om hur du visar jobbförfrågningar i användargränssnittet finns i användarhandboken för [Privacy Service](ui/user-guide.md).

## Hur hämtar jag resultaten från mina slutförda sekretessjobb?

API:t [!DNL Privacy Service] och användargränssnittet innehåller båda metoder för att hämta resultaten av slutförda jobb i ZIP-format.

### Använda API

Gör en begäran till rotslutpunkten (`GET /`) i [!DNL Privacy Service] API:t med ID:t för jobbet vars resultat du vill hämta i sökvägen för begäran. Om jobbets status är slutförd inkluderar API:t ett `downloadURL` -attribut i svarstexten. Det här attributet innehåller en URL som du kan klistra in i webbläsarens adressfält för att hämta ZIP-filen.

Mer information finns i avsnittet om att [söka efter ett jobb med hjälp av dess ID](api/privacy-jobs.md#check-the-status-of-a-job) i [!DNL Privacy Service] utvecklarhandboken.

### Använda gränssnittet

På [!DNL Privacy Service] UI-kontrollpanelen hittar du det jobb du vill hämta från widgeten **Jobbförfrågningar** . Klicka på ID:t för jobbet för att öppna sidan _Jobbinformation_ . Hämta ZIP-filen genom att klicka på **Hämta** i det övre högra hörnet. Mer information finns i användarhandboken [för](ui/user-guide.md) Privacy Service.

## Vanliga felmeddelanden

I följande tabell beskrivs några vanliga fel i [!DNL Privacy Service], med beskrivningar som hjälper dig att lösa respektive problem.

| Felmeddelande | Beskrivning |
| --- | --- |
| Det gick inte att hitta användar-ID:n. | Vissa användar-ID:n som angavs i begäran kunde inte hittas och hoppades över. Kontrollera att du använder rätt namnutrymme(n) och ID-värden i nyttolasten för begäran. Mer information finns i dokumentet om [att tillhandahålla identitetsdata](./identity-data.md) . |
| Ogiltigt namnutrymme | Ett angivet ID-namnområde för ett användar-ID var ogiltigt. En lista över godkända namnutrymmen finns i avsnittet om [standardnamnutrymmen](./api/appendix.md#standard-namespaces) för [!DNL Privacy Service] utvecklarhandboken. Om du använder ett anpassat namnutrymme måste du se till att du anger ID:ts egenskap som `type` &quot;anpassad&quot;. |
| Delvis slutförd | Jobbet slutfördes, men vissa data var inte tillämpliga för den angivna begäran och hoppades över. |
| Data har inte det format som krävs. | Ett eller flera av datavärdena för det angivna programmet var felaktigt formaterade. Mer information finns i jobbinformationen. |
| IMS-organisationen har inte etablerats. | Det här meddelandet visas när din IMS-organisation inte har etablerats för [!DNL Privacy Service]. Kontakta administratören om du vill ha mer information. |
| Åtkomst och behörigheter krävs. | Åtkomst och behörigheter krävs för att kunna använda [!DNL Privacy Service]. Kontakta administratören för att få åtkomst. |
| Ett problem uppstod vid överföring och arkivering av åtkomstdata. | När det här felet inträffar överför du åtkomstdata igen och försöker igen. |
| Arbetsbelastningen har överskridits för den aktuella dokumenthastighetsgränsen. | Minska överföringshastigheten och försök igen när felet inträffar. |