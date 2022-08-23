---
title: Prediktiv lead- och kontobedömning i realtid CDP B2B
type: Documentation
description: En översikt och mer information om den prediktiva lead- och kontopoängsfunktionen i Experience Platform CDP B2B.
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 99b3b2d73b87a64fcaa9ba51563c0942fc21a0dc
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# Prediktiv lead- och kontobedömning i realtid CDP B2B

B2B-marknadsförarna står inför flera utmaningar i toppen av marknadsföringstratten. För att vara effektiv behöver B2B-marknadsförarna ett automatiskt sätt att kvalificera det stora antalet människor så att de kan fokusera på de värdefulla målen. Kvalificeringen bör anpassas till det slutliga försäljningsresultatet, inte bara marknadsföringskonverteringen.

Konton är de ultimata enheterna som köper produkter och tjänster från B2B. För att B2B-marknadsförarna ska kunna marknadsföra och sälja effektivt måste de känna till både individens och kontots sannolikhet att köpa.

Kontobaserad marknadsföring, i synnerhet, gör konton till marknadsmål. Kundbenägenhet att köpa poäng hjälper B2B-marknadsförarna att prioritera bland kontona för att maximera avkastningen på investeringen.

Tjänsten för prediktiv lead- och kontobedömning löser ovanstående problem genom att lära sig av och förutsäga konverteringshändelser i affärsmöjlighetsfasen och samla aktiviteter på kontonivå för att ta fram kontouppgifterna. Poängen finns enkelt som anpassade fält på personprofiler och kontoprofiler och kan enkelt inkluderas som segmentkriterier för att förfina er målgrupp. De viktigaste inflytelserika faktorerna finns också tillgängliga både på aggregat- och enhetsnivå för att hjälpa B2B-marknadsförarna att bättre förstå vilka element som låg bakom poängen.

## Förstå prediktiv lead- och kontobedömning {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] datakälla krävs för närvarande eftersom det är den enda datakälla som kan tillhandahålla konverteringshändelserna på personprofilnivå.

Predictive Lead and Account Scoring använder en trädbaserad (slumpmässig skog/övertoningsförbättring) maskininlärningsmetod för att bygga den förutsägbara modellen för poängsättning av leads.

Administratörer kan konfigurera flera profilbedömningsmål, som också kallas modeller, en för varje konfigurerad konverteringshändelse, så att separata poängvärden kan genereras för varje konfigurerat mål.

Prediktiv lead- och kontobedömning har stöd för följande typer och fält för konverteringsmål:

| Måltyp | Fält |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Exempel: `opportunityEvent.dataValueChanges.attributeName` är lika med `Stage` och `opportunityEvent.dataValueChanges.newValue` är lika med `Contract`</ul> |

Algoritmen tar hänsyn till följande attribut och indata:

* Personprofil

| XDM-fält | Obligatoriskt/valfritt |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Obligatoriskt |
| `workAddress.country` | Valfritt |
| `extSourceSystemAudit.createdDate` | Obligatoriskt |
| `extendedWorkDetails.jobTitle` | Valfritt |

>[!NOTE]
> 
>Algoritmen inspekterar bara `sourceAccountKey.sourceKey` i fältgruppen Person:personComponents.

* Kontoprofil

| XDM-fält | Obligatoriskt/valfritt |
| --- | --- |
| `accountKey.sourceKey` | Obligatoriskt |
| `extSourceSystemAudit.createdDate` | Obligatoriskt |
| `accountOrganization.industry` | Valfritt |
| `accountOrganization.numberOfEmployees` | Valfritt |
| `accountOrganization.annualRevenue.amount` | Valfritt |

* Experience Event

| XDM-fält | Obligatoriskt/valfritt |
| --- | --- |
| `_id` | Obligatoriskt |
| `personKey.sourceKey` | Obligatoriskt |
| `timestamp` | Obligatoriskt |
| `eventType` | Obligatoriskt |

Flera modeller stöds, med följande fasta begränsningar:

* Varje produktionssandlåda är berättigad till fem modeller.
* Varje utvecklingssandlåda är berättigad till en modell.

Datakvalitetskraven är följande:

* Helst finns det två års senaste uppgifter för utbildningsändamål.
* Minimilängden data som krävs är sex månader plus förutsägelsefönstret.
* För varje förutsägelsemål krävs minst 10 kvalificerade konverteringshändelser.

Bedömningsjobb körs dagligen och resultaten sparas som profilattribut och kontoattribut, som sedan kan användas i segmentdefinitioner och personalisering. Det finns även användningsklara analysinsikter på kontrollpanelen för kontoöversikt.

Mer information om hur du gör det finns i dokumentationen [hantera prediktiv lead- och kontobedömning](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) service.

## Visa prediktiva lead- och kontopoängresultat {#how-to-view}

Efter jobbkörningen sparas resultaten i en ny systemdatauppsättning för varje modell under namnet `LeadsAI.Scores` - ***bakgrundsmusiken***. Varje poängfältgrupp finns på `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Attribut | Beskrivning |
| --- | --- |
| Poäng | Den relativa sannolikheten för att en profil ska uppnå det förväntade målet inom den definierade tidsramen. Detta värde ska inte behandlas som sannolikhetsprocent utan snarare som sannolikheten för en profil jämfört med den totala populationen. Poängen varierar mellan 0 och 100. |
| Procent | Det här värdet ger information om en profils prestanda i förhållande till andra profiler med liknande resultat. Percentiler varierar mellan 1 och 100. |
| Modelltyp | Den valda modelltypen, anger om det är en person eller ett kontonummer. |
| Resultatdatum | Det datum som poängsättningen inträffade. |
| Influensafaktorer | Förväntade orsaker till varför en profil kan konverteras. Faktorer består av följande attribut:<ul><li>Kod: Profilen eller beteendeattributet som positivt påverkar en profils förväntade poäng.</li><li>Värde: Värdet på profilen eller beteendeattributet.</li><li>Prioritet: Anger den vikt som profilen eller beteendeattributet har på det förväntade poängvärdet (låg, medel, hög).</li></ul> |

### Visa kundprofilpoäng

Om du vill visa prediktiva poäng för en personprofil väljer du **[!UICONTROL Profiles]** under kundavsnittet i den vänstra panelen och ange sedan ID-namnutrymmet och identitetsvärdet. När du är klar väljer du **[!UICONTROL View]**.

Välj sedan profilen i listan.

![Kundprofil](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

The **[!UICONTROL Detail]** sidan innehåller nu prediktiva poäng. Klicka på diagramsymbolen bredvid prediktiva poäng.

![Kundprofilprediktiv poäng](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

En popup-dialogruta visar poängen, den övergripande poängfördelningen, de viktigaste inflytelserika faktorerna för poängen och poängmålsdefinitionen.

![Information om prediktiva kundpoäng](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Övervaka prediktiva lead- och kontopoängjobb {#monitoring-jobs}

Du kan övervaka grundläggande mått och daglig jobbkörningsstatus via kontrollpanelen. Mätvärdena omfattar:

* Totalt antal person-/kontoprofiler som har sparats
* Nästa bedömningsjobb (datum)
* Nästa utbildningsjobb (datum)

Mer information finns i dokumentationen om [övervaka jobb för prediktiv lead- och kontobedömning](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
