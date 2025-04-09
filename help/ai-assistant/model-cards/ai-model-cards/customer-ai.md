---
title: Kort för AI-poängsättningsmodell för kund
description: Lär dig mer om AI-modellen som används för kundens AI.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# Kort för AI-poängsättningsmodell för kund

Som en del av [Intelligenta tjänster i Adobe Experience Platform](../../../intelligent-services/home.md) kan du använda [Customer AI](../../../intelligent-services/customer-ai/overview.md) för att generera kundprognoser och förklaringar på individnivå.

Med hjälp av inflytelserika faktorer kan ni använda kundens artificiella intelligens för att tala om för er vad en kund kan förväntas göra och varför. Dessutom kan ni dra nytta av kundernas AI-prognoser och insikter för att personalisera kundupplevelser genom att leverera de lämpligaste erbjudandena och budskapen.

Läs det här modellkortet för information om AI-modellen som används för att driva kundens AI.

## Modellöversikt {#model-overview}

* Kundens AI är en AI-baserad modell som utformats för att generera benägenhetspoäng för användare baserat på deras tidigare beteenden och interaktioner med ett företag. Använd AI för att förutsäga sannolikheten för att en kund vidtar specifika åtgärder, som att göra ett köp, engagera med innehåll eller krama. Den här modellen används i Experience Platform och kan integreras med olika arbetsflöden för marknadsföring och kundanalys.
* Modellen är utformad för att ge marknadsförare och kundinteraktionsteam åtgärdbara insikter genom att förutsäga sannolikheten för att en kund kommer att utföra en viss åtgärd, som att göra ett köp, registrera sig för en prenumeration eller engagera sig i en e-postkampanj. Tack vare resultaten kan företag optimera målgruppssegmentering och personalisera kundinteraktioner baserat på förutsedda beteenden.
* Detta är en **övervakad inlärningsklassificeringsmodell** som förutser sannolikheten för en händelse som inträffar (inköp, köp, köp, engagemang) utifrån historiska kunddata. Den har tränats med hjälp av övertoningsstartsbeslutsträd (GBDT) med logistisk regression för att modellera benägenhetspoäng.
* De främsta användarna i den här modellen är marknadsförare, dataanalytiker och kundinteraktionsteam som utnyttjar Experience Platform för att utveckla datadrivna marknadsföringsstrategier.
* Kundens AI integreras direkt i Experience Platform AI-tjänster, vilket gör det möjligt för användare att få tillgång till modellutdata via fördefinierade API:er och instrumentpaneler. Propensitetspoängen som genereras av modellen kan användas i [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) och [Real-Time CDP](../../../rtcdp/home.md) för att förfina målgruppssegmenteringen och skräddarsy marknadsföringsstrategier.

## Avsedd användning {#intended-use}

* Den här modellen används främst för **kundsegmentering, riktad marknadsföring och bortfallsförutsägelse**. Företag använder den här modellen för att **förutsäga kundens inköpsmetod, optimera marknadsföringskampanjer och förbättra personaliseringen**. Ett e-handelsföretag kan till exempel använda modellen för att identifiera kunder med hög återgivning och erbjuda dem exklusiva erbjudanden.
* Marknadsförare kämpar ofta med att **identifiera rätt kunder för att målinrikta** och **optimera engagemanget**. Den här modellen **minskar gissningsarbetet** genom att tillhandahålla en datadriven metod för kundanpassning, vilket säkerställer att marknadsföringsresurserna fördelas effektivt.
* Modellen kan användas i olika branscher, inklusive e-handel, detaljhandel, finansiella tjänster, telekommunikation och media. Any business that relies on customer engagement and personalized marketing can benefit from this model.
* The model **should not be used for high-risk decision-making**, such as financial credit scoring, medical diagnostics, or legal assessments. Additionally, it is not intended for use in predicting personally sensitive behaviors (health conditions, political preferences) due to potential ethical concerns.

## Model inputs and outputs {#model-inputs-and-outputs}

* The model processes customer behavioral data, demographic attributes, and historical interactions. This includes data such as website visit frequency, past purchase history, engagement with marketing emails, and demographic information.
* Input data must be structured as JSON objects containing customer attributes and behavioral signals. For batch processing, the model accepts CSV files formatted according to Experience Platform&#39;s data ingestion standards.
* The model outputs a propensity score between 0 and 1, where higher values indicate a higher likelihood of the predicted event occurring. Additionally, it provides feature importance scores, allowing users to understand which factors influenced the prediction.

**Example input**

```json
{
  "customer_id": 12345,
  "past_purchases": 3,
  "last_visit_days": 7,
  "email_click_rate": 0.4
}
```

**Example output**

```json
{
  "customer_id": 12345,
  "propensity_score": 0.82
}
```

## Training data

* Modellen har tränats på **anonyma kundinteraktionsdata från första part** som samlats in via Experience Platform. Den innehåller historiska kundbeteendedata **för kunder, transaktionsposter, e-postinteraktioner och interaktionsstatistik** för flera branscher.
* Utbildningsdatauppsättningen består av **10 miljoner kundposter** som kommer från en rad olika Experience Platform-kunder. Dessa poster omfattar **historiska kundinteraktioner, transaktionsdata, beteendeloggar och demografisk information** från olika branscher som detaljhandel, e-handel, telekommunikation och ekonomi. Data samlades in under en 24-månadersperiod för att säkerställa en tillräcklig representation av säsongstrender och långsiktiga engagemangsmönster.
* Datauppsättningen kommer huvudsakligen från engagerande användare, vilket kan innebära en förskjutning av urvalet. För att minska detta tillämpar modellen stratifierad provtagning, teknik för revision av avvikelser och strategier för datainsamling.
* Datauppsättningen genomgår omfattande förbehandling för att säkerställa att data är konsekventa, håller hög kvalitet och är användbara.
   * **Handling Missing Values**: Missing values are addressed using a combination of mean imputation (for numerical fields), mode imputation (for categorical fields), and predictive modeling (for complex missing cases).
   * **Kategorisisk kodning**: Kategorivariabler som kundsegment och inköpskategorier konverteras till numeriska representationer med kodnings- och målkodningstekniker som varmar ett och ett.
   * **Funktionsskalning och normalisering**: Min-max-skalning används för avgränsade variabler (ålder, inkomst), medan z-score-standardisering används för normalt distribuerade funktioner.
   * **Ytterligare förbehandling**: Pipelinen innehåller avdataidentifiering och borttagning, duplicerad filtrering, tidsstämpelstandardisering och funktionsteknik för att förbättra prediktiv modellering.

## Modellarkitektur och utbildning

* Modellen utnyttjar **[!DNL Gradient Boosting Decision Trees](GBDT) med[!DNL XGBoost]**, optimerat för strukturerade data. Det har utbildats på historiska kundhändelsesekvenser för att identifiera prediktiva beteendemönster.
* Modellen byggs med en övervakad inlärningsmetod som utnyttjar GBDT med [!DNL XGBoost] som den primära inlärningsalgoritmen. Dessutom ingår logistisk regression som en basmodell för riktmärkning av prediktiv precision.
* Modellen utvecklades med **[!DNL TensorFlow]**, **[!DNL XGBoost]** och **[!DNL scikit-learn]**. Utbildning körs på Adobe AI-molninfrastruktur med **[!DNL NVIDIA V100]GPU:er** som stöder storskaliga datamängder.
* [!DNL NVIDIA V100 GPUs], utbildad i Google Cloud-infrastruktur.
* [!DNL AUC-ROC], precisionsåterkallning och korsvalidering.

## Resultat och utvärdering

* Modellen testades med en demovalideringsmetod, där 80 % av data användes för utbildning och 20 % reserverades för utvärdering.
* Modellens effektivitet mäts med [!DNL AUC-ROC] (0,85), precisionsåterkallning (0,78) och F1-poäng (0,80). Dessa mätvärden hjälper till att bedöma modellens prediktiva styrka i olika segment.
* Lägre precision för nya kundsegment med begränsade historiska data.
* Modellen kanske inte fungerar som den ska för kunder med begränsade historiska data (problem med kallstart). Dessutom kan säsongseffekter (semestershoppingtrender) kräva frekvent omskolning för att bibehålla noggrannheten.

## Fairness and bias

* Modellen genomgick **demografisk paritetstestning** och **bedömning av om det är rättvist mot en kontrast** för att upptäcka prestandaskillnader mellan olika användarsegment.
* Analysen avslöjade en **5 %-prestandaförsämring för användare med låga historiska interaktionsdata**. Modellen innehåller omviktningstekniker under utbildningen.
* Datauppsättningen är stratifierad för att säkerställa proportionell återgivning av olika kunddemografi, och under utbildningens gång införs krav på rättvisa för att förhindra att modellen gynnar en viss grupp. Regelbunden kontroll av systematiska avvikelser genomförs med hjälp av demografiska analyser, vilket gör det möjligt att justera om resultatskillnader upptäcks.

## Förklara och tolka

* Modellen utnyttjar **[!DNL SHapley Additive Explanations](SHAP)** för att kvantifiera effekten av varje indatafunktion på dess prognoser, vilket ger transparens i hur kundattribut påverkar benägenhetspoängen. SHAP-värden möjliggör både global tolkning och identifierar de mest inflytelserika faktorerna i alla prognoser, samt lokal tolkning som förklarar individuella prognoser för specifika kunder.
* Modellen stöder **[!DNL Local Interpretable Model-Agnostic Explanations](LIME)** och SHAP för att ge insikter om hur indatafunktioner påverkar prognoser. LIME genererar lokala förklaringar genom att skapa störda versioner av indata och observera förändringar i förutsägelser, medan SHAP tilldelar bidragsvärden till varje funktion, vilket ger både global och lokal tolkning av modellbeslut.

## Robusta funktioner och generalisering

* Modellen behåller 80 % [!DNL AUC-ROC] när den testas på osynliga datamängder, vilket visar en stark generalisering till nya kundposter. Prestandan är stabil för olika kundsegment men försämras något när användarbeteendet avviker avsevärt från historiska mönster.
* Modellen har utvärderats mot störd och konsariell inmatning, inklusive saknade data, avledningsbar injektion och avsiktlig felmärkning. Prestandan är stabil under normala förhållanden, men en mindre noggrannhetsförsämring (cirka 3-5%) observerades under extrema negativa förändringar.

## Säkerhet och integritet

* Modellen **bearbetar eller behåller ingen personligt identifierbar information (PII)**, och alla data som används för utbildning anonymiseras och aggregeras. Den följer strikta regler för efterlevnad av GDPR, CCPA och Adobe interna integritetspolicyer för att säkerställa ansvarsfull dataanvändning.
* Modellen innehåller olika integritetstekniker som lägger till kontrollerat brus i data och förhindrar återidentifiering av individer. Dessutom används metoderna **hashing, anonymisation och tokenisering för att ta bort PII** före modellutbildning och härledning.

## Driftsättning och integrering

* Modellen ligger hos Adobe Experience Platform AI-tjänster och är integrerad med olika Adobe-program. Det är tillgängligt via API-slutpunkter, vilket ger smidig åtkomst för realtidspreditioner och batchbearbetning i arbetsflöden för marknadsföring och kundengagemang.
* Modellen körs på en **[!DNL Kubernetes]-baserad distribution** med funktioner för automatisk skalning för att hantera varierande arbetsbelastningar effektivt. Beräkningsresurserna innehåller [!DNL NVIDIA V100] grafikprocessorer för utbildning och optimerad CPU-baserad härledning för skalbarhet i realtid.

## Övervakning och underhåll

* Modellen övervakas kontinuerligt **via[!DNL WatsonX]**, och nyckeltal för prestanda spåras, till exempel noggrannhetsavvikelse, viktiga funktionsändringar och förutsägelsestabilitet. Mekanismerna för avvikelseidentifiering och varningar meddelar teamet när det finns betydande avvikelser från förväntat beteende.
* Modellen omskolas månadsvis med uppdaterade kundinteraktionsdata för att säkerställa fortsatt relevans. Regelbunden omskolning bidrar till att minska dataavdrift och säsongsrelaterade fluktuationer som kan påverka den prediktiva noggrannheten

## Etik oro och ansvarsfull AI

* The model could potentially introduce bias in decision-making if not monitored correctly. For example, if certain demographics are overrepresented in the training data, the model might unfairly favor specific customer groups.
* Experience Platform follows responsible AI guidelines, ensuring that models undergo **bias audits, fairness testing, and human oversight** before deployment.

## Kända begränsningar

* The model may struggle to accurately predict outcomes for newly launched products or customer segments where insufficient historical data is available. Additionally, seasonal variations in customer behavior can cause fluctuations in predictive accuracy if not accounted for during retraining.
* Performance declines when customer history is sparse, such as for first-time buyers or users with minimal engagement data. Additionally, if customer behaviors **shift due to external factors like economic downturns or industry trends**, the model may require rapid adaptation to maintain accuracy.

## Future improvements

* Future iterations will include transfer learning techniques to improve performance for cold-start users and enhance adaptability to changing customer behaviors. Additionally, real-time data integration will be introduced to improve model responsiveness and accuracy in dynamic marketing environments.
