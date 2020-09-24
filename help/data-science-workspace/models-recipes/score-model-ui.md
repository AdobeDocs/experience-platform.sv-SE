---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics;ui;scoring run;scoring results
solution: Experience Platform
title: Skapa en modell (UI)
topic: tutorial
type: Tutorial
description: 'Du kan göra poängsättningen i Adobe Experience Platform Data Science Workspace genom att mata in indata i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp. '
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Skapa en modell (UI)

Du kan göra poängsättningen i Adobe Experience Platform [!DNL Data Science Workspace] genom att mata in indata i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp.

I den här självstudiekursen visas de steg som krävs för att göra en modell i [!DNL Data Science Workspace] användargränssnittet.

## Komma igång

Du måste ha tillgång till den här självstudiekursen för att kunna slutföra den [!DNL Experience Platform]. Om du inte har tillgång till en IMS-organisation i [!DNL Experience Platform]kontaktar du systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en utbildad modell. Om du inte har någon tränad modell följer du [tåget och utvärderar en modell i självstudiekursen för användargränssnittet](./train-evaluate-model-ui.md) innan du fortsätter.

## Skapa en ny poängkörning

En bedömningsrunda skapas med optimerade konfigurationer från en tidigare slutförd och utvärderad utbildningskurs. Uppsättningen optimala konfigurationer för en modell bestäms vanligtvis genom att man granskar utvärderingsvärden för utbildningskörning.

1. Hitta den bästa kursen för att använda dess konfigurationer för poängsättning. Öppna önskad utbildningskurs genom att klicka på namnet.

2. Klicka på **[!UICONTROL Evaluation]** **[!UICONTROL Score]** knappen längst upp till höger på skärmen på fliken Utbildningskörning. Detta kommer att starta ett nytt arbetsflöde för *att köra poängberäkning* .
   ![](../images/models-recipes/score/training_run_overview.png)

3. Markera datamängden för indataskalförändring och klicka på **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. Välj datauppsättningen för resultaträkning, det här är den dedikerade utdatamängden där poängsättningsresultaten lagras. Confirm your selection and click **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. I det sista steget i arbetsflödet uppmanas du att konfigurera din poängkörning. Dessa konfigurationer används av modellen för poängkörningen.
Observera att du inte kan ta bort ärvda parametrar som angavs när modellen skapades. Du kan redigera eller återställa icke ärvda parametrar genom att dubbelklicka på värdet eller klicka på återställningsikonen när du håller markören över posten.
   ![](../images/models-recipes/score/configuration.png)
Granska och bekräfta poängkonfigurationerna och klicka på **[!UICONTROL Finish]** för att skapa och köra poängkörningen. Du dirigeras till **[!UICONTROL Scoring Runs]** fliken och den nya poängsättningen visas med en status.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
I en bedömningsrunda visas någon av följande fyra statusvärden: Väntande, Fullständigt, Misslyckades eller Körs och uppdateras automatiskt. Fortsätt till nästa steg om statusen är antingen Slutförd eller Misslyckad.

## Visa poängresultat

1. Hitta den utbildningskörning som användes för poängsättningen och klicka på namnet för att visa **[!UICONTROL Evaluation]** sidan.

2. Längst upp på sidan för utvärdering av utbildningskörning klickar du på **[!UICONTROL Scoring Runs]** fliken för att visa en lista över befintliga poängsättningar. Klicka på poänglistan för att visa informationen i den högra kolumnen.
   ![](../images/models-recipes/score/view_details.png)

3. Om den valda poängkörningen har statusvärdet &quot;Slutförd&quot; eller &quot;Misslyckad&quot;, är den **[!UICONTROL View Activity Logs]** länk som finns i den högra kolumnen aktiv. Klicka på länken för att visa eller hämta körningsloggarna. Om en poängkörning misslyckades kan körningsloggarna ge användbar information för att fastställa orsaken till felet.
   ![](../images/models-recipes/score/activity_logs.png)

4. Klicka på **[!UICONTROL Preview Scoring Results Dataset]** länken i den högra kolumnen. Du kan se en förhandsvisning av utdata från poängkörningen.
   ![](../images/models-recipes/score/preview_results.png)

5. Klicka på länken i den högra kolumnen om du vill se hela uppsättningen poängresultat. **[!UICONTROL Scoring Results Dataset]**

## Nästa steg

I den här självstudiekursen steg för steg visades data med hjälp av en tränad modell i [!DNL Data Science Workspace]. Följ självstudiekursen om hur du [publicerar en modell som en tjänst i användargränssnittet](./publish-model-service-ui.md) för att göra det möjligt för användare i organisationen att få poäng på data genom att ge enkel åtkomst till en maskininlärningstjänst.
