---
keywords: Experience Platform;hantera taggar;taggar;
title: Hantera administrativa taggar
description: Det här dokumentet innehåller information om hur du hanterar administrativa taggar i Adobe Experience Cloud
source-git-commit: f184e94350a79936cbbd9072791650af99fa945f
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# Hantera taggar

Med taggar kan du hantera metadatataxonomier för att klassificera affärsobjekt så att de blir enklare att identifiera och kategorisera. Taggar kan hjälpa er att identifiera viktiga taxonomiska attribut för de målgrupper era team arbetar med, så att de kan hitta dem snabbare och även gruppera gemensamma målgrupper i en beskrivning. Du bör identifiera vanliga taggkategorier som geografiska regioner, affärsenheter, produktlinjer, projekt, team, tidsintervall (kvartal, månader, år) eller något annat som kan bidra till att ge ditt team en meningsfull upplevelse. 

## Skapa en tagg {#create-tag}

Om du vill skapa en ny tagg väljer du **[!UICONTROL tags]** i den vänstra navigeringen väljer du önskad taggkategori.

![Välj en taggkategori](./images/tag-selection.png)

Välj **[!UICONTROL Create tag]** för att skapa en ny tagg.

![Skapa en ny tagg](./images/new-tag.png)

The **[!UICONTROL Create tag]** visas och du uppmanas att ange ett unikt taggnamn. När du är klar väljer du **[!UICONTROL Save]**.

![Skapa taggdialogruta med nytt taggnamn](./images/create-tag-dialog.png)

Den nya taggen har skapats och du omdirigeras till taggskärmen där du ser den nyligen skapade taggen i listan.

![Tagg som nyligen skapats för taggkategorin](./images/new-tag-listed.png)

## Redigera en tagg {#edit-tag}

Om du redigerar en tagg blir det lättare att felstava, uppdatera namnkonventioner eller terminologi. Om du redigerar en tagg behålls taggens koppling till de objekt där de används.

Om du vill redigera en befintlig tagg väljer du ellipsen i listan med taggkategorier (`...`) bredvid taggens namn som du vill redigera. I en listruta visas kontroller för att redigera, flytta eller arkivera taggen. Välj **[!UICONTROL Edit]** i listrutan.

![Redigeringsåtgärden som visas i listrutan](./images/edit-action.png)

The **[!UICONTROL Edit tag]** visas och du uppmanas att redigera taggnamnet. När du är klar väljer du **[!UICONTROL Save]**.

![Redigera taggdialogruta med uppdaterat taggnamn](./images/edit-dialog.png)

Taggnamnet har uppdaterats och du omdirigeras till taggskärmen där den uppdaterade taggen visas i listan.

![Uppdaterad tagg för taggkategorin](./images/updated-tag-listed.png)

## Flytta en tagg mellan kategorier {#move-tag}

Taggar kan flyttas till andra taggkategorier. Om du flyttar en tagg behålls taggens koppling till de objekt där de används.

Om du vill flytta en befintlig tagg väljer du ellipsen i listan med taggkategorier (`...`) bredvid taggens namn som du vill flytta. I en listruta visas kontroller för att redigera, flytta eller arkivera taggen. Välj **[!UICONTROL Edit]** i listrutan.

![Flyttåtgärd som visas i listrutan](./images/move-action.png)

The **[!UICONTROL Move tag]** öppnas en dialogruta där du uppmanas att välja den taggkategori som den markerade taggen ska flyttas till.

Du kan bläddra och välja i listan, eller också kan du använda sökfunktionen för att ange kategorinamnet. När du är klar väljer du **[!UICONTROL Move]**.

![Flytta en dialogruta med sökvillkor för att hitta taggkategorin](./images/move-dialog.png)

Taggen har flyttats och du omdirigeras till taggskärmen där du ser den uppdaterade tagglistan, där taggen inte längre visas.

![Uppdaterad tagglista för den aktuella taggkategorin](./images/current-tag-category.png)

Taggen visas nu i den tidigare markerade taggkategorin.

![Tagglista för den markerade taggkategorin som ska flyttas](./images/moved-to-tag-category.png)

## Arkivera en tagg {#archive-tag}

Status för en tagg kan växlas mellan aktiv och arkiverad. Arkiverade taggar tas inte bort från objekt där de redan har tillämpats, men de kan inte längre tillämpas på nya objekt. För varje tagg återspeglas samma status i alla objekt. Detta är särskilt användbart när du vill behålla aktuella taggobjektsassociationer men inte vill att taggen ska användas i framtiden.

Om du vill arkivera en befintlig tagg markerar du ellipsen i listan med taggkategorier (`...`) bredvid taggens namn som du vill arkivera. I en listruta visas kontroller för att redigera, flytta eller arkivera taggen. Välj **[!UICONTROL Archive]** i listrutan.

![Arkivåtgärd som visas i listrutan](./images/archive-action.png)

The **[!UICONTROL Archive tag]** visas och du uppmanas att bekräfta taggarkivet. Välj **[!UICONTROL Archive]**.

![Dialogrutan Arkivera tagg med en bekräftelse](./images/archive-dialog.png)

Taggen har arkiverats och du omdirigeras till taggskärmen. Den uppdaterade tagglistan visar nu taggens status som `Archived`.

![Uppdaterad tagglista för den aktuella taggkategorin som visar taggen som arkiverad](./images/archive-status.png)

## Återställa en arkiverad tagg {#restore-archived-tag}

Om du vill använda en `Archived` tagga till nya objekt, taggen måste finnas i `Active` tillstånd. Om du återställer en arkiverad tagg återgår taggen till den `Active` tillstånd.

Om du vill återställa en arkiverad tagg markerar du ellipsen i listan med taggkategorier (`...`) bredvid taggens namn som du vill återställa. I en listruta visas kontroller för att återställa eller ta bort taggen. Välj **[!UICONTROL Restore]** i listrutan.

![Återställningsåtgärd som visas i listrutan](./images/restore-action.png)

The **[!UICONTROL Restore tag]** visas en uppmaning om att bekräfta taggåterställningen. Välj **[!UICONTROL Restore]**.

![Dialogrutan Återställ tagg där en bekräftelse begärs](./images/restore-dialog.png)

Taggen har återställts och du omdirigeras till taggskärmen. Den uppdaterade tagglistan visar nu taggens status som `Active`.

![Uppdaterad tagglista för den aktuella taggkategorin som visar taggen som aktiv](./images/restored-active-status.png)

## Ta bort en tagg {#delete-tag}

>[!NOTE]
>
>Endast taggar som finns i en `Archived` och inte är kopplade till några objekt kan tas bort.

Om du tar bort en tagg tas den bort helt från systemet.

Om du vill ta bort en arkiverad tagg markerar du ellipsen i listan med taggkategorier (`...`) bredvid taggens namn som du vill ta bort. I en listruta visas kontroller för att återställa eller ta bort taggen. Välj **[!UICONTROL Delete]** i listrutan.

![Ta bort åtgärd som visas i listrutan](./images/delete-action.png)

The **[!UICONTROL Delete tag]** visas och du uppmanas att bekräfta borttagningen av taggen. Välj **[!UICONTROL Delete]**.

![Ta bort taggdialogrutan och begär bekräftelse](./images/delete-dialog.png)

Taggen har tagits bort och du omdirigeras till taggskärmen. Taggen visas inte längre i listan och har tagits bort helt.

![Uppdaterad tagglista för den aktuella taggkategorin som visar taggen visas inte längre i listan](./images/deleted-updated-list.png)

## Visa taggade objekt {#view-tagged}

Varje tagg har en detaljsida som kan nås från tagglagret. På den här sidan visas alla objekt som för närvarande har den taggen, vilket gör att användare kan se relaterade objekt från olika program och funktioner i en enda vy.

Om du vill visa listan med taggade objekt söker du efter taggen i en taggkategori och markerar taggen.

![Tagga markeringen i taggkategorin](./images/view-tag-selection.png)

The [!UICONTROL Tagged objects] visas en lista med taggade objekt.

![Lager med taggade objekt](./images/tagged-objects.png)

## Nästa steg

Du har nu lärt dig hur du hanterar taggar. En översikt över taggarna i Experience Platform finns på [taggöversikt dokumentation](../overview.md).
