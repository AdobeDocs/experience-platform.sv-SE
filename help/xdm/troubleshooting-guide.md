---
keywords: Experience Platform;hem;populära ämnen;XDM;XDM system;XDM individuell profil;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event event;XDM Experience Event;XDM ExperienceEvent;experience data model;Experience data model;Experience data model;data model;data model;schema;felsökning;FAQ;faq;Union schema;UNION PROFILE;union profile profile http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;
solution: Experience Platform
title: Felsökningsguide för XDM-system
description: Hitta svar på vanliga frågor om Experience Data Model (XDM), inklusive steg för att lösa vanliga API-fel.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 415938f6f3aeec342774b73d1ae5f2dc0e27349c
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# Felsökningsguide för XDM-system

Det här dokumentet innehåller svar på vanliga frågor om [!DNL Experience Data Model] (XDM) och XDM System i Adobe Experience Platform, inklusive en felsökningsguide för vanliga fel. För frågor och felsökning som rör andra plattformstjänster, se [felsökningsguiden för Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** är en öppen källkodsspecifikation som definierar standardiserade scheman för kundupplevelsehantering. Metoden som [!DNL Experience Platform] byggs på, **XDM System**, använder [!DNL Experience Data Model] scheman för [!DNL Platform]-tjänster. **[!DNL Schema Registry]** innehåller ett användargränssnitt och ett RESTful-API för att komma åt **[!DNL Schema Library]** i [!DNL Experience Platform]. Mer information finns i [XDM-dokumentationen](home.md).

## Vanliga frågor och svar 

Nedan följer en lista med svar på vanliga frågor om XDM-systemet och användning av API:t [!DNL Schema Registry].

### Hur lägger jag till fält i ett schema?

Du kan lägga till fält i ett schema med hjälp av en schemafältgrupp. Varje fältgrupp är kompatibel med en eller flera klasser, vilket gör att fältgruppen kan användas i alla scheman som implementerar en av dessa kompatibla klasser. Adobe Experience Platform tillhandahåller flera branschfältgrupper med sina egna fördefinierade fält, men du kan lägga till egna fält i ett schema genom att skapa anpassade fältgrupper med API:t eller användargränssnittet.

Mer information om hur du skapar fältgrupper i [!DNL Schema Registry] API:t finns i [guiden för fältgruppsslutpunkter](api/field-groups.md#create). Om du använder gränssnittet läser du i självstudiekursen [Schemaredigeraren](./tutorials/create-schema-ui.md).

### Vilket är det bästa användningsområdet för fältgrupper jämfört med datatyper?

[Fältgrupper är ](./schema/composition.md#field-group) komponenter som definierar ett eller flera fält i ett schema. Fältgrupper styr hur deras fält visas i schemats hierarki och visar därför samma struktur i varje schema som de ingår i. Fältgrupper är bara kompatibla med specifika klasser, vilket identifieras av deras `meta:intendedToExtend`-attribut.

[Datatyper ](./schema/composition.md#data-type) kan även innehålla ett eller flera fält för ett schema. Till skillnad från fältgrupper är datatyperna dock inte begränsade till en viss klass. Detta gör datatyper till ett mer flexibelt alternativ för att beskriva vanliga datastrukturer som kan återanvändas i flera scheman med potentiellt olika klasser.

### Vilket unikt ID har ett schema?

Alla [!DNL Schema Registry]-resurser (scheman, fältgrupper, datatyper, klasser) har en URI som fungerar som ett unikt ID för referens- och sökningsändamål. När du visar ett schema i API:t finns det i attributen `$id` och `meta:altId` på den översta nivån.

Mer information finns i avsnittet [resursidentifiering](api/getting-started.md#resource-identification) i [!DNL Schema Registry] API-handboken.

### När börjar ett schema förhindra att ändringar bryts?

Du kan göra ändringar i ett schema så länge det aldrig har använts för att skapa en datauppsättning eller aktiverats för användning i [[!DNL Real-time Customer Profile]](../profile/home.md). När ett schema har använts när datauppsättningar skapades eller aktiverats för användning med [!DNL Real-time Customer Profile], kommer reglerna för [schemautveckling](schema/composition.md#evolution) att tillämpas strikt av systemet.

### Vilken är den maximala storleken för en lång fälttyp?

En lång fälttyp är ett heltal med en maximal storlek på 53 (+1) bitar, vilket ger den ett möjligt intervall mellan -9007199254740992 och 900719925474092. Detta beror på en begränsning av hur JavaScript-implementeringar av JSON representerar långa heltal.

Mer information om fälttyper finns i dokumentet om [XDM-fälttypsbegränsningar](./schema/field-constraints.md).

### Hur definierar jag identiteter för mitt schema?

I [!DNL Experience Platform] används identiteter för att identifiera ett ämne (vanligtvis en enskild person) oavsett vilka datakällor som tolkas. De definieras i scheman genom att nyckelfält markeras som&quot;Identitet&quot;. Vanliga fält för identitet är e-postadress, telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM-ID och andra unika ID-fält.

Fält kan markeras som identiteter med antingen API:t eller användargränssnittet.

#### Definiera identiteter i API:t

I API:t etableras identiteter genom att skapa identitetsbeskrivningar. Identitetsbeskrivare signalerar att en viss egenskap för ett schema är en unik identifierare.

Identitetsbeskrivare skapas av en POST-begäran till slutpunkten /descriptors. Om det lyckas får du ett HTTP Status 201 (Skapad) och ett svarsobjekt med information om den nya beskrivningen.

Mer information om hur du skapar identitetsbeskrivningar i API:t finns i dokumentet om [beskrivningar](api/descriptors.md) i [!DNL Schema Registry]-utvecklarhandboken.

#### Definiera identiteter i användargränssnittet

Med schemat öppet i Schemaredigeraren markerar du det fält i **[!UICONTROL Structure]**-delen av redigeraren som du vill markera som en identitet. Markera kryssrutan **[!UICONTROL Identity]** under **[!UICONTROL Field Properties]** till höger.

Mer information om hur du hanterar identiteter i användargränssnittet finns i avsnittet [definiera identitetsfält](./tutorials/create-schema-ui.md#identity-field) i schemaredigerarens självstudiekurs.

### Behöver mitt schema en primär identitet?

Primära identiteter är valfria eftersom scheman kan ha antingen noll eller en av dem. Ett schema måste dock ha en primär identitet för att schemat ska kunna aktiveras för användning i [!DNL Real-time Customer Profile]. Mer information finns i [identity](./tutorials/create-schema-ui.md#identity-field)-avsnittet i Schemaredigerarens självstudiekurs.

### Hur aktiverar jag ett schema för användning i [!DNL Real-time Customer Profile]?

Scheman kan användas i [[!DNL Real-time Customer Profile]](../profile/home.md) genom att en &quot;union&quot;-tagg läggs till i schemats `meta:immutableTags`-attribut. Du kan aktivera ett schema för användning med [!DNL Profile] med API:t eller användargränssnittet.

#### Aktivera ett befintligt schema för [!DNL Profile] med API

Gör en PATCH-begäran om att uppdatera schemat och lägg till attributet `meta:immutableTags` som en array som innehåller värdet &quot;union&quot;. Om uppdateringen lyckas visas det uppdaterade schemat som nu innehåller unionstaggen.

Mer information om hur du använder API:t för att aktivera ett schema för användning i [!DNL Real-time Customer Profile] finns i dokumentet [union](./api/unions.md) i utvecklarhandboken för [!DNL Schema Registry].

#### Aktivera ett befintligt schema för [!DNL Profile] med användargränssnittet

I [!DNL Experience Platform] väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen och väljer namnet på schemat som du vill aktivera i listan med scheman. Sedan väljer du **[!UICONTROL Profile]** till höger om redigeraren under **[!UICONTROL Schema Properties]** för att aktivera den.


Mer information finns i avsnittet om [användning i kundprofil för realtid](./tutorials/create-schema-ui.md#profile) i [!UICONTROL Schema Editor]-självstudiekursen.

### Kan jag redigera ett unionsschema direkt?

Unionsscheman är skrivskyddade och genereras automatiskt av systemet. De kan inte redigeras direkt. Unionsscheman skapas för en viss klass när en&quot;union&quot;-tagg läggs till i schemat som implementerar den klassen.

Mer information om fackföreningar i XDM finns i avsnittet [union](./api/unions.md) i [!DNL Schema Registry] API-handboken.

### Hur ska jag formatera min datafil för att importera data till mitt schema?

[!DNL Experience Platform] använder datafiler i antingen  [!DNL Parquet] eller JSON-format. Innehållet i dessa filer måste överensstämma med det schema som datauppsättningen refererar till. Mer information om de bästa sätten att mata in datafiler finns i [översikten över gruppöverföring](../ingestion/home.md).

## Fel och felsökning

Nedan följer en lista över felmeddelanden som du kan stöta på när du arbetar med API:t [!DNL Schema Registry].

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
>Beroende på vilken resurstyp som hämtas kan det här felet använda någon av följande URI:er för `type`:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Mer information om hur du skapar sökvägar i API:t finns i avsnitten [container](./api/getting-started.md#container) och [resource identifier](api/getting-started.md#resource-identification) i utvecklarhandboken för [!DNL Schema Registry].

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

Resurser som definieras av din IMS-organisation måste namnge sina fält under ditt innehavar-ID för att undvika konflikter med andra bransch- och leverantörsresurser. När du skapar ett schema med standardfältgrupper måste alla anpassade fält som du lägger till i strukturen för dessa fältgrupper också namnges under ditt klient-ID.

>[!NOTE]
>
>Beroende på namnområdesfelets specifika karaktär kan det här felet använda någon av följande `type`-URI:er tillsammans med olika meddelandedetaljer:
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

GET-begäranden i API:t [!DNL Schema Registry] kräver en `Accept`-rubrik för att systemet ska kunna avgöra hur svaret ska formateras. Det här felet inträffar när en obligatorisk `Accept`-rubrik är ogiltig eller saknas.

Beroende på vilken slutpunkt du använder anger egenskapen `detailed-message` hur en giltig `Accept`-rubrik ska se ut för ett lyckat svar. Kontrollera att du har angett ett `Accept`-huvud som är korrekt kompatibelt med den API-begäran du försöker göra innan du försöker igen.

>[!NOTE]
>
>Beroende på vilken slutpunkt som används kan det här felet använda någon av följande `type`-URI:er:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


En lista över kompatibla Accept-huvuden för olika API-begäranden finns i motsvarande avsnitt i [Utvecklarhandbok för schemaregister](./api/overview.md).

### [!DNL Real-time Customer Profile] fel

Följande felmeddelanden är associerade med åtgärder som används för att aktivera scheman för [!DNL Real-time Customer Profile]. Mer information finns i avsnittet [union](./api/unions.md) i [!DNL Schema Registry] API-handboken.

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

Om du vill aktivera scheman som innehåller relationsbeskrivningar för användning i [!DNL Profile] måste källfältets namnutrymme och målfältets primära namnutrymme vara samma. Det här felmeddelandet visas när du försöker aktivera ett schema som innehåller ett omatchat namnutrymme för dess referensidentitetsbeskrivning. Kontrollera att `xdm:namespace`-värdet för målschemats identitetsfält matchar `xdm:identityNamespace`-egenskapen i källfältets beskrivare för referens-ID för att lösa problemet.

En lista med standardkoder för identitetsnamnutrymmen finns i avsnittet [standardnamnutrymmen](../identity-service/namespaces.md) i översikten över identitetsnamnutrymmet.

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

Innan du aktiverar ett schema för profilen måste du först [skapa en primär identitetsbeskrivning](./api/descriptors.md#create) för schemat, eller inkludera ett identitetsmappningsfält som ska fungera vid den primära identiteten i stället.