---
keywords: Experience Platform;home;populära topics;relational schema;relational schemas;schema;schema;xdm;experience data model;
solution: Experience Platform
title: Relationsscheman
description: Läs om relationsscheman i Adobe Experience Platform, inklusive funktioner, obligatoriska fält, relationer och begränsningar.
badge: Begränsad tillgänglighet
exl-id: 397e5937-b892-4fd3-b90e-29ed9229dc69
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 0%

---

# Relationsscheman

>[!AVAILABILITY]
>
>Data Mirror och relationsscheman är tillgängliga för Adobe Journey Optimizer **licensinnehavare för samordnade kampanjer**. De är också tillgängliga som en **begränsad version** för Customer Journey Analytics-användare, beroende på din licens och aktivering av funktioner. Kontakta din Adobe-representant för att få åtkomst.

Relationsscheman är ett flexibelt, kontrollerat modelleringsmönster för att representera strukturerade data i dataströmmen i Adobe Experience Platform. De har stöd för tvingande primärnycklar, relationer på schemanivå och detaljerad kontroll över poster, utan att man behöver förlita sig på fackscheman eller fullständiga relationsdatabassystem.

>[!IMPORTANT]
>
>Överväganden om dataradering gäller för alla relationsschemaimplementeringar. Program som använder dessa scheman måste förstå hur borttagningar påverkar relaterade datauppsättningar, kompatibilitetskrav och processer i senare led. Planera för borttagningsscenarier och granska [vägledningen för datahygien](../../hygiene/ui/record-delete.md#relational-record-delete) innan implementeringen.

Använd relationsscheman för att:

* Säkerställ dataintegriteten med enkla eller sammansatta primärnycklar.
* Aktivera exakt ändringsspårning med hjälp av versionshantering för infogningar, uppdateringar och borttagningar.
* Definiera återanvändbara relationer på schemanivå för att modellera entitetsanslutningar i verkligheten.
* Undvik att duplicera schemastrukturer mellan program genom att ha stöd för flera datamodeller.
* Hoppa över begränsningar i fackliga scheman för att effektivisera introduktionen, minska schemablockering och undvika oönskade schemaändringar.

## Hur relationsscheman skiljer sig från vanliga XDM-scheman

XDM-standardscheman i Experience Platform följer en av tre databeteenden: Record, Time-series eller Ad-hoc. Mer information och definitioner finns i [XDM-databeteenden](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home#data-behaviors).

I den traditionella modellen deltar scheman för inspelning och tidsserier i [fackscheman](../api/unions.md) (se även [gränssnittsguiden för unionsscheman](../../profile/ui/union-schema.md)). Dessa scheman utvecklas automatiskt när delade [fältgrupper](./composition.md#field-group) uppdateras och anpassade fält måste kapslas under ett innehavarnamnområde. Den här modellen är kraftfull och kan göra onboarding långsammare, skapa alltför komplexa scheman med oanvända fält och kräva ytterligare datamappning eller dataomvandling. Dessa faktorer ökar inlärningskurvan och den pågående underhållsinsatsen.

Relationsscheman tar bort unionens schemaberoenden, vilket eliminerar automatiska uppdateringar från delade fältgrupper och tillåter direkta fältdefinitioner utan begränsningar för innehavarens namnområde. Du får explicit kontroll över primärnycklar, relationer och inledande schemadesign, vilket gör det enklare att modellera data efter dina behov när de skapas.

## Funktioner för relationsscheman

Använd följande funktioner för att modellera strukturerade data i datasjön med bibehållen styrning, integritet och interoperabilitet.

* **Stöd för schemabeteende**: Konfigurera med:
   * **Postbeteende**: Hämtar det aktuella tillståndet för en entitet, till exempel en kund, ett konto eller en kampanj.
   * **Tidsseriebeteende**: Hämtar händelser och den tid de inträffar, vilket är användbart för att spåra sekvenser eller ändringar över tid.
* **Tillämpning av primärnyckel**: Definiera en primärnyckel för att unikt identifiera varje post och förhindra dubbletter under importen.
* **Versionskontroll**: Använd en **versionsidentifierare** (en beskrivning) för att se till att uppdateringar tillämpas i rätt ordning, även om posterna kommer ut ur sekvensen.
* **Relationsmappning**: Skapa en-till-en- eller många-till-en-relationer mellan relationsscheman eller mellan relationsscheman och standardscheman. Relationsdefinitioner lagras som beskrivningar för att aktivera effektiva kopplingar.
* **Förenklad utveckling**: Relationsscheman deltar inte i unionsvyer och uppdateras inte när delade fältgrupper ändras, vilket förhindrar oväntade ändringar i senare led.
* **Flexibel fältdefinition**: Lägg till fält direkt utan namnutrymme för klient-id. Relationsscheman stöder inte XDM-fältgrupper.
* **Inget beroende av unionsscheman**: Förbättrar frågeprestanda och minskar driftskostnaderna för hantering av globala schemavyer.
* **Evenemangstidsortering**: För tidsseriescheman använder du en **tidsstämpelidentifierare** för att ordna händelser efter förekomsttid i stället för att lägga till tid.

## Obligatoriska fält

Relationsscheman kräver vissa beskrivningar - metadata i schemadefinitionen som styr nyckelbeteenden och begränsningar. Lägg till följande beskrivningar som en del av schemadefinitionen.

### Primär nyckelbeskrivning

Använd en primärnyckelbeskrivning för att säkerställa att varje post är unikt identifierbar. De konfigurationer som stöds är:

* **Primärnyckel för ett fält**: Använd ett fält med ett unikt värde för varje post.
* **Sammansatt primärnyckel**: Använd flera fält för att skapa en unik identifierare. För tidsseriescheman måste den sammansatta nyckeln innehålla det tidsstämpelfält som identifieras av tidsstämpelsbeskrivningen.

>[!NOTE]
>
>I UI-schemaredigeraren visas versionsbeskrivningarna och tidsstämpelbeskrivningarna som [!UICONTROL Version identifier] respektive [!UICONTROL Timestamp identifier].

**Exempel (enfält):**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**Exempel (sammansatt för tidsserie)**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### Versionsbeskrivare (identifierare)

Definiera en versionsbeskrivning (identifierare) för att behålla rätt posttillstånd och se till att den senaste uppdateringen tillämpas. När flera poster delar samma primärnyckel anses posten med det högsta versionsvärdet vara den senaste.

**Exempel:**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### Tidsstämpelbeskrivning (identifierare)

För scheman för tidsserier definierar du en tidsstämpelbeskrivning (identifierare) för att ange händelsetiden för beställningen.

**Exempel:**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>Beskrivningar ingår i schemadefinitionsmetadata och lagras inte i datarader.

Instruktioner om hur du skapar beskrivningar i Schemaredigeraren finns i [Skapa beskrivningar i Schemaredigeraren](../tutorials/relationship-ui.md). Information om API-baserad generering finns i [Skapa beskrivningar med API:t](../tutorials/relationship-api.md).

## Relationsstöd {#relationship-support}

Relationsdatamodellering är den primära användningen av relationsscheman. Användningsexempel kan till och med hänvisa till dessa scheman som&quot;relationsscheman&quot;. Relationsbeskrivare aktiverar dessa anslutningar genom att länka datauppsättningar mellan scheman utan att bädda in främmande nycklar i datarader. De förbättrar referensintegriteten, möjliggör återanvändbara modelleringsmönster och stöder kopplade frågor i olika program.

Skapa relationsbeskrivare på schemanivå för dynamisk upplösning vid frågetiden. Kardinalvärden (1:1, många-till-ett) ger vägledning men tvingar inte till begränsningar vid intag, vilket stöder flexibel datamodellering över anslutna datamängder.

Innan du lägger till relationsbeskrivare bör du fastställa lämplig typ och mål:

* **En-till-en** - Varje post i källschemat motsvarar högst en post i målschemat.
* **Många-till-ett** - Flera poster i källschemat kan referera till samma post i målschemat.

>[!NOTE]
>
>Du kan definiera relationer mellan två relationsscheman eller mellan ett relationsschema och ett standardschema. Relationer till ad hoc-scheman stöds inte.

**Exempel: En-till-en-relation**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

**Exempel: Många-till-ett-relation**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

En lista över relationstyper och syntax finns i [API-referensen för beskrivningar](../api/descriptors.md).Om du vill lära dig hur du tillämpar dessa begrepp i praktiken kan du följa självstudiekurserna för att [definiera en relation i API:t](../tutorials/relationship-api.md) eller [skapa en relation i gränssnittet](../tutorials/relationship-ui.md).

>[!NOTE]
>
>När relationer definieras på schemanivå måste du se till att explicit koppla relaterade datauppsättningar i dina frågor. Använd ett verktyg som Data Distiller för att lösa dessa relationer under frågetiden.

>[!IMPORTANT]
>
>Kardinaliteten i relationen är informativ och upprätthålls inte vid förtäring. Det används bara när relationer löses under en fråga eller analys. Förlita dig inte på kardinalinställningar för att validera dina data vid intag. Kontrollera och rensa dina data själv och se till att de relationsregler du definierar matchar det sätt du tänker fråga eller analysera data på.

>[!NOTE]
>
>Relationsscheman kan länka till standardscheman, men kan inte länka till ad hoc-scheman.

## Ta bort data och ta hänsyn till hygienen {#data-hygiene-support}

Relationsscheman möjliggör exakt borttagning på postnivå som har universella konsekvenser för alla program och användningsfall. Beskrivningar av primärnyckel, version och tidsstämpel utgör grunden för korrekt identifiering av poster under borttagningsåtgärder.

### Inverkan vid universell borttagning

Alla program som använder relationsscheman måste ta hänsyn till:

* **Referensintegritet**: Borttagningar kan påverka relaterade poster i kopplade datauppsättningar
* **Krav för efterlevnad**: Vissa branscher kräver specifika raderingsbeteenden och granskningsspår
* **Programbeteende**: Nedströmssystem kan behöva hantera borttagningshändelser på rätt sätt
* **Datakonsekvens**: Relaterade datauppsättningar måste bibehålla konsekvensen under borttagningsåtgärder
* **Borttagningsplanering**: Konto för efterföljande effekter för alla anslutna datauppsättningar och program under designfasen

Implementeringsvägledning finns i [Ta bort poster från datauppsättningar baserat på relationsscheman](../../hygiene/ui/record-delete.md#relational-record-delete).

## Begränsningar och överväganden {#limitations}

Granska följande begränsningar innan du använder relationsscheman:

* Relationsscheman ingår inte i unionsscheman.
* Schemautvecklingen är manuell. Den uppdateras inte automatiskt när fältgrupper ändras.

>[!IMPORTANT]
>
>Schemautvecklingen begränsas efter att en datauppsättning har initierats med schemat. Planera fältnamn och typer noggrant i förväg eftersom det inte går att ta bort eller ändra fält när data har importerats.

* Relationer är begränsade till 1:1 och många-till-1.
* Tillgängligheten beror på licensen eller funktionens aktivering.
* Sammansatta primärnycklar krävs för tidsseriescheman.
