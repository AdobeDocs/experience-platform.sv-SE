---
title: Användargränssnittshandbok för kopplingsprofiler
type: Documentation
description: Lär dig hur du arbetar med sammanfogningsprinciper med hjälp av Adobe Experience Platform användargränssnitt.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 0%

---


# Användargränssnittshandbok för sammanslagningsprinciper

Med Adobe Experience Platform kan ni sammanföra datafragment från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanfogar dessa data är sammanfogningsprinciper de regler som [!DNL Experience Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn.

Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Den här handboken innehåller stegvisa instruktioner för hur du arbetar med sammanfogningsprinciper med hjälp av användargränssnittet i Adobe Experience Platform.

Om du vill veta mer om sammanfogningsprinciper och vilken roll de spelar i Experience Platform kan du börja med att läsa översikten för [sammanfogningsprinciper](overview.md).

## Komma igång

Den här handboken kräver en fungerande förståelse av flera viktiga [!DNL Experience Platform]-funktioner. Innan du följer den här handboken bör du läsa dokumentationen för följande tjänster:

* [Kundprofil i realtid](../home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Adobe Experience Platform identitetstjänst](../../identity-service/home.md): Aktiverar kundprofil i realtid genom att brygga identiteter från olika datakällor som importeras till [!DNL Experience Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.

## Visa sammanslagningsprinciper {#view-merge-policies}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_101221_404"
>title="Det gick inte att hitta sammanfogningsprincipen"
>abstract="Detta innebär att Experience Platform inte kunde hitta den begärda sammanfogningsprincipen. Försök med någon av följande lösningar för att åtgärda felet:<ul><li>Kontrollera att rätt ID för sammanfogningsprincip finns i webbadressen.</li><li>Kontrollera att du har rätt kombination av organisation och sandlåda för den sammanslagningsprincip du försöker få åtkomst till.</li></ul>"

I användargränssnittet för [!DNL Experience Platform] kan du börja arbeta med sammanfogningsprinciper genom att välja **[!UICONTROL Profiles]** i den vänstra navigeringen och sedan välja fliken **[!UICONTROL Merge Policies]** .

På den här fliken finns en lista med alla befintliga sammanfogningsprinciper för din organisation, samt information för varje sammanfogningsprincip, inklusive principnamnet, oavsett om sammanfogningsprincipen är standardprincipen för sammanfogning eller inte, samt schemaklassen som sammanfogningsprincipen gäller.

![Bläddringssidan för sammanslagningsprinciper visas.](../images/merge-policies/landing.png)

Om du vill välja vilken information som ska visas, eller om du vill lägga till fler kolumner till visningen, markerar du ![ikonen för kolumninställningar](../../images/icons/column-settings.png) och väljer ett kolumnnamn som ska läggas till eller tas bort från vyn.

![De tillgängliga alternativen för att anpassa webbläsarsidan för sammanfogningsprinciper visas.](../images/merge-policies/adjust-view.png)

## Skapa en sammanfogningsprincip {#create-a-merge-policy}

Om du vill skapa en ny sammanfogningsprincip väljer du **[!UICONTROL Create merge policy]** på fliken för sammanfogningsprinciper och anger det nya arbetsflödet för sammanfogningsprincip.

![Landningssidan för sammanslagningsprinciper med knappen Skapa markerad.](../images/merge-policies/create-new.png)

Arbetsflödet i **[!UICONTROL New merge policy]** kräver att du anger viktig information för den nya sammanfogningsprincipen genom en serie guidade steg. De här stegen beskrivs i de efterföljande avsnitten.

![Det nya arbetsflödet för sammanfogningsprincip.](../images/merge-policies/create.png)

## [!UICONTROL Configure] {#configure}

I det första steget i arbetsflödet kan du konfigurera sammanfogningsprincipen genom att ange grundläggande information. Denna information omfattar

* **[!UICONTROL Name]**: Namnet på sammanfogningsprincipen bör vara beskrivande men koncist.
* **[!UICONTROL Schema class]**: Den XDM-schemaklass som är associerad med sammanfogningsprincipen. Detta anger schemaklassen som sammanfogningsprincipen skapas för. Organisationer kan skapa flera sammanfogningsprinciper per per schemaklass. För närvarande är bara klassen [!UICONTROL XDM Individual Profile] tillgänglig i användargränssnittet. Du kan förhandsgranska unionsschemat för schemaklassen genom att välja **[!UICONTROL View Union Schema]**. Mer information finns i avsnittet [Visa det efterföljande unionsschemat](#view-union-schema).
* **[!UICONTROL ID stitching]**: Det här fältet definierar hur en kunds relaterade identiteter ska fastställas. Det finns två möjliga värden för identitetssammanfogning, och det är viktigt att förstå hur den typ av identitetssammanfogning som du väljer påverkar dina data. Mer information finns i översikten [Sammanslagningsprinciper](overview.md).
   * **[!UICONTROL None]**: Utför ingen identitetssammanslagning.
   * **[!UICONTROL Private Graph]**: Utför identitetssammanfogning baserat på ditt privata identitetsdiagram.
* **[!UICONTROL Default merge policy]**: En växlingsknapp som gör att du kan välja om den här sammanfogningsprincipen ska vara standard för din organisation eller inte. Om väljaren är aktiverad visas en varning om att du vill ändra organisationens standardpolicy för sammanslagning. Mer information om standardprinciper för sammanfogning finns i översikten [för sammanfogningsprinciper](overview.md).
  ![En portfölj som förklarar vad som händer när sammanfogningsprincipen har angetts som standardprincip för sammanfogning.](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Active-On-Edge Merge Policy]**: En växlingsknapp som gör att du kan välja om den här sammanfogningsprincipen ska vara aktiv i kant eller inte. För att säkerställa att alla profilkonsumenter arbetar med samma vy på kanterna kan sammanfogningsprinciper markeras som aktiva på kanten. För att en målgrupp ska kunna aktiveras på kanten (markeras som en målgrupp) måste den vara kopplad till en sammanfogningspolicy som är markerad som aktiv på kanten. Om en målgrupp **inte** är kopplad till en sammanfogningsprincip som är markerad som aktiv i kant, markeras målgruppen inte som aktiv i kant och markeras som en målgrupp för direktuppspelning. Dessutom kan varje sandlåda i en organisation bara ha **en**-sammanslagningsprincip som är aktiv på kanten.

När de obligatoriska fälten har slutförts kan du välja **[!UICONTROL Next]** för att fortsätta med arbetsflödet.

![En färdig konfigurationsskärm med knappen Nästa markerad.](../images/merge-policies/create-complete.png)

## [!UICONTROL View Union Schema] {#view-union-schema}

När du skapar eller redigerar en sammanfogningsprincip kan du visa unionsschemat för den valda schemaklassen genom att välja **[!UICONTROL View Union Schema]**.

![Knappen Visa unionsschema är markerad i det nya policyarbetsflödet för sammanslagning.](../images/merge-policies/view-union-schema.png)

Dialogrutan [!UICONTROL View Union Schema] öppnas med alla scheman, identiteter och relationer som är kopplade till unionsschemat. Du kan använda dialogrutan för att utforska unionsschemat på samma sätt som du gör genom att gå till fliken [!UICONTROL Union Schema] i avsnittet [!UICONTROL Profiles] i Experience Platform-gränssnittet.

Detaljerad information om unionsscheman, inklusive hur du interagerar med dem på fliken [!UICONTROL Union Schema] eller i dialogrutan [!UICONTROL View Union Schema] som visas i arbetsflödet för sammanfogningsprinciper, finns i [gränssnittshandboken för unionsscheman](../ui/union-schema.md).

![Dialogrutan Visa unionens schema.](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Select Profile datasets] {#select-profile-datasets}

På skärmen **[!UICONTROL Select Profile datasets]** måste du välja den **[!UICONTROL Merge method]** som du vill använda för sammanfogningsprincipen. På skärmen visas även det totala antalet [!UICONTROL Profile datasets] i organisationen som relaterar till schemaklassen som valdes på föregående skärm.

Beroende på vilken sammanfogningsmetod du väljer sammanfogas alla profildatauppsättningar i den ordning som de senast uppdaterades (tidsstämpelsortering). Du kan också behöva välja vilka profildatauppsättningar som ska inkluderas i sammanfogningsprincipen och i vilken ordning de ska sammanfogas (datauppsättningsprioritet).

Mer information om sammanfogningsmetoder finns i översikten [för sammanfogningsprinciper](overview.md).

>[!BEGINTABS]

>[!TAB Tidsstämpeln har ordnats]

Om du väljer **[!UICONTROL Timestamp ordered]** som sammanfogningsmetod får attribut från de senast uppdaterade datauppsättningarna företräde. Detta gäller för alla profildatauppsättningar.

>[!NOTE]
>
>Antalet hakparenteser bredvid **[!UICONTROL Profile datasets]** (till exempel `(37)` i bilden som visas) visar det totala antalet profildatamängder som kommer att inkluderas.

![En bild som visar den tidstämpelsorterade sammanslagningsmetoden som väljs.](../images/merge-policies/timestamp-ordered.png)

>[!TAB Datauppsättningsprioritet]

Om du väljer **[!UICONTROL Dataset precedence]** som sammanfogningsmetod måste du välja profildatamängder och prioritera dem manuellt. Varje datamängd som visas innehåller också status för den senaste batchimporten eller visar ett meddelande om att inga batchar har importerats till den datauppsättningen.

Du kan välja upp till 50 datauppsättningar från datauppsättningslistan som ska ingå i sammanfogningsprincipen.

>[!NOTE]
>
>Antalet hakparenteser bredvid **[!UICONTROL Profile datasets]** (till exempel `(37)` i bilden som visas) visar det totala antalet profildatamängder som är tillgängliga för markering.

När du väljer datauppsättningar läggs de till i avsnittet **[!UICONTROL Select datasets]**, vilket gör att du kan dra och släppa datauppsättningarna och ordna dem enligt dina önskemål. När datauppsättningarna justeras i listan uppdateras ordningstalet (1, 2, 3 osv.) bredvid datauppsättningen och prioriteten visas (1 ges den högsta prioriteten, 2 och framåt).

Om du väljer en datauppsättning uppdateras även avsnittet **[!UICONTROL Union schema]**, som visar fälten i det unionsschema som varje datauppsättning bidrar med data till. Mer information om unionsscheman, inklusive hur du interagerar med visualiseringar i användargränssnittet, finns i [gränssnittshandboken för unionsscheman](../ui/union-schema.md)

![En bild som visar datauppsättningens prioritet som väljs, tillsammans med motsvarande inställningar som du måste välja om det alternativet är markerat.](../images/merge-policies/dataset-precedence.png)

>[!ENDTABS]

## [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

Nästa steg i arbetsflödet kräver att du väljer ExperienceEvent-datamängder. Den här skärmen påverkas av den sammanfogningsmetod som du valde på skärmen [[!UICONTROL Select Profile datasets]](#select-profile-datasets).

>[!BEGINTABS]

>[!TAB Tidsstämpeln har ordnats]

Om du valde **[!UICONTROL Timestamp ordered]** som sammanfogningsmetod för profildatauppsättningar prioriteras även attributen från de senast uppdaterade ExperienceEvent-datauppsättningarna här.

>[!NOTE]
>
>Antalet hakparenteser bredvid **[!UICONTROL ExperienceEvent datasets]** (till exempel `(1)` i den bild som visas) visar det totala antalet ExperienceEvent-datamängder som har skapats av din organisation och som relaterar till den schemaklass som du valde på konfigurationsskärmen för sammanfogningsprincipen.

![Det totala antalet ExperienceEvent-datauppsättningar som kan relatera till schemaklassen visas.](../images/merge-policies/timestamp-experienceevent.png)

>[!TAB Datauppsättningsprioritet]

Om du valde **[!UICONTROL Dataset precedence]** som sammanfogningsmetod för profildatamängder måste du välja ExperienceEvent-datamängder som ska inkluderas. Du kan välja upp till 50 ExperienceEvent-datamängder i datauppsättningslistan.

>[!NOTE]
>
>Antalet hakparenteser bredvid **[!UICONTROL ExperienceEvent datasets]** (till exempel `(1)` i den bild som visas) visar det totala antalet ExperienceEvent-datamängder som har skapats av din organisation och som relaterar till den schemaklass som du valde på konfigurationsskärmen för sammanfogningsprincipen.

När datauppsättningar väljs visas de i avsnittet [!UICONTROL Select datasets].

ExperienceEvent-datamängder kan inte ordnas manuellt, i stället läggs attributen i ExperienceEvent-datamängderna till i profildatamängderna om de ingår i samma profilfragment.

Om du väljer en ExperienceEvent-datauppsättning uppdateras även **[!UICONTROL Union schema]**-avsnittet när du väljer profildatauppsättningar, och fälten i det unionsschema som varje datauppsättning bidrar med data till visas. Mer information om unionsscheman, inklusive hur du interagerar med visualiseringar i användargränssnittet, finns i [gränssnittshandboken för unionsscheman](../ui/union-schema.md).

![De valbara ExperienceEvent-datamängderna visas.](../images/merge-policies/dataset-precedence-experienceevent.png)

>[!ENDTABS]

## [!UICONTROL Review] {#review}

Det sista steget i arbetsflödet är att granska din kopplingsprofil. Skärmen **[!UICONTROL Review]** visar information om din sammanfogningsprincip, inklusive vald ID-sammanfogningsmetod, vald sammanfogningsmetod och inkluderade datauppsättningar. (Om du vill visa alla profildata eller ExperienceEvent-datamängder som ingår väljer du antalet datamängder som du vill expandera listrutan.)

Den **[!UICONTROL Preview data]**-tabell som innehåller exempelprofilposter med hjälp av din sammanfogningsprincip ingår också på granskningsskärmen. På så sätt kan du förhandsgranska hur en kundprofil ser ut innan du sparar sammanfogningspolicyn.

Kontrollera att du granskar konfigurationen av sammanfogningsprincipen och förhandsgranskar data noggrant innan du väljer **[!UICONTROL Finish]** för att slutföra arbetsflödet.

>[!BEGINTABS]

>[!TAB Tidsstämpeln har ordnats]

Om du valde **[!UICONTROL Timestamp ordered]** som sammanfogningsmetod för din sammanfogningsprincip innehåller listan med profildatauppsättningar alla datauppsättningar som har skapats av din organisation relaterade till schemaklassen, i tidsstämpelordning. Listan med ExperienceEvent-datamängder innehåller alla datauppsättningar som din organisation har skapat för den valda schemaklassen och som kommer att läggas till i profildatamängderna.

Tabellen **[!UICONTROL Preview data]** visar exempelprofilposter baserat på en tidsstämpelordning för datauppsättningarna. På så sätt kan du förhandsgranska hur en kundprofil ser ut innan du sparar sammanfogningspolicyn.

Välj **[!UICONTROL Finish]** om du vill skapa en ny sammanfogningsprincip.

![Granskningssidan visas. På den här sidan kan du granska information om din nya sammanfogningsprincip.](../images/merge-policies/timestamp-review.png)

>[!TAB Datauppsättningsprioritet]

Om du valde **[!UICONTROL Dataset precedence]** som sammanfogningsmetod för din sammanfogningsprincip innehåller listorna med datauppsättningarna Profile och ExperienceEvent endast de data för profil och ExperienceEvent som du valde när du skapade arbetsflödet. Ordningen på profildatauppsättningarna ska matcha den prioritet som du angav när du skapade dem. Om så inte är fallet använder du knappen [!UICONTROL Back] för att återgå till föregående arbetsflödessteg och justera prioriteten.

Tabellen **[!UICONTROL Preview data]** visar exempelprofilposter med de valda datauppsättningarna. På så sätt kan du förhandsgranska hur en kundprofil ser ut innan du sparar sammanfogningspolicyn.

Välj **[!UICONTROL Finish]** om du vill skapa en ny sammanfogningsprincip.

![Granskningssidan visas. På den här sidan kan du granska information om din nya sammanfogningsprincip.](../images/merge-policies/dataset-precedence-review.png)

>[!ENDTABS]

## Redigera en sammanfogningsprincip {#edit}

På fliken [!UICONTROL Merge Policies] kan du ändra en befintlig sammanfogningsprincip som har skapats för klassen [!DNL XDM Individual Profile] genom att välja **[!UICONTROL Policy name]** för den sammanfogningsprincip som du vill redigera.

När skärmen **[!UICONTROL Edit merge policy]** visas kan du ändra namnet och metoden [!UICONTROL ID stitching] samt ändra om den här principen är standardprincipen för sammanfogning för din organisation eller inte.

Välj **[!UICONTROL Next]** om du vill fortsätta genom sammanslagningsprinciparbetsflödet för att uppdatera sammanfogningsmetoden och dataset som ingår i sammanfogningsprincipen.

![Arbetsflödet för redigering av sammanfogningsprincip visas.](../images/merge-policies/edit-screen.png)

När du har gjort de ändringar du behöver granskar du sammanfogningsprincipen och väljer **[!UICONTROL Finish]** för att spara ändringarna och gå tillbaka till fliken [!UICONTROL Merge policies].

>[!WARNING]
>
>Om du ändrar en sammanfogningsprincip kan det påverka segmenterings- och profilresultaten, eftersom det ändrar det sätt på vilket datakonflikter löses. Granska ändringarna av sammanfogningsprinciperna noggrant innan du sparar dem.

![Granskningssidan för redigeringsprinciparbetsflödet visas.](../images/merge-policies/edit-review.png)

## Policyöverträdelser för datastyrning

När du skapar eller uppdaterar en sammanfogningsprincip görs en kontroll för att avgöra om sammanfogningsprincipen bryter mot någon av de dataanvändningsprinciper som din organisation har definierat. Dataanvändningsprinciper ingår i Adobe Experience Platform Data Governance och är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från för att utföra på specifika [!DNL Experience Platform]-data.

Om en sammanfogningsprincip till exempel användes för att skapa en målgrupp som aktiverats för ett tredjepartsmål, och din organisation har en dataanvändningsprincip som förhindrar export av specifika data till tredje part, får du ett **[!UICONTROL Data governance policy violation detected]**-meddelande när du försöker spara sammanfogningsprincipen.

Det här meddelandet innehåller en lista över dataanvändningsprinciper som har överträtts och gör att du kan visa information om överträdelsen genom att välja en princip i listan. När du har valt en princip som inte följs anger fliken **[!UICONTROL Data lineage]** orsaken till överträdelsen och de aktiveringar som påverkas, där var och en ger mer information om hur dataanvändningsprincipen har brutits.

Om du vill veta mer om hur datastyrning utförs inom Adobe Experience Platform kan du börja med att läsa [översikten över datastyrning](../../data-governance/home.md).

## Nästa steg

Nu när du har skapat och konfigurerat samkörningsprinciper för din organisation kan du använda dem för att justera visningen av kundprofiler inom Experience Platform och för att skapa målgrupper utifrån dina profildata. Se [segmenteringsöversikten](../../segmentation/home.md) för mer information om hur du skapar och arbetar med målgrupper med hjälp av [!DNL Experience Platform]-gränssnittet och API:erna.
