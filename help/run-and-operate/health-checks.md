---
title: Hälsokontroller
description: Lär dig hur du använder hälsokontroller i Adobe Experience Platform för att proaktivt upptäcka problem med schema- och identitetskonfigurationer innan de påverkar dataåtgärderna.
solution: Experience Platform
type: Documentation
role: Admin, User
hide: true
source-git-commit: ab2420b898dc38d19187cee627b5c44e7fb44a6c
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 0%

---

# Hälsokontroller

Hälsokontroller skannar in dina scheman och identiteter som används i din sandlåda och ger en sammanfattning av problem som du kan använda för att utforska och felsöka med [!UICONTROL AI Assistant]. I framtiden kan fler objekt skannas för en mer omfattande rapport.

Dåliga schema- och identitetskonfigurationer leder till betydande problem längre fram i kedjan, bland annat felaktigt skapande av profiler, misslyckade segmentkvalificeringar och felaktig aktivering. Dessa problem är svåra att upptäcka och kräver ofta specialiserad expertis för att diagnostisera. Hälsokontroller förändrar ditt tillvägagångssätt från reaktiv felsökning till förebyggande, förebyggande underhåll.

Med hälsokontroller kan du

* **Identifiera konfigurationsproblem tidigt**: Identifiera bästa praxis, felkonfigurationer och mönster som saknas och som leder till ineffektivitet i personalisering, aktivering med mera.
* **Få guidad korrigering**: Få tydlig vägledning om vad varje problem är och vad du ska göra åt det.
* **Övervaka kontinuerligt**: I det här ögonblicket körs hälsokontroller automatiskt varje dag så att du kan fånga upp problem innan de blir kritiska fel. Schemat kan ändras i framtida versioner.

## Förutsättningar {#prerequisites}

Om du vill komma åt hälsokontroller måste du ha **[!UICONTROL View Health Checks]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Kontakta systemadministratören för att kontrollera att du har rätt behörigheter.

## Få tillgång till hälsokontroller {#access-health-checks}

Så här får du åtkomst till hälsokontroller från [!UICONTROL Experience Platform]-gränssnittet:

1. Välj **[!UICONTROL Run and Operate]** i den vänstra navigeringen.
1. Välj **[!UICONTROL Health Checks]**.

Kontrollpanelen för hälsokontroller visar en sammanfattning av de senaste sökresultaten.

![Kontrollpanelen för hälsokontroller visar utvärderade objekt, sökresultat och identifierade problem](assets/health-checks/dashboard.png)

## Kontrollpanelen {#understanding-dashboard}

Kontrollpanelen för hälsokontroller innehåller tre informationsområden som hjälper dig att bedöma hur implementeringen fortskrider.

### Utvärderade objekt {#objects-evaluated}

Avsnittet **[!UICONTROL Objects evaluated]** visar det totala antalet inskannade scheman och identitetsnamnutrymmen tillsammans med hur många problem som hittades för varje kategori. Detta ger dig en snabb översikt över omfattningen och svårighetsgraden av konfigurationsproblem i din sandlåda.

### Sökresultat {#scan-results}

Avsnittet **[!UICONTROL Scan results]** visar antalet misslyckade kontroller. En misslyckad kontroll indikerar att en eller flera av hälsokontrollerna identifierade konfigurationsproblem som kräver åtgärd. **Den senaste dagliga hälsogenomsökningen som slutfördes** tidsstämpeln visar när den senaste genomsökningen utfördes.

### Identifierade problem {#identified-issues}

Avsnittet **[!UICONTROL Identified issues]** visar ett kort för varje hälsokontroll. Varje kort visas:

* Hälsokontrollens namn och en kort beskrivning av problemet.
* Antal problem som påträffats eller en bekräftelse på att inga problem förekommer.
* En statusindikator som visar om kontrollen passerade eller kräver åtgärd.

Välj ett kort för att utforska detaljerna om hälsokontrollen.

## Tillgängliga hälsokontroller {#available-health-checks}

Hälsokontroller utvärderar för närvarande fem grundläggande områden i schema- och identitetskonfigurationen. Dessa kontroller är inriktade på de mest effektiva datamodelleringsproblemen i hela plattformen.

### Validering av identitetsfält {#identity-field-validation}

Skanningar för att säkerställa att identitetsfält har begränsningar för minsta och högsta längd och regex-mönsterregler för dataintegritet.

| Detalj | Beskrivning |
| --- | --- |
| **Utgåva** | Fält som markerats som identiteter saknar minimi-/maximilängd eller mönstervalidering. |
| **Effekt** | Utan validering kan skräpinärden ange [!UICONTROL Identity Service]. Värden som &quot;0&quot;, &quot;Gäst&quot; eller ett hölje som inte matchar (till exempel &quot;xyz123&quot; jämfört med &quot;XYZ123&quot;) äventyrar integriteten hos den profil som sätts ihop under segmentering och aktivering. |
| **Reparation** | Ange minsta/högsta längd och mönsterbegränsningar för anpassade fält som är markerade som identiteter. Använd reguljära uttryck för att tillämpa regler som enbart siffror, versaler, gemener eller specifika teckenkombinationer. |

När du väljer kortet **[!UICONTROL Identity Field Validation]** öppnas en detaljpanel till höger. Panelen visar:

* **[!UICONTROL Description]**: Inläsningar för att säkerställa att identitetsfält har min/max-längder och regex-mönsterregler för dataintegritet. Visar scheman och fält som påverkas.
* **[!UICONTROL Impact]**: Om identitetsfält i scheman inte har min/max-längder och mönstervalideringar angivna kan det leda till inkonsekventa data, vilket kan äventyra dataintegriteten och datakvaliteten.
* **[!UICONTROL General areas of impact]**: Identifierare med låg kvalitet i [!UICONTROL Identity Service], otillförlitlig sammanfogning.
* **[!UICONTROL Experience League Documentation]**: En länk till bästa praxis för datamodellering.
* **[!UICONTROL Affected Schemas]**: En lista med berörda scheman, där var och en har en utökare för att visa mer information och en länk för att öppna schemat.

![Detaljpanel för validering av identitetsfält som visar beskrivning, påverkan och berörda scheman](assets/health-checks/identity-field-validation-detail.png)

Mer information finns i [dataintegritetstipsen](/help/xdm/schema/best-practices.md#data-integrity-tips) i dokumentationen om metodtips för scheman.

### Länkningsregler för identitetsdiagram {#identity-graph-linking-rules}

Verifierar att länkningsreglerna för identitetsdiagram har konfigurerats för en sandlåda för att förhindra komprimerade profiler.

| Detalj | Beskrivning |
| --- | --- |
| **Utgåva** | Länkningsregler för identitetsdiagram har inte konfigurerats för den här sandlådan. |
| **Effekt** | Utan att länka regler kan flera olika profiler sammanfogas till en enda profil (komprimering av diagram). Vissa data från delade enheter eller icke-unika identiteter kan utlösa oönskade sammanslagningar, vilket leder till felaktig personalisering. |
| **Reparation** | Navigera till menyn **[!UICONTROL Identities]**, markera **[!UICONTROL Settings]** och markera minst en unik identitet per diagram. Detta aktiverar länkningsregler för identitetsdiagram och förhindrar komprimering av profiler. |

När du väljer kortet **[!UICONTROL Identity Graph Linking Rules]** öppnas en detaljpanel till höger. Panelen visar:

* **[!UICONTROL Description]**: Verifierar att rätt länkningsregler har konfigurerats för att förhindra komprimerade profiler. Den visar aktuell regelstatus och unika identifieringar per diagram.
* **[!UICONTROL Impact]**: Om länkningsreglerna för identitetsdiagram inte anges kan vissa data försöka sammanfoga flera olika profiler till en enda profil. För att förhindra oönskade sammanfogningar bör konfigurationer som tillhandahålls via länkningsregler för identitetsdiagram användas.
* **[!UICONTROL General areas of impact]**: Komprimerade eller sammanfogade profiler.
* **[!UICONTROL Experience League Documentation]**: En länk till översikten över länkningsregler för identitetsdiagram om du vill ha mer information.
* **[!UICONTROL Configure linking rules]**: När kontrollen misslyckas visas en knapp så att du kan konfigurera länkningsregler direkt från panelen.

![Detaljpanel för länkningsregler för identitetsdiagram som visar beskrivning, effekt och knappen Konfigurera länkningsregler](assets/health-checks/identity-graph-linking-detail.png)

Mer information finns i översikten över länkningsregler för [identitetsdiagram](/help/identity-service/identity-graph-linking-rules/overview.md) och [implementeringsguiden](/help/identity-service/identity-graph-linking-rules/implementation-guide.md).

### Konfiguration av identitet för personer och icke-personer {#people-non-people-identity}

Validerar korrekt användning av identitetstyper för personer och icke-personer i olika schemaklasser.

| Detalj | Beskrivning |
| --- | --- |
| **Utgåva** | Identifierare som inte är personer används i enskilda profiler eller i Experience Event-klassscheman, eller så används personidentifierare i sökscheman. |
| **Effekt** | Identifierare som inte är personer i profilscheman deltar inte i identitetsdiagrammet, vilket leder till ofullständig identitetsmatchning. Identifierare av personer i uppslagsscheman ökar profilantalet och gör data icke-åtkomliga för sökanvändningsfall. Båda fallen riskerar att framtida produktförbättringar kommer att bryta implementeringen. |
| **Reparation** | Granska flaggade scheman och korrigera identitetstyptilldelningar. Ta bort icke-personidentifierare från enskilda profilscheman när det är möjligt. Information om scheman som redan används av datauppsättningar finns i [schemaförändringsreglerna](/help/xdm/schema/composition.md#evolution). |

När du väljer kortet **[!UICONTROL People & Non-People Identity Config]** öppnas en detaljpanel till höger. Panelen visar:

* **[!UICONTROL Description]**: Verifierar korrekt användning av identitetstyper över schemaklasser. Visar felkonfigurerade scheman och markerar fel tilldelningar.
* **[!UICONTROL Impact]**: Om en icke-personentitet tilldelas en personidentitet ökar detta antalet profiler och gör dessa data oanvändbara som en sökning. Om en personenhet ges en icke-personidentitet är uppgifterna inte tillgängliga för direktuppspelning eller kantsegmentering.
* **[!UICONTROL General areas of impact]**: Ofullständiga identitetsdiagram, uppblåst profilantal, felaktig sökningsanvändning.
* **[!UICONTROL Affected Schemas]**: En lista med scheman med problem. Expandera en schemarad för att visa sökväg, identitetsnamn och schematyp för varje felkonfiguration. Använd länkikonen för att öppna schemat.

![Detaljpanel för identitetskonfiguration för människor och icke-människor som visar beskrivning, påverkan och påverkade scheman med utökningsbara rader](assets/health-checks/people-non-people-identity-detail.png)

Mer information finns i [identitetstypsdokumentationen](/help/identity-service/features/namespaces.md#identity-type) och [schemats bästa praxis](/help/xdm/schema/best-practices.md).

### Beskrivning av namnutrymme för anpassad identitet {#namespace-missing-description}

Söker efter anpassade metadata och beskrivningar för identitetsnamnutrymmen.

| Detalj | Beskrivning |
| --- | --- |
| **Utgåva** | Anpassade ID-namnutrymmen saknar beskrivningsfält. |
| **Effekt** | Beskrivningar som saknas kan leda till förvirring under användning och felsökning. |
| **Reparation** | Dokumentera varje anpassat namnutrymme genom att fylla i beskrivningsfältet. Inkludera valideringskriterier (minsta/högsta längd, mönster) och livscykelinformation som identifierar vilket externt källsystem som skapar dessa identiteter. |

När du väljer kortet **[!UICONTROL Custom Identity Namespace Description]** öppnas en detaljpanel till höger. Panelen visar:

* **[!UICONTROL Description]**: Söker för att säkerställa att namnområdesmetadata och beskrivningar är fullständiga. Visar namnutrymmen och ägare med tomma beskrivningsfält.
* **[!UICONTROL Impact]**: Om du anger en beskrivning för ett anpassat ID-namnområde blir det tydligare eftersom syftet med varje namnutrymme anges i kontexten. Detta gör att teammedlemmar och intressenter snabbt kan förstå funktionen för varje namnutrymme utan att behöva trassla.
* **[!UICONTROL General areas of impact]**: Felsök eller använd förvirring; otydlig verifieringsmetod.
* **[!UICONTROL Experience League Documentation]**: En länk för att skapa anpassade namnutrymmen om du vill ha mer information.
* **[!UICONTROL Affected namespaces]**: En lista med anpassade identitetsnamnutrymmen som saknar beskrivningar. Använd länkikonen bredvid varje namnutrymme för att visa eller redigera det.

![Detaljpanel för beskrivning av namnområde för anpassad identitet med beskrivning, påverkan och lista över namnutrymmen som påverkas](assets/health-checks/custom-namespace-description-detail.png)

Mer information finns i dokumentationen om att [skapa anpassade namnutrymmen](/help/identity-service/features/namespaces.md#create-namespaces).

### Inaktuellt ID-namnutrymme {#deprecated-namespace}

Identifierar föråldrade eller oanvända identitetsnamnutrymmen som ska markeras för rensning.

| Detalj | Beskrivning |
| --- | --- |
| **Utgåva** | Föråldrade ID-namnutrymmen markeras inte som inaktuella. |
| **Effekt** | Oanvända eller föråldrade namnutrymmen skapar förvirring om vad som används och ökar risken för felmärkning av identitetsfält. |
| **Reparation** | Byt namn på namnutrymmen som inte används om du vill inkludera ett prefix av typen &quot;Använd inte&quot; (till exempel &quot;Använd inte - [ursprungligt namn]&quot;). Adobe Experience Platform stöder för närvarande inte borttagning av namnutrymme, så vi rekommenderar att du byter namn. |

När du väljer kortet **[!UICONTROL Deprecated Identity Namespace]** öppnas en detaljpanel till höger. Panelen visar:

* **[!UICONTROL Description]**: Identifierar föråldrade eller oanvända identitetsnamnutrymmen för rensning. Visar namnutrymmen som inte används tillsammans med den senaste tidsstämpeln eller schemareferensen.
* **[!UICONTROL Impact]**: Identitetsnamnutrymmen som inte används i något schema bör markeras för borttagning genom att en DEPRECATED- eller DO NOT USE-tagg läggs till i namnen. Det går inte att ta bort identitetsnamnutrymmen för närvarande.
* **[!UICONTROL General areas of impact]**: Förvirring och felmärkning.
* **[!UICONTROL Experience League Documentation]**: En länk till Föråldrada identitetsnamn om du vill ha mer information.
* **[!UICONTROL Affected namespaces]**: En lista med föråldrade eller oanvända identitetsnamnutrymmen. Använd länkikonen bredvid varje namnutrymme för att visa eller hantera det.

![Detaljpanel för inaktuell namnområdesinformation för identitet med beskrivning, påverkan och lista över namnområden som påverkas](assets/health-checks/deprecated-namespace-detail.png)

Mer information finns i artikeln [Experience Cloud kunskapsbas om föråldrade namnutrymmen](https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-18155){target="_blank"}.

## Nästa steg {#next-steps}

När du har granskat resultaten från hälsokontrollen kan du utforska följande resurser för att fördjupa din förståelse:

* Lär dig mer om [metodtips](/help/xdm/schema/best-practices.md) för att utforma tillförlitliga datamodeller.
* Förstå [identitetsdiagramlänkningsregler](/help/identity-service/identity-graph-linking-rules/overview.md) för att förhindra att profilen komprimeras.
* Granska [dokumentationen för identitetsnamnrymden](/help/identity-service/features/namespaces.md) för bästa praxis för namnområdeshantering.
* Utforska andra [Kör- och operationsverktyg](/help/run-and-operate/overview.md), inklusive [[!UICONTROL Job Schedules]](/help/run-and-operate/job-schedules.md), för synlighet av gruppåtgärd.
