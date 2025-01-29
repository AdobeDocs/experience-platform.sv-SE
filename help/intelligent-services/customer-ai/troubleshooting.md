---
keywords: Experience Platform;komma igång;kundinformation;populära ämnen;kundinformation;kunddata;kundmeddelanden, felsökning;kundmeddelanden, fel
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Felsökning av kund-AI
description: Hitta svar på vanliga fel i kundens AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 0%

---

# Felsökning av kund-AI

Kund-AI visar fel när modellutbildning, poängsättning och konfiguration misslyckas. I avsnittet **[!UICONTROL Service instances]** visar en kolumn för **[!UICONTROL LAST RUN STATUS]** ett av följande meddelanden: **[!UICONTROL Success]**, **[!UICONTROL Training issue]** och **[!UICONTROL Failed]**.

![status för senaste körning](./images/errors/last-run-status.png)

Om **[!UICONTROL Failed]** eller **[!UICONTROL Training issue]** visas kan du välja körningsstatus för att öppna en sidopanel. Sidpanelen innehåller din **[!UICONTROL Last run status]** och **[!UICONTROL Last run details]**. **[!UICONTROL Last run details]** innehåller information om varför körningen misslyckades. Om kundens AI inte kan ge detaljerad information om felet kontaktar du supporten med den felkod som anges.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Det går inte att komma åt kundens AI i Chrome Incognito

Det finns inläsningsfel i Google Chrome inkognito-läge på grund av uppdateringar i Google Chrome inkognito-lägessäkerhetsinställningarna. Vi arbetar aktivt med Chrome för att göra experience.adobe.com till en betrodd domän.

![Felbild](./images/errors/error.PNG){width=500}

### Rekommenderad åtgärd

För att lösa det här problemet måste du lägga till experience.adobe.com som en webbplats som alltid kan använda cookies. Börja med att gå till **chrome://settings/cookies**. Bläddra sedan nedåt till avsnittet **Anpassade beteenden** följt av att klicka på knappen **Lägg till** bredvid&quot;webbplatser som alltid kan använda cookies&quot;. Kopiera och klistra in `[*.]experience.adobe.com` i den pover som visas och markera sedan kryssrutan **Inkludera cookies från tredje part** på den här webbplatsen. När du är klar väljer du **Lägg till** och läser in kundens AI igen i incognito.

![rekommenderad korrigering](./images/errors/cookies2.gif)

## Modellkvaliteten är dålig

Om du får felet [!UICONTROL Model Quality is poor. We recommend creating a new app with the modified configuration]. Följ de rekommenderade stegen nedan för att felsöka.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Rekommenderad åtgärd

&quot;Modellkvaliteten är dålig&quot; betyder att modellens noggrannhet inte ligger inom ett acceptabelt intervall. Kundens AI kunde inte skapa en tillförlitlig modell och AUC (område under ROC-kurvan) &lt; 0,65 efter utbildning. För att åtgärda felet rekommenderar vi att du ändrar en av konfigurationsparametrarna och kör kursen igen.

Börja med att kontrollera att era data är korrekta. Det är viktigt att dina data innehåller de fält som behövs för prediktiva resultat.

- Kontrollera om din datauppsättning har de senaste datumen. Kunds-AI antar alltid att data är aktuella när modellen aktiveras.
- Kontrollera om det finns data som saknas i det definierade förutsägelsefönstret och berättigandefönstret. Dina data behöver vara kompletta utan luckor. Kontrollera också att datauppsättningen uppfyller [kundernas AI-krav](./data-requirements.md#data-requirements).
- Kontrollera om det finns data som saknas i e-handel, program, webb och sökning i egenskaperna för schemafält.

Om dina data inte verkar vara problemet kan du försöka ändra villkoren för berättigandepopulation för att begränsa modellen till vissa profiler (till exempel finns `_experience.analytics.customDimensions.eVars.eVar142` under de senaste 56 dagarna). Detta begränsar populationen och storleken på de data som används i utbildningsfönstret.

Om det inte gick att begränsa behörighetspopulationen eller om det inte går, ändrar du förutsägelsefönstret.

- Försök att ändra förutsägelsefönstret till 7 dagar och se om felet kvarstår. Om felet inte längre inträffar indikerar det att du kanske inte har tillräckligt med data för det definierade förutsägelsefönstret.

### Fel

| Felkod | Titel | Meddelandemall | Exempel på meddelande |
| ---------- | ----- | ---------------- | --------------- |
| 400 | INTE TILLRÄCKLIGT MÅL | Det finns för få användare ({{actual_num_samples}} totalt) som uppfyller förutsägelsemåldefinitionen från {{outcome_window_start}} till {{outcome_window_end}}. Minst {{min_num_samples}} användare med kvalificerande händelser måste skapa en modell. <br><br>Föreslagna lösningar: <br><br>1. Kontrollera datatillgänglighet <br>2. Minska tidsramen <br>3 för förutsägelsemålet. Ändra definitionen för förutsägelsemålet så att fler användare inkluderas (Felkod: VALIDATION-400 NOT_ENOUGH_OBJECTIVE) | Det finns för få användare (totalt 200) som uppfyller förutsägelsemåldefinitionen från 2020-04-01 till 2021-04-01. Vi kräver att minst 500 användare med kvalificerande händelser skapar en modell. <br><br>Föreslagna lösningar: <br>1. Kontrollera datatillgänglighet <br>2. Minska tidsramen <br>3 för förutsägelsemålet. Ändra definitionen för förutsägelsemålet så att fler användare inkluderas. (Felkod: VALIDATION-400 NOT_ENOUGH_OBJECTIVE) |
| 401 | INTE TILLRÄCKLIGT MED BEFOLKNINGEN | Det finns för få berättigade användare ({{actual_num_samples}} totalt) från {{eligibility_window_start}} till {{eligibility_window_end}}. Minst {{min_num_samples}} berättigade användare måste skapa en modell. <br><br>Föreslagna lösningar: <br>1. Kontrollera datatillgänglighet <br>2. Om en definition för en berättigad population anges, minskar du tidsramen för berättigandefiltret 3. Om ingen giltig populationsdefinition finns kan du försöka lägga till en (Felkod: VALIDATION-401 NOT_ENOUGH_POPULATION) | Det finns för få berättigade användare (totalt 200) mellan 2020-04-01 och 2021-04-01. Vi kräver att minst 500 berättigade användare skapar en modell.<br><br>Föreslagna lösningar:<br>1. Kontrollera datatillgänglighet<br>2. Om en definition av en berättigad population anges, minskar du tidsramen för berättigandefiltret.<br>3. Om ingen definition av en berättigad population anges kan du försöka med att lägga till en. (Felkod: VALIDATION-401 NOT_ENOUGH_POPULATION) |
| 402 | FELAKTIG MODELL | Det går inte att skapa en kvalitetsmodell med den aktuella indatauppsättningen och konfigurationen. <br><br>Några förslag är: <br>1. Ändra konfigurationen för att lägga till en tillämplig populationsdefinition. <br>2. Använd ytterligare datakällor för att förbättra modellkvaliteten <br>3. Lägg till anpassade händelser för att inkludera fler data i modellen (felkod: VALIDATION-402 BAD_MODEL) | Det går inte att skapa en kvalitetsmodell med den aktuella indatauppsättningen och konfigurationen. <br><br>Några förslag är: <br>1. Överväg att ändra konfigurationen för att lägga till en tillämplig populationsdefinition. <br>2. Överväg att använda ytterligare datakällor för att förbättra modellkvaliteten. (Felkod: VALIDATION-402 BAD_MODEL) |
| 403 | OBEHÖRIGA SKOR | Poängfördelningen avviker för mycket från förväntat. <br><br>Några förslag är: <br>1. Se till att modellen har tränats med senaste data, och om inte, överväg att träna om modellen. <br>2. Se till att det inte finns något dataproblem (t.ex. att data saknas/att data fördröjs) i bedömningsåtgärderna. (Felkod: VALIDATION-403 INELIGIBLE_SCORES) | Poängfördelningen avviker för mycket från förväntat. <br><br>Några förslag är: <br>1. Se till att modellen har tränats med senaste data, och om inte, överväg att träna om modellen. <br>2. Se till att det inte finns något dataproblem (t.ex. att data saknas/att data fördröjs) i bedömningsåtgärderna. (Felkod: VALIDATION-403 INELIGIBLE_SCORES) |
| 405 | INGA SPEKNINGSDATA | Det finns inga tillgängliga användarbeteendedata eller profildata för bedömning från {{eligibility_window_start}} till {{eligibility_window_end}}. Kontrollera att data uppdateras regelbundet. (Felkod: VALIDATION-405 NO_SCORING_DATA) | Det finns inga tillgängliga användarbeteendedata eller profildata för poängsättning mellan 2020-04-01 och 2021-04-01. Kontrollera informationen för att säkerställa att den uppdateras regelbundet. (Felkod: VALIDATION-405 NO_SCORING_DATA) |
| 407 | INTE TILLRÄCKLIGT MED HISTORISKA HÄNDELSEDATA | Det finns inte tillräckligt med data för att skapa en modell. Från 2020-04-01 till 2021-04-01 finns det bara 90 dagar med data. <br><br>Vi behöver 120 dagar med senaste data. Mer information finns i dokumentationen om datakrav. <br><br>Föreslagna lösningar: <br>1. Kontrollera datatillgänglighet <br>2. Minska tidsramen <br>3 för förutsägelsemålet. Om en definition för en berättigad population anges, minskar du tidsramen för berättigandefiltret <br>4. Om ingen giltig populationsdefinition finns kan du försöka med att lägga till en (Felkod: VALIDATION-407 NOT_ENOUGH_HISTORICAL_EVENT_DATA) | Det finns inte tillräckligt med data för att skapa en modell. Från 2020-04-01 till 2021-04-01 finns det bara 90 dagar med data.<br><br>Vi behöver 120 dagar med senaste data. Mer information finns i dokumentationen om datakrav.<br><br>Föreslagna lösningar:<br>1. Kontrollera datatillgänglighet.<br>2. Minska tidsramen för förutsägelsemålet.<br>3. Om en definition av en berättigad population anges, minskar du tidsramen för berättigandefiltret.<br>4. Om ingen definition av en berättigad population anges kan du försöka med att lägga till en. (Felkod: VALIDATION-407 NOT_ENOUGH_HISTORICAL_EVENT_DATA) |
| 408 | INGA NYA DATA FÖR BERÄTTIGANDE | Det finns inga användarbeteendedata för berättigade användare inom {{data_days}} dagar före {{etl_window_end}}. Kontrollera datauppsättningen för att se till att den uppdateras regelbundet. (Felkod: VALIDATION-408 NO_RECENT_DATA_FOR_ELIGIBLE_POPULATION) | Det finns inga användarbeteendedata för berättigade användare under de 60 dagarna före 2021-04-01. Kontrollera datauppsättningen för att se till att den uppdateras regelbundet. (Felkod: VALIDATION-408 NO_RECENT_DATA_FOR_ELIGIBLE_POPULATION) |
| 409 | INGET MÅL | Det finns inga användare som uppfyller förutsägelsemåldefinitionen från {{outcome_window_start}} till {{outcome_window_end}}. Minst {{min_num_samples}} användare med kvalificerande händelser måste skapa en modell. <br><br>Föreslagna lösningar: <br>1. Kontrollera datatillgänglighet <br>2. Ändra definition för förutsägelsemål (felkod: VALIDATION-409 NO_OBJECTIVE) | Det finns inga användare som uppfyller förutsägelsemåldefinitionen från 2020-04-01 till 2021-04-01. Vi kräver att minst 500 användare med kvalificerande händelser skapar en modell. <br><br>Föreslagna lösningar:<br>1. Kontrollera datatillgänglighet.<br>2. Ändra definitionen för förutsägelsemålet. (Felkod: VALIDATION-409 NO_OBJECTIVE) |
| 410 | INGEN POPTION | Det finns inga berättigade användare från {{eligibility_window_start}} till {{eligibility_window_end}}. Minst {{min_num_samples}} berättigade användare måste skapa en modell. <br><br>Föreslagna lösningar: <br>1. Kontrollera datatillgänglighet <br>2. Om det finns en definition av en berättigad population ändrar du villkoret eller ökar tidsramen för berättigandefiltret (felkod: VALIDATION-410 NO_POPULATION) | Det finns inga berättigade användare mellan 2020-04-01 och 2021-04-01. Vi kräver att minst 500 berättigade användare skapar en modell. <br><br>Föreslagna lösningar:<br>1. Kontrollera datatillgänglighet. <br> 2. Om det finns en definition av en berättigad population ändrar du villkoret eller ökar tidsramen för berättigandefiltret. (Felkod: VALIDATION-410 NO_POPULATION) |
| 411 | INGA INDATADATA EFTER ETL | Det finns inga tillgängliga användarbeteendedata eller profildata för modellen som kan användas mellan {{etl_start_date}} och {{etl_end_date}}. Kontrollera att datauppsättningen har tillräckligt med data. (Felkod: VALIDATION-411 NO_INPUT_DATA_AFTER_ETL) | Det finns inga tillgängliga användarbeteendedata eller profildata för modellen mellan 2020-04-01 och 2021-04-01. Kontrollera att datauppsättningen har tillräckligt med data. (Felkod: VALIDATION-411 NO_INPUT_DATA_AFTER_ETL) |
| 412 | INGEN HÄNDELSE EFTER ETL | Det finns inga tillgängliga användarbeteendedata för modellen att använda mellan {{etl_start_date}} och {{etl_end_date}}. Kontrollera att datauppsättningen har tillräckligt med data. | Det finns inga tillgängliga användarbeteendedata för modellen mellan 2020-04-01 och 2021-04-01. Kontrollera att datauppsättningen har tillräckligt med data. (Felkod: VALIDATION-412 NO_EVENT_DATA_AFTER_ETL) |
| 413 | ENSKILT VÄRDE I OBJEKT | CustomerAI kräver att datauppsättningen har både kvalificerande och icke-kvalificerande händelser för förutsägelsemåldefinitionen. Indatauppsättningen innehåller bara kvalificerande händelser mellan {{etl_window_start}} och {{etl_window_end}}. <br><br>Föreslagna lösningar: <br>1. Ändra definitionen för förutsägelsemålet <br> . Verifiera datafullständighet eller använd en annan som innehåller exempel på icke-kvalificerande händelser för förutsägelsemålet (felkod: VALIDATION-413 SINGLE_VALUE_IN_OBJECTIVE) | CustomerAI kräver att datauppsättningen har både kvalificerande och icke-kvalificerande händelser för förutsägelsemåldefinitionen. Indatauppsättningen innehåller endast kvalificerade händelser mellan 2020-04-01 och 2021-04-01.<br><br>Föreslagna lösningar:<br>1. Ändra definitionen för förutsägelsemålet.<br>2. Verifiera att data är fullständiga eller använd en annan som innehåller exempel på icke-kvalificerande händelser för förutsägelsemålet. (Felkod: VALIDATION-413 SINGLE_VALUE_IN_OBJECTIVE) |
| 414 | INGA INFLUENTIELLA FAKTORER | Den inflytelserika faktormodellen genererade oväntade utdata. Vi rekommenderar att du skapar ett nytt program med en ändrad konfiguration. (Felkod: VALIDATION-414 NO_INFLUENTIAL_FACTORS) | Den inflytelserika faktormodellen genererade oväntade utdata. Vi rekommenderar att du skapar ett nytt program med en ändrad konfiguration. (Felkod: VALIDATION-414 NO_INFLUENTIAL_FACTORS) |