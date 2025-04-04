---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Privacy Service felsökningsguide
description: Det här dokumentet innehåller svar på vanliga frågor om Privacy Service samt information om vanliga fel i API:t.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 1%

---

# [!DNL Privacy Service] felsökningsguide

Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful API och användargränssnitt som hjälper företag att hantera förfrågningar om kunddata. Med [!DNL Privacy Service] kan du skicka begäranden om åtkomst till och radering av privata eller personliga kunddata, vilket underlättar automatisk efterlevnad av organisatoriska och juridiska sekretessbestämmelser.

Det här dokumentet innehåller svar på vanliga frågor om [!DNL Privacy Service] samt information om vanliga fel i API:t.

## Vad är skillnaden mellan en användare och ett användar-ID när sekretessförfrågningar görs i API:t? {#user-ids}

För att kunna göra ett nytt sekretessjobb i API:t måste JSON-nyttolasten för begäran innehålla en `users`-matris med specifik information för varje användare som sekretessbegäran gäller för. Varje objekt i arrayen `users` är ett objekt som representerar en viss användare, som identifieras av dess `key`-värde.

Varje användarobjekt (eller `key`) innehåller i sin tur en egen `userIDs`-array. Den här arrayen visar specifika ID-värden **för den aktuella användaren**.

Titta på följande exempel på `users`-matris:

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

Arrayen innehåller två objekt, som representerar enskilda användare som identifieras av deras `key`-värden (&quot;DavidSmith&quot; och&quot;user12345&quot;). &quot;DavidSmith&quot; har bara ett angivet ID (deras e-postadress), medan &quot;user12345&quot; har två (deras e-postadress och ECID).

Mer information om att tillhandahålla information om användaridentitet finns i guiden om [identitetsdata för sekretessförfrågningar](identity-data.md).


## Kan jag använda [!DNL Privacy Service] för att rensa data som av misstag har skickats till [!DNL Experience Platform]?

Adobe stöder inte att [!DNL Privacy Service] används för att rensa bort data som av misstag har skickats till en produkt. [!DNL Privacy Service] är utformat för att hjälpa dig att uppfylla dina skyldigheter för den registrerade (eller konsumenten) att få tillgång till eller ta bort data. All annan användning av Privacy Service för datarensning eller datareferenser stöds inte eller tillåts inte.

Begäran om sekretess är tidskänslig och har fyllts i med avseende på tillämplig integritetslagstiftning. Inlämningen av förfrågningar som inte är registrerade/kunder eller förfrågningar om åtkomst eller borttagning påverkar alla [!DNL Privacy Service]-kunder och möjligheten för [!DNL Privacy Service] att stödja lämpliga juridiska tidslinjer. Det finns nu en hög överföringsgräns per dag för att förhindra missbruk av tjänsten.

Kontakta Adobe kontoteam för att koordinera och åtgärda eventuella PII- eller dataproblem.

## Hur får jag information om status för min sekretessförfrågan eller mitt jobb?

Du kan hämta information om ett visst jobb genom att använda API:t [!DNL Privacy Service] eller användargränssnittet.

### Använda API:et

Om du vill hämta statusen för ett visst jobb med API:t [!DNL Privacy Service], gör du en begäran till rotslutpunkten (`GET /`) med hjälp av jobbets ID i begärandesökvägen. Mer information finns i avsnittet [Kontrollera statusen för ett jobb](api/privacy-jobs.md#check-the-status-of-a-job) i API-guiden för [!DNL Privacy Service].

### Använda gränssnittet

Alla aktiva jobbbegäranden visas i **[!UICONTROL Job Requests]**-widgeten på kontrollpanelen för användargränssnittet i [!DNL Privacy Service]. Statusen för varje jobbförfrågan visas under kolumnen **[!UICONTROL Status]**. Mer information om hur du visar jobbförfrågningar i användargränssnittet finns i [Privacy Service användarhandbok](ui/user-guide.md).

## Hur hämtar jag resultaten från mina slutförda sekretessjobb?

API:t [!DNL Privacy Service] och användargränssnittet innehåller båda metoder för att hämta resultaten av slutförda jobb i ZIP-format.

### Använda API:et

Gör en begäran till rotslutpunkten (`GET /`) i API:t [!DNL Privacy Service] med ID:t för jobbet vars resultat du vill hämta i sökvägen för begäran. Om jobbets status är slutförd inkluderar API:t ett `downloadURL`-attribut i svarstexten. Det här attributet innehåller en URL som du kan klistra in i webbläsarens adressfält för att hämta ZIP-filen.

Mer information finns i avsnittet [Söka efter ett jobb med hjälp av dess ID](api/privacy-jobs.md#check-the-status-of-a-job) i API-guiden för [!DNL Privacy Service].

### Använda gränssnittet

På [!DNL Privacy Service] UI-kontrollpanelen hittar du det jobb du vill hämta från widgeten **Jobbförfrågningar**. Välj ID för jobbet för att öppna sidan Jobbinformation. Här väljer du **Hämta** i det övre högra hörnet för att hämta ZIP-filen. Mer information finns i [Privacy Service användarhandbok](ui/user-guide.md).

## Vanliga felmeddelanden {#common-error-messages}

I följande tabell visas några vanliga fel i [!DNL Privacy Service], med beskrivningar som hjälper dig att lösa deras respektive problem.

| Felmeddelande | Beskrivning |
| --- | --- |
| Användar-ID:n hittades inte. | Vissa användar-ID:n som angavs i begäran kunde inte hittas och hoppades över. Kontrollera att du använder rätt namnutrymme(n) och ID-värden i nyttolasten för begäran. Mer information finns i dokumentet om [att tillhandahålla identitetsdata](./identity-data.md). |
| Ogiltigt namnutrymme | Ett angivet ID-namnområde för ett användar-ID var ogiltigt. En lista över godkända namnutrymmen finns i avsnittet [Standardnamnutrymmen för identiteter](./api/appendix.md#standard-namespaces) i [!DNL Privacy Service] API-handboken. Om du använder ett anpassat namnutrymme måste du se till att du anger egenskapen `type` för ID:t till &quot;anpassad&quot;. |
| Delvis slutförd | Jobbet slutfördes, men vissa data var inte tillämpliga för den angivna begäran och hoppades över. |
| Data har inte det format som krävs. | Ett eller flera av datavärdena för det angivna programmet var felaktigt formaterade. Mer information finns i jobbinformationen. |
| IMS-organisationen har inte etablerats. | Det här meddelandet visas när din organisation inte har etablerats för [!DNL Privacy Service]. Kontakta administratören om du vill ha mer information. |
| Åtkomst och behörigheter krävs. | Åtkomst och behörigheter krävs för att använda [!DNL Privacy Service]. Kontakta administratören för att få åtkomst. |
| Ett problem uppstod vid överföring och arkivering av åtkomstdata. | När det här felet inträffar överför du åtkomstdata igen och försöker igen. |
| Arbetsbelastningen har överskridits för den aktuella dokumenthastighetsgränsen. | När det här felet inträffar ska du minska överföringshastigheten och försöka igen. |
| För många begäranden <br> (HTTP 429-fel) | Om dina överföringsmönster överskrider den övervakade gränsen för tillåtna datatypsjobb får du ett HTTP 429-fel som svar på fortsatt trafik från din organisation. Privacy Service är avsett för behandling av förfrågningar om integritet hos registrerade. Den ska inte användas för datarensning. Om du får HTTP 429-fel implementeras begränsnings- och begärandebegränsningar för att skydda Adobe från missbruk som kan äventyra regelefterlevnad.<br>Alternativa metoder för att minimera dina data tillhandahålls genom [att ange förfalloscheman för datauppsättningar](../hygiene/ui/dataset-expiration.md) och använda [funktionen för borttagning av dataposter](../hygiene/ui/record-delete.md). Mer information om hur du använder funktionerna finns i respektive dokumentation. |
