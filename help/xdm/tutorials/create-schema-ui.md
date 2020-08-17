---
keywords: Experience Platform;home;popular topics;schema;Schema;create schema;enum;XDM individual profile;primary identity;primary idenity;enum datatype;schema design
solution: Experience Platform
title: Skapa ett schema med Schemaredigeraren
topic: tutorials
description: I den här självstudiekursen beskrivs stegen för hur du skapar ett schema med Schemaredigeraren i Experience Platform.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '3183'
ht-degree: 0%

---


# Skapa ett schema med [!DNL Schema Editor]

Det [!DNL Schema Registry] innehåller ett användargränssnitt och RESTful API som du kan använda för att visa och hantera alla resurser i Adobe Experience Platform [!DNL Schema Library]. Här [!DNL Schema Library] finns resurser som Adobe, Experience Platform partners och leverantörer har gett dig tillgång till, samt resurser som du kan definiera och spara i [!DNL Schema Registry].

I den här självstudiekursen beskrivs stegen för hur du skapar ett schema med Schemaredigeraren i [!DNL Experience Platform]. Om du föredrar att skapa ett schema med API:t för schemaregister börjar du med att läsa [utvecklarhandboken](../api/getting-started.md) för schemaregistret innan du försöker [skapa ett schema med API](create-schema-api.md).

Den här självstudiekursen innehåller även steg för att [definiera en ny klass](#create-new-class) som du sedan kan använda för att skapa ett schema.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika aspekter av Adobe Experience Platform som används i schemaredigeraren. Innan du börjar med den här självstudiekursen bör du läsa om följande koncept i dokumentationen:

* [!DNL Experience Data Model (XDM)](../home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [Grundläggande om schemakomposition](../schema/composition.md): En översikt över XDM-scheman och deras byggstenar, inklusive klasser, mixins, datatyper och fält.
* [!DNL Real-time Customer Profile](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudiekursen kräver att du har tillgång till [!DNL Experience Platform]. Om du inte har tillgång till en IMS-organisation i [!DNL Experience Platform]kontaktar du systemadministratören innan du fortsätter.

## Bläddra bland befintliga scheman på arbetsytan Scheman {#browse}

På arbetsytan Scheman i [!DNL Experience Platform] finns en visualisering av [!DNL Schema Library]som gör att du kan visa och hantera alla scheman som är tillgängliga för dig, samt skapa nya. Arbetsytan innehåller även Schemaredigeraren, arbetsytan som du kommer att komponera ett schema på i hela kursen.

När du har loggat in [!DNL Experience Platform]klickar du **[!UICONTROL Schemas]** i den vänstra navigeringen så kommer du till arbetsytan Scheman. Du ser en lista med scheman (en representation av [!DNL Schema Library]) där du kan visa, hantera och anpassa alla scheman som är tillgängliga för dig. Listan innehåller namn, typ, klass och beteende (post- eller tidsserie) som schemat baseras på samt datum och tid då schemat senast ändrades.

Klicka på filterikonen bredvid sökfältet för att använda filterfunktioner för alla resurser i registret, inklusive klasser, mixins och datatyper.

![Visa schemabiblioteket](../images/tutorials/create-schema/schemas_filter.png)

## Skapa och namnge ett schema {#create}

Börja komponera ett schema genom att klicka **[!UICONTROL Create Schema]** i det övre högra hörnet på arbetsytan Scheman.

![Knappen Skapa schema](../images/tutorials/create-schema/create_schema_button.png)

Schemaredigeraren ** visas. Det här är arbetsytan som du kommer att komponera ditt schema på. När du kommer till redigeraren skapas automatiskt ett namnlöst schema i *strukturdelen* på arbetsytan så att du kan börja anpassa.

![Schemaredigerare](../images/tutorials/create-schema/schema_editor.png)

Till höger om redigeraren finns *Schemaegenskaper* där du kan ange ett namn för schemat (med hjälp av **[!UICONTROL Display Name]** fältet). När ett namn har angetts uppdateras arbetsytan med det nya namnet på schemat.

![Arbetsyta för schema](../images/tutorials/create-schema/name_schema.png)

Det finns flera viktiga saker att tänka på när du ska bestämma ett namn för schemat:

* Schemanamn ska vara korta och beskrivande så att schemat kan hittas i biblioteket senare.
* Schemanamn måste vara unika, vilket innebär att de också måste vara tillräckligt specifika för att de inte ska återanvändas i framtiden. Om din organisation till exempel har separata lojalitetsprogram för olika varumärken är det klokt att kalla ditt schema&quot;Varumärke A lojalitetsmedlemmar&quot; för att göra det enkelt att skilja på dem från andra lojalitetsrelaterade scheman som du kan definiera senare.
* Du kan också ange ytterligare information om schemat med hjälp av **[!UICONTROL Description]** fältet.

I den här självstudiekursen skapas ett schema för att importera data som är relaterade till medlemmarna i ett lojalitetsprogram, och schemat kallas därför&quot;lojalitetsmedlemmar&quot;.

## Tilldela en klass {#class}

Till vänster om redigeraren finns delen *Disposition* . Den innehåller för närvarande två underavsnitt: *[!UICONTROL Schema]* och *[!UICONTROL Class]*.

Nu när schemat har ett namn är det dags att tilldela klassen som schemat ska implementera. Click **[!UICONTROL Assign]** next to *[!UICONTROL Class]*.

![](../images/tutorials/create-schema/assign_class_button.png)

Dialogrutan *[!UICONTROL Assign Class]* visas. I det här fönstret visas en lista med alla tillgängliga klasser, inklusive alla som definierats av din organisation (ägaren är&quot;kund&quot;) samt standardklasser som definierats av Adobe.

Klicka på klassnamnet för att visa beskrivningen av klassen. Du kan också välja **[!UICONTROL Preview Class Structure]** att visa de fält och metadata som är associerade med klassen.

I den här självstudien används [!DNL XDM Individual Profile] klassen. Klicka på alternativknappen bredvid klassen för att markera den och klicka sedan på **[!UICONTROL Assign Class]**.

![Dialogrutan Tilldela klass](../images/tutorials/create-schema/assign_class.png)

Arbetsytan visas igen. Avsnittet *[!UICONTROL Class]* innehåller nu den klass du valde ([!DNL XDM Individual Profile]) och fälten som klassen bidragit med är nu synliga i [!DNL XDM Individual Profile] *[!UICONTROL Structure]* avsnittet.

![Tilldelad klass för enskild XDM-profil](../images/tutorials/create-schema/class_assigned_structure.png)

Fälten visas i formatet &quot;fieldName | Datatyp&quot;. Steg för att definiera schemafält i användargränssnittet finns senare i den här självstudiekursen.

>[!NOTE]
>
>Du kan [ändra schemaklassen](#change-class) när som helst under den inledande dispositionsprocessen innan schemat har sparats, men detta bör göras med yttersta försiktighet. Blandningar är bara kompatibla med vissa klasser. Om du ändrar klassen återställs arbetsytan och alla fält du har lagt till.

## Lägga till en blandning {#mixin}

Nu när en klass har tilldelats innehåller *dispositionssektionen* ett tredje underavsnitt: *[!UICONTROL Mixins]*.

Nu kan du börja lägga till fält i ditt schema genom att lägga till mixar. En blandning är en grupp med ett eller flera fält som beskriver ett visst koncept. I den här självstudiekursen används mixins för att beskriva medlemmarna i bonusprogrammet och samla in viktig information som namn, födelsedag, telefonnummer, adress med mera.

Om du vill lägga till en blandning klickar du på **Lägg till** i underavsnittet *Blandningar* .

![](../images/tutorials/create-schema/add_mixin_button.png)

Dialogrutan *[!UICONTROL Add Mixin]* visas. Mixer är bara avsedda att användas med specifika klasser, och därför visas bara de som är kompatibla med den klass du valde (i det här fallet [!DNL XDM Individual Profile] klassen) i listan över blandningar.

Om du markerar alternativknappen bredvid en mixin kan du välja att **[!UICONTROL Preview Mixin Structure]**. Välj&quot;Profilpersonsinformation&quot; och klicka sedan på **[!UICONTROL Add Mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Arbetsytan för schemat visas igen. I *[!UICONTROL Mixins]* avsnittet visas nu&quot;[!UICONTROL Profile Person Details]&quot;-blandningen och i avsnittet finns de fält som har bidragit med blandningen *[!UICONTROL Structure]* .

![](../images/tutorials/create-schema/person_details_structure.png)

Den här blandningen bidrar med flera fält under namnet&quot;person&quot; på den översta nivån med datatypen&quot;person&quot;. Den här gruppen med fält beskriver information om en individ, inklusive namn, födelsedatum och kön.

>[!NOTE]
>
>Kom ihåg att fält kan använda skalära typer (till exempel sträng, heltal, matris eller datum) som datatyp, liksom alla&quot;datatyper&quot; (en grupp fält som representerar ett gemensamt koncept) i [!DNL Schema Registry].

Observera att&quot;[!UICONTROL name]&quot;-fältet har datatypen&quot;[!UICONTROL Person Name]&quot;, vilket innebär att det beskriver ett gemensamt koncept och innehåller namnrelaterade underfält som förnamn, efternamn och fullständigt namn.

Klicka på olika fält på arbetsytan för att se ytterligare fält som de bidrar till schemastrukturen.

## Lägg till ytterligare en blandning {#mixin-2}

Nu kan du upprepa samma steg för att lägga till en annan blandning. När du visar *[!UICONTROL Add Mixin]* dialogrutan den här gången kan du lägga märke till att&quot;[!UICONTROL Profile Person Details]&quot;-mixinen är nedtonad och att alternativknappen bredvid den inte kan markeras. Detta förhindrar att du av misstag duplicerar blandningar som du redan har inkluderat i det aktuella schemat.

Nu kan du lägga till&quot;[!DNL Profile Personal Details" mixin] från *[!UICONTROL Add Mixin]* dialogrutan.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

När arbetsytan har lagts till visas den igen. &quot;[!UICONTROL Profile Personal Details]&quot; visas nu under *[!UICONTROL Mixins]* i *[!UICONTROL Composition]* avsnittet, och fält för hemadress, mobiltelefon med mera har lagts till under *[!UICONTROL Structure]*.

Ungefär som i fältet&quot;[!UICONTROL name]&quot; representerar de fält du just lade till koncept för flera fält. &quot;[!UICONTROL homeAddress]&quot; har till exempel datatypen &quot;[!UICONTROL Address]&quot; och &quot;[!UICONTROL mobilePhone]&quot; har datatypen &quot;[!UICONTROL Phone Number]&quot;. Du kan klicka på vart och ett av dessa fält för att expandera dem och visa de ytterligare fält som ingår i datatypen.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definiera en ny blandning {#define-mixin}

&quot;[!UICONTROL Loyalty Members]&quot;-schemat är avsett för att samla in data som är relaterade till medlemmarna i ett lojalitetsprogram, så det kräver vissa specifika lojalitetsrelaterade fält. Det finns inga standardblandningar som innehåller de nödvändiga fälten, och du måste därför definiera en ny blandning.

När du öppnar dialogrutan väljer du den här gången *[!UICONTROL Add Mixin]* **[!UICONTROL Create New Mixin]**. Du ombeds sedan ange en **[!UICONTROL Display Name]** och **[!UICONTROL Description]** en för din blandning.

![](../images/tutorials/create-schema/mixin_create_new.png)

Precis som med klassnamn ska mixnamnet vara kort och enkelt och innehålla en beskrivning av vad mixinen kommer att bidra till schemat. Även dessa är unika, så du kan inte återanvända namnet och måste därför se till att det är tillräckligt specifikt.

I den här självstudiekursen anger du den nya blandningen&quot;[!UICONTROL Loyalty Details]&quot;.

Klicka **[!UICONTROL Add Mixin]** för att återgå till schemaredigeraren. &quot;[!UICONTROL Loyalty Details]&quot; ska nu visas under *[!UICONTROL Mixins]* till vänster på arbetsytan, men det finns inga fält som är kopplade till den ännu och därför visas inga nya fält under *[!UICONTROL Structure]*.

## Lägg till fält i mixinen {#mixin-fields}

Nu när du har skapat&quot;[!UICONTROL Loyalty Details]&quot;-blandningen är det dags att definiera de fält som blandningen ska bidra till schemat.

Börja med att klicka på blandningsnamnet i *[!UICONTROL Mixins]* avsnittet. När du har gjort det visas *[!UICONTROL Mixin Properties]* den till höger om redigeraren och en **[!UICONTROL Add Field]** knapp visas bredvid namnet på schemat under *[!UICONTROL Structure]*.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Klicka **[!UICONTROL Add Field]** bredvid&quot;[!UICONTROL Loyalty Members]&quot; för att skapa en ny nod i strukturen. Den här noden (kallas &quot;_tenantId&quot; i det här exemplet) representerar din IMS-organisations klient-ID, föregånget av ett understreck. Närvaron av innehavar-ID anger att fälten som du lägger till finns i organisationens namnutrymme.

Fälten som du lägger till är alltså unika för din organisation och kommer att sparas i [!DNL Schema Registry] i ett specifikt område som bara är tillgängligt för din IMS-organisation. Fält som du definierar måste alltid läggas till i namnutrymmet för att förhindra kollisioner med namn från andra standardklasser, mixins, datatyper och fält.

I den namngivna noden finns ett &quot;[!UICONTROL New Field]&quot;. Detta är början på &quot;[!UICONTROL Loyalty Details]&quot;-mixinen.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Börja med att skapa ett &quot; *[!UICONTROL Field Properties]* &quot;-fält med typen &quot;[!UICONTROL loyalty]&quot; som ska användas för dina lojalitetsrelaterade fält[!UICONTROL Object]till höger om redigeraren. Klicka på **[!UICONTROL Apply]** när du är klar.

![](../images/tutorials/create-schema/loyalty_object.png)

Ändringarna tillämpas och det nyskapade&quot;[!UICONTROL loyalty]&quot; objektet visas. Klicka **[!UICONTROL Add Field]** bredvid objektet för att lägga till fler lojalitetsrelaterade fält. Ett nytt fält visas och avsnittet visas till höger på arbetsytan *[!UICONTROL Field Properties]* .

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Varje fält kräver följande information:

* **[!UICONTROL Field Name]:** Fältets namn, skrivet i kameraläge. Exempel: loyaltyLevel
* **[!UICONTROL Display Name]:** Fältets namn, skrivet i versaler. Exempel: Lojalitetsnivå
* **[!UICONTROL Type]:** Fältets datatyp. Detta inkluderar grundläggande skalära typer och alla datatyper som definieras i [!DNL Schema Registry]. Exempel: sträng, heltal, boolesk, person, adress, telefonnummer osv.
* **[!UICONTROL Description]:** En valfri beskrivning av fältet ska inkluderas, skriven i inledande mening. (Högst 200 tecken)

Det första fältet för Loyalty-objektet blir en sträng med namnet &quot;[!UICONTROL loyaltyId]&quot;. När du ställer in det nya fältets typ till &quot;[!UICONTROL String]&quot; fylls *[!UICONTROL Field Properties]* fönstret i med flera alternativ för att tillämpa begränsningar, inklusive **[!UICONTROL Default Value]**, **[!UICONTROL Format]** och **[!UICONTROL Maximum Length]**.

![](../images/tutorials/create-schema/string_constraints.png)

Olika begränsningsalternativ är tillgängliga beroende på vilken datatyp som har valts. Eftersom&quot;[!UICONTROL loyaltyId]&quot; blir en e-postadress väljer du&quot;[!UICONTROL email]&quot; i **[!UICONTROL Format]** listrutan. Välj **[!UICONTROL Apply]** om du vill använda ändringarna.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Lägg till fler fält som ska blandas {#mixin-fields-2}

Nu när du har lagt till fältet&quot;[!UICONTROL loyaltyId]&quot; kan du lägga till ytterligare fält för att hämta lojalitetsrelaterad information som:

* Punkter (heltal)
* Medlem sedan (datum)

Varje fält läggs till genom att klicka **[!UICONTROL Add Field]** på förmånsobjektet och fylla i den obligatoriska informationen.

När det är klart innehåller Loyalty-objektet fält för: Förmåns-ID, poäng och Medlem sedan.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Lägg till enum-fält som ska blandas {#enum}

När du definierar fält i Schemaredigeraren finns det ytterligare alternativ som du kan använda för grundläggande fälttyper för att tillhandahålla ytterligare begränsningar för de data som fältet kan innehålla.

Ett exempel på detta är ett&quot;[!UICONTROL Loyalty Level]&quot;-fält där värdet bara kan vara ett av fyra möjliga alternativ. Om du vill lägga till det här fältet i schemat klickar du **[!UICONTROL Add Field]** bredvid&quot;[!UICONTROL loyalty]&quot;-objektet och fyller i de obligatoriska fälten under *[!UICONTROL Field Properties]*.

Välj **[!UICONTROL Type]** String så visas ytterligare kryssrutor för **[!UICONTROL Array]**, **[!UICONTROL Enum]** och **[!UICONTROL Identity]**.

Markera **[!UICONTROL Enum]** kryssrutan för att öppna *[!UICONTROL Enum Values]* avsnittet nedan. Här kan du ange **[!UICONTROL Value]** (i camelCase) och **[!UICONTROL Label]** (ett valfritt, läsvänligt namn i Title Case) för varje godtagbar lojalitetsnivå.

När du har slutfört alla fältegenskaper klickar du på **[!UICONTROL Apply]** och&quot;[!UICONTROL loyaltyLevel]&quot;-fältet läggs till i objektet &quot;loyalty&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

Mer information om tillgängliga ytterligare begränsningar:

* **[!UICONTROL Required]:** Anger att fältet är obligatoriskt för datainmatning. Alla data som överförs till en datauppsättning som baseras på det här schemat och som inte innehåller det här fältet kommer att misslyckas vid inmatning.
* **[!UICONTROL Array]:** Anger att fältet innehåller en array med värden, var och en med den angivna datatypen. Om du t.ex. markerar datatypen String och kryssrutan Array betyder det att fältet kommer att innehålla en array med strängar.
* **[!UICONTROL Enum]:** Anger att det här fältet måste innehålla ett av värdena från en numrerad lista med möjliga värden.
* **[!UICONTROL Identity]:** Anger att det här fältet är ett identitetsfält. Mer information om identitetsfält finns [senare i den här självstudiekursen](#identity-field).

## Konvertera ett flerfältsobjekt till en datatyp {#datatype}

När du har lagt till flera lojalitetsspecifika fält innehåller objektet&quot;[!UICONTROL loyalty]&quot; nu en gemensam datastruktur som kan vara användbar i andra scheman.

När du känner att en struktur med flera fält kan återanvändas, och du vill ha flexibiliteten att använda samma datastruktur någon annanstans, kan du konvertera strukturen till en datatyp med Schemaredigeraren.

Datatyper möjliggör konsekvent användning av flerfältsstrukturer och ger större flexibilitet än en blandning eftersom de kan användas var som helst inom ett schema. Detta görs genom att ställa in fältets storlek **[!UICONTROL Type]** i en blandning till datatypen i registret.

Om du vill konvertera&quot;[!UICONTROL loyalty]&quot;-objektet till en datatyp klickar du på fältet&quot;lojalitet&quot; under *[!UICONTROL Structure]* och väljer **[!UICONTROL Convert to New Data Type]** till höger om redigeraren under *[!UICONTROL Field Properties]*. Ett litet grönt popup-fönster visas som bekräftar &quot;[!UICONTROL Object Converted to Data Type]&quot;.

När du nu tittar under *[!UICONTROL Structure]* ser du att datatypen&quot;[!UICONTROL loyalty]&quot; finns i fältet&quot;[!UICONTROL Loyalty]&quot; och att fälten har små låsikoner bredvid sig som anger att de inte längre är enskilda fält, utan snarare är en del av en struktur med flera fält.

I ett framtida schema kan du nu tilldela ett fält **[!UICONTROL Type]** av typen &quot;[!UICONTROL Loyalty]&quot; och då inkluderas automatiskt fälten för lojalitetsnivå, poäng, Medlem sedan och Förmåns-ID.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## Ange ett schemafält som identitetsfält {#identity-field}

Scheman används för inmatning av data i [!DNL Experience Platform]och dessa data används i slutändan för att identifiera individer och sammanfoga information från flera källor. Nyckelfält kan markeras som&quot;[!UICONTROL Identity]&quot; för att underlätta med den här processen.

[!DNL Experience Platform] gör det enkelt att ange ett identitetsfält med hjälp av en **[!UICONTROL Identity]** kryssruta i [!DNL Schema Editor].

Det kan till exempel finnas tusentals medlemmar i bonusprogrammet som tillhör samma&quot;nivå&quot;, men varje medlem i bonusprogrammet har ett unikt&quot;lojalitetsId&quot; (som i det här fallet är den enskilda medlemmens e-postadress). Det faktum att &quot;loyaltyId&quot; är en unik identifierare för varje medlem gör det till en bra kandidat för ett identitetsfält, medan &quot;level&quot; inte är det.

I redigerarens *[!UICONTROL Structure]* avsnitt klickar du på fältet &quot;[!UICONTROL loyaltyId]&quot; som du skapade och du ser **[!UICONTROL Identity]** kryssrutan under *[!UICONTROL Field Properties]*. Markera rutan så kan du välja att ange den som **[!UICONTROL Primary Identity]**. Markera även den rutan.

Sedan måste du ange en **[!UICONTROL Identity Namepsace]**. Det finns flera fördefinierade namnutrymmen, men eftersom&quot;[!UICONTROL loyaltyId]&quot; är medlemmens e-postadress väljer du&quot;E-post&quot; i listrutan. Du kan nu klicka **[!UICONTROL Apply]** för att bekräfta uppdateringarna av fältet&quot;[!UICONTROL loyaltyId]&quot;.

Nu kommer alla data som hämtas in i&quot;[!UICONTROL loyaltyId]&quot;-fältet att användas för att identifiera den personen och sammanfoga en enda bild av kunden.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>När ett schemafält har angetts som primär identitet får du ett felmeddelande om du senare försöker ange ett annat fält i schemat som primärt. Varje schema får endast innehålla ett primärt identitetsfält.

Läs mer om hur du arbetar med identiteter i [!DNL Identity Service](../../identity-service/home.md) dokumentationen.

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## Aktivera schemat för användning i [!DNL Real-time Customer Profile] {#profile}

Schemaredigeraren gör det möjligt att aktivera ett schema för användning med [!DNL Real-time Customer Profile](../../profile/home.md). [!DNL Profile] ger en helhetsbild av varje enskild kund genom att skapa en robust, 360-gradig profil med kundattribut samt en tidsstämplad redovisning av varje interaktion som kunden har haft i alla system som är integrerade med [!DNL Experience Platform].

För att ett schema ska kunna aktiveras för användning med [!DNL Real-time Customer Profile]måste en primär identitet ha definierats. Du får felmeddelandet&quot;Saknad primär identitet&quot; om du försöker aktivera ett schema utan att först definiera en primär identitet.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Om du vill aktivera schemat &quot;Förmånsmedlemmar&quot; för användning i [!DNL Profile]börjar du med att klicka på &quot;Förmånsmedlemmar&quot; i *strukturdelen* i redigeraren.

Till höger om redigeraren visas information om schemat, inklusive visningsnamn, beskrivning och typ, under *Schemaegenskaper*. Förutom den här informationen finns det en växlingsknapp **[!UICONTROL Profile]**.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

Klicka **[!UICONTROL Profile]** så visas ett popup-fönster där du ombeds bekräfta att du vill aktivera schemat för [!DNL Profile].

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>När ett schema har aktiverats för [!DNL Real-time Customer Profile] och sparats kan det inte inaktiveras.

## Nästa steg och ytterligare resurser

Nu när du har skapat ett&quot;[!UICONTROL Loyalty Members]&quot;-schema kan du se hela schemat i *strukturdelen* i redigeraren. Klicka **[!UICONTROL Save]** så sparas schemat i [!DNL Schema Library]och blir tillgängligt för [!DNL Schema Registry]användaren.

Ditt nya schema kan nu användas för att importera data till [!DNL Platform]. Kom ihåg att när schemat väl har använts för att importera data får endast additiva ändringar göras. Mer information om schemaversion finns i [grunderna för schemakomposition](../schema/composition.md) .

&quot;[!UICONTROL Loyalty Members]&quot;-schemat är också tillgängligt för att visas och hanteras med [!DNL Schema Registry] -API:t. Börja med att läsa utvecklarhandboken [för](../api/getting-started.md)schematabellens API när du vill börja arbeta med API:t.

>[!WARNING]
>
>Gränssnittet [!DNL Platform] som visas i följande videofilmer är inaktuellt. Läs dokumentationen ovan för de senaste skärmbilderna och funktionerna i användargränssnittet.

I följande video visas hur du skapar ett enkelt schema i [!DNL Platform] användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

Följande video är tänkt att förstärka din förståelse för att arbeta med mixiner och klasser.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Bilaga

Följande information finns som komplement till självstudiekursen för Schemaredigeraren.

### Skapa en ny klass {#create-new-class}

[!DNL Experience Platform] ger flexibilitet att definiera ett schema baserat på en klass som är unik för din organisation.

Öppna *[!UICONTROL Assign Class]* dialogrutan genom att klicka **[!UICONTROL Assign]** i *[!UICONTROL Class]* avsnittet Schemaredigeraren. Välj **C[!UICONTROL reate New Class]** i dialogrutan.

Du kan sedan ge den nya klassen ett **[!UICONTROL Display Name]** (kort, beskrivande, unikt och användarvänligt namn för klassen), ett **[!UICONTROL Description]** och ett **[!UICONTROL Behavior]** (&quot;[!UICONTROL Record]&quot; eller&quot;[!UICONTROL Time Series]&quot;) för de data som schemat ska definiera.

![Ny klassinformation](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>När du skapar ett schema som implementerar en klass som definierats av din organisation, måste du komma ihåg att mixar bara är tillgängliga för användning med kompatibla klasser. Eftersom den klass du definierade är ny finns det inga kompatibla blandningar i listan i dialogrutan *Lägg till mixning* . Du måste i stället markera **[!UICONTROL Create New Mixin]** och definiera en blandning som ska användas med den klassen. Nästa gång du skapar ett schema som implementerar den nya klassen, kommer den mixin som du definierade att listas och vara tillgänglig för användning.

### Ändra klassen för ett schema {#change-class}

Du kan när som helst under den inledande schemakompositionsprocessen, innan schemat sparas, ändra den klass som schemat baseras på.

>[!WARNING]
>
>Var försiktig innan du byter klass. Blandningar är bara kompatibla med vissa klasser. Om du ändrar klassen återställs arbetsytan och alla fält som du har lagt till tas bort.

Om du vill ändra klassen klickar du på **[!UICONTROL Assign]** bredvid *[!UICONTROL Class]* i *[!UICONTROL Composition]* redigerarens avsnitt.

När *[!UICONTROL Assign Class]* dialogrutan öppnas kan du välja en ny klass i listan. Klicka **[!UICONTROL Assign Class]** och en ny dialogruta öppnas där du får bekräfta att du vill tilldela en ny klass.

![Ändra klass](../images/tutorials/create-schema/assign_new_class_warning.png)

Om du bekräftar klassändringen återställs arbetsytan och alla kompositionsförlopp går förlorade.