---
keywords: Experience Platform;hemmabruk;populära ämnen;direktuppspelning;direktuppspelningsuppläsning;felsökning;direktuppspelningsuppläsning, frågor och svar;frågor;
solution: Experience Platform
title: Felsökningsguide för direktuppspelning av inmatningsproblem
description: Det här dokumentet innehåller svar på vanliga frågor om direktuppspelning på Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 0%

---

# Felsökningsguide för direktuppspelning

Det här dokumentet innehåller svar på vanliga frågor om direktuppspelning på Adobe Experience Platform. För frågor och felsökning relaterade till andra [!DNL Platform] tjänster, inklusive sådana som påträffas i alla [!DNL Platform] API:er, se [Felsökningsguide för Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] innehåller RESTful-API:er som du kan använda för att importera data till [!DNL Experience Platform]. Inkapslade data används för att uppdatera enskilda kundprofiler i nära realtid, så att ni kan leverera personaliserade, relevanta upplevelser över flera kanaler. Läs [Översikt över datainmatning](../home.md) om du vill ha mer information om tjänsten och de olika intagsmetoderna. Anvisningar om hur du använder API:er för direktuppspelning finns i [översikt över direktuppspelning](../streaming-ingestion/overview.md).

## Vanliga frågor och svar

Nedan följer en lista med svar på vanliga frågor om direktuppspelning.

### Hur vet jag att nyttolasten jag skickar är korrekt formaterad?

[!DNL Data Ingestion] hävstångar [!DNL Experience Data Model] (XDM) scheman för validering av inkommande data. Om du skickar data som inte följer strukturen i ett fördefinierat XDM-schema, kommer det att leda till att importen misslyckas. Mer information om XDM och dess användning i [!DNL Experience Platform], se [XDM - systemöversikt](../../xdm/home.md).

Direktuppspelningsinmatning har stöd för två valideringslägen: synkron och asynkron. Varje verifieringsmetodhanterare misslyckades med data på olika sätt.

**Synkron validering** ska användas under utvecklingsprocessen. Poster som inte godkänns vid validering tas bort och returnerar ett felmeddelande om varför de misslyckades (till exempel: &quot;Ogiltigt XDM-meddelandeformat&quot;).

**Asynkron validering** bör användas i produktionen. Alla felaktiga data som inte godkänns vid valideringen skickas till [!DNL Data Lake] som en misslyckad batchfil, där den kan hämtas senare för ytterligare analys.

Mer information om synkron och asynkron validering finns i [översikt över direktuppspelningsvalidering](../quality/streaming-validation.md). Anvisningar om hur du visar batchar som inte kan valideras finns i handboken [hämta misslyckade batchar](../quality/retrieve-failed-batches.md).

### Kan jag validera nyttolasten innan jag skickar den till [!DNL Platform]?

Begär nyttolaster kan bara utvärderas efter att de har skickats till [!DNL Platform]. Vid synkron validering returnerar giltiga nyttolaster ifyllda JSON-objekt medan ogiltiga nyttolaster returnerar felmeddelanden. Under asynkron validering upptäcker och skickar tjänsten felformaterade data till [!DNL Data Lake] där den senare kan hämtas för analys. Se [översikt över direktuppspelningsvalidering](../quality/streaming-validation.md) för mer information.

### Vad händer när synkron validering begärs på en kant som inte stöder det?

Om synkron validering inte stöds för den begärda platsen returneras ett 501-felsvar. Se [översikt över direktuppspelningsvalidering](../quality/streaming-validation.md) för mer information om synkron validering.

### Hur ser jag till att data bara samlas in från betrodda källor?

[!DNL Experience Platform] har stöd för säker datainsamling. När autentiserad datainsamling är aktiverad måste klienterna skicka en JSON Web Token (JWT) och deras organisations-ID som begärandehuvuden. Mer information om hur du skickar autentiserade data till [!DNL Platform], se guiden på [autentiserad datainsamling](../tutorials/create-authenticated-streaming-connection.md).

### Vad är fördröjningen för direktuppspelning av data till? [!DNL Real-Time Customer Profile]?

Strömmade händelser återspeglas i allmänhet i [!DNL Real-Time Customer Profile] på under 60 sekunder. Faktiska latenser kan variera beroende på datavolym, meddelandestorlek och bandbreddsbegränsningar.

### Kan jag inkludera flera meddelanden i samma API-begäran?

Du kan gruppera flera meddelanden inom en enskild nyttolast och strömma dem till [!DNL Platform]. När det används på rätt sätt är gruppering av flera meddelanden i en enda begäran ett utmärkt sätt att optimera dataåtgärderna. Läs självstudiekursen om [skicka flera meddelanden i en begäran](../tutorials/streaming-multiple-messages.md) för mer information.

### Hur vet jag om de data jag skickar tas emot?

Alla data som skickas till [!DNL Platform] (utan fel eller på annat sätt) lagras som gruppfiler innan de sparas i datauppsättningar. Batchernas bearbetningsstatus visas i den datauppsättning de skickades till.

Du kan verifiera om data har importerats korrekt genom att kontrollera datauppsättningsaktiviteten med [Experience Platform användargränssnitt](https://platform.adobe.com). Klicka **[!UICONTROL Datasets]** i den vänstra navigeringen för att visa en lista med datauppsättningar. Markera den datauppsättning som du direktuppspelar till i den lista som visas för att öppna den **[!UICONTROL Dataset activity]** sida, visa alla batchar som har skickats under en vald tidsperiod. Mer information om hur du använder [!DNL Experience Platform] för att övervaka dataströmmar, se guiden [övervaka strömmande dataflöden](../quality/monitor-data-ingestion.md).

Om dina data inte kunde importera och du vill återställa dem från [!DNL Platform]kan du hämta de misslyckade batcharna genom att skicka deras ID:n till [!DNL Data Access API]. Se guiden [hämta misslyckade batchar](../quality/retrieve-failed-batches.md) för mer information.

### Varför är mina strömmande data inte tillgängliga i datasjön?

Det finns många orsaker till att batchintagning inte når upp till [!DNL Data Lake], t.ex. ogiltig formatering, saknade data eller systemfel. Du måste hämta batchen med [!DNL Data Ingestion Service API] och visa information om den. Detaljerade steg för hur du hämtar en misslyckad batch finns i guiden [hämta misslyckade batchar](../quality/retrieve-failed-batches.md).

### Hur tolkar jag det svar som returnerats för API-begäran?

Du kan tolka ett svar genom att först kontrollera serverns svarskod för att avgöra om din begäran accepterades. Om en svarskod returneras kan du granska `responses` arrayobjekt för att fastställa inmatningsaktivitetens status.

En slutförd API-begäran med ett meddelande returnerar statuskoden 200. En slutförd (eller delvis slutförd) API-begäran för gruppmeddelanden returnerar statuskod 207.

Följande JSON är ett exempelsvarsobjekt för en API-begäran med två meddelanden: ett lyckades och ett misslyckades. Meddelanden som kan direktuppspelas returnerar ett `xactionId` -egenskap. Meddelanden som inte direktuppspelas returnerar `statusCode` egenskap och ett svar `message` med mer information.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Varför tas mina skickade meddelanden inte emot av [!DNL Real-Time Customer Profile]?

If [!DNL Real-Time Customer Profile] avvisar ett meddelande. Det beror troligtvis på felaktig identitetsinformation. Detta kan bero på att ett ogiltigt värde eller namnutrymme har angetts för en identitet.

Det finns två typer av identitetsnamnutrymmen: standard och anpassad. Kontrollera att namnutrymmet har registrerats i [!DNL Identity Service]. Se [Översikt över namnutrymmet identity](../../identity-service/namespaces.md) om du vill ha mer information om hur du använder standardnamnutrymmen och anpassade namnutrymmen.

Du kan använda [[!DNL Experience Platform UI]](https://platform.adobe.com) om du vill ha mer information om varför ett meddelande inte kunde hämtas. Klicka **[!UICONTROL Monitoring]** i den vänstra navigeringen, visa sedan **[!UICONTROL Streaming end-to-end]** om du vill visa meddelandebatchar som direktuppspelas under en viss tidsperiod.
