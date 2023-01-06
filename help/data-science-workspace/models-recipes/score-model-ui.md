---
keywords: Experience Platform;göra poäng i en modell;Data Science Workspace;populära topics;ui;poäng run;scoring results
solution: Experience Platform
title: Posta en modell i användargränssnittet för datavetenskapen
type: Tutorial
description: Du kan göra poängsättningen i Adobe Experience Platform Data Science Workspace genom att mata in indata i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Visa en modell i gränssnittet för datavetenskapen

Poäng i Adobe Experience Platform [!DNL Data Science Workspace] kan uppnås genom att mata in indata i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp.

I den här självstudiekursen visas de steg som krävs för att göra en modell i [!DNL Data Science Workspace] användargränssnitt.

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform]. Om du inte har tillgång till en IMS-organisation i [!DNL Experience Platform]bör du kontakta systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en utbildad modell. Om du inte har någon tränad modell följer du [utbilda och utvärdera en modell i användargränssnittet](./train-evaluate-model-ui.md) självstudiekurs innan du fortsätter.

## Skapa en ny poängkörning

En bedömningsrunda skapas med optimerade konfigurationer från en tidigare slutförd och utvärderad utbildningskurs. Uppsättningen optimala konfigurationer för en modell bestäms vanligtvis genom att man granskar utvärderingsvärden för utbildningskörning.

Hitta den bästa kursen för att använda dess konfigurationer för poängsättning. Öppna sedan kursen genom att markera hyperlänken som är kopplad till namnet.

![Välj utbildningskurs](../images/models-recipes/score/select-run.png)

Från kursen **[!UICONTROL Evaluation]** flik, välja **[!UICONTROL Score]** som finns längst upp till höger på skärmen. Ett nytt bedömningsarbetsflöde börjar.

![](../images/models-recipes/score/training_run_overview.png)

Välj datamängden för indataskalförändring och välj **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_input.png)

Välj datauppsättningen för resultaträkning, det här är den dedikerade utdatamängden där poängsättningsresultaten lagras. Bekräfta markeringen och välj **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_results.png)

I det sista steget i arbetsflödet uppmanas du att konfigurera din poängkörning. Dessa konfigurationer används av modellen för poängkörningen.
Observera att du inte kan ta bort ärvda parametrar som angavs när modellerna skapades. Du kan redigera eller återställa icke ärvda parametrar genom att dubbelklicka på värdet eller välja återställningsikonen när du håller markören över posten.

![konfiguration](../images/models-recipes/score/configuration.png)

Granska och bekräfta poängkonfigurationerna och välj **[!UICONTROL Finish]**  för att skapa och köra poängkörningen. Du dirigeras till **[!UICONTROL Scoring Runs]** och den nya poängsättningen körs med **[!UICONTROL Pending]** visas.

![resultatfliken](../images/models-recipes/score/scoring_runs_tab.png)

En bedömningskörning kan visas med någon av följande statusar:
- Väntande
- Slutförd
- Misslyckades
- Körs

Status uppdateras automatiskt. Fortsätt till nästa steg om statusen är **[!UICONTROL Complete]** eller **[!UICONTROL Failed]**.

## Visa poängresultat

Om du vill visa poängresultat börjar du med att välja en utbildningskurs.

![Välj utbildningskurs](../images/models-recipes/score/select-run.png)

Du omdirigeras till utbildningskörningarna **[!UICONTROL Evaluation]** sida. I närheten av den övre delen av sidan för utvärdering av utbildningskörning väljer du **[!UICONTROL Scoring Runs]** om du vill visa en lista med befintliga poängserier.

![utvärderingssida](../images/models-recipes/score/view_scoring_runs.png)

Välj sedan en poängkörning för att visa körningsinformationen.

![körningsinformation](../images/models-recipes/score/view_details.png)

Om den valda betygskörningen har statusen antingen Slutförd eller Misslyckad, visas **[!UICONTROL View Activity Logs]** länken är tillgänglig. Om en poängkörning misslyckas kan körningsloggarna ge användbar information för att fastställa orsaken till felet. Om du vill hämta körningsloggarna väljer du **[!UICONTROL View Activity Logs]**.

![Välj visningsloggar](../images/models-recipes/score/view_logs.png)

The **[!UICONTROL View activity logs]** popover visas. Välj en URL för att automatiskt hämta de associerade loggarna.

![](../images/models-recipes/score/activity_logs.png)

Du kan också visa dina poängresultat genom att välja  **[!UICONTROL Preview scoring results dataset]**.

![Välj förhandsgranskningsresultat](../images/models-recipes/score/view_results.png)

En förhandsgranskning av utdatamängden tillhandahålls.

![förhandsgranskningsresultat](../images/models-recipes/score/preview_results.png)

För alla poängresultat väljer du **[!UICONTROL Scoring Results Dataset]** -länk hittades i den högra kolumnen.

## Nästa steg

Den här självstudiekursen gick dig igenom stegen för att få fram data med hjälp av en utbildad modell i [!DNL Data Science Workspace]. Följ självstudiekursen på [publicera en modell som en tjänst i användargränssnittet](./publish-model-service-ui.md) för att ge användare i organisationen möjlighet att få poäng på data genom att ge enkel åtkomst till en maskininlärningstjänst.
