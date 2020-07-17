---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Användarhandbok för sammanslagningsprinciper
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 0%

---


# Användarhandbok för sammanslagningsprinciper

Med Adobe Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn.

Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Den här handboken innehåller stegvisa instruktioner för hur du arbetar med sammanfogningsprinciper i användargränssnittet i Adobe Experience Platform.

Om du föredrar att arbeta med sammanfogningsprinciper med hjälp av [!DNL Real-time Customer Profile] API:t följer du instruktionerna i API-självstudiekursen för [sammanfogningsprinciper](../api/merge-policies.md).

## Komma igång

Den här guiden kräver en fungerande förståelse av de olika [!DNL Experience Platform] tjänsterna som är kopplade till sammanslagningsprinciper. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

* [!DNL Real-time Customer Profile](../home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [!DNL Identity Service](../../identity-service/home.md): Möjliggör [!DNL Real-time Customer Profile] genom att överbrygga identiteter från olika datakällor som inhämtas till [!DNL Platform].
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.

## Visa kopplingsprinciper

I användargränssnittet kan du börja arbeta med sammanfogningsprinciper och se en lista över organisationens befintliga sammanfogningsprinciper genom att klicka [!DNL Experience Platform] i den vänstra listen och sedan välja **[!UICONTROL Profile]** **[!UICONTROL Merge policies]** fliken.

![Landningssida för sammanslagningspolicyer](../images/merge-policies/landing.png)

Information om alla kopplingsregler som är tillgängliga för din organisation finns på landningssidan, inklusive *[!UICONTROL Policy Name]*, *[!UICONTROL Default Merge Policy]* och *[!UICONTROL Schema]*.

Om du vill välja vilka detaljer som ska visas, eller om du vill lägga till fler kolumner till visningen, markerar du kolumnvalsikonen till höger och klickar på ett kolumnnamn för att lägga till eller ta bort det från vyn.

![](../images/merge-policies/adjust-view.png)

## Skapa en kopplingsprofil

Om du vill skapa en ny sammanfogningsprincip klickar du på **[!UICONTROL Create merge policy]** uppe till höger på **[!UICONTROL Merge policies]** fliken.

![Landningssida för sammanslagningspolicyer](../images/merge-policies/create-new.png)

Skärmen visas så att du kan ange viktig information för den nya sammanfogningsprincipen **[!UICONTROL Create merge policy]** .

![](../images/merge-policies/create.png)

* **[!UICONTROL Name]**: Namnet på sammanfogningsprincipen ska vara beskrivande men koncist.
* **[!UICONTROL Schema]**: Schemat som är associerat med sammanfogningsprincipen. Detta anger XDM-schemat som sammanfogningsprincipen skapas för. Organisationer kan skapa flera sammanfogningsprinciper per per schema.
* **[!UICONTROL ID stitching]**: I det här fältet definieras hur en kunds relaterade identiteter ska fastställas. Det finns två möjliga värden:
   * **[!UICONTROL None]**: Utför ingen identitetssammanfogning.
   * **[!UICONTROL Private Graph]**: Utför identitetssammanfogning baserat på ditt privata identitetsdiagram.
* **[!UICONTROL Attribute merge]**: Ett profilfragment är profilinformationen för endast en identitet från listan över identiteter som finns för en enskild kund. När typen av identitetsdiagram som används resulterar i mer än en identitet, finns det en risk för att egenskapsvärden för profiler som står i konflikt med varandra, och prioritet måste anges. Om du använder *attributsammanfogning* kan du ange vilka datamängdsprofilvärden som ska prioriteras om en sammanfogningskonflikt inträffar. Det finns två möjliga värden:
   * **[!UICONTROL Timestamp ordered]**: Om det uppstår en konflikt ska du prioritera profilen som uppdaterades senast.
   * **[!UICONTROL Dataset precedence]** : Prioritera profilfragment baserat på den datauppsättning som de kommer från. När du väljer det här alternativet måste du välja relaterade datauppsättningar och deras prioritetsordning. Mer information finns i informationen om [datauppsättningsprioritet](#dataset-precedence) nedan.
* **[!UICONTROL Default merge policy]**: En växlingsknapp som gör att du kan välja om sammanfogningsprincipen ska vara standard för din organisation eller inte. Om väljaren är aktiverad och den nya profilen sparas, uppdateras din tidigare standardprofil automatiskt till att inte längre vara standard.

### Datauppsättningsprioritet {#dataset-precedence}

När du väljer ett *[!UICONTROL Attribute merge]* värde kan du välja *[!UICONTROL Dataset precedence]* vilket gör att du kan prioritera profilfragment baserat på den datauppsättning som de kommer från.

Ett exempel är om din organisation har information i en datauppsättning som är att föredra eller lita på framför data i en annan datauppsättning.

När du markerar *[!UICONTROL Dataset precedence]*&#x200B;öppnas en separat panel där du måste välja *[!UICONTROL Available datasets]* (eller markera alla) vilka datauppsättningar som ska inkluderas. Du kan sedan dra och släppa datauppsättningarna på *[!UICONTROL Selected Datasets]* panelen och dra dem till rätt prioritetsordning. Den översta datauppsättningen får högsta prioritet, den andra datauppsättningen får näst högsta prioritet och så vidare.

![](../images/merge-policies/dataset-precedence.png)

När du är klar med sammanfogningsprincipen klickar du på **[!UICONTROL Save]** för att gå tillbaka till den *[!UICONTROL Merge policies]* flik där den nya sammanfogningsprincipen nu visas i listan över profiler.

## Redigera en kopplingsprofil

Du kan ändra en befintlig kopplingsprofil på *[!UICONTROL Merge policies]* fliken genom att klicka på *[!UICONTROL Policy Name]* för den kopplingsprofil som du vill redigera.

![Landningssida för sammanslagningspolicyer](../images/merge-policies/select-edit.png)

När *[!UICONTROL Edit merge policy]* skärmen visas kan du ändra *[!UICONTROL Name]*, *[!UICONTROL Schema]*, *[!UICONTROL ID stitching]* typ och *[!UICONTROL Attribute merge]* typ samt välja om profilen ska användas *[!UICONTROL Default merge policy]* för din organisation eller inte.

>[!Note]
>Du kan inte redigera sammanfogningsprincip-ID:t, som visas högst upp på redigeringsskärmen. Detta är ett skrivskyddat, systemgenererat ID som inte kan ändras.

![](../images/merge-policies/edit-screen.png)

När du har gjort de nödvändiga ändringarna klickar du för **[!UICONTROL Save]** att gå tillbaka till den *[!UICONTROL Merge policies]* flik där den uppdaterade informationen om sammanfogningsprincipen visas.

![](../images/merge-policies/edited.png)

## Policyöverträdelser för datastyrning

När du skapar eller uppdaterar en sammanfogningsprincip görs en kontroll för att avgöra om sammanfogningsprincipen bryter mot någon av de dataanvändningsprinciper som din organisation har definierat. Dataanvändningspolicyer är en del av Adobe Experience Platform [!DNL Data Governance] och är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från, för att utföra på specifika [!DNL Platform] data. Om en sammanfogningsprincip till exempel användes för att skapa ett segment som aktiverats för ett tredjepartsmål, och din organisation har en dataanvändningsprincip som förhindrar export av specifika data till tredje part, får du ett meddelande om att en datastyrningsprincip överträds när du försöker spara sammanfogningsprincipen.

Det här meddelandet innehåller en lista över dataanvändningsprinciper som har överträtts och gör att du kan visa information om överträdelsen genom att välja en princip i listan. När du har valt en obehörig princip innehåller fliken *Datalinje* en beskrivning av *orsaken till överträdelse* och de aktiveringar *som* påverkas, där var och en ger mer information om hur dataanvändningsprincipen har överträtts.

Om du vill veta mer om hur datastyrning utförs i Adobe Experience Platform börjar du med att läsa [datastyrningsöversikten](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Nästa steg

Nu när du har skapat och konfigurerat sammanfogningsprinciper för din IMS-organisation kan du använda dem för att skapa målgruppssegment utifrån dina profildata. Mer information om hur du skapar och arbetar med segment med finns i [Segmenteringsöversikten](../../segmentation/home.md) [!DNL Experience Platform].