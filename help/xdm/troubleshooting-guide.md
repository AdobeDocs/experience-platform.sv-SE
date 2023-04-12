---
keywords: Experience Platform;populära ämnen;XDM;XDM system;XDM individuell profil;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event;experience event;XDM Experience Event;XDM ExperienceEvent;experience data model;Experience data model;Experience data model;data model;data model;schema;troublesholeshooting;FAQ;faq;Union schema;UNION PROFILE;union profile profile profile;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Felsökningsguide för XDM-system
description: Hitta svar på vanliga frågor om Experience Data Model (XDM), inklusive steg för att lösa vanliga API-fel.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 0%

---

# Felsökningsguide för XDM-system

Det här dokumentet innehåller svar på vanliga frågor om [!DNL Experience Data Model] (XDM) och XDM System i Adobe Experience Platform, inklusive en felsökningsguide för vanliga fel. För frågor och felsökning som rör andra plattformstjänster, se [Felsökningsguide för Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** är en öppen källkodsspecifikation som definierar standardiserade scheman för kundupplevelsehantering. Den metod som [!DNL Experience Platform] är byggd, **XDM-system**, operaliserar [!DNL Experience Data Model] scheman för användning av [!DNL Platform] tjänster. The **[!DNL Schema Registry]** har ett användargränssnitt och ett RESTful API för att få åtkomst till **[!DNL Schema Library]** inom [!DNL Experience Platform]. Se [XDM-dokumentation](home.md) för mer information.

## Vanliga frågor och svar

Nedan följer en lista med svar på vanliga frågor om XDM-systemet och användning av [!DNL Schema Registry] API.

### Hur lägger jag till fält i ett schema?

Du kan lägga till fält i ett schema med hjälp av en schemafältgrupp. Varje fältgrupp är kompatibel med en eller flera klasser, vilket gör att fältgruppen kan användas i alla scheman som implementerar en av dessa kompatibla klasser. Adobe Experience Platform tillhandahåller flera branschfältgrupper med sina egna fördefinierade fält, men du kan lägga till egna fält i ett schema genom att skapa anpassade fältgrupper med API:t eller användargränssnittet.

Mer information om hur du skapar fältgrupper i [!DNL Schema Registry] API, se [slutpunktsguide för fältgrupp](api/field-groups.md#create). Om du använder användargränssnittet läser du [Schemaredigeraren, genomgång](./tutorials/create-schema-ui.md).

### Vilket är det bästa användningsområdet för fältgrupper jämfört med datatyper?

[Fältgrupper](./schema/composition.md#field-group) är komponenter som definierar ett eller flera fält i ett schema. Fältgrupper styr hur deras fält visas i schemats hierarki och visar därför samma struktur i varje schema som de ingår i. Fältgrupper är bara kompatibla med specifika klasser, vilket identifieras av deras `meta:intendedToExtend` -attribut.

[Datatyper](./schema/composition.md#data-type) kan även tillhandahålla ett eller flera fält för ett schema. Till skillnad från fältgrupper är datatyperna dock inte begränsade till en viss klass. Detta gör datatyper till ett mer flexibelt alternativ för att beskriva vanliga datastrukturer som kan återanvändas i flera scheman med potentiellt olika klasser.

### Vilket unikt ID har ett schema?

Alla [!DNL Schema Registry] resurser (scheman, fältgrupper, datatyper, klasser) har en URI som fungerar som ett unikt ID för referens- och sökningsändamål. När du visar ett schema i API:t finns det på den översta nivån `$id` och `meta:altId` attribut.

Mer information finns i [resursidentifiering](api/getting-started.md#resource-identification) i [!DNL Schema Registry] API-guide.

### När börjar ett schema förhindra att ändringar bryts?

Du kan göra ändringar i ett schema så länge det aldrig har använts för att skapa en datauppsättning eller aktiverats för användning i [[!DNL Real-Time Customer Profile]](../profile/home.md). När ett schema har använts när datauppsättningen skapades eller aktiverats för användning med [!DNL Real-Time Customer Profile], reglerna i [Schemautveckling](schema/composition.md#evolution) blir strikt införd av systemet.

### Vilken är den maximala storleken för en lång fälttyp?

En lång fälttyp är ett heltal med en maximal storlek på 53 (+1) bitar, vilket ger den ett möjligt intervall mellan -9007199254740992 och 900719925474092. Detta beror på en begränsning av hur JavaScript-implementeringar av JSON representerar långa heltal.

Mer information om fälttyper finns i dokumentet om [Begränsningar för XDM-fälttyp](./schema/field-constraints.md).

### Hur definierar jag identiteter för mitt schema?

I [!DNL Experience Platform]används identiteter för att identifiera ett ämne (vanligtvis en enskild person) oavsett vilka informationskällor som tolkas. De definieras i scheman genom att nyckelfält markeras som&quot;Identitet&quot;. Vanliga fält för identitet är e-postadress, telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM-ID och andra unika ID-fält.

Fält kan markeras som identiteter med antingen API:t eller användargränssnittet.

#### Definiera identiteter i API:t

I API:t etableras identiteter genom att skapa identitetsbeskrivningar. Identitetsbeskrivare signalerar att en viss egenskap för ett schema är en unik identifierare.

Identitetsbeskrivare skapas av en POST-begäran till slutpunkten /descriptors. Om det lyckas får du ett HTTP Status 201 (Skapad) och ett svarsobjekt med information om den nya beskrivningen.

Mer information om hur du skapar identitetsbeskrivningar i API:t finns i dokumentet om [beskrivare](api/descriptors.md) i [!DNL Schema Registry] utvecklarhandbok.

#### Definiera identiteter i användargränssnittet

När schemat är öppet i Schemaredigeraren markerar du fältet i **[!UICONTROL Structure]** i redigeraren som du vill markera som en identitet. Under **[!UICONTROL Field Properties]** till höger väljer du **[!UICONTROL Identity]** kryssrutan.

Mer information om hur du hanterar identiteter i användargränssnittet finns i avsnittet om [definiera identitetsfält](./tutorials/create-schema-ui.md#identity-field) i schemaredigerarens självstudiekurs.

### Behöver mitt schema en primär identitet?

Primära identiteter är valfria eftersom scheman kan ha antingen noll eller en av dem. Ett schema måste dock ha en primär identitet för att schemat ska kunna aktiveras för användning i [!DNL Real-Time Customer Profile]. Se [identity](./tutorials/create-schema-ui.md#identity-field) för mer information.

### Hur aktiverar jag ett schema i [!DNL Real-Time Customer Profile]?

Scheman är aktiverade för användning i [[!DNL Real-Time Customer Profile]](../profile/home.md) genom att lägga till en&quot;union&quot;-tagg i `meta:immutableTags` schemats attribut. Aktivera ett schema för användning med [!DNL Profile] kan göras med API:t eller användargränssnittet.

#### Aktivera ett befintligt schema för [!DNL Profile] med API

Begär att PATCH ska uppdatera schemat och lägga till `meta:immutableTags` som en array som innehåller värdet &quot;union&quot;. Om uppdateringen lyckas visas det uppdaterade schemat som nu innehåller unionstaggen.

Mer information om hur du använder API för att aktivera ett schema för användning i [!DNL Real-Time Customer Profile], se [föreningar](./api/unions.md) dokumentet [!DNL Schema Registry] utvecklarhandbok.

#### Aktivera ett befintligt schema för [!DNL Profile] med användargränssnittet

I [!DNL Experience Platform], markera **[!UICONTROL Schemas]** i den vänstra navigeringen och välj namnet på schemat som du vill aktivera i listan med scheman. Sedan till höger om redigeraren under **[!UICONTROL Schema Properties]**, markera **[!UICONTROL Profile]** för att aktivera det.


Mer information finns i avsnittet om [användning i kundprofil i realtid](./tutorials/create-schema-ui.md#profile) i [!UICONTROL Schema Editor] självstudiekurs.

### Kan jag redigera ett unionsschema direkt?

Unionsscheman är skrivskyddade och genereras automatiskt av systemet. De kan inte redigeras direkt. Unionsscheman skapas för en viss klass när en&quot;union&quot;-tagg läggs till i schemat som implementerar den klassen.

Mer information om fackföreningar i XDM finns i [föreningar](./api/unions.md) i [!DNL Schema Registry] API-guide.

### Hur ska jag formatera min datafil för att importera data till mitt schema?

[!DNL Experience Platform] godkänner datafiler i antingen [!DNL Parquet] eller JSON-format. Innehållet i dessa filer måste överensstämma med det schema som datauppsättningen refererar till. Mer information om de bästa sätten att mata in datafiler finns i [batchvis hantering - översikt](../ingestion/home.md).

## Fel och felsökning

Här följer en lista över felmeddelanden som du kan stöta på när du arbetar med [!DNL Schema Registry] API.

### Resursen hittades inte

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

Det här felet visas när systemet inte kan hitta en viss resurs. Resursen kan ha tagits bort eller så är sökvägen i API-anropet ogiltig. Kontrollera att du har angett en giltig sökväg för API-anropet innan du försöker igen. Du kanske vill kontrollera att du har angett rätt ID för resursen och att sökvägen har rätt namn tillsammans med rätt behållare (global eller klientorganisation).

>[!NOTE]
>
>Beroende på vilken resurstyp som hämtas kan det här felet använda något av följande `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Mer information om hur du skapar sökvägar i API:t finns i [container](./api/getting-started.md#container) och [resursidentifiering](api/getting-started.md#resource-identification) i [!DNL Schema Registry] utvecklarhandbok.

### Titeln är inte unik

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

Det här felmeddelandet visas när du försöker skapa en resurs med en titel som redan används av en annan resurs. Titlar måste vara unika för alla resurstyper. Om du till exempel försöker skapa en fältgrupp med en titel som redan används av ett schema, visas det här felet.

### Valideringsfel för namnområde

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

Det här felmeddelandet visas när du försöker skapa en resurs med felaktigt namngivna fält eller lägga till felaktigt namngivna fält i en befintlig resurs.

Resurser som definieras av din organisation måste namnge sina fält under ditt innehavar-ID för att undvika konflikter med andra bransch- och leverantörsresurser. När du skapar ett schema med standardfältgrupper måste alla anpassade fält som du lägger till i strukturen för dessa fältgrupper också namnges under ditt klient-ID.

>[!NOTE]
>
>Beroende på namnutrymmesfelets specifika karaktär kan det här felet använda något av följande `type` URI:er tillsammans med olika meddelandedetaljer:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Detaljerade exempel på lämpliga datastrukturer för XDM-resurser finns i API-handboken för schematabellen:

* [Skapa en anpassad klass](./api/classes.md#create)
* [Skapa en anpassad fältgrupp](./api/field-groups.md#create)
* [Skapa en anpassad datatyp](./api/data-types.md#create)

### Ogiltigt accepteringshuvud

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

GET-förfrågningar i [!DNL Schema Registry] API kräver `Accept` för att systemet ska kunna avgöra hur svaret ska formateras. Det här felet inträffar när en `Accept` huvudet är ogiltigt eller saknas.

Beroende på vilken slutpunkt du använder visas `detailed-message` egenskapen anger vad som är giltigt `Accept` sidhuvudet ska se ut som om det är ett lyckat svar. Kontrollera att du har angett en `Accept` som är kompatibel med den API-begäran du försöker göra innan du försöker igen.

>[!NOTE]
>
>Beroende på vilken slutpunkt som används kan det här felet använda något av följande `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


En lista över kompatibla Acceptera rubriker för olika API-begäranden finns i motsvarande avsnitt i [Utvecklarhandbok för schemaregister](./api/overview.md).

### [!DNL Real-Time Customer Profile] fel

Följande felmeddelanden är associerade med åtgärder som används för att aktivera scheman för [!DNL Real-Time Customer Profile]. Se [föreningar](./api/unions.md) i [!DNL Schema Registry] API-guide för mer information.

#### Det måste finnas en beskrivning av en referensidentitet

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

Det här felmeddelandet visas när du försöker aktivera ett schema för [!DNL Profile] och en av dess egenskaper innehåller en relationsbeskrivare utan någon referensidentitetsbeskrivare. Lös det här felet genom att lägga till en beskrivare för referens-ID i schemafältet i fråga.

#### Namnutrymmena för referensbeskrivningsfältet och målschemat måste matcha

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

>[!NOTE]
>
>För det här felet refererar &quot;målschema&quot; till referensschemat i relationen.

För att aktivera scheman som innehåller relationsbeskrivare för användning i [!DNL Profile]måste namnutrymmet för källfältet och det primära namnutrymmet för referensfältet vara detsamma. Det här felmeddelandet visas när du försöker aktivera ett schema som innehåller ett omatchat namnutrymme för dess referensidentitetsbeskrivning.

Se till att `xdm:namespace` värdet för referensschemats identitetsfält matchar det för `xdm:identityNamespace` -egenskapen i källfältets referensidentitetsbeskrivning för att lösa problemet.

En lista med standardkoder för identitetsnamn finns i avsnittet om [standardnamnutrymmen](../identity-service/namespaces.md) i översikten över namnutrymmet identity.

#### Schemat måste innehålla en identityMap eller primär identitet

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

Innan du aktiverar ett schema för profilen måste du först [skapa en primär identitetsbeskrivning](./api/descriptors.md#create) för schemat, eller inkludera ett fält för identitetskarta som ska fungera som primär identitet i stället.

#### Det går inte att sammanfoga inkompatibla datatyper

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

Alla profilaktiverade scheman som tillhör samma klass måste kunna sammanfogas för att det ska gå att skapa ett unionsschema för den klassen. Det här felet uppstår när du försöker lägga till ett fält i ett schema vars sökväg delas av ett annat profilaktiverat schema och datatypen skiljer sig från den ursprungliga. Eftersom scheman båda är profilaktiverade och innehåller samma fältsökväg, försöker profilen sammanfoga dessa två fält till ett när man skapar unionsschemat. Eftersom olika datatyper inte kan sammanfogas skulle detta betraktas som en sammanslagningskonflikt och är inte tillåtet.

Du löser problemet genom att välja ett annat namn för fältet eller kapsla det under ett unikt namngivet objekt för att undvika sammanslagningskonflikter med andra profilaktiverade scheman under samma klass med liknande fält.
