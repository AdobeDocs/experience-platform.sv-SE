---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Skicka in din Source
description: I följande dokument beskrivs hur du testar och verifierar en ny källa med API:t för Flow Service och integrerar en ny källa med självbetjäningskällor (Batch SDK).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Skicka din källa

Det sista steget mot att integrera din nya källa till Adobe Experience Platform med självbetjäningskällor (Batch SDK) är att testa källan för verifiering. När det är klart kan du sedan skicka in din nya källfil genom att kontakta Adobe.

Följande dokument innehåller steg om hur du testar och felsöker källan med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

* Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../landing/api-guide.md).
* Mer information om hur du genererar autentiseringsuppgifter för Experience Platform API:er finns i självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md).
* Information om hur du konfigurerar [!DNL Postman] för Experience Platform API:er finns i självstudiekursen [Konfigurera utvecklarkonsol och [!DNL Postman]](../../../landing/postman.md).
* Om du vill ha hjälp med testnings- och felsökningsprocessen kan du hämta verifieringssamlingen och miljön för [självbetjänade källor här](../assets/sdk-verification.zip) och följa stegen som beskrivs nedan.

## Testa källan

Om du vill testa källan måste du köra verifieringssamlingen och miljön ](../assets/sdk-verification.zip) för [!DNL Postman]-källor med [självbetjäning, samtidigt som du anger lämpliga miljövariabler som hör till källan.

Om du vill börja testa måste du först konfigurera samlingen och miljön på [!DNL Postman]. Ange sedan det ID för anslutningsspecifikationen som du vill testa.

### Ange `authSpecName`

När du har angett ditt anslutningsspecifikations-ID måste du ange `authSpecName` som du använder för din basanslutning. Beroende på vad du väljer kan det vara antingen `OAuth 2 Refresh Code` eller `Basic Authentication`. När du har angett din `authSpecName` måste du inkludera de nödvändiga autentiseringsuppgifterna i din miljö. Om du till exempel anger `authSpecName` som `OAuth 2 Refresh Code` måste du ange de nödvändiga autentiseringsuppgifterna för OAuth 2, som är `host` och `accessToken`.

### Ange `sourceSpec`

När du har lagt till parametrar för autentiseringsspecifikation måste du lägga till de egenskaper som krävs från källspecifikationen. Du kan hitta de nödvändiga egenskaperna i `sourceSpec.spec.properties`. När det gäller exemplet [!DNL MailChimp Members] nedan är den enda obligatoriska egenskapen `listId`, vilket betyder `listId` och det är motsvarande ID-värde för din [!DNL Postman]-miljö.

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

När du har angett parametrarna för autentisering och källspecifikation kan du börja fylla i resten av dina miljövariabler. Se tabellen nedan för referens:

>[!NOTE]
>
>Alla exempelvariabler nedan är platshållarvärden som du måste uppdatera, förutom för `flowSpecificationId` och `targetConnectionSpecId`, som är fasta värden.

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `x-api-key` | En unik identifierare som används för att autentisera anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen [Konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din `x-gw-ims-org-id`-information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | För att källdata ska kunna användas i Experience Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Detaljerade steg om hur du skapar ett mål-XDM-schema finns i självstudiekursen [Skapa ett schema med API:t](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Den unika version som motsvarar ditt schema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | `meta:altId` som returneras tillsammans med `schemaId` när ett nytt schema skapas. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Detaljerade steg om hur du skapar en måldatauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:t](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Mappningsuppsättningar kan användas för att definiera hur data i ett källschema mappas till data i ett målschema. Detaljerade anvisningar om hur du skapar en mappning finns i självstudiekursen [om hur du skapar en mappningsuppsättning med API:t](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | Det unika ID som motsvarar din mappningsuppsättning. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | Anslutningsspecifikations-ID som motsvarar källan. Detta är det ID som du genererade efter [att du har skapat en ny anslutningsspecifikation](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Flödesspecifikation-ID för `RestStorageToAEP`. **Det här är ett fast värde**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | Målanslutnings-ID för den datasjön där inmatade data landar. **Det här är ett fast värde**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Det angivna tidsintervallet som ska följas när en flödeskörning slutförs. | `40` |
| `startTime` | Starttiden för dataflödet. Starttiden måste formateras i unix-tid. | `1597784298` |

När du har angett alla dina miljövariabler kan du börja köra samlingen med gränssnittet [!DNL Postman]. I gränssnittet [!DNL Postman] markerar du ellipserna (**..**) bredvid [!DNL Sources SSSs Verification Collection] och väljer sedan **Kör samlingen**.

![runner](../assets/runner.png)

Gränssnittet [!DNL Runner] visas så att du kan konfigurera körningsordningen för dataflödet. Välj **Kör SSS-verifieringssamling** för att köra samlingen.

>[!NOTE]
>
>Du kan inaktivera **Ta bort flöde** från checklistan för körningsordning om du föredrar att använda kontrollpanelen för källövervakning i Experience Platform-gränssnittet. När du är klar med testningen måste du dock se till att testflödena tas bort.

![run-collection](../assets/run-collection.png)

## Skicka din källa

När källan är klar med hela arbetsflödet kan du fortsätta att kontakta Adobe-representanten och skicka in källan för integrering.
