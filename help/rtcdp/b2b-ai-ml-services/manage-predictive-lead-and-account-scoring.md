---
title: Hantera prediktiv lead- och kontobedömning i Real-Time CDP B2B
type: Documentation
description: Det här dokumentet innehåller information om hur du hanterar funktionen för prediktiv lead och kontobedömning i Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 2%

---

# Hantera prediktiv lead- och kontobedömning i Adobe Real-time Customer Data Platform, B2B Edition

>[!NOTE]
>
>Endast användare med behörigheten Hantera B2B AI kan skapa, ändra och ta bort poängmål.

I den här självstudiekursen får du hjälp med att hantera poängmål för den prediktiva lead- och kontopoängstjänsten. Poängmålen kan vara antingen för personprofilen eller kontoprofilen

## Skapa ett nytt musikspår

Om du vill skapa en ny bakgrundsmusik markerar du **[!UICONTROL Services]** i sidlisten och väljer **[!UICONTROL Create score]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

Skärmen **[!UICONTROL Basic information]** visas och du uppmanas att välja en profiltyp, ange ett namn och en valfri beskrivning. När du är klar väljer du **[!UICONTROL Next]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

Skärmen **[!UICONTROL Define your goal]** visas. Välj listrutepilen och välj sedan en måltyp i listrutan som visas.

![plas-select-a-target](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

Dialogrutan **[!UICONTROL Goal specifics]** öppnas. Markera listrutepilen och välj sedan målfältets namn i listrutan som visas.

![plas-select-a-target-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

Markeringen **[!UICONTROL Goal conditions]** visas. Markera listrutepilen och välj sedan ett villkor i listrutan som visas.

![plas-target-specific-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

Fältet **[!UICONTROL Goal value]** visas. Konfigurera sedan din [!UICONTROL Goal specifics]. Välj panelen [!UICONTROL Enter Field Value] och ange ditt målvärde.

>[!NOTE]
>
>Flera målvärden kan läggas till.

![plas-target-specific-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Om du vill lägga till fler fält väljer du **[!UICONTROL Add field]**.

![plas-target-specific-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Om du vill konfigurera tidsramen för förutsägelse väljer du listrutepilen och väljer sedan önskad tidsram.

![plas-predication-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

Den valda sammanfogningsprincipen avgör hur fältvärdena för en personprofil markeras. Använd listrutepilen och välj önskad kopplingsprofil och välj sedan **[!UICONTROL Finish]**.

Dialogrutan **[!UICONTROL Scoring setup is complete]** visas som bekräftar att det nya poängtalet har skapats. Välj **[!UICONTROL OK]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Det kan ta upp till 24 timmar för varje poängprocess att slutföra.

Du återgår till fliken **[!UICONTROL Services]** där du kan se det nya resultatet som har skapats i listan med bakgrundsmusik.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Välj bakgrundsmusik om du vill visa information och ytterligare information om den senaste körningen.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Mer detaljerad information om felkoder som kan visas under den senaste körningen finns i avsnittet [leads AI-pipeline-felkoder](#leads-ai-pipeline-error-codes) i det här dokumentet.

## Redigera ett musikspår

Om du vill redigera ett musikspår väljer du ett musikspår på fliken **[!UICONTROL Services]** och väljer **[!UICONTROL Edit]** på panelen med ytterligare information till höger på skärmen.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

Dialogrutan **[!UICONTROL Edit instance]** visas där du kan redigera beskrivningen för poängen. Gör ändringarna och välj **[!UICONTROL Save]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>Det går inte att ändra poängkonfigurationen eftersom detta kommer att utlösa omskolning och ompoängtering av modellen. Det motsvarar att ta bort poängen och skapa en ny poäng. Om du vill redigera konfigurationen av poängen måste du klona poängen eller skapa en ny poäng.

Du återgår till fliken **[!UICONTROL Services]**. Välj bakgrundsmusik om du vill visa den uppdaterade beskrivningsinformationen på panelen med ytterligare information till höger på skärmen.

## Klona en poäng

Om du vill klona ett musikspår väljer du ett musikspår på fliken **[!UICONTROL Services]** och väljer **[!UICONTROL Clone]** på panelen med ytterligare information till höger på skärmen.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

Skärmen **[!UICONTROL Basic information]** visas. Profiltypen, namnet och beskrivningen klonas från det ursprungliga resultatet. Ändra informationen och välj **[!UICONTROL Next]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

Skärmen **[!UICONTROL Define your goal]** visas. Slutför målavsnittet på samma sätt som när du skapar en ny poäng och välj **[!UICONTROL Finish]**.

Du återgår till fliken **[!UICONTROL Services]** där du kan se det nya klonade poängen i listan.

>[!NOTE]
>
>Avsnittet **[!UICONTROL Define your goal]** är inte klonat från det ursprungliga poängtalet.

## Ta bort ett musikspår

Om du vill ta bort ett musikspår väljer du ett musikspår på fliken **[!UICONTROL Services]** och väljer **[!UICONTROL Delete]** på panelen med ytterligare information till höger på skärmen.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

Bekräftelsedialogrutan **[!UICONTROL Delete documentation]** visas. Välj **[!UICONTROL Delete]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>Om du tar bort poängdefinitionen tas även alla prediktiva poäng i personprofilen eller kontoprofilen bort, men inte fältgruppen som skapats för poängdefinitionen. Fältgruppen lämnas &quot;överbliven&quot; i datamodellen.

Du återgår till fliken **[!UICONTROL Services]** där du inte längre kan se poängen i listan.

## Leads-AI-pipeline-felkoder

| Felkod | Felmeddelande |
| --- | --- |
| 401 | FEL 401. Leads-AI-pipeline har stoppats: det finns inte tillräckligt med giltiga konton för kontopoängsättningen. Antal konton: {}. |
| 402 | FEL 402. Leads-AI-pipeline har stoppats: det finns inte tillräckligt med giltiga kontakter för kontaktbedömning. Antal kontakter: {}. |
| 403 | FEL 403. Leads-AI-pipeline stoppades: det finns inte tillräckligt med aktivitetsvolym för modellutbildning. Antal händelser: {}. |
| 404 | FEL 404. Ledarnas AI-pipeline stoppades: inte tillräckligt många konverteringar för modellutbildning. Antal konverteringar: {}. |
| 405 | FEL 405. Leads-AI-pipeline stoppades: aktiviteten är för sparsam för giltig modellutbildning. Endast {} procent av kontona har aktivitet. |
| 406 | FEL 406. Leads-AI-pipeline stoppades: aktiviteten är för sparsam för giltig modellutbildning. Endast {} procent av kontakterna har aktivitet. |
| 407 | FEL 407. Leads-AI-pipeline har stoppats: typer av bedömningsdataaktiviteter matchar inte utbildningsdata. |
| 408 | FEL 408. Leads-AI-pipeline har stoppats: Frekvensen som saknas är för hög för aktivitetsfunktioner. Frekvens saknas: {}. |
| 409 | FEL 409. Leads-AI-pipeline stoppades: test auc är för lågt. Testa auc: {}. |
| 410 | FEL 410. Leads-AI-pipeline stoppades: test auc är för lågt efter parameterjustering. Testa auc: {}. |
| 411 | FEL 411. Ledarnas AI-pipeline har stoppats: utbildningsdata har inte tillräckligt många konverteringar för att skapa en tillförlitlig modell. Konverteringar: {}. |
| 412 | FEL 412. Leads-AI-pipeline har stoppats: testdata har ingen konvertering för att beräkna AUC-ROC. |

| Varnings-/infokod | Meddelande |
| --- | --- |
| 100 | INFORMATION 100. Leads-AI-kvalitetskontroll: antalet konton är: {}. |
| 101 | INFORMATION 101. Kvalitetskontroll av lead-AI: antalet kontakter är: {}. |
| 102 | INFORMATION 102. Kvalitetskontroll av lead-AI: antalet affärsmöjligheter är: {}. |
| 103 | INFORMATION 103. Leads AI-kvalitetskontroll: det är lågt att testa auc. Starta parameterjustering. Testar auc: {}. |
| 200 | VARNING 200. Leads-AI-kvalitetskontroll: Frekvensen med saknade firmografiska funktioner är: {}. |
| 201 | VARNING 201. Leads-AI-kvalitetskontroll: aktivitetsfunktionerna som saknas är: {}. |

## Nästa steg

Genom att följa den här självstudiekursen kan du nu skapa och hantera bakgrundsmusik. Mer information finns i följande dokument:

* [Prediktiv lead- och kontobedömning](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Övervaka prediktiva lead- och kontopoängjobb](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
