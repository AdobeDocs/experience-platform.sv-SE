---
keywords: Experience Platform;home;populära topics;streaming;direktuppspelningsuppläsning;felsökning;felsökning av direktuppspelningsuppläsning;frågor och svar;
solution: Experience Platform
title: Felsökningsguide för direktuppspelning av inmatningsproblem
description: Det här dokumentet innehåller svar på vanliga frågor om direktuppspelning på Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Felsökningsguide för direktuppspelning

Det här dokumentet innehåller svar på vanliga frågor om direktuppspelning på Adobe Experience Platform. För frågor och felsökning som rör andra [!DNL Experience Platform]-tjänster, inklusive de som påträffas i alla [!DNL Experience Platform] API:er, se [Experience Platform felsökningsguide](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] innehåller RESTful-API:er som du kan använda för att importera data till [!DNL Experience Platform]. Inkapslade data används för att uppdatera enskilda kundprofiler i nära realtid, så att ni kan leverera personaliserade, relevanta upplevelser över flera kanaler. Läs [Översikt över datainmatning](../home.md) om du vill ha mer information om tjänsten och de olika matningsmetoderna. Anvisningar om hur du använder API:er för direktuppspelning av inläsning finns i [översikten över direktuppspelning](../streaming-ingestion/overview.md).

## Vanliga frågor och svar

Nedan följer en lista med svar på vanliga frågor om direktuppspelning.

### Hur vet jag att nyttolasten jag skickar är korrekt formaterad?

[!DNL Data Ingestion] använder [!DNL Experience Data Model] (XDM)-scheman för att validera formatet för inkommande data. Om du skickar data som inte följer strukturen i ett fördefinierat XDM-schema, kommer det att leda till att importen misslyckas. Mer information om XDM och hur det används i [!DNL Experience Platform] finns i [ översikten över XDM-systemet](../../xdm/home.md).

Direktuppspelningsuppläsning stöder två valideringslägen: synkron och asynkron. Varje verifieringsmetodhanterare misslyckades med data på olika sätt.

**Synkron validering** ska användas under utvecklingsprocessen. Poster som inte godkänns vid validering tas bort och returnerar ett felmeddelande om varför de misslyckades (t.ex. &quot;Ogiltigt XML-meddelandeformat&quot;).

**Asynkron validering** ska användas i produktionen. Alla felformaterade data som inte godkänns vid validering skickas till [!DNL Data Lake] som en misslyckad gruppfil, där de kan hämtas senare för ytterligare analys.

Mer information om synkron och asynkron validering finns i [översikt över direktuppspelningsvalidering](../quality/streaming-validation.md). Anvisningar om hur du visar batchar som inte kan valideras finns i guiden [Hämta misslyckade batchar](../quality/retrieve-failed-batches.md).

### Kan jag validera nyttolasten för en begäran innan jag skickar den till [!DNL Experience Platform]?

Nyttolaster för begäranden kan bara utvärderas efter att de har skickats till [!DNL Experience Platform]. Vid synkron validering returnerar giltiga nyttolaster ifyllda JSON-objekt medan ogiltiga nyttolaster returnerar felmeddelanden. Under asynkron validering upptäcker och skickar tjänsten alla felformaterade data till [!DNL Data Lake], där de senare kan hämtas för analys. Mer information finns i [översikten för direktuppspelningsvalidering](../quality/streaming-validation.md).

### Vad händer när synkron validering begärs på en kant som inte stöder det?

Om synkron validering inte stöds för den begärda platsen returneras ett 501-felsvar. Mer information om synkron validering finns i [översikten för direktuppspelningsvalidering](../quality/streaming-validation.md).

### Hur ser jag till att data bara samlas in från betrodda källor?

[!DNL Experience Platform] har stöd för säker datainsamling. När autentiserad datainsamling är aktiverad måste klienterna skicka en JSON Web Token (JWT) och deras organisations-ID som begärandehuvuden. Mer information om hur du skickar autentiserade data till [!DNL Experience Platform] finns i guiden om [autentiserad datainsamling](../tutorials/create-authenticated-streaming-connection.md).

### Vilken fördröjning har direktuppspelning av data till [!DNL Real-Time Customer Profile]?

Direktuppspelade händelser återspeglas i allmänhet i [!DNL Real-Time Customer Profile] på mindre än 60 sekunder. Faktiska latenser kan variera beroende på datavolym, meddelandestorlek och bandbreddsbegränsningar.

### Kan jag inkludera flera meddelanden i samma API-begäran?

Du kan gruppera flera meddelanden inom en enskild nyttolast för begäran och strömma dem till [!DNL Experience Platform]. När det används på rätt sätt är gruppering av flera meddelanden i en enda begäran ett utmärkt sätt att optimera dataåtgärderna. Mer information finns i självstudiekursen om att [skicka flera meddelanden i en begäran](../tutorials/streaming-multiple-messages.md).

### Hur vet jag om de data jag skickar tas emot?

Alla data som skickas till [!DNL Experience Platform] (utan fel eller på annat sätt) lagras som gruppfiler innan de lagras i datauppsättningar. Batchernas bearbetningsstatus visas i den datauppsättning de skickades till.

Du kan verifiera om data har importerats genom att kontrollera datauppsättningsaktiviteten med [Experience Platform-användargränssnittet](https://platform.adobe.com). Klicka på **[!UICONTROL Datasets]** i den vänstra navigeringen för att visa en lista med datauppsättningar. Markera den datauppsättning som du direktuppspelar till i den lista som visas för att öppna sidan **[!UICONTROL Dataset activity]** med alla batchar som har skickats under en vald tidsperiod. Mer information om hur du använder [!DNL Experience Platform] för att övervaka dataströmmar finns i guiden [Övervaka dataflöden för direktuppspelning](../quality/monitor-data-ingestion.md).

Om dina data inte kunde importera och du vill återställa dem från [!DNL Experience Platform], kan du hämta de misslyckade batcharna genom att skicka deras ID:n till [!DNL Data Access API]. Mer information finns i guiden [Hämta misslyckade batchar](../quality/retrieve-failed-batches.md).

### Varför är mina strömmande data inte tillgängliga i datasjön?

Det finns många orsaker till varför gruppinmatning inte kan nå [!DNL Data Lake], till exempel ogiltig formatering, saknade data eller systemfel. Om du vill ta reda på varför din batch misslyckades måste du hämta gruppen med [!DNL Data Ingestion Service API] och visa information om den. Detaljerade steg för hur du hämtar en misslyckad batch finns i guiden [Hämta misslyckade batchar](../quality/retrieve-failed-batches.md).

### Hur tolkar jag det svar som returnerats för API-begäran?

Du kan tolka ett svar genom att först kontrollera serverns svarskod för att avgöra om din begäran accepterades. Om en svarskod returneras kan du sedan granska `responses`-arrayobjektet för att fastställa statusen för den nya uppgiften.

En slutförd API-begäran med ett meddelande returnerar statuskoden 200. En slutförd (eller delvis slutförd) API-begäran för gruppmeddelanden returnerar statuskod 207.

Följande JSON är ett exempelsvarsobjekt för en API-begäran med två meddelanden: ett lyckades och ett misslyckades. Meddelanden som kan direktuppspelas returnerar en `xactionId`-egenskap. Meddelanden som inte kan direktuppspelas returnerar en `statusCode`-egenskap och ett svar `message` med mer information.

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

Om [!DNL Real-Time Customer Profile] avvisar ett meddelande beror det troligtvis på felaktig identitetsinformation. Detta kan bero på att ett ogiltigt värde eller namnutrymme har angetts för en identitet.

Det finns två typer av identitetsnamnutrymmen: standard och anpassad. När du använder anpassade namnutrymmen måste du kontrollera att namnutrymmet har registrerats i [!DNL Identity Service]. Mer information om hur du använder standardnamnutrymmen och anpassade namnutrymmen finns i [översikten för identitetsnamnrymden](../../identity-service/features/namespaces.md).

Du kan använda [[!DNL Experience Platform UI]](https://platform.adobe.com) för att se mer information om varför ett meddelande inte kunde hämtas. Klicka på **[!UICONTROL Monitoring]** i den vänstra navigeringen och visa sedan fliken **[!UICONTROL Streaming end-to-end]** för att se meddelandebatchar som direktuppspelats under en vald tidsperiod.
