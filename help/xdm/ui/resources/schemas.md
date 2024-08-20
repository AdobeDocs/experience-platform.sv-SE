---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;schema;schemas;schemas;
solution: Experience Platform
title: Skapa och redigera scheman i användargränssnittet
description: Lär dig grunderna i hur du skapar och redigerar scheman i användargränssnittet i Experience Platform.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '3705'
ht-degree: 0%

---

# Skapa och redigera scheman i användargränssnittet {#create-edit-schemas-in-ui}

Den här guiden ger en översikt över hur du skapar, redigerar och hanterar XDM-scheman (Experience Data Model) för din organisation i Adobe Experience Platform användargränssnitt.

>[!IMPORTANT]
>
>XDM-scheman är extremt anpassningsbara, och därför kan stegen som krävs för att skapa ett schema variera beroende på vilken typ av data du vill att schemat ska hämta. Det innebär att det här dokumentet endast omfattar de grundläggande interaktioner du kan göra med scheman i användargränssnittet, och att relaterade steg som att anpassa klasser, schemafältgrupper, datatyper och fält inte tas med.
>
>Om du vill få en genomgång av schemaskapandet kan du följa med i självstudiekursen [för att skapa scheman](../../tutorials/create-schema-ui.md) och skapa ett fullständigt exempelschema och bekanta dig med de många funktionerna i [!DNL Schema Editor].

## Förhandskrav {#prerequisites}

Handboken kräver en fungerande förståelse för XDM System. Se [XDM-översikten](../../home.md) för en introduktion till XDM-rollen i ekosystemet Experience Platform och [grunderna i schemakomposition](../../schema/composition.md) för en översikt över hur scheman är uppbyggda.

## Skapa ett nytt schema {#create}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du manuellt skapar ett nytt schema i användargränssnittet. Om du importerar CSV-data till plattformen kan du använda HTML-algoritmer (Machine Learning) för att **generera ett schema från CSV-exempeldata**. Det här arbetsflödet matchar ditt dataformat och skapar automatiskt ett nytt schema baserat på strukturen och innehållet i din CSV-fil. Mer information om det här arbetsflödet finns i guiden [Skapa ML-stödda scheman](../ml-assisted-schema-creation.md).

Välj **[!UICONTROL Create schema]** i det övre högra hörnet på arbetsytan [!UICONTROL Schemas].

![Arbetsytan Scheman med [!UICONTROL Create Schema] är markerad.](../../images/ui/resources/schemas/create-schema.png)

Dialogrutan [!UICONTROL Create a schema] visas. I den här dialogrutan kan du välja att antingen skapa ett schema manuellt genom att lägga till fält och fältgrupper, eller så kan du överföra en CSV-fil och använda ML-algoritmer för att generera ett schema. Välj ett arbetsflöde för att skapa schema i dialogrutan.

![Dialogrutan Skapa ett schema med arbetsflödesalternativen och välj markerad.](../../images/tutorials/create-schema/create-a-schema-dialog.png)

### Manuell eller ML-assisterad schemagenerering {#manual-or-assisted}

Mer information om hur du kan använda en ML-algoritm för att rekommendera en schemastruktur baserad på en csv-fil finns i [handboken ](../ml-assisted-schema-creation.md) som hjälper dig att skapa scheman. Den här användargränssnittshandboken fokuserar på det manuella arbetsflödet.

### Manuell schemagenerering {#manual-creation}

Arbetsflödet [!UICONTROL Create schema] visas. Du kan välja en basklass för schemat genom att välja antingen **[!UICONTROL Individual Profile]**, **[!UICONTROL Experience Event]** eller **[!UICONTROL Other]** följt av **[!UICONTROL Next]** för att bekräfta ditt val. Mer information om de här klasserna finns i dokumentationen för [[!UICONTROL XDM individual profile]](../../classes/individual-profile.md) och [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md).

![Arbetsflödet [!UICONTROL Create schema] med tre klassalternativ och [!UICONTROL Next] markerat.](../../images/ui/resources/schemas/schema-class-options.png)

När du har valt en klass visas avsnittet [!UICONTROL Name and review]. I det här avsnittet anger du ett namn och en beskrivning som identifierar ditt schema. &#x200B;Schemats grundstruktur (tillhandahålls av klassen) visas på arbetsytan så att du kan granska och verifiera den valda klassen och schemastrukturen.

Ange en [!UICONTROL Schema display name] som är användarvänlig i textfältet. Ange sedan en lämplig beskrivning för att identifiera schemat. När du har granskat din schemastruktur och är nöjd med dina inställningar väljer du **[!UICONTROL Finish]** för att skapa ditt schema.

![Avsnittet [!UICONTROL Name and review] i arbetsflödet [!UICONTROL Create schema] med [!UICONTROL Schema display name], [!UICONTROL Description] och [!UICONTROL Finish] markerade.](../../images/ui/resources/schemas/name-and-review.png)

Fliken [!UICONTROL Schema] [!UICONTROL Browse] visas. Ditt nyligen skapade schema visas nu i schemabiblioteket och kan redigeras i [!DNL Schema Editor].

![Fliken Bläddra på arbetsytan Scheman som visar det schema som du nyligen har skapat.](../../images/ui/resources/schemas/example-schema.png)

## Redigera ett befintligt schema {#edit}

>[!NOTE]
>
>När ett schema har sparats och använts vid datainmatning kan endast additiva ändringar göras. Mer information finns i [reglerna för schemautveckling](../../schema/composition.md#evolution).

Om du vill redigera ett befintligt schema väljer du fliken **[!UICONTROL Browse]** och markerar sedan namnet på schemat som du vill redigera. Du kan även använda sökfältet för att begränsa listan med tillgängliga alternativ.

![Schemaarbetsytan med ett schema markerat.](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Du kan använda arbetsytans sök- och filtreringsfunktioner för att enklare hitta schemat. Mer information finns i guiden [Utforska XDM-resurser](../explore.md).

När du har valt ett schema visas [!DNL Schema Editor] med schemats struktur på arbetsytan. Du kan nu [lägga till fältgrupper](#add-field-groups) i schemat (eller [lägga till enskilda fält](#add-individual-fields) från dessa grupper), [redigera fältvisningsnamn](#display-names) eller [redigera befintliga anpassade fältgrupper](./field-groups.md#edit) om schemat använder några.

## Fler åtgärder {#more}

I Schemaredigeraren kan du även utföra snabba åtgärder för att kopiera JSON-strukturen för schemat eller ta bort schemat om det inte har aktiverats för kundprofilen i realtid eller har associerade datauppsättningar. Välj [!UICONTROL More] högst upp i vyn om du vill visa en listruta med snabbåtgärder.

Med strukturfunktionen Kopiera JSON kan du se hur en exempelnyttolast skulle se ut när du fortfarande skapar schemat och dina dataledningar. Det är särskilt användbart i situationer där det finns komplexa objektmappningsstrukturer i schemat, till exempel en identitetskarta.

![Schemaredigeraren med knappen Mer markerad och de nedrullningsbara alternativen visas.](../../images/tutorials/create-schema/more-actions.png)

## Växla visningsnamn {#display-name-toggle}

För enkelhetens skull kan du växla mellan de ursprungliga fältnamnen och de mer läsbara visningsnamnen i Schemaredigeraren. Tack vare den här flexibiliteten blir det enklare att hitta och redigera dina scheman. Växlingsknappen finns längst upp till höger i vyn Schemaredigeraren.

>[!NOTE]
>
>Ändringen från fältnamn till visningsnamn är helt kosmetisk och påverkar inte längre några resurser längre fram i kedjan.

![Schemaredigeraren med [!UICONTROL Show display names for fields] markerat.](../../images/ui/resources/schemas/display-name-toggle.png)

Visningsnamnen för standardfältgrupper genereras av systemet men kan anpassas enligt beskrivningen i avsnittet [visningsnamn](#display-names). Visningsnamn visas i flera olika gränssnittsvyer, inklusive mappning och förhandsvisningar av datauppsättningar. Standardinställningen är inaktiverad och fältnamnen visas med sina ursprungliga värden.

## Lägga till fältgrupper i ett schema {#add-field-groups}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du lägger till befintliga fältgrupper i ett schema. Om du vill skapa en ny anpassad fältgrupp läser du i handboken [Skapa och redigera fältgrupper](./field-groups.md#create) i stället.

När du har öppnat ett schema i [!DNL Schema Editor] kan du lägga till fält i schemat med hjälp av fältgrupper. Börja genom att välja **[!UICONTROL Add]** bredvid **[!UICONTROL Field groups]** i den vänstra listen.

![Schemaredigeraren med [!UICONTROL Add] från avsnittet [!UICONTROL Field groups] markerat.](../../images/ui/resources/schemas/add-field-group-button.png)

En dialogruta visas med en lista över fältgrupper som du kan välja för schemat. Eftersom fältgrupper endast är kompatibla med en klass, visas endast de fältgrupper som är associerade med schemats valda klass. Som standard sorteras listade fältgrupper baserat på hur populära de är i din organisation.

![Dialogrutan [!UICONTROL Add field groups] är markerad med kolumnen [!UICONTROL Popularity] markerad.](../../images/ui/resources/schemas/field-group-popularity.png)

Om du känner till den allmänna aktiviteten eller affärsområdet för de fält som du vill lägga till, väljer du en eller flera av de branschlodräta kategorierna i den vänstra listen för att filtrera den visade listan med fältgrupper.

![Dialogrutan [!UICONTROL Add field groups] är markerad med filtren [!UICONTROL Industry] och kolumnen [!UICONTROL Industry] markerad.](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Mer information om de effektivaste strategierna för branschspecifik datamodellering i XDM finns i dokumentationen om [branschdatamodeller](../../schema/industries/overview.md).

Du kan också använda sökfältet för att hitta den fältgrupp du vill använda. Fältgrupper vars namn matchar frågan visas högst upp i listan. Under **[!UICONTROL Standard Fields]** visas fältgrupper som innehåller fält som beskriver önskade dataattribut.

![Dialogrutan [!UICONTROL Add field groups] med sökfunktionen [!UICONTROL Standard fields] markerad.](../../images/ui/resources/schemas/field-group-search.png)

Markera kryssrutan bredvid namnet på den fältgrupp som du vill lägga till i schemat. Du kan markera flera fältgrupper i listan, där varje markerad fältgrupp visas i den högra listen.

![Dialogrutan [!UICONTROL Add field groups] med markeringsfunktionen för kryssrutor markerad.](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>För alla fältgrupper i listan kan du hovra eller fokusera på informationsikonen (![informationsikonen](/help/images/icons/info.png)) om du vill visa en kort beskrivning av den typ av data som fältgruppen hämtar. Du kan också markera förhandsvisningsikonen (![förhandsgranskningsikonen](/help/images/icons/preview.png)) för att visa strukturen för fälten som fältgruppen tillhandahåller innan du bestämmer dig för att lägga till den i schemat.

När du har valt fältgrupper väljer du **[!UICONTROL Add field groups]** för att lägga till dem i schemat.

![Dialogrutan [!UICONTROL Add field groups] med fältgrupper markerade och markerade [!UICONTROL Add field groups].](../../images/ui/resources/schemas/add-field-group-finish.png)

[!DNL Schema Editor] visas igen med fältgruppstillhandahållna fält som visas på arbetsytan.

![[!DNL Schema Editor] med ett exempelschema visas.](../../images/ui/resources/schemas/field-groups-added.png)

>[!NOTE]
>
>I Schemaredigeraren visas standardklasser (som genererats av Adobe) och fältgrupper med hänglåsikonen (![En hänglåsikon.](/help/images/icons/lock-closed.png). hänglåset visas i den vänstra listen bredvid namnet på klassen eller fältgruppen, samt intill ett fält i schemagrafiken som är en del av en systemgenererad resurs.
>
>![Schemaredigeraren med hänglåsikonen markerad](../../images/ui/explore/schema-editor-padlock-icon.png)

När du har lagt till en fältgrupp i ett schema kan du [ta bort befintliga fält](#remove-fields) eller [lägga till nya anpassade fält](#add-fields) i dessa grupper, beroende på dina behov.

### Ta bort fält som lagts till från fältgrupper {#remove-fields}

När du har lagt till en fältgrupp i ett schema kan du ta bort fält som du inte behöver.

>[!NOTE]
>
>Om du tar bort fält från en fältgrupp påverkas bara schemat som du arbetar med och påverkar inte själva fältgruppen. Om du tar bort fält i ett schema är dessa fält fortfarande tillgängliga i alla andra scheman som använder samma fältgrupp.

I följande exempel har standardfältgruppen **[!UICONTROL Demographic Details]** lagts till i ett schema. Om du vill ta bort ett enskilt fält, till exempel `taxId`, markerar du fältet på arbetsytan och väljer sedan **[!UICONTROL Remove]** i den högra listen.

![[!DNL Schema Editor] med [!UICONTROL Remove] markerat. Den här åtgärden tar bort ett enskilt fält.](../../images/ui/resources/schemas/remove-single-field.png)

Om det finns flera fält som du vill ta bort kan du hantera fältgruppen som helhet. Markera ett fält som tillhör gruppen på arbetsytan och välj sedan **[!UICONTROL Manage related fields]** i den högra listen.

![[!DNL Schema Editor] med [!UICONTROL Manage related fields] markerat.](../../images/ui/resources/schemas/manage-related-fields.png)

En dialogruta visas med strukturen för fältgruppen i fråga. Härifrån kan du använda de angivna kryssrutorna för att markera eller avmarkera de fält som du behöver. Välj **[!UICONTROL Confirm]** när du är nöjd.

![Dialogrutan [!UICONTROL Manage related fields] med markerade fält och [!UICONTROL Confirm] markerat.](../../images/ui/resources/schemas/select-fields.png)

Arbetsytan visas igen med endast de markerade fälten i schemastrukturen.

![Fält har lagts till](../../images/ui/resources/schemas/fields-added.png)

### Lägg till anpassade fält i fältgrupper {#add-fields}

När du har lagt till en fältgrupp i ett schema kan du definiera ytterligare fält för den gruppen. Alla fält som läggs till i en fältgrupp i ett schema visas emellertid också i alla andra scheman som använder samma fältgrupp.

Om ett anpassat fält dessutom läggs till i en standardfältgrupp, kommer den fältgruppen att konverteras till en anpassad fältgrupp och den ursprungliga standardfältgruppen kommer inte längre att vara tillgänglig.

Om du vill lägga till ett anpassat fält i en standardfältgrupp finns mer information i avsnittet [nedan](#custom-fields-for-standard-groups). Om du lägger till fält i en anpassad fältgrupp, se avsnittet [Redigera anpassade fältgrupper](./field-groups.md) i gränssnittshandboken för fältgrupper.

Om du inte vill ändra någon befintlig fältgrupp kan du [skapa en ny anpassad fältgrupp](./field-groups.md#create) och definiera ytterligare fält i stället.

## Lägga till enskilda fält i ett schema {#add-individual-fields}

Med Schemaredigeraren kan du lägga till enskilda fält direkt i ett schema om du inte vill lägga till en hel fältgrupp för ett visst användningsfall. Du kan [lägga till enskilda fält från standardfältgrupper](#add-standard-fields) eller [lägga till egna anpassade fält](#add-custom-fields) i stället.

>[!IMPORTANT]
>
>Även om schemaredigeraren tillåter att du lägger till enskilda fält direkt i ett schema, ändrar detta inte det faktum att alla fält i ett XDM-schema måste anges av dess klass eller en fältgrupp som är kompatibel med den klassen. Som framgår av avsnitten nedan är alla enskilda fält fortfarande kopplade till en klass eller fältgrupp som ett nyckelsteg när de läggs till i ett schema.

### Lägg till standardfält {#add-standard-fields}

Du kan lägga till fält från standardfältgrupper direkt i ett schema utan att först behöva känna till deras motsvarande fältgrupp. Om du vill lägga till ett standardfält i ett schema väljer du plusikonen (**+**) bredvid schemats namn på arbetsytan. En **[!UICONTROL Untitled Field]**-platshållare visas i schemastrukturen och de högra uppdateringarna för att visa kontroller för att konfigurera fältet.

![Fältplatshållare](../../images/ui/resources/schemas/root-custom-field.png)

Under **[!UICONTROL Field name]** börjar du skriva namnet på fältet som du vill lägga till. Systemet söker automatiskt efter standardfält som matchar frågan och listar dem under **[!UICONTROL Recommended Standard Fields]**, inklusive de fältgrupper som de tillhör.

![Rekommenderade standardfält](../../images/ui/resources/schemas/standard-field-search.png)

Vissa standardfält har samma namn, men strukturen kan variera beroende på vilken fältgrupp de kommer ifrån. Om ett standardfält är kapslat i ett överordnat objekt i fältgruppsstrukturen, kommer det överordnade fältet också att inkluderas i schemat om det underordnade fältet läggs till.

Välj förhandsvisningsikonen (![Förhandsgranskningsikonen](/help/images/icons/preview.png)) bredvid ett standardfält om du vill visa strukturen för fältgruppen och förstå hur den kan kapslas. Om du vill lägga till standardfältet i schemat väljer du plusikonen (![plusikonen](/help/images/icons/add-circle.png)).

![Lägg till standardfält](../../images/ui/resources/schemas/add-standard-field.png)

Arbetsytan uppdateras för att visa det standardfält som lagts till i schemat, inklusive alla överordnade fält som är kapslade i fältgruppsstrukturen. Namnet på fältgruppen visas också under **[!UICONTROL Field groups]** i den vänstra listen. Om du vill lägga till fler fält från samma fältgrupp väljer du **[!UICONTROL Manage related fields]** i den högra listen.

![Standardfältet har lagts till](../../images/ui/resources/schemas/standard-field-added.png)

### Lägg till anpassade fält {#add-custom-fields}

På samma sätt som arbetsflödet för standardfält kan du även lägga till egna anpassade fält direkt i ett schema.

Om du vill lägga till fält på rotnivån för ett schema väljer du plusikonen (**+**) bredvid schemats namn på arbetsytan. En **[!UICONTROL Untitled Field]**-platshållare visas i schemastrukturen och de högra uppdateringarna för att visa kontroller för att konfigurera fältet.

![Anpassat rotfält](../../images/ui/resources/schemas/root-custom-field.png)

Börja skriva in namnet på det fält som du vill lägga till så börjar systemet automatiskt att söka efter matchande standardfält. Om du vill skapa ett nytt anpassat fält i stället väljer du det översta alternativet som lagts till med **([!UICONTROL New Field])**.

![Nytt fält](../../images/ui/resources/schemas/custom-field-search.png)

När du har angett ett visningsnamn och en datatyp för fältet är nästa steg att tilldela fältet till en överordnad XDM-resurs. Om schemat använder en anpassad klass kan du välja att [lägga till fältet i den tilldelade klassen](#add-to-class) eller en [fältgrupp](#add-to-field-group) i stället. Om schemat använder en standardklass kan du bara tilldela ett anpassat fält till en fältgrupp.

#### Tilldela fältet till en anpassad fältgrupp {#add-to-field-group}

>[!NOTE]
>
>I det här avsnittet beskrivs bara hur du tilldelar fältet till en anpassad fältgrupp. Om du vill utöka en standardfältgrupp med det nya anpassade fältet i stället läser du avsnittet [Lägga till anpassade fält i standardfältgrupper](#custom-fields-for-standard-groups).

Under **[!UICONTROL Assign to]** väljer du **[!UICONTROL Field Group]**. Om schemat använder en standardklass är detta det enda tillgängliga alternativet och markeras som standard.

Sedan måste du välja en fältgrupp för det nya fältet som ska kopplas. Börja skriva in namnet på fältgruppen i den angivna textinmatningen. Om du har befintliga anpassade fältgrupper som matchar indata visas de i listrutan. Du kan också skriva ett unikt namn för att skapa en ny fältgrupp i stället.

![Välj fältgrupp](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Om du väljer en befintlig anpassad fältgrupp kommer alla andra scheman som använder den fältgruppen också att ärva det nya fältet när du har sparat ändringarna. Därför bör du bara markera en befintlig fältgrupp om du vill använda den här typen av spridning. Annars bör du välja att skapa en ny anpassad fältgrupp i stället.

När du har valt fältgruppen i listan väljer du **[!UICONTROL Apply]**.

![Använd fält](../../images/ui/resources/schemas/apply-field.png)

Det nya fältet läggs till på arbetsytan och namnges under ditt [klientorganisations-ID](../../api/getting-started.md#know-your-tenant_id) för att undvika konflikter med standard-XDM-fält. Fältgruppen som du har associerat det nya fältet med visas även under **[!UICONTROL Field groups]** i den vänstra listen.

![Klient-ID](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>Resten av fälten i den valda anpassade fältgruppen tas som standard bort från schemat. Om du vill lägga till några av dessa fält i schemat markerar du ett fält som tillhör gruppen och väljer sedan **[!UICONTROL Manage related fields]** i den högra listen.

#### Tilldela fältet till en anpassad klass {#add-to-class}

Under **[!UICONTROL Assign to]** väljer du **[!UICONTROL Class]**. Indatafältet nedan ersätts med namnet på det aktuella schemats anpassade klass, vilket anger att det nya fältet kommer att tilldelas den här klassen.

![Det [!UICONTROL Class]-alternativ som väljs för den nya fälttilldelningen.](../../images/ui/resources/schemas/assign-field-to-class.png)

Fortsätt konfigurera fältet efter behov och välj **[!UICONTROL Apply]** när du är klar.

![[!UICONTROL Apply] väljs för det nya fältet.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

Det nya fältet läggs till på arbetsytan och namnges under ditt [klientorganisations-ID](../../api/getting-started.md#know-your-tenant_id) för att undvika konflikter med standard-XDM-fält. Om du väljer klassnamnet i den vänstra listen visas det nya fältet som en del av klassens struktur.

![Det nya fältet som används i den anpassade klassens struktur, som visas på arbetsytan.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### Lägga till anpassade fält i strukturen för standardfältgrupper {#custom-fields-for-standard-groups}

Om schemat du arbetar med har ett objekttypsfält från en standardfältgrupp, kan du lägga till egna anpassade fält till det standardobjektet.

>[!WARNING]
>
>Alla fält som läggs till i en fältgrupp i ett schema visas också i alla andra scheman som använder samma fältgrupp. Om ett anpassat fält dessutom läggs till i en standardfältgrupp, kommer den fältgruppen att konverteras till en anpassad fältgrupp och den ursprungliga standardfältgruppen kommer inte längre att vara tillgänglig.
>
>Om du deltar i betaversionen av den här funktionen får du en dialogruta som informerar dig om vilka standardfältgrupper du tidigare har anpassat. När du har valt **[!UICONTROL Acknowledge]** konverteras resurserna i listan till anpassade fältgrupper.
>
>![Bekräftelsedialogruta för konvertering av standardfältgrupper](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Börja med att markera plusikonen (**+**) bredvid roten för objektet som tillhandahålls av standardfältgruppen.

![Lägg till fält i standardobjekt](../../images/ui/resources/schemas/add-field-to-standard-object.png)

Ett varningsmeddelande visas som uppmanar dig att bekräfta om du vill konvertera standardfältgruppen. Välj **[!UICONTROL Continue creating field group]** om du vill fortsätta.

![Bekräfta konvertering av fältgrupp](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

Arbetsytan visas igen med en namnlös platshållare för det nya fältet. Observera att namnet på standardfältgruppen har lagts till med &quot;([!UICONTROL Extended])&quot; för att ange att den har ändrats från den ursprungliga versionen. Använd kontrollerna i den högra listen för att definiera fältets egenskaper.

![Fältet har lagts till i standardobjektet](../../images/ui/resources/schemas/standard-field-group-converted.png)

När du har gjort ändringarna visas det nya fältet under ditt innehavar-ID-namnutrymme i standardobjektet. Det här kapslade namnutrymmet förhindrar konflikter mellan fält och namn inom själva fältgruppen för att undvika att bryta ändringar i andra scheman som använder samma fältgrupp.

![Fältet har lagts till i standardobjektet](../../images/ui/resources/schemas/added-to-standard-object.png)

## Aktivera ett schema för kundprofil i realtid {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Aktivera ett schema för profil"
>abstract="När ett schema har aktiverats för profilen, deltar alla datauppsättningar som skapats från det här schemat i kundprofilen i realtid, som sammanfogar data från olika källor för att skapa en fullständig bild av varje kund. När ett schema används för att importera data till profilen kan det inte inaktiveras. Mer information finns i dokumentationen."

[Kundprofil i realtid](../../../profile/home.md) sammanfogar data från olika källor för att skapa en fullständig bild av varje enskild kund. Om du vill att data som har hämtats av ett schema ska kunna delta i den här processen måste du aktivera schemat för användning i [!DNL Profile].

>[!IMPORTANT]
>
>Om du vill aktivera ett schema för [!DNL Profile] måste ett primärt identitetsfält ha definierats. Mer information finns i handboken [Definiera identitetsfält](../fields/identity.md).

Om du vill aktivera schemat börjar du med att markera schemats namn i den vänstra listen och väljer sedan alternativet **[!UICONTROL Profile]** i den högra listen.

![](../../images/ui/resources/schemas/profile-toggle.png)

En pover visas som varnar om att när ett schema väl har aktiverats och sparats kan det inte inaktiveras. Välj **[!UICONTROL Enable]** om du vill fortsätta.

![](../../images/ui/resources/schemas/profile-confirm.png)

Arbetsytan visas igen när växlingen [!UICONTROL Profile] är aktiverad.

>[!IMPORTANT]
>
>Eftersom schemat inte har sparats ännu är detta inget returtecken om du ändrar dig angående att låta schemat delta i kundprofilen i realtid: när du har sparat ett aktiverat schema kan det inte längre inaktiveras. Välj **[!UICONTROL Profile]**-växeln igen för att inaktivera schemat.

Om du vill slutföra processen väljer du **[!UICONTROL Save]** för att spara schemat.

![](../../images/ui/resources/schemas/profile-enabled.png)

Schemat är nu aktiverat för användning i kundprofilen i realtid. När Platform samlar in data i datauppsättningar som baseras på det här schemat, kommer dessa data att införlivas i dina sammanställda profildata.

## Redigera visningsnamn för schemafält {#display-names}

När du har tilldelat en klass och lagt till fältgrupper till ett schema kan du redigera visningsnamnen för alla fält i schemat, oavsett om dessa fält har tillhandahållits av standard eller anpassade XDM-resurser.

>[!NOTE]
>
>Tänk på att visningsnamnen för fält som tillhör standardklasser eller fältgrupper bara kan redigeras i ett specifikt schema. Om du ändrar visningsnamnet för ett standardfält i ett schema påverkas alltså inte andra scheman som använder samma associerade klass eller fältgrupp.
>
>När du ändrar visningsnamnen för ett schemas fält återspeglas dessa ändringar omedelbart i befintliga datauppsättningar som baseras på det schemat.

Om du vill redigera visningsnamnet för ett schemafält markerar du fältet på arbetsytan. Ange det nya namnet under **[!UICONTROL Display name]** i den högra listen.

![](../../images/ui/resources/schemas/display-name.png)

Välj **[!UICONTROL Apply]** i den högra listen så uppdateras arbetsytan till att visa fältets nya visningsnamn. Välj **[!UICONTROL Save]** om du vill använda ändringarna i schemat.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Ändra en schemaklass {#change-class}

Du kan ändra schemaklassen när som helst under den inledande dispositionsprocessen innan schemat har sparats.

>[!WARNING]
>
>Omtilldelning av klassen för ett schema bör göras med extrem försiktighet. Fältgrupper är bara kompatibla med vissa klasser. Om du ändrar klassen återställs arbetsytan och alla fält du har lagt till.

Om du vill tilldela om en klass väljer du **[!UICONTROL Assign]** till vänster på arbetsytan.

![](../../images/ui/resources/schemas/assign-class-button.png)

En dialogruta visas med en lista över alla tillgängliga klasser, inklusive alla som definierats av din organisation (ägaren är [!UICONTROL Customer]) samt standardklasser som definierats av Adobe.

Välj en klass i listan för att visa dess beskrivning till höger i dialogrutan. Du kan också välja **[!UICONTROL Preview class structure]** om du vill visa de fält och metadata som är associerade med klassen. Välj **[!UICONTROL Assign class]** om du vill fortsätta.

![](../../images/ui/resources/schemas/assign-class.png)

En ny dialogruta öppnas där du ombeds bekräfta att du vill tilldela en ny klass. Bekräfta genom att välja **[!UICONTROL Assign]**.

![](../../images/ui/resources/schemas/assign-confirm.png)

När du har bekräftat klassändringen återställs arbetsytan och alla dispositionsförlopp går förlorade.

## Nästa steg {#next-steps}

Det här dokumentet innehåller grunderna för att skapa och redigera scheman i plattformsgränssnittet. Vi rekommenderar starkt att du går igenom självstudiekursen [för att skapa scheman](../../tutorials/create-schema-ui.md) för ett omfattande arbetsflöde för att skapa ett fullständigt schema i användargränssnittet, inklusive att skapa anpassade fältgrupper och datatyper för unika användningsfall.

Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] finns i översikten för arbetsytan [[!UICONTROL Schemas] ](../overview.md).

Mer information om hur du hanterar scheman i [!DNL Schema Registry] API finns i [schemas slutpunktshandbok](../../api/schemas.md).
