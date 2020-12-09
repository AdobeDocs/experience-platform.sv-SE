---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile details;details
title: Anpassning av profildetaljer
description: 'Den här guiden innehåller stegvisa instruktioner för hur kundprofildata i realtid visas i Adobe Experience Platform användargränssnitt. '
topic: guide
translation-type: tm+mt
source-git-commit: d05884c87445ec16b0ad44f593cf782b8c80d646
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] anpassning av detaljer {#profile-detail-customization}

I Adobe Experience Platform användargränssnitt kan du visa och interagera med [!DNL Real-time Customer Profile] data i form av kundprofiler. Profilinformationen som visas i användargränssnittet har sammanfogats från flera profilfragment till en enda vy över varje enskild kund. Detta inkluderar information som grundläggande attribut, länkade identiteter och kanalinställningar. Standardfälten som visas i profiler kan också ändras på organisationsnivå för att visa önskade [!DNL Profile] attribut. Den här handboken innehåller stegvisa instruktioner för hur du anpassar hur [!DNL Profile] data visas i plattformens användargränssnitt.

En fullständig guide till användargränssnittet för profiler finns i [användargränssnittsguiden](user-guide.md)för profiler.

## Ändra ordning på och storlek på kort {#reorder-and-resize-cards}

På **[!UICONTROL Detail]** fliken i kundprofilen kan du välja **[!UICONTROL Modify dashboard]** för att ändra storlek på och ordna om befintliga kort.

![](../images/profile-customization/profiles-modify-dashboard.png)

När du har valt att ändra kontrollpanelen kan du ändra ordning på korten genom att markera korttiteln och dra och släppa korten i önskad ordning. Du kan också ändra storlek på ett kort genom att markera vinkelsymbolen i kortets (`⌟`) nedre högra hörn och dra kortet till önskad storlek. I det här exemplet ändras storleken på **[!UICONTROL Basic attributes]** kortet.

![](../images/profile-customization/profiles-resize-cards.png)

Det valda kortet justeras till önskad storlek och omgivande kort flyttas dynamiskt. Detta kan medföra att vissa kort flyttas till ytterligare rader, vilket kräver att du rullar nedåt för att se alla kort. Om du till exempel ändrar storlek på &quot;[!UICONTROL Basic attributes]&quot;-kortet visas inte &quot;[!UICONTROL Linked identities]&quot;-kortet längre på den översta raden och visas nu på en ny andra rad i profilen (visas inte). Om du vill flytta tillbaka &quot;[!UICONTROL Linked identities]&quot;-kortet till den översta raden kan du dra och släppa det till den aktuella positionen för &quot;[!UICONTROL Channel preferences]&quot;-kortet.

![](../images/profile-customization/profiles-card-resized.png)

## Redigera och ta bort kort

Förutom att ändra storlek på och ordna om kort kan du redigera innehållet på vissa kort och ta bort vissa kort från kontrollpanelen helt. Markera ellipserna (`...`) i kortets övre högra hörn för att redigera eller ta bort det. Då öppnas en listruta med alternativ för att antingen redigera eller ta bort kortet, beroende på egenskaperna för det valda kortet.

>[!NOTE]
>
>Alla kort kan inte redigeras eller tas bort. Detta beror på att vissa kort innehåller skrivskyddad eller obligatorisk information. Om ett kort inte har några ellipser i det övre högra hörnet innehåller det skrivskyddad OCH nödvändig information och kan inte redigeras eller tas bort. Om ett kort har ovaler i hörnet och du markerar det visas endast ett alternativ för att ta bort kortet, är kortinformationen skrivskyddad och kan inte redigeras.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Välj **[!UICONTROL Edit]** i listrutan för att öppna **[!UICONTROL Edit widget]** arbetsytan, där du kan uppdatera korttiteln, ändra ordning på eller ta bort synliga attribut, eller lägga till ytterligare attribut med **[!UICONTROL Add attributes]** knappen.

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## Lägg till attribut {#add-attributes}

På **[!UICONTROL Edit widget]** skärmen väljer du **[!UICONTROL Add attributes]** i kortets övre högra hörn för att börja lägga till attribut till kortet.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

När **[!UICONTROL Select union schema field]** dialogrutan öppnas visas det fullständiga [!UICONTROL XDM Individual Profile] unionsschemat till vänster, med inkapslade fält under. Mer information om unionsscheman finns i avsnittet [unionsscheman i [!DNL Profile] användarhandboken](user-guide.md#union-schema).

I avsnittet till höger i dialogrutan visas de attribut som finns på kortet som du redigerar. **[!UICONTROL Selected Attributes]** Du kan även ta bort och ändra ordning på attribut här. Det totala antalet valda attribut visas, liksom det maximala antalet attribut (20) som kan läggas till på ett kort.

![](../images/profile-customization/profiles-select-field-before.png)

Du kan välja något av de tillgängliga fackliga schemafälten för att anpassa attributen på kortet som du redigerar. Markerade fält visas med en bockmarkering bredvid sig och läggs automatiskt till i listan med valda attribut. När du har lagt till alla attribut som du vill visa på kortet väljer du **[!UICONTROL Select]** att gå tillbaka till **[!UICONTROL Edit widget]** skärmen.

![](../images/profile-customization/profiles-select-field-after.png)

När du kommer tillbaka till **[!UICONTROL Edit widget]** skärmen bör listan över attribut på kortet nu uppdateras för att återspegla dina val. Du kan fortfarande ta bort eller ändra ordning på kortattributen eller redigera kortets titel efter behov. När redigeringarna är klara väljer du **[!UICONTROL Save]** att spara ändringarna.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

När du har sparat programmet återgår du till den **[!UICONTROL Detail]** flik där det uppdaterade kortet och attributen visas.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Lägg till ett nytt kort {#add-a-new-card}

Om du vill anpassa utseendet på profiler i Experience Platform ytterligare kan du välja att lägga till nya kort på kontrollpanelen och välja de attribut som du vill visa på dessa kort. Börja med att välja **[!UICONTROL Modify dashboard]** på **[!UICONTROL Detail]** fliken.

![](../images/profile-customization/profiles-modify-dashboard.png)

Välj sedan **[!UICONTROL Add widget]** i det övre vänstra hörnet av kontrollpanelen.

![](../images/profile-customization/profiles-add-widget.png)

Om du väljer att lägga till ett nytt kort öppnas skärmen där du kan ange en rubrik för det nya kortet och välja de attribut som du vill att kortet ska visas. **[!UICONTROL Edit widget]** Om du vill lägga till attribut till kortet väljer du **[!UICONTROL Add attributes]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

När **[!UICONTROL Select union schema field]** dialogrutan öppnas visar den vänstra sidan av dialogrutan det fullständiga [!UICONTROL XDM Individual Profile] **[!UICONTROL Selected Attributes]** unionsschemat och i avsnittet till höger i dialogrutan visas de attribut som du väljer för kortet. Mer information om hur du lägger till attribut finns i [avsnittet om att lägga till attribut](#add-attributes) som visas tidigare i det här dokumentet.

Det totala antalet valda attribut visas, liksom det maximala antalet attribut (20) som kan läggas till på ett kort. Du kan också ta bort och ändra ordning på de valda attributen från den här skärmen. När du har lagt till alla attribut som du vill visa på kortet väljer du **[!UICONTROL Select]** att gå tillbaka till **[!UICONTROL Edit widget]** skärmen.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

När du kommer tillbaka till **[!UICONTROL Edit widget]** skärmen bör listan med attribut på kortet återspegla dina val från föregående skärm. Du kan också ändra ordning på och ta bort kortattribut efter behov.

Om du vill spara ditt nya kort måste du först ange ett **[!UICONTROL Card title]** kort. Sedan kan du välja **[!UICONTROL Save]** och slutföra kortskapandet.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

När du har sparat programmet återgår du till den **[!UICONTROL Detail]** flik där det nya kortet och attributen visas.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Återställ standardkort

Om du någon gång bestämmer dig för att du vill återställa standardkort som sedan dess har tagits bort, kan du snabbt och enkelt göra det. Markera först **[!UICONTROL Modify dashboard]** och sedan **[!UICONTROL Restore default cards]**. När standardkorten visas kan du välja **[!UICONTROL Save]** att spara dina ändringar eller välja **[!UICONTROL Cancel]** om du inte vill återställa standardkorten.

![](../images/profile-customization/profiles-restore-default.png)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna uppdatera profilvyn för din organisation, inklusive lägga till och ta bort kort, redigera kortinformation och attribut samt ändra ordning på och storlek på kort. Mer information om hur du arbetar med [!DNL Profile] data i användargränssnittet i Experience Platform finns i [[!DNL Profile] användarhandboken](user-guide.md).