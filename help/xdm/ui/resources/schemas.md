---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;schema;schemas;schemas;
solution: Experience Platform
title: Skapa och redigera scheman i användargränssnittet
description: Lär dig grunderna i hur du skapar och redigerar scheman i användargränssnittet i Experience Platform.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: a95e5cf02e993d6c761abd74c98c0967a89eb678
workflow-type: tm+mt
source-wordcount: '2823'
ht-degree: 0%

---

# Skapa och redigera scheman i användargränssnittet

Den här guiden ger en översikt över hur du skapar, redigerar och hanterar XDM-scheman (Experience Data Model) för din organisation i Adobe Experience Platform användargränssnitt.

>[!IMPORTANT]
>
>XDM-scheman är extremt anpassningsbara, och därför kan stegen som krävs för att skapa ett schema variera beroende på vilken typ av data du vill att schemat ska hämta. Det innebär att det här dokumentet endast omfattar de grundläggande interaktioner du kan göra med scheman i användargränssnittet, och att relaterade steg som att anpassa klasser, schemafältgrupper, datatyper och fält inte tas med.
>
>Om du vill få en genomgång av hur du skapar scheman kan du följa med i [självstudiekurs om att skapa scheman](../../tutorials/create-schema-ui.md) för att skapa ett komplett exempelschema och bekanta dig med de många funktionerna i [!DNL Schema Editor].

## Förutsättningar

Handboken kräver en fungerande förståelse för XDM System. Se [XDM - översikt](../../home.md) en introduktion till XDM:s roll i Experience Platform-ekosystemet, och [grunderna för schemakomposition](../../schema/composition.md) för en översikt över hur scheman är uppbyggda.

## Skapa ett nytt schema {#create}

I [!UICONTROL Schemas] arbetsyta, välja **[!UICONTROL Create schema]** i det övre högra hörnet. I listrutan som visas kan du välja mellan **[!UICONTROL XDM Individual Profile]** och **[!UICONTROL XDM ExperienceEvent]** som basklass för schemat. Du kan också välja **[!UICONTROL Browse]** att välja i den fullständiga listan över tillgängliga klasser, eller [skapa en ny anpassad klass](./classes.md#create) i stället.

![](../../images/ui/resources/schemas/create-schema.png)

När du har valt en klass visas [!DNL Schema Editor] visas och schemats grundstruktur (tillhandahålls av klassen) visas på arbetsytan. Härifrån kan du använda rätt spår för att lägga till en **[!UICONTROL Display name]** och **[!UICONTROL Description]** för schemat.

![](../../images/ui/resources/schemas/schema-details.png)

Nu kan du börja skapa schemats struktur genom att [lägga till schemafältgrupper](#add-field-groups).

## Redigera ett befintligt schema {#edit}

>[!NOTE]
>
>När ett schema har sparats och använts vid datainmatning kan endast additiva ändringar göras. Se [regler för schemautveckling](../../schema/composition.md#evolution) för mer information.

Om du vill redigera ett befintligt schema väljer du **[!UICONTROL Browse]** och markera sedan namnet på schemat som du vill redigera.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Du kan använda arbetsytans sök- och filtreringsfunktioner för att enklare hitta schemat. Se guiden [utforska XDM-resurser](../explore.md) för mer information.

När du har valt ett schema visas [!DNL Schema Editor] visas med schemats struktur på arbetsytan. Nu kan du [lägg till fältgrupper](#add-field-groups) till schemat (eller [lägg till enskilda fält](#add-individual-fields) från dessa grupper), [redigera fältvisningsnamn](#display-names), eller [redigera befintliga anpassade fältgrupper](./field-groups.md#edit) om schemat använder något.

## Lägga till fältgrupper i ett schema {#add-field-groups}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du lägger till befintliga fältgrupper i ett schema. Om du vill skapa en ny anpassad fältgrupp läser du i guiden [skapa och redigera fältgrupper](./field-groups.md#create) i stället.

När du har öppnat ett schema i [!DNL Schema Editor]kan du lägga till fält i schemat med hjälp av fältgrupper. Börja genom att välja **[!UICONTROL Add]** nästa **[!UICONTROL Field groups]** till vänster.

![](../../images/ui/resources/schemas/add-field-group-button.png)

En dialogruta visas med en lista över fältgrupper som du kan välja för schemat. Eftersom fältgrupper endast är kompatibla med en klass, visas endast de fältgrupper som är associerade med schemats valda klass. Som standard sorteras listade fältgrupper baserat på hur populära de är i din organisation.

![](../../images/ui/resources/schemas/field-group-popularity.png)

Om du känner till den allmänna aktiviteten eller affärsområdet för de fält som du vill lägga till, väljer du en eller flera av de branschvertikala kategorierna i den vänstra listen för att filtrera den visade listan med fältgrupper.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Mer information om de bästa metoderna för branschspecifik datamodellering i XDM finns i dokumentationen om [branschdatamodeller](../../schema/industries/overview.md).

Du kan också använda sökfältet för att hitta den fältgrupp du vill använda. Fältgrupper vars namn matchar frågan visas högst upp i listan. Under **[!UICONTROL Standard Fields]** visas fältgrupper som innehåller fält som beskriver önskade dataattribut.

![](../../images/ui/resources/schemas/field-group-search.png)

Markera kryssrutan bredvid namnet på den fältgrupp som du vill lägga till i schemat. Du kan markera flera fältgrupper i listan, där varje markerad fältgrupp visas i den högra listen.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>För alla fältgrupper i listan kan du hovra eller fokusera på informationsikonen (![](../../images/ui/resources/schemas/info-icon.png)) för att visa en kort beskrivning av den typ av data som fältgruppen hämtar. Du kan också välja förhandsvisningsikonen (![](../../images/ui/resources/schemas/preview-icon.png)) för att visa strukturen för fälten som fältgruppen tillhandahåller innan du bestämmer dig för att lägga till den i schemat.

När du har valt fältgrupper väljer du **[!UICONTROL Add field groups]** för att lägga till dem i schemat.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

The [!DNL Schema Editor] visas igen med fälten som tillhandahålls av fältgruppen och som visas på arbetsytan.

![](../../images/ui/resources/schemas/field-groups-added.png)

När du har lagt till en fältgrupp i ett schema kan du välja att [ta bort befintliga fält](#remove-fields) eller [lägg till nya anpassade fält](#add-fields) till de grupperna, beroende på dina behov.

### Ta bort fält som lagts till från fältgrupper {#remove-fields}

När du har lagt till en fältgrupp i ett schema kan du ta bort fält som du inte behöver.

>[!NOTE]
>
>Om du tar bort fält från en fältgrupp påverkas bara schemat som du arbetar med och påverkar inte själva fältgruppen. Om du tar bort fält i ett schema är dessa fält fortfarande tillgängliga i alla andra scheman som använder samma fältgrupp.

I följande exempel är standardfältgruppen **[!UICONTROL Demographic Details]** har lagts till i ett schema. Ta bort ett enskilt fält som `taxId`markerar du fältet på arbetsytan och väljer **[!UICONTROL Remove]** i rätt spår.

![Ta bort ett fält](../../images/ui/resources/schemas/remove-single-field.png)

Om det finns flera fält som du vill ta bort kan du hantera fältgruppen som helhet. Markera ett fält som tillhör gruppen på arbetsytan och välj sedan **[!UICONTROL Manage related fields]** i rätt spår.

![Hantera relaterade fält](../../images/ui/resources/schemas/manage-related-fields.png)

En dialogruta visas med strukturen för fältgruppen i fråga. Härifrån kan du använda de angivna kryssrutorna för att markera eller avmarkera de fält som du behöver. När du är nöjd väljer du **[!UICONTROL Confirm]**.

![Välj fält från fältgrupp](../../images/ui/resources/schemas/select-fields.png)

Arbetsytan visas igen med endast de markerade fälten i schemastrukturen.

![Fält har lagts till](../../images/ui/resources/schemas/fields-added.png)

### Lägg till anpassade fält i fältgrupper {#add-fields}

När du har lagt till en fältgrupp i ett schema kan du definiera ytterligare fält för den gruppen. Alla fält som läggs till i en fältgrupp i ett schema visas emellertid också i alla andra scheman som använder samma fältgrupp.

Om ett anpassat fält dessutom läggs till i en standardfältgrupp, kommer den fältgruppen att konverteras till en anpassad fältgrupp och den ursprungliga standardfältgruppen kommer inte längre att vara tillgänglig.

Om du vill lägga till ett anpassat fält i en standardfältgrupp, se [avsnitt nedan](#custom-fields-for-standard-groups) för specifika instruktioner. Om du lägger till fält i en anpassad fältgrupp, se avsnittet om [redigera anpassade fältgrupper](./field-groups.md) i fältgruppsguiden.

Om du inte vill ändra några fältgrupper kan du [skapa en ny anpassad fältgrupp](./field-groups.md#create) om du vill definiera ytterligare fält i stället.

## Lägga till enskilda fält i ett schema {#add-individual-fields}

Med Schemaredigeraren kan du lägga till enskilda fält direkt i ett schema om du inte vill lägga till en hel fältgrupp för ett visst användningsfall. Du kan [lägga till enskilda fält från standardfältgrupper](#add-standard-fields) eller [lägga till egna fält](#add-custom-fields) i stället.

>[!IMPORTANT]
>
>Även om schemaredigeraren tillåter att du lägger till enskilda fält direkt i ett schema, ändrar detta inte det faktum att alla fält i ett XDM-schema måste anges av dess klass eller en fältgrupp som är kompatibel med den klassen. Som framgår av avsnitten nedan är alla enskilda fält fortfarande kopplade till en fältgrupp som ett nyckelsteg när de läggs till i ett schema.

### Lägg till standardfält {#add-standard-fields}

Du kan lägga till fält från standardfältgrupper direkt i ett schema utan att först behöva känna till deras motsvarande fältgrupp. Om du vill lägga till ett standardfält i ett schema väljer du plustecknet (**+**) bredvid schemats namn på arbetsytan. An **[!UICONTROL Untitled Field]** platshållaren visas i schemastrukturen och uppdaterar den högra listen för att visa kontroller för att konfigurera fältet.

![Platshållare för fält](../../images/ui/resources/schemas/root-custom-field.png)

Under **[!UICONTROL Field name]** börjar du skriva namnet på det fält som du vill lägga till. Systemet söker automatiskt efter standardfält som matchar frågan och listar dem under **[!UICONTROL Recommended Standard Fields]**, inklusive de fältgrupper som de tillhör.

![Rekommenderade standardfält](../../images/ui/resources/schemas/standard-field-search.png)

Vissa standardfält har samma namn, men strukturen kan variera beroende på vilken fältgrupp de kommer ifrån. Om ett standardfält är kapslat i ett överordnat objekt i fältgruppsstrukturen, kommer det överordnade fältet också att inkluderas i schemat om det underordnade fältet läggs till.

Välj förhandsvisningsikonen (![Ikonen Förhandsgranska](../../images/ui/resources/schemas/preview-icon.png)) bredvid ett standardfält för att visa strukturen för dess fältgrupp och bättre förstå hur den kan kapslas. Om du vill lägga till standardfältet i schemat väljer du plusikonen (![Plustecken](../../images/ui/resources/schemas/add-icon.png)).

![Lägg till standardfält](../../images/ui/resources/schemas/add-standard-field.png)

Arbetsytan uppdateras för att visa det standardfält som lagts till i schemat, inklusive alla överordnade fält som är kapslade i fältgruppsstrukturen. Namnet på fältgruppen visas också under **[!UICONTROL Field groups]** till vänster. Om du vill lägga till fler fält från samma fältgrupp väljer du **[!UICONTROL Manage related fields]** i rätt spår.

![Standardfältet har lagts till](../../images/ui/resources/schemas/standard-field-added.png)

### Lägg till anpassade fält {#add-custom-fields}

På samma sätt som arbetsflödet för standardfält kan du även lägga till egna anpassade fält direkt i ett schema.

Om du vill lägga till fält på rotnivån för ett schema väljer du plustecknet (**+**) bredvid schemats namn på arbetsytan. An **[!UICONTROL Untitled Field]** platshållaren visas i schemastrukturen och uppdaterar den högra listen för att visa kontroller för att konfigurera fältet.

![Anpassat rotfält](../../images/ui/resources/schemas/root-custom-field.png)

Börja skriva in namnet på det fält som du vill lägga till så börjar systemet automatiskt att söka efter matchande standardfält. Om du vill skapa ett nytt anpassat fält i stället väljer du det översta alternativet som bifogas med **([!UICONTROL New Field])**.

![Nytt fält](../../images/ui/resources/schemas/custom-field-search.png)

Här anger du ett visningsnamn och en datatyp för fältet. Under **[!UICONTROL Assign field group]** måste du välja en fältgrupp för det nya fältet som ska associeras med. Börja skriva in namnet på fältgruppen och om du tidigare har [skapade anpassade fältgrupper](./field-groups.md#create) visas i listrutan. Du kan också skriva ett unikt namn i fältet för att skapa en ny fältgrupp i stället.

![Välj fältgrupp](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Om du väljer en befintlig anpassad fältgrupp kommer alla andra scheman som använder den fältgruppen också att ärva det nya fältet när du har sparat ändringarna. Därför bör du bara markera en befintlig fältgrupp om du vill använda den här typen av spridning. Annars bör du välja att skapa en ny anpassad fältgrupp i stället.

När du är klar väljer du **[!UICONTROL Apply]**.

![Använd fält](../../images/ui/resources/schemas/apply-field.png)

Det nya fältet läggs till på arbetsytan och får ett namn under [klient-ID](../../api/getting-started.md#know-your-tenant_id) för att undvika konflikter med XDM-standardfält. Fältgruppen som du kopplade det nya fältet till visas också under **[!UICONTROL Field groups]** till vänster.

![Klient-ID](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>Resten av fälten i den valda anpassade fältgruppen tas som standard bort från schemat. Om du vill lägga till några av dessa fält i schemat markerar du ett fält som tillhör gruppen och väljer sedan **[!UICONTROL Manage related fields]** i rätt spår.

#### Lägga till anpassade fält i strukturen för standardfältgrupper {#custom-fields-for-standard-groups}

Om schemat du arbetar med har ett objekttypsfält från en standardfältgrupp, kan du lägga till egna anpassade fält till det standardobjektet.

>[!WARNING]
>
>Alla fält som läggs till i en fältgrupp i ett schema visas också i alla andra scheman som använder samma fältgrupp. Om ett anpassat fält dessutom läggs till i en standardfältgrupp, kommer den fältgruppen att konverteras till en anpassad fältgrupp och den ursprungliga standardfältgruppen kommer inte längre att vara tillgänglig.
>
>Om du deltar i betaversionen av den här funktionen får du en dialogruta som informerar dig om vilka standardfältgrupper du tidigare har anpassat. När du har valt **[!UICONTROL Acknowledge]**, konverteras resurserna till anpassade fältgrupper.
>
>![Bekräftelsedialogruta för konvertering av standardfältgrupper](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Börja med att välja plustecknet (**+**) bredvid roten för objektet som anges av standardfältgruppen.

![Lägg till fält i standardobjekt](../../images/ui/resources/schemas/add-field-to-standard-object.png)

Ett varningsmeddelande visas som uppmanar dig att bekräfta om du vill konvertera standardfältgruppen. Välj **[!UICONTROL Continue creating field group]** för att fortsätta.

![Bekräfta konvertering av fältgrupp](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

Arbetsytan visas igen med en namnlös platshållare för det nya fältet. Observera att namnet på standardfältgruppen har lagts till med &quot;([!UICONTROL Extended])&quot; för att ange att den har ändrats från den ursprungliga versionen. Använd kontrollerna i den högra listen för att definiera fältets egenskaper.

![Fält tillagt i standardobjekt](../../images/ui/resources/schemas/standard-field-group-converted.png)

När du har gjort ändringarna visas det nya fältet under ditt innehavar-ID-namnutrymme i standardobjektet. Det här kapslade namnutrymmet förhindrar konflikter mellan fält och namn inom själva fältgruppen för att undvika att bryta ändringar i andra scheman som använder samma fältgrupp.

![Fält tillagt i standardobjekt](../../images/ui/resources/schemas/added-to-standard-object.png)

## Aktivera ett schema för kundprofil i realtid {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Aktivera ett schema för profil"
>abstract="När ett schema har aktiverats för profilen, deltar alla datauppsättningar som skapats från det här schemat i kundprofilen i realtid, som sammanfogar data från olika källor för att skapa en fullständig bild av varje kund. När ett schema används för att importera data till profilen kan det inte inaktiveras. Mer information finns i dokumentationen."

[Kundprofil i realtid](../../../profile/home.md) sammanfogar data från olika källor för att skapa en komplett bild av varje enskild kund. Om du vill att de data som hämtas av ett schema ska delta i processen måste du aktivera schemat för användning i [!DNL Profile].

>[!IMPORTANT]
>
>För att aktivera ett schema för [!DNL Profile]måste ett primärt identitetsfält ha definierats. Se guiden [definiera identitetsfält](../fields/identity.md) för mer information.

Aktivera schemat genom att först markera schemats namn i den vänstra listen och sedan välja **[!UICONTROL Profile]** till höger.

![](../../images/ui/resources/schemas/profile-toggle.png)

En pover visas som varnar om att när ett schema väl har aktiverats och sparats kan det inte inaktiveras. Välj **[!UICONTROL Enable]** för att fortsätta.

![](../../images/ui/resources/schemas/profile-confirm.png)

Arbetsytan visas igen med [!UICONTROL Profile] växla aktiverat.

>[!IMPORTANT]
>
>Eftersom schemat ännu inte har sparats är detta inget returtecken om du ändrar dig angående att låta schemat delta i kundprofilen i realtid: När du har sparat ett aktiverat schema kan det inte längre inaktiveras. Välj **[!UICONTROL Profile]** växla igen för att inaktivera schemat.

Avsluta processen genom att välja **[!UICONTROL Save]** för att spara schemat.

![](../../images/ui/resources/schemas/profile-enabled.png)

Schemat är nu aktiverat för användning i kundprofilen i realtid. När Platform samlar in data i datauppsättningar som baseras på det här schemat, kommer dessa data att införlivas i dina sammanställda profildata.

## Redigera visningsnamn för schemafält {#display-names}

När du har tilldelat en klass och lagt till fältgrupper till ett schema kan du redigera visningsnamnen för alla fält i schemat, oavsett om dessa fält har tillhandahållits av standard eller anpassade XDM-resurser.

>[!NOTE]
>
>Tänk på att visningsnamnen för fält som tillhör standardklasser eller fältgrupper bara kan redigeras i ett specifikt schema. Om du ändrar visningsnamnet för ett standardfält i ett schema påverkas alltså inte andra scheman som använder samma associerade klass eller fältgrupp.
>
>När du ändrar visningsnamnen för ett schemas fält återspeglas dessa ändringar omedelbart i befintliga datauppsättningar som baseras på det schemat.

Om du vill redigera visningsnamnet för ett schemafält markerar du fältet på arbetsytan. Ange det nya namnet under **[!UICONTROL Display name]**.

![](../../images/ui/resources/schemas/display-name.png)

Välj **[!UICONTROL Apply]** till höger och arbetsytan uppdateras för att visa fältets nya visningsnamn. Välj **[!UICONTROL Save]** för att tillämpa ändringarna i schemat.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Ändra en schemaklass {#change-class}

Du kan ändra schemaklassen när som helst under den inledande dispositionsprocessen innan schemat har sparats.

>[!WARNING]
>
>Omtilldelning av klassen för ett schema bör göras med extrem försiktighet. Fältgrupper är bara kompatibla med vissa klasser. Om du ändrar klassen återställs arbetsytan och alla fält du har lagt till.

Om du vill tilldela om en klass väljer du **[!UICONTROL Assign]** till vänster på arbetsytan.

![](../../images/ui/resources/schemas/assign-class-button.png)

En dialogruta visas med en lista över alla tillgängliga klasser, inklusive alla som definierats av organisationen (ägaren är[!UICONTROL Customer]&quot;) samt standardklasser som definieras av Adobe.

Välj en klass i listan för att visa dess beskrivning till höger i dialogrutan. Du kan också välja **[!UICONTROL Preview class structure]** om du vill visa de fält och metadata som är associerade med klassen. Välj **[!UICONTROL Assign class]** för att fortsätta.

![](../../images/ui/resources/schemas/assign-class.png)

En ny dialogruta öppnas där du ombeds bekräfta att du vill tilldela en ny klass. Välj **[!UICONTROL Assign]** för att bekräfta.

![](../../images/ui/resources/schemas/assign-confirm.png)

När du har bekräftat klassändringen återställs arbetsytan och alla dispositionsförlopp går förlorade.

## Nästa steg

Det här dokumentet innehåller grunderna för att skapa och redigera scheman i plattformsgränssnittet. Vi rekommenderar att du granskar [självstudiekurs om att skapa scheman](../../tutorials/create-schema-ui.md) för ett omfattande arbetsflöde för att skapa ett komplett schema i användargränssnittet, inklusive att skapa anpassade fältgrupper och datatyper för unika användningsfall.

Mer information om funktionerna i [!UICONTROL Schemas] arbetsytan, se [[!UICONTROL Schemas] arbetsyta - översikt](../overview.md).

Så här hanterar du scheman i [!DNL Schema Registry] API, se [slutpunktshandbok för scheman](../../api/schemas.md).
