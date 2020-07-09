---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa ett schema med Schemaredigeraren
topic: tutorials
translation-type: tm+mt
source-git-commit: d55dc9776968099901325c58506c5e322449368e
workflow-type: tm+mt
source-wordcount: '3462'
ht-degree: 0%

---


# Skapa ett schema med Schemaredigeraren

Schemaregistret innehåller ett användargränssnitt och RESTful API som du kan använda för att visa och hantera alla resurser i schemabiblioteket i Adobe Experience Platform. Schemabiblioteket innehåller resurser som gjorts tillgängliga av Adobe, Experience Platform partners och leverantörer vars program du använder, samt resurser som du definierar och sparar i schemaregistret.

I den här självstudiekursen beskrivs stegen för hur du skapar ett schema med Schemaredigeraren i Experience Platform. Om du föredrar att skapa ett schema med API:t för schemaregister börjar du med att läsa [utvecklarhandboken](../api/getting-started.md) för schemaregistret innan du försöker [skapa ett schema med API](create-schema-api.md).

Den här självstudiekursen innehåller även steg för att [definiera en ny klass](#create-new-class) som du sedan kan använda för att skapa ett schema.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika aspekter av Adobe Experience Platform som används i schemaredigeraren. Innan du börjar med den här självstudiekursen bör du läsa om följande koncept i dokumentationen:

* [Experience Data Model (XDM)](../home.md): Det standardiserade ramverk som Platform använder för att ordna kundupplevelsedata.
* [Grundläggande om schemakomposition](../schema/composition.md): En översikt över XDM-scheman och deras byggstenar, inklusive klasser, mixins, datatyper och fält.
* [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudiekursen kräver att du har tillgång till Experience Platform. Om du inte har tillgång till en IMS-organisation i Experience Platform, tala med systemadministratören innan du fortsätter.

## Bläddra bland befintliga scheman på arbetsytan Scheman {#browse}

På arbetsytan Scheman i Experience Platform finns en visualisering av schemabiblioteket som gör att du kan visa och hantera alla scheman som är tillgängliga för dig, samt skapa nya. Arbetsytan innehåller även Schemaredigeraren, arbetsytan som du kommer att komponera ett schema på i hela kursen.

När du har loggat in i Experience Platform klickar du på **Scheman** i den vänstra navigeringen så kommer du till arbetsytan Scheman. Du ser en lista med scheman (en representation av schemabiblioteket) där du kan visa, hantera och anpassa alla scheman som är tillgängliga för dig. Listan innehåller namn, typ, klass och beteende (post- eller tidsserie) som schemat baseras på samt datum och tid då schemat senast ändrades.

Klicka på filterikonen bredvid sökfältet för att använda filterfunktioner för alla resurser i registret, inklusive klasser, mixins och datatyper.

![Visa schemabiblioteket](../images/tutorials/create-schema/schemas_filter.png)

## Skapa och namnge ett schema {#create}

Om du vill börja komponera ett schema klickar du på **Skapa schema** i det övre högra hörnet på arbetsytan Scheman.

![Knappen Skapa schema](../images/tutorials/create-schema/create_schema_button.png)

Schemaredigeraren ** visas. Det här är arbetsytan som du kommer att komponera ditt schema på. När du kommer till redigeraren skapas automatiskt ett namnlöst schema i *strukturdelen* på arbetsytan så att du kan börja anpassa.

![Schemaredigerare](../images/tutorials/create-schema/schema_editor.png)

Till höger om redigeraren finns *Schemaegenskaper* där du kan ange ett namn för schemat (med hjälp av fältet **Visningsnamn** ). När ett namn har angetts uppdateras arbetsytan med det nya namnet på schemat.

![Arbetsyta för schema](../images/tutorials/create-schema/name_schema.png)

Det finns flera viktiga saker att tänka på när du ska bestämma ett namn för schemat:

* Schemanamn ska vara korta och beskrivande så att schemat kan hittas i biblioteket senare.
* Schemanamn måste vara unika, vilket innebär att de också måste vara tillräckligt specifika för att de inte ska återanvändas i framtiden. Om din organisation till exempel har separata lojalitetsprogram för olika varumärken är det klokt att kalla ditt schema&quot;Varumärke A lojalitetsmedlemmar&quot; för att göra det enkelt att skilja på dem från andra lojalitetsrelaterade scheman som du kan definiera senare.
* Du kan också ange ytterligare information om schemat med hjälp av fältet **Beskrivning** .

I den här självstudiekursen skapas ett schema för att importera data som är relaterade till medlemmarna i ett lojalitetsprogram, och schemat kallas därför&quot;lojalitetsmedlemmar&quot;.

## Tilldela en klass {#class}

Till vänster om redigeraren finns delen *Disposition* . Den innehåller för närvarande två underavsnitt: *Schema* och *klass*.

Nu när schemat har ett namn är det dags att tilldela klassen som schemat ska implementera. Klicka på **Tilldela** bredvid *Klass*.

![](../images/tutorials/create-schema/assign_class_button.png)

Dialogrutan *Tilldela klass* visas. I det här fönstret visas en lista med alla tillgängliga klasser, inklusive alla som definierats av din organisation (ägaren är&quot;kund&quot;) samt standardklasser som definierats av Adobe.

Klicka på klassnamnet för att visa beskrivningen av klassen. Du kan också välja **Förhandsgranska klassstruktur** för att se de fält och metadata som är associerade med klassen.

I den här självstudien används klassen XDM Individual Profile. Klicka på alternativknappen bredvid klassen för att markera den och klicka sedan på **Tilldela klass**.

![Dialogrutan Tilldela klass](../images/tutorials/create-schema/assign_class.png)

Arbetsytan visas igen. Avsnittet *Klass* innehåller nu den klass du har valt (enskild XDM-profil) och fälten från klassen XDM Individual Profile visas nu i avsnittet *Struktur* .

![Tilldelad klass för enskild XDM-profil](../images/tutorials/create-schema/class_assigned_structure.png)

Fälten visas i formatet &quot;fieldName | Datatyp&quot;. Steg för att definiera schemafält i användargränssnittet finns senare i den här självstudiekursen.

>[!NOTE]
>
>Du kan [ändra schemaklassen](#change-class) när som helst under den inledande dispositionsprocessen innan schemat har sparats, men detta bör göras med yttersta försiktighet. Blandningar är bara kompatibla med vissa klasser. Om du ändrar klassen återställs arbetsytan och alla fält du har lagt till.

## Lägga till en blandning {#mixin}

Nu när en klass har tilldelats innehåller *dispositionssektionen* ett tredje underavsnitt: *Blandningar*.

Nu kan du börja lägga till fält i ditt schema genom att lägga till mixar. En blandning är en grupp med ett eller flera fält som beskriver ett visst koncept. I den här självstudiekursen används mixins för att beskriva medlemmarna i bonusprogrammet och samla in viktig information som namn, födelsedag, telefonnummer, adress med mera.

Om du vill lägga till en blandning klickar du på **Lägg till** i underavsnittet *Blandningar* .

![](../images/tutorials/create-schema/add_mixin_button.png)

Dialogrutan *Lägg till mixning* visas. Mixer är bara avsedda att användas med specifika klasser, och därför visas bara de som är kompatibla med den klass du valde (i det här fallet klassen XDM Individual Profile) i listan över blandningar.

Om du markerar alternativknappen bredvid en mixin kan du välja att **förhandsgranska blandningsstruktur**. Välj blandningen &quot;Profilpersoninformation&quot; och klicka sedan på **Lägg till mixning**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Arbetsytan för schemat visas igen. Avsnittet *Mixins* visar nu blandningen &quot;Profile Person Details&quot; och avsnittet *Structure* innehåller de fält som har bidragit med blandningen.

![](../images/tutorials/create-schema/person_details_structure.png)

Den här blandningen bidrar med flera fält under namnet&quot;person&quot; på den översta nivån med datatypen&quot;person&quot;. Den här gruppen med fält beskriver information om en individ, inklusive namn, födelsedatum och kön.

>[!NOTE]
>
>Kom ihåg att fält kan använda skalära typer (till exempel sträng, heltal, matris eller datum) som datatyp, samt alla&quot;datatyper&quot; (en grupp fält som representerar ett gemensamt koncept) i schemaregistret.

Observera att fältet &quot;name&quot; har datatypen &quot;Person Name&quot;, vilket innebär att det beskriver ett vanligt koncept och innehåller namnrelaterade underfält som förnamn, efternamn och fullständigt namn.

Klicka på olika fält på arbetsytan för att se ytterligare fält som de bidrar till schemastrukturen.

## Lägg till ytterligare en blandning {#mixin-2}

Nu kan du upprepa samma steg för att lägga till en annan blandning. När du visar dialogrutan *Lägg till mixning* den här gången kan du lägga märke till att mixinen &quot;Profilpersondetaljer&quot; har blivit nedtonad och att alternativknappen bredvid inte kan markeras. Detta förhindrar att du av misstag duplicerar blandningar som du redan har inkluderat i det aktuella schemat.

Nu kan du lägga till blandningen &quot;Profil - personlig information&quot; från dialogrutan *Lägg till mixning* .

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

När arbetsytan har lagts till visas den igen. &quot;Profilens personuppgifter&quot; visas nu under *Blandningar* i *dispositionsdelen* , och fält för hemadress, mobiltelefon med mera har lagts till under *Struktur*.

Ungefär som i fältet &quot;name&quot; representerar de fält du just lade till koncept för flera fält. &quot;homeAddress&quot; har till exempel datatypen &quot;Address&quot; och &quot;mobilePhone&quot; har datatypen &quot;Phone Number&quot;. Du kan klicka på vart och ett av dessa fält för att expandera dem och visa de ytterligare fält som ingår i datatypen.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definiera en ny blandning {#define-mixin}

Schemat&quot;Förmånsmedlemmar&quot; är avsett för att samla in data som är relaterade till medlemmarna i ett lojalitetsprogram, så det kräver vissa specifika lojalitetsrelaterade fält. Det finns inga standardblandningar som innehåller de nödvändiga fälten, och du måste därför definiera en ny blandning.

När du nu öppnar dialogrutan *Lägg till mixning* väljer du **Skapa ny mixning**. Du ombeds sedan ange ett **visningsnamn** och en **beskrivning** för din blandning.

![](../images/tutorials/create-schema/mixin_create_new.png)

Precis som med klassnamn ska mixnamnet vara kort och enkelt och innehålla en beskrivning av vad mixinen kommer att bidra till schemat. Även dessa är unika, så du kan inte återanvända namnet och måste därför se till att det är tillräckligt specifikt.

I den här självstudiekursen anger du den nya mixen&quot;Loyalty Details&quot; (Förmånsinformation).

Klicka på **Lägg till mixning** för att återgå till schemaredigeraren. &quot;Lojalitetsinformation&quot; ska nu visas under *Blandningar* till vänster på arbetsytan, men det finns inga fält som är kopplade till den ännu och därför visas inga nya fält under *Struktur*.

## Lägg till fält i mixinen {#mixin-fields}

Nu när du har skapat blandningen &quot;Loyalty Details&quot; är det dags att definiera de fält som blandningen ska bidra till schemat.

Börja med att klicka på blandningsnamnet i *avsnittet Blandningar* . När du har gjort det visas *Blandade egenskaper* till höger om redigeraren och knappen **Lägg till fält** visas bredvid schemats namn under *Struktur*.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Klicka på **Lägg till fält** bredvid&quot;Förmånsmedlemmar&quot; för att skapa en ny nod i strukturen. Den här noden (kallas &quot;_tenantId&quot; i det här exemplet) representerar din IMS-organisations klient-ID, föregånget av ett understreck. Närvaron av innehavar-ID anger att fälten som du lägger till finns i organisationens namnutrymme.

Fälten som du lägger till är alltså unika för din organisation och kommer att sparas i schemaregistret i ett specifikt område som bara är tillgängligt för din IMS-organisation. Fält som du definierar måste alltid läggas till i namnutrymmet för att förhindra kollisioner med namn från andra standardklasser, mixins, datatyper och fält.

I den namngivna noden finns ett &quot;Nytt fält&quot;. Det här är början på&quot;Lojalitetsinformation&quot;-mixen.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Använd *Fältegenskaper* till höger om redigeraren och börja med att skapa ett&quot;lojalitetsfält&quot; med typen&quot;Objekt&quot; som ska användas för dina lojalitetsrelaterade fält. När du är klar klickar du på **Använd**.

![](../images/tutorials/create-schema/loyalty_object.png)

Ändringarna tillämpas och det nyskapade&quot;lojalitetsobjektet&quot; visas. Klicka på **Lägg till fält** bredvid objektet om du vill lägga till fler lojalitetsrelaterade fält. Ett nytt fält visas och avsnittet *Fältegenskaper* visas till höger på arbetsytan.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Varje fält kräver följande information:

* **Fältnamn:** Fältets namn, skrivet i kameraläge. Exempel: loyaltyLevel
* **Visningsnamn:** Fältets namn, skrivet i versaler. Exempel: Lojalitetsnivå
* **Typ:** Fältets datatyp. Detta inkluderar grundläggande skalära typer och alla datatyper som definieras i schemaregistret. Exempel: sträng, heltal, boolesk, person, adress, telefonnummer osv.
* **Beskrivning:** En valfri beskrivning av fältet ska inkluderas, skriven i inledande mening. (Högst 200 tecken)

Det första fältet för Loyalty-objektet blir en sträng med namnet&quot;loyaltyId&quot;. När du ställer in det nya fältets typ till String fylls fönstret *Fältegenskaper* i med flera alternativ för att tillämpa begränsningar, inklusive **Standardvärde**, **Format** och **Maximal längd**.

![](../images/tutorials/create-schema/string_constraints.png)

Olika begränsningsalternativ är tillgängliga beroende på vilken datatyp som har valts. Eftersom&quot;loyaltyId&quot; blir en e-postadress väljer du&quot;email&quot; i listrutan **Format** . Välj **Använd** för att tillämpa ändringarna.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Lägg till fler fält som ska blandas {#mixin-fields-2}

Nu när du har lagt till fältet&quot;loyaltyId&quot; kan du lägga till ytterligare fält för att hämta lojalitetsrelaterad information som:

* Punkter (heltal)
* Medlem sedan (datum)

Varje fält läggs till genom att klicka på **Lägg till fält** i förmånsobjektet och fylla i den obligatoriska informationen.

När det är klart innehåller Loyalty-objektet fält för: Förmåns-ID, poäng och Medlem sedan.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Lägg till enum-fält som ska blandas {#enum}

När du definierar fält i Schemaredigeraren finns det ytterligare alternativ som du kan använda för grundläggande fälttyper för att tillhandahålla ytterligare begränsningar för de data som fältet kan innehålla.

Ett exempel på detta är ett&quot;lojalitetsfält&quot; där värdet bara kan vara ett av fyra möjliga alternativ. Om du vill lägga till det här fältet i schemat klickar du på **Lägg till fält** bredvid objektet &quot;loyalty&quot; och fyller i de obligatoriska fälten under *Fältegenskaper*.

För **Typ** väljer du String så visas ytterligare kryssrutor för **Array**, **Enum** och **Identity**.

Markera kryssrutan **Uppräkning** om du vill öppna avsnittet *Uppräkningsvärden* nedan. Här kan du ange **Value** (i camelCase) och **Label** (ett valfritt, läsvänligt namn i Title Case) för varje godtagbar lojalitetsnivå.

När du har slutfört alla fältegenskaper klickar du på **Använd** och fältet&quot;loyaltyLevel&quot; läggs till i objektet&quot;loyalty&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

Mer information om tillgängliga ytterligare begränsningar:

* **Obligatoriskt:** Anger att fältet är obligatoriskt för datainmatning. Alla data som överförs till en datauppsättning som baseras på det här schemat och som inte innehåller det här fältet kommer att misslyckas vid inmatning.
* **Array:** Anger att fältet innehåller en array med värden, var och en med den angivna datatypen. Om du t.ex. markerar datatypen String och kryssrutan Array betyder det att fältet kommer att innehålla en array med strängar.
* **Uppräkning:** Anger att det här fältet måste innehålla ett av värdena från en numrerad lista med möjliga värden.
* **Identitet:** Anger att det här fältet är ett identitetsfält. Mer information om identitetsfält finns [senare i den här självstudiekursen](#identity-field).

## Konvertera ett flerfältsobjekt till en datatyp {#datatype}

När du har lagt till flera lojalitetsspecifika fält innehåller objektet&quot;lojalitet&quot; nu en gemensam datastruktur som kan vara användbar i andra scheman.

När du känner att en struktur med flera fält kan återanvändas, och du vill ha flexibiliteten att använda samma datastruktur någon annanstans, kan du konvertera strukturen till en datatyp med Schemaredigeraren.

Datatyper möjliggör konsekvent användning av flerfältsstrukturer och ger större flexibilitet än en blandning eftersom de kan användas var som helst inom ett schema. Detta görs genom att ställa in **fälttypen** i en blandning till datatypen i registret.

Om du vill konvertera&quot;lojalitetsobjektet&quot; till en datatyp klickar du på fältet&quot;lojalitet&quot; under *Struktur* och väljer **Konvertera till ny datatyp** till höger om redigeraren under *Fältegenskaper*. Ett litet grönt popup-fönster visas som bekräftar&quot;Objekt konverterat till datatyp&quot;.

När du nu tittar under *Struktur* ser du att fältet&quot;Förtroende&quot; har datatypen&quot;Förtroende&quot; och att fälten har små låsikoner bredvid sig som anger att de inte längre är enskilda fält, utan snarare är en del av en struktur med flera fält.

I ett framtida schema kan du nu tilldela ett fält **typen** av &quot;Lojalitet&quot; och det skulle automatiskt inkludera fälten Lojalitetsnivå, Punkter, Medlems-ID och Lojalitets-ID.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## Ange ett schemafält som identitetsfält {#identity-field}

Scheman används för inmatning av data i Experience Platform, och dessa data används i slutändan för att identifiera individer och sammanfoga information från olika källor. Nyckelfält kan markeras som Identity-fält för att underlätta med den här processen.

Med Experience Platform är det enkelt att ange ett identitetsfält med hjälp av en **identitetskryssruta** i Schemaläggaren.

Det kan till exempel finnas tusentals medlemmar i bonusprogrammet som tillhör samma&quot;nivå&quot;, men varje medlem i bonusprogrammet har ett unikt&quot;lojalitetsId&quot; (som i det här fallet är den enskilda medlemmens e-postadress). Det faktum att &quot;loyaltyId&quot; är en unik identifierare för varje medlem gör det till en bra kandidat för ett identitetsfält, medan &quot;level&quot; inte är det.

I *strukturdelen* av redigeraren klickar du på fältet&quot;loyaltyId&quot; som du skapade och kryssrutan **Identitet** visas under *Fältegenskaper*. Markera kryssrutan så kan du ange den som **primär identitet**. Markera även den rutan.

Sedan måste du ange ett **identitetsnamn**. Det finns flera fördefinierade namnutrymmen, men eftersom &quot;loyaltyId&quot; är medlemmens e-postadress väljer du &quot;E-post&quot; i listrutan. Du kan nu klicka på **Använd** för att bekräfta uppdateringarna i fältet&quot;loyaltyId&quot;.

Nu kommer alla data som hämtas in i fältet&quot;loyaltyId&quot; att användas för att identifiera den enskilda personen och sammanfoga en enda vy av den kunden.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>När ett schemafält har angetts som primär identitet får du ett felmeddelande om du senare försöker ange ett annat fält i schemat som primärt. Varje schema får endast innehålla ett primärt identitetsfält.

Mer information om hur du arbetar med identiteter finns i dokumentationen för [identitetstjänsten](../../identity-service/home.md) .

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## Aktivera schemat för användning i kundprofilen i realtid {#profile}

Schemaredigeraren gör det möjligt att aktivera ett schema för användning med kundprofilen [i](../../profile/home.md)realtid. Profilen ger en helhetsbild av varje enskild kund genom att skapa en robust 360-gradersprofil med kundattribut samt en tidsstämplad översikt över varje interaktion som kunden har haft i alla system som är integrerade med Experience Platform.

För att ett schema ska kunna aktiveras för användning med kundprofilen i realtid måste en primär identitet ha definierats. Du får felmeddelandet&quot;Saknad primär identitet&quot; om du försöker aktivera ett schema utan att först definiera en primär identitet.

![](../images/tutorials/create-schema/missing_primary_identity.png)

Om du vill aktivera schemat &quot;Förmånsmedlemmar&quot; för användning i profilen börjar du med att klicka på &quot;Förmånsmedlemmar&quot; under *Struktur* i redigeraren.

Till höger om redigeraren visas information om schemat, inklusive visningsnamn, beskrivning och typ, under *Schemaegenskaper*. Förutom den här informationen finns det en växlingsknapp med namnet **Profil**.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

Klicka på **Profil** så visas ett popup-fönster där du ombeds bekräfta att du vill aktivera schemat för profilen.

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>När ett schema har aktiverats för kundprofil i realtid och sparats kan det inte inaktiveras.

## Nästa steg och ytterligare resurser

Nu när du är klar med att komponera ett&quot;Loyalty Members&quot;-schema kan du se hela schemat i *strukturdelen* i redigeraren. Klicka på **Spara** så sparas schemat i schemabiblioteket så att det blir tillgängligt för schemaregistret.

Ditt nya schema kan nu användas för att importera data till Platform. Kom ihåg att när schemat väl har använts för att importera data får endast additiva ändringar göras. Mer information om schemaversion finns i [grunderna för schemakomposition](../schema/composition.md) .

Schemat &quot;Bonusmedlemmar&quot; är också tillgängligt för att visas och hanteras med API:t för schemaregister. Börja med att läsa utvecklarhandboken [för](../api/getting-started.md)schematabellens API när du vill börja arbeta med API:t.

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

Experience Platform erbjuder flexibilitet att definiera ett schema baserat på en klass som är unik för din organisation.

Öppna dialogrutan *Tilldela klass* genom att klicka på **Tilldela** i avsnittet *Klass* i Schemaläggaren. Välj **Skapa ny klass** i dialogrutan.

Du kan sedan ge den nya klassen ett **visningsnamn** (ett kort, beskrivande, unikt och användarvänligt namn för klassen), en **beskrivning** och ett **beteende** (&quot;Spela in&quot; eller&quot;Tidsserie&quot;) för de data som schemat ska definiera.

![Ny klassinformation](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>När du skapar ett schema som implementerar en klass som definierats av din organisation, måste du komma ihåg att mixar bara är tillgängliga för användning med kompatibla klasser. Eftersom den klass du definierade är ny finns det inga kompatibla blandningar i listan i dialogrutan *Lägg till mixning* . I stället måste du välja **Skapa ny mixning** och definiera en mixin som ska användas med den klassen. Nästa gång du skapar ett schema som implementerar den nya klassen, kommer den mixin som du definierade att listas och vara tillgänglig för användning.

### Ändra klassen för ett schema {#change-class}

Du kan när som helst under den inledande schemakompositionsprocessen, innan schemat sparas, ändra den klass som schemat baseras på.

>[!WARNING]
>
>Var försiktig innan du byter klass. Blandningar är bara kompatibla med vissa klasser. Om du ändrar klassen återställs arbetsytan och alla fält som du har lagt till tas bort.

Om du vill ändra klassen klickar du på **Tilldela** bredvid *Klass* i *dispositionsdelen* av redigeraren.

När dialogrutan *Tilldela klass* öppnas kan du välja en ny klass i den tillgängliga listan. Klicka på **Tilldela klass** och en ny dialogruta öppnas där du ombeds bekräfta att du vill tilldela en ny klass.

![Ändra klass](../images/tutorials/create-schema/assign_new_class_warning.png)

Om du bekräftar klassändringen återställs arbetsytan och alla kompositionsförlopp går förlorade.