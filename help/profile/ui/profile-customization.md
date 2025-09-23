---
keywords: Experience Platform;profil;kundprofil i realtid;användargränssnitt;anpassning;profilinformation;information
title: Anpassning av profildetaljer i användargränssnittet
description: Den här guiden innehåller stegvisa instruktioner för hur kundprofildata i realtid visas i Adobe Experience Platform användargränssnitt.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: e253be0c4e02b82bfc8926ac4531589782b9c8fe
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile]-detaljanpassning {#profile-detail-customization}

I Adobe Experience Platform användargränssnitt kan du visa och interagera med [!DNL Real-Time Customer Profile]-data i form av kundprofiler. Profilinformationen som visas i användargränssnittet har sammanfogats från flera profilfragment till en enda vy över varje enskild kund. Detta inkluderar information som grundläggande attribut, länkade identiteter och kanalinställningar. Standardfälten som visas i profiler kan också ändras på organisationsnivå för att visa önskade [!DNL Profile]-attribut. Den här handboken innehåller stegvisa instruktioner för hur du anpassar hur [!DNL Profile]-data visas i användargränssnittet i Experience Platform.

En fullständig guide till användargränssnittet för profiler finns i [gränssnittsguiden för profiler](user-guide.md).

## Ändra ordning på och storlek på kort {#reorder-and-resize-cards}

På fliken **[!UICONTROL Detail]** i kundprofilen kan du välja **[!UICONTROL Customize profile details]** om du vill ändra storlek på och ordna om befintliga kort.

![Knappen Anpassa profilinformation är markerad på profilkontrollpanelen.](../images/profile-customization/customize-profile-details.png)

När du har valt att ändra kontrollpanelen kan du ändra ordning på korten genom att markera korttiteln och dra och släppa korten i önskad ordning. Du kan också ändra storlek på ett kort genom att markera vinkelsymbolen i kortets nedre högra hörn (`⌟`) och dra kortet till önskad storlek. I det här exemplet ändras storleken på **[!UICONTROL Basic attributes]**-kortet.

![Knappen för att ändra storlek är markerad i Basic-attributkortet.](../images/profile-customization/resize.png)

Det valda kortet justeras till önskad storlek och omgivande kort flyttas dynamiskt. Detta kan medföra att vissa kort flyttas till ytterligare rader, vilket kräver att du rullar nedåt för att se alla kort. Om du till exempel ändrar storlek på kortet [!UICONTROL Basic attributes] visas inte längre kortet [!UICONTROL Linked identities] på den översta raden och visas nu på en ny andra rad i profilen (visas inte). Om du vill returnera [!UICONTROL Linked identities]-kortet till den översta raden kan du dra och släppa det till den aktuella positionen för [!UICONTROL Channel preferences]-kortet.

## Redigera och ta bort kort

Förutom att ändra storlek på och ordna om kort kan du redigera innehållet på vissa kort och ta bort vissa kort från kontrollpanelen helt. Markera ellipserna (`...`) i kortets övre högra hörn för att redigera eller ta bort det. Då öppnas en listruta med alternativ för att antingen redigera eller ta bort kortet, beroende på egenskaperna för det valda kortet.

>[!NOTE]
>
>Alla kort kan inte redigeras eller tas bort. Detta beror på att vissa kort innehåller skrivskyddad eller obligatorisk information. Om ett kort inte har några ellipser i det övre högra hörnet innehåller det skrivskyddad OCH nödvändig information och kan inte redigeras eller tas bort. Om ett kort har ovaler i hörnet och du markerar det visas endast ett alternativ för att ta bort kortet, är kortinformationen skrivskyddad och kan inte redigeras.

![Listrutan Redigera kort är markerad. Detta inkluderar alternativ för att redigera eller ta bort kortet.](../images/profile-customization/edit-card.png)

Välj **[!UICONTROL Edit]** i listrutan för att öppna arbetsytan i **[!UICONTROL Edit widget]**, där du kan uppdatera korttiteln, ändra ordning på eller ta bort synliga attribut, eller lägga till ytterligare attribut med knappen **[!UICONTROL Add attributes]** .

![Kortet för grundläggande attribut visas.](../images/profile-customization/basic-attributes.png)

## Lägg till attribut {#add-attributes}

På skärmen **[!UICONTROL Edit widget]** väljer du **[!UICONTROL Add attributes]** i kortets övre högra hörn för att börja lägga till attribut till kortet.

![Knappen Lägg till attribut på Basic-attributkortet är markerad.](../images/profile-customization/add-attributes.png)

När dialogrutan **[!UICONTROL Select union schema field]** öppnas visar den vänstra sidan av dialogrutan det fullständiga [!UICONTROL XDM Individual Profile]-unionsschemat, med kapslade fält under. Mer information om unionsscheman finns i avsnittet [unionsscheman i  [!DNL Profile] användarhandboken](user-guide.md#union-schema).

Avsnittet **[!UICONTROL Selected Attributes]** till höger i dialogrutan visar de attribut som för närvarande finns på kortet som du redigerar. Du kan även ta bort och ändra ordning på attribut här. Det totala antalet valda attribut visas, liksom det maximala antalet attribut (20) som kan läggas till på ett kort.

![Attributen som för närvarande utgör attributen på kortet är markerade.](../images/profile-customization/select-before.png)

Du kan välja något av de tillgängliga fackliga schemafälten för att anpassa attributen på kortet som du redigerar. När du markerar fälten kan du välja att visa antingen filsökvägsnamnet eller visningsnamnet. Om du vill växla mellan dessa två skärmar väljer du alternativet **[!UICONTROL Show display names]**.

![Växlingsknappen [!UICONTROL Show display names] är markerad på sidan Profilinformation.](../images/profile-customization/show-display-names.png)

Markerade fält visas med en bockmarkering bredvid sig och läggs automatiskt till i listan med valda attribut. När du har lagt till alla attribut som du vill visa på kortet väljer du **[!UICONTROL Select]** för att gå tillbaka till skärmen **[!UICONTROL Edit widget]**.

![De nya attributen är markerade.](../images/profile-customization/select-after.png)

När du återgår till skärmen **[!UICONTROL Edit widget]** bör listan med attribut på kortet nu uppdateras för att återspegla dina val. Du kan fortfarande ta bort eller ändra ordning på kortattributen eller redigera kortets titel efter behov. När redigeringarna är klara väljer du **[!UICONTROL Save]** för att spara ändringarna.

![De nya attributen visas på det redigerade kortet.](../images/profile-customization/new-attributes.png)

När du har sparat återgår du till fliken **[!UICONTROL Detail]** där det uppdaterade kortet och attributen visas.

## Lägg till ett nytt kort {#add-a-new-card}

Om du vill anpassa utseendet på profiler i Experience Platform ytterligare kan du välja att lägga till nya kort på kontrollpanelen och välja de attribut som du vill visa på dessa kort. Börja med att välja **[!UICONTROL Modify dashboard]** på fliken **[!UICONTROL Detail]**.

![Knappen Anpassa profilinformation är markerad.](../images/profile-customization/customize-profile-details.png)

Välj sedan **[!UICONTROL Add widget]** i det övre vänstra hörnet av instrumentpanelen.

![Knappen Lägg till widget är markerad.](../images/profile-customization/add-widget.png)

Om du väljer att lägga till ett nytt kort öppnas skärmen **[!UICONTROL Edit widget]** där du kan ange en rubrik för det nya kortet och välja de attribut som du vill att kortet ska visas. Om du vill lägga till attribut till kortet väljer du **[!UICONTROL Add attributes]**.

![Ett tomt nytt widgetkort visas i fönstret Redigera widget.](../images/profile-customization/edit-widget.png)

När dialogrutan **[!UICONTROL Select union schema field]** öppnas visar den vänstra sidan av dialogrutan det fullständiga [!UICONTROL XDM Individual Profile] union-schemat och avsnittet **[!UICONTROL Selected Attributes]** till höger i dialogrutan de attribut som du väljer för kortet. Mer information om hur du lägger till attribut finns i avsnittet [om att lägga till attribut](#add-attributes) som visas tidigare i det här dokumentet.

Det totala antalet valda attribut visas, liksom det maximala antalet attribut (20) som kan läggas till på ett kort. Du kan också ta bort och ändra ordning på de valda attributen från den här skärmen. När du har lagt till alla attribut som du vill visa på kortet väljer du **[!UICONTROL Select]** för att gå tillbaka till skärmen **[!UICONTROL Edit widget]**.

![Fälten som du lägger till på kortet markeras.](../images/profile-customization/add-widget-attributes.png)

När du återgår till skärmen **[!UICONTROL Edit widget]** bör listan med attribut på kortet återspegla dina val från föregående skärm. Du kan också ändra ordning på och ta bort kortattribut efter behov.

Om du vill spara ditt nya kort måste du först ange **[!UICONTROL Card title]**, sedan kan du välja **[!UICONTROL Save]** och slutföra kortskapandet.

![Den nya widgeten förhandsvisas i fönstret Redigera widget.](../images/profile-customization/new-widget.png)

När du har sparat återgår du till fliken **[!UICONTROL Detail]** där ditt nya kort och attribut visas.

## Återställ standardkort

Om du någon gång bestämmer dig för att du vill återställa standardkort som sedan dess har tagits bort, kan du snabbt och enkelt göra det. Välj först **[!UICONTROL Modify dashboard]** och sedan **[!UICONTROL Restore default cards]**. När standardkorten är synliga kan du välja **[!UICONTROL Save]** för att spara dina ändringar eller välja **[!UICONTROL Cancel]** om du inte vill återställa standardkorten.

![Knappen Återställ standardkort är markerad på profilkontrollpanelen.](../images/profile-customization/restore-default.png)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna uppdatera profilvyn för din organisation, inklusive lägga till och ta bort kort, redigera kortinformation och attribut samt ändra ordning på och storlek på kort. Mer information om hur du arbetar med [!DNL Profile]-data i Experience Platform-gränssnittet finns i [[!DNL Profile] användarhandboken](user-guide.md).
