---
keywords: Experience Platform;profil;kundprofil i realtid;användargränssnitt;gränssnitt;anpassning;profilinformation;information
title: Anpassning av profildetaljer i användargränssnittet
description: Den här guiden innehåller stegvisa instruktioner för hur kundprofildata i realtid visas i Adobe Experience Platform användargränssnitt.
topic-legacy: guide
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 681418b4198c2b1303fda937c3ffc60dad21b672
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] anpassning av detaljer {#profile-detail-customization}

I Adobe Experience Platform användargränssnitt kan du visa och interagera med [!DNL Real-time Customer Profile] data i form av kundprofiler. Profilinformationen som visas i användargränssnittet har sammanfogats från flera profilfragment till en enda vy över varje enskild kund. Detta inkluderar information som grundläggande attribut, länkade identiteter och kanalinställningar. Standardfälten som visas i profiler kan också ändras på organisationsnivå för att visa de som du föredrar [!DNL Profile] attribut. Den här handboken innehåller stegvisa instruktioner för hur du anpassar det sätt på vilket [!DNL Profile] data visas i plattformens användargränssnitt.

En fullständig guide till användargränssnittet för profiler finns på [Användargränssnittshandbok för profil](user-guide.md).

## Ändra ordning på och storlek på kort {#reorder-and-resize-cards}

Från **[!UICONTROL Detail]** fliken för kundprofilen kan du välja **[!UICONTROL Customize profile details]** för att ändra storlek på och ordna om befintliga kort.

![Knappen Anpassa profilinformation är markerad på profilkontrollpanelen.](../images/profile-customization/customize-profile-details.png)

När du har valt att ändra kontrollpanelen kan du ändra ordning på korten genom att markera korttiteln och dra och släppa korten i önskad ordning. Du kan också ändra storlek på ett kort genom att markera vinkelsymbolen i kortets nedre högra hörn (`⌟`) och dra kortet till önskad storlek. I det här exemplet **[!UICONTROL Basic attributes]** storleksändras.

![Knappen för storleksändring är markerad på attributkortet Grundläggande.](../images/profile-customization/resize.png)

Det valda kortet justeras till önskad storlek och omgivande kort flyttas dynamiskt. Detta kan medföra att vissa kort flyttas till ytterligare rader, vilket kräver att du rullar nedåt för att se alla kort. När till exempel[!UICONTROL Basic attributes]&quot; ändras storleken på kortet &quot;[!UICONTROL Linked identities]&quot;är inte längre synligt på den översta raden och visas nu på en ny andra rad i profilen (visas inte). Returnera &quot;[!UICONTROL Linked identities]&quot; till den översta raden kan du dra och släppa den i den aktuella positionen för &quot;[!UICONTROL Channel preferences]&quot;kort.

![Ett kort med ny storlek markeras.](../images/profile-customization/resized.png)

## Redigera och ta bort kort

Förutom att ändra storlek på och ordna om kort kan du redigera innehållet på vissa kort och ta bort vissa kort från kontrollpanelen helt. Markera ellipserna (`...`) i kortets övre högra hörn för att redigera eller ta bort det. Då öppnas en listruta med alternativ för att antingen redigera eller ta bort kortet, beroende på egenskaperna för det valda kortet.

>[!NOTE]
>
>Alla kort kan inte redigeras eller tas bort. Detta beror på att vissa kort innehåller skrivskyddad eller obligatorisk information. Om ett kort inte har några ellipser i det övre högra hörnet innehåller det skrivskyddad OCH nödvändig information och kan inte redigeras eller tas bort. Om ett kort har ovaler i hörnet och du markerar det visas endast ett alternativ för att ta bort kortet, är kortinformationen skrivskyddad och kan inte redigeras.

![Listrutan Redigera kort är markerad. Detta inkluderar alternativ för att redigera eller ta bort kortet.](../images/profile-customization/edit-card.png)

Välj **[!UICONTROL Edit]** i listrutan för att öppna **[!UICONTROL Edit widget]** på arbetsytan där du kan uppdatera kortets titel, ändra ordning på eller ta bort synliga attribut eller lägga till ytterligare attribut med **[!UICONTROL Add attributes]** -knappen.

![Kortet för grundläggande attribut visas.](../images/profile-customization/basic-attributes.png)

## Lägg till attribut {#add-attributes}

Från **[!UICONTROL Edit widget]** skärm, välja **[!UICONTROL Add attributes]** i kortets övre högra hörn för att börja lägga till attribut till kortet.

![Knappen Lägg till attribut på Basic-attributkortet markeras.](../images/profile-customization/add-attributes.png)

När **[!UICONTROL Select union schema field]** öppnas visas hela [!UICONTROL XDM Individual Profile] union-schema, med kapslade fält under. Mer information om fackliga scheman finns i [union av scheman i [!DNL Profile] användarhandbok](user-guide.md#union-schema).

The **[!UICONTROL Selected Attributes]** till höger i dialogrutan visar de attribut som finns på kortet som du redigerar. Du kan även ta bort och ändra ordning på attribut här. Det totala antalet valda attribut visas, liksom det maximala antalet attribut (20) som kan läggas till på ett kort.

![De attribut som för närvarande utgör attributen på kortet markeras.](../images/profile-customization/select-before.png)

Du kan välja något av de tillgängliga fackliga schemafälten för att anpassa attributen på kortet som du redigerar. Markerade fält visas med en bockmarkering bredvid sig och läggs automatiskt till i listan med valda attribut. När du har lagt till alla attribut som du vill visa på kortet väljer du **[!UICONTROL Select]** för att gå tillbaka till **[!UICONTROL Edit widget]** skärm.

![De nya attributen markeras.](../images/profile-customization/select-after.png)

När du återgår till **[!UICONTROL Edit widget]** visas listan med attribut på kortet. Du kan fortfarande ta bort eller ändra ordning på kortattributen eller redigera kortets titel efter behov. När redigeringarna är klara väljer du **[!UICONTROL Save]** för att spara ändringarna.

![De nya attributen visas på det redigerade kortet.](../images/profile-customization/new-attributes.png)

När du har sparat programmet återgår du till **[!UICONTROL Detail]** där det uppdaterade kortet och attributen visas.

![De nya attributen visas på kortet på kontrollpanelen Profil.](../images/profile-customization/added-attributes.png)

## Lägg till ett nytt kort {#add-a-new-card}

Om du vill anpassa utseendet på profiler i Experience Platform ytterligare kan du välja att lägga till nya kort på kontrollpanelen och välja de attribut som du vill visa på dessa kort. Börja genom att välja **[!UICONTROL Modify dashboard]** på **[!UICONTROL Detail]** -fliken.

![Knappen Anpassa profilinformation är markerad.](../images/profile-customization/customize-profile-details.png)

Nästa, välj **[!UICONTROL Add widget]** i det övre vänstra hörnet av kontrollpanelen.

![Knappen Lägg till widget är markerad.](../images/profile-customization/add-widget.png)

Om du väljer att lägga till ett nytt kort öppnas **[!UICONTROL Edit widget]** där du kan ange en titel för det nya kortet och välja de attribut som du vill att kortet ska visas. Om du vill lägga till attribut till kortet väljer du **[!UICONTROL Add attributes]**.

![Ett tomt nytt widgetkort visas i fönstret Redigera widget.](../images/profile-customization/edit-widget.png)

När **[!UICONTROL Select union schema field]** öppnas visas hela [!UICONTROL XDM Individual Profile] union och **[!UICONTROL Selected Attributes]** till höger i dialogrutan visar de attribut du väljer för kortet. Mer information om hur du lägger till attribut finns i [avsnitt om att lägga till attribut](#add-attributes) som visas tidigare i det här dokumentet.

Det totala antalet valda attribut visas, liksom det maximala antalet attribut (20) som kan läggas till på ett kort. Du kan också ta bort och ändra ordning på de valda attributen från den här skärmen. När du har lagt till alla attribut som du vill visa på kortet väljer du **[!UICONTROL Select]** för att gå tillbaka till **[!UICONTROL Edit widget]** skärm.

![Fälten som du lägger till på kortet markeras.](../images/profile-customization/add-widget-attributes.png)

När du återgår till **[!UICONTROL Edit widget]** på skärmen bör listan med attribut på kortet återspegla dina val från föregående skärm. Du kan också ändra ordning på och ta bort kortattribut efter behov.

Om du vill spara ditt nya kort måste du först ange en **[!UICONTROL Card title]** kan du välja **[!UICONTROL Save]** och slutföra processen för att skapa kort.

![Den nya widgeten förhandsvisas i fönstret Redigera widget.](../images/profile-customization/new-widget.png)

När du har sparat programmet återgår du till **[!UICONTROL Detail]** där ditt nya kort och attribut visas.

![Den nya widgeten läggs till på profilkontrollpanelen.](../images/profile-customization/added-widget.png)

## Återställ standardkort

Om du någon gång bestämmer dig för att du vill återställa standardkort som sedan dess har tagits bort, kan du snabbt och enkelt göra det. Välj först **[!UICONTROL Modify dashboard]** väljer **[!UICONTROL Restore default cards]**. När standardkorten visas kan du välja **[!UICONTROL Save]** för att spara ändringarna eller välja **[!UICONTROL Cancel]** om du inte vill återställa standardkorten.

![Knappen Återställ standardkort är markerad på kontrollpanelen Profil.](../images/profile-customization/restore-default.png)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna uppdatera profilvyn för din organisation, inklusive lägga till och ta bort kort, redigera kortinformation och attribut samt ändra ordning på och storlek på kort. Mer information om att arbeta med [!DNL Profile] data i användargränssnittet för Experience Platform, se [[!DNL Profile] användarhandbok](user-guide.md).
