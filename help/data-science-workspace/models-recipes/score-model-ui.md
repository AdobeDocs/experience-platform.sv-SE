---
keywords: Experience Platform;göra en modellpoäng;Data Science Workspace;populära ämnen;ui;poängsättning;poängresultat
solution: Experience Platform
title: Skapa en modell i användargränssnittet för datavetenskap i Workspace
type: Tutorial
description: Du kan göra en bedömning i Adobe Experience Platform Data Science Workspace genom att mata in indata i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Visa en modell i användargränssnittet för datavetenskap i Workspace

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

Du kan göra poängsättningen i Adobe Experience Platform [!DNL Data Science Workspace] genom att mata in indata i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp.

I den här självstudiekursen visas de steg som krävs för att göra en modell i användargränssnittet för [!DNL Data Science Workspace].

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform] för att kunna slutföra den här självstudiekursen. Om du inte har åtkomst till en organisation i [!DNL Experience Platform], ska du tala med systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en utbildad modell. Om du inte har någon tränad modell följer du [tåget och utvärderar en modell i självstudiekursen ](./train-evaluate-model-ui.md) innan du fortsätter.

## Skapa en ny poängkörning

En bedömningsrunda skapas med optimerade konfigurationer från en tidigare slutförd och utvärderad utbildningskurs. Uppsättningen optimala konfigurationer för en modell bestäms vanligtvis genom att man granskar utvärderingsvärden för utbildningskörning.

Hitta den mest optimala kursen för att använda dess konfigurationer för poängsättning. Öppna sedan kursen genom att markera hyperlänken som är kopplad till namnet.

![Välj utbildningskörning](../images/models-recipes/score/select-run.png)

Välj **[!UICONTROL Score]** som finns högst upp till höger på skärmen på fliken **[!UICONTROL Evaluation]** i utbildningskörningen. Ett nytt bedömningsarbetsflöde börjar.

![](../images/models-recipes/score/training_run_overview.png)

Välj datauppsättningen för indataskörning och välj **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_input.png)

Välj datauppsättningen för resultaträkning, det här är den dedikerade utdatamängden där poängsättningsresultaten lagras. Bekräfta ditt val och välj **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_results.png)

I det sista steget i arbetsflödet uppmanas du att konfigurera din poängkörning. Dessa konfigurationer används av modellen för poängkörningen.
Observera att du inte kan ta bort ärvda parametrar som angavs när modellerna skapades. Du kan redigera eller återställa icke ärvda parametrar genom att dubbelklicka på värdet eller välja återställningsikonen när du håller markören över posten.

![konfiguration](../images/models-recipes/score/configuration.png)

Granska och bekräfta poängkonfigurationerna och välj **[!UICONTROL Finish]** för att skapa och köra poängkörningen. Du dirigeras till fliken **[!UICONTROL Scoring Runs]** och den nya poängsättningen som körs med statusen **[!UICONTROL Pending]** visas.

![poäng kör flik](../images/models-recipes/score/scoring_runs_tab.png)

En bedömningskörning kan visas med någon av följande statusar:
- Väntande
- Complete
- Misslyckades
- Körs

Status uppdateras automatiskt. Fortsätt till nästa steg om statusen är **[!UICONTROL Complete]** eller **[!UICONTROL Failed]**.

## Visa poängresultat

Om du vill visa poängresultat börjar du med att välja en utbildningskurs.

![Välj utbildningskörning](../images/models-recipes/score/select-run.png)

Du omdirigeras till sidan **[!UICONTROL Evaluation]** för utbildningskörningar. Långt upp på sidan för utvärdering av utbildningskörning väljer du fliken **[!UICONTROL Scoring Runs]** om du vill visa en lista över befintliga poängsättningar.

![utvärderingssida](../images/models-recipes/score/view_scoring_runs.png)

Välj sedan en poängkörning för att visa körningsinformationen.

![körningsinformation](../images/models-recipes/score/view_details.png)

Om den valda poängkörningen har statusen Slutförd eller Misslyckad, blir länken **[!UICONTROL View Activity Logs]** tillgänglig. Om en poängkörning misslyckas kan körningsloggarna ge användbar information för att fastställa orsaken till felet. Om du vill hämta körningsloggarna väljer du **[!UICONTROL View Activity Logs]**.

![Välj visningsloggar](../images/models-recipes/score/view_logs.png)

**[!UICONTROL View activity logs]**-pekaren visas. Välj en URL för att automatiskt hämta de associerade loggarna.

![](../images/models-recipes/score/activity_logs.png)

Du kan också visa dina poängresultat genom att välja **[!UICONTROL Preview scoring results dataset]**.

![Välj förhandsgranskningsresultat](../images/models-recipes/score/view_results.png)

En förhandsgranskning av utdatamängden tillhandahålls.

![förhandsgranskningsresultat](../images/models-recipes/score/preview_results.png)

För den fullständiga uppsättningen poängresultat väljer du länken **[!UICONTROL Scoring Results Dataset]** som finns i den högra kolumnen.

## Nästa steg

Den här självstudiekursen gick igenom stegen för att göra poäng för data med hjälp av en tränad modell i [!DNL Data Science Workspace]. Följ självstudiekursen [Publicera en modell som en tjänst i användargränssnittet](./publish-model-service-ui.md) för att göra det möjligt för användare i organisationen att få poäng genom att ge enkel åtkomst till en maskininlärningstjänst.
