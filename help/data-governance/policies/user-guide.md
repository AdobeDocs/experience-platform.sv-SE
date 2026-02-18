---
keywords: Experience Platform;hem;populära ämnen;datastyrning;användarhandbok för dataanvändningspolicy
solution: Experience Platform
title: Hantera dataanvändningsprinciper i användargränssnittet
description: Adobe Experience Platform Data Governance har ett användargränssnitt där du kan skapa och hantera dataanvändningspolicyer. Det här dokumentet innehåller en översikt över de åtgärder som du kan utföra på arbetsytan Profiler i Experience Platform användargränssnitt.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 364a92bde1a1629d2811e7ff16bd6a4fb5287249
workflow-type: tm+mt
source-wordcount: '2380'
ht-degree: 0%

---

# Hantera dataanvändningsprinciper i användargränssnittet {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="Integrera och få kundens samtycke i era profildata"
>abstract="<h2>Beskrivning</h2><p>Med Experience Platform kan ni integrera de data ni samlat in från era kunder i deras respektive profiler. Du kan sedan ange profiler för samtycke för att avgöra om dessa data kan inkluderas i segment som aktiveras för vissa destinationer.</p>"

Det här dokumentet beskriver hur du använder arbetsytan **[!UICONTROL Policies]** i Adobe Experience Platform-gränssnittet för att skapa och hantera dataanvändningsprinciper.

>[!NOTE]
>
>Mer information om hur du hanterar åtkomstkontrollprinciper i användargränssnittet finns i [gränssnittsguiden för attributbaserad åtkomstkontroll](../../access-control/abac/ui/policies.md) i stället.

>[!IMPORTANT]
>
>Alla dataanvändningspolicyer (inklusive kärnpolicyer från Adobe) är inaktiverade som standard. För att en enskild princip ska kunna användas för verkställighet måste du manuellt aktivera den principen. I avsnittet [Aktivera principer](#enable) finns mer information om hur du gör detta i användargränssnittet.

## Förhandskrav

Handboken kräver en fungerande förståelse av följande [!DNL Experience Platform]-koncept:

* [Dataförvaltning](../home.md)
* [Dataanvändningspolicyer](./overview.md)

## Visa befintliga policyer {#view-policies}

I gränssnittet för [!DNL Experience Platform] väljer du **[!UICONTROL Policies]** för att öppna arbetsytan för **[!UICONTROL Policies]**. På fliken **[!UICONTROL Browse]** kan du se en lista över tillgängliga principer, inklusive deras associerade etiketter, marknadsföringsåtgärder och status.

![](../images/policies/browse-policies.png)

Om du har åtkomst till profiler för samtycke väljer du **[!UICONTROL Consent policies]** för att visa dem på fliken [!UICONTROL Browse].

![](../images/policies/consent-policy-toggle.png)

Välj en listad profil för att visa dess beskrivning och typ. Om en anpassad profil väljs visas ytterligare kontroller för att redigera, ta bort eller [aktivera/inaktivera profilen](#enable).

![](../images/policies/policy-details.png)

## Skapa en anpassad profil {#create-policy}

Om du vill skapa en ny anpassad dataanvändningsprincip väljer du **[!UICONTROL Create policy]** i det övre högra hörnet på fliken **[!UICONTROL Browse]** på arbetsytan i **[!UICONTROL Policies]**.

![](../images/policies/create-policy-button.png)

Dialogrutan [!UICONTROL Choose type of policy] visas. Välj antingen en [medgivandeprincip](#consent-policy) eller en [datastyrningsprincip](#create-governance-policy).

![Dialogrutan Välj typ av princip.](../images/policies/choose-policy-type.png)

### Använd datastyrning och godkännandeprinciper tillsammans {#combine-policies}

>[!NOTE]
>
>Samtyckesregler är för närvarande endast tillgängliga för organisationer som har köpt Adobe Healthcare Shield eller Adobe Privacy &amp; Security Shield.

Regler för styrning och samtycke kan användas tillsammans för att skapa robusta regler för styrning av målgrupper som mappas till en destination. Samtyckesregler är inkluderande till sin natur, vilket innebär att de avgör vilka profiler som kan inkluderas i varje marknadsföringsupplevelse. På samma sätt utesluter styrningsprinciper användning av specifika märkta attribut från konfigurering för aktivering.

Genom att använda det här beteendet kan du skapa en kombination av profiler och regler för samtycke som innehåller rätt profiler, men förhindrar att du tar med data som strider mot de angivna organisationsreglerna. Ett exempel är när man vill utesluta känsliga data från att inkluderas, men ändå kan rikta sig till godkända användare för marknadsföring via sociala medier. Nödvändiga steg för detta scenario beskrivs i informationsbilden nedan.

![En infografik som visar stegen för att använda styrnings- och medgivandeprinciper tillsammans för att skapa robusta regler för målgrupper.](../images/policies/governance-and-consent-policies-infographic.png)

### Skapa en datastyrningspolicy {#create-governance-policy}

Arbetsflödet **[!UICONTROL Create policy]** visas. Börja med att ange ett namn och en beskrivning för den nya principen.

![](../images/policies/create-policy-description.png)

Välj sedan de dataanvändningsetiketter som profilen ska baseras på. När du väljer flera etiketter kan du välja om informationen ska innehålla alla etiketter eller bara en av dem för att profilen ska kunna användas. Välj **[!UICONTROL Next]** när du är klar.

![](../images/policies/add-labels.png)

**[!UICONTROL Select marketing actions]**-steget visas. Välj lämpliga marknadsföringsåtgärder i listan och välj sedan **[!UICONTROL Next]** för att fortsätta.

>[!NOTE]
>
>När man väljer flera marknadsföringsåtgärder tolkas de som en &quot;OR&quot;-regel. Med andra ord gäller principen om **någon** av de valda marknadsföringsåtgärderna utförs.

![](../images/policies/add-marketing-actions.png)

Steg **[!UICONTROL Review]** visas, så att du kan granska informationen om den nya profilen innan du skapar den. När du är nöjd väljer du **[!UICONTROL Finish]** för att skapa profilen.

![](../images/policies/policy-review.png)

Fliken **[!UICONTROL Browse]** visas igen, där den nya principen visas med statusen Utkast. Om du vill aktivera profilen går du till nästa avsnitt.

![](../images/policies/created-policy.png)

### Skapa en medgivandeprincip {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="Instruktioner"
>abstract="<ul><li>Se till att du samlar in inställningsdata i dina fackliga scheman via OneTrust-källkopplingen eller XDM-standardschemat för samtycke.</li><li>Välj <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html">Profiler</a> i den vänstra navigeringen och välj sedan <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">Skapa profil</a>.</li><li>Beskriv villkoren eller åtgärderna som kommer att utlösa principkontrollen under avsnittet <b>If</b>.</li><li>Under avsnittet <b>Sedan</b> anger du de medgivandeattribut som måste finnas för en profil som ska inkluderas i den åtgärd som utlöste principen.</li><li>Välj <b>Spara</b> för att skapa profilen. Om du vill aktivera principen väljer du alternativet <b>Status</b> i den högra listen.</li><li>Experience Platform tillämpar automatiskt de regler för samtycke du har aktiverat när du aktiverar segment till destinationer och ger information om hur varje policy påverkar målgruppens storlek.</li><li>Mer hjälp om den här funktionen finns i guiden <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#consent-policy">Skapa medgivandeprinciper</a> för Experience League.</li></ul>"

>[!IMPORTANT]
>
>Samtyckespolicyer är bara tillgängliga för organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**.

Om du väljer att skapa en profil för samtycke visas en ny skärm där du kan konfigurera den nya principen.

![](../images/policies/consent-policy-dialog.png)

Om du vill kunna använda profiler för samtycke måste du ha attribut för samtycke i dina profildata. I guiden om [medgivandebearbetning i Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) finns detaljerade anvisningar om hur du inkluderar de nödvändiga attributen i ditt unionsschema.

Samtyckesprinciper består av två logiska komponenter:

* **[!UICONTROL If]**: Villkoret som utlöser principkontrollen. Detta kan baseras på en viss marknadsföringsåtgärd som utförs, förekomsten av vissa dataanvändningsetiketter eller en kombination av de två.
* **[!UICONTROL Then]**: Medgivandeattributen som måste finnas för att en profil ska kunna inkluderas i åtgärden som utlöste principen.

>[!NOTE]
>
>Samtyckesprinciper stöder avancerad regelgenerering med olika fälttyper och operatorer. En fullständig referens till fälttyper, operatorer och exempel på regelgenerering som stöds finns i [Referens för policyregler för samtycke](./consent-policy-rule-building-reference.md).

#### Konfigurera villkor {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Om villkor"
>abstract="Börja med att definiera villkoren som utlöser principkontrollen. Villkoren kan omfatta vissa marknadsföringsåtgärder som vidtas, vissa datastyrningsetiketter finns eller en kombination av båda. Använd AND/OR-logik för att skapa komplexa villkorsstyrda relationer mellan flera villkor."

Under avsnittet **[!UICONTROL If]** väljer du de marknadsföringsåtgärder och/eller etiketter för dataanvändning som ska utlösa den här principen. Välj **[!UICONTROL View all]** och **[!UICONTROL Select labels]** om du vill visa en fullständig lista över tillgängliga marknadsföringsåtgärder och etiketter.

När du har lagt till minst ett villkor kan du välja **[!UICONTROL Add condition]** om du vill fortsätta lägga till ytterligare villkor efter behov och välja lämplig villkorstyp i listrutan.

![](../images/policies/add-condition.png)

Om du markerar mer än ett villkor kan du använda ikonen som visas mellan dem för att växla den villkorliga relationen mellan &quot;AND&quot; och &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Välj medgivandeattribut {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Villkor"
>abstract="När ditt If-villkor har definierats kan du använda sektionen &#39;then&#39; för att välja minst ett medgivandeattribut från unionsschemat. Du måste navigera i behållarfält (Object, Map, Array) för att kunna nå primitiva fält (String, Number, Boolean osv.) för att skapa regler. Det här primitiva fältet är det attribut som måste finnas för att profiler ska kunna inkluderas i åtgärden som styrs av den här principen."

Under avsnittet **[!UICONTROL Then]** väljer du minst ett medgivandeattribut från unionsschemat. Det här är attributet som måste finnas för att profiler ska kunna inkluderas i åtgärden som styrs av den här principen. Du kan välja ett av de föreslagna alternativen eller välja **[!UICONTROL View all]** för att välja attributet direkt från unionsschemat.

>[!NOTE]
>
>Samtyckesprofiler stöder primitiva fälttyper (String, Number, Boolean, Date) och behållartyper (Object, Map, Array). Du kan navigera i behållare för att välja specifika attribut och använda AND/OR-logik för att kombinera regler. En fullständig referens till fälttyper, operatorer och exempel på regelgenerering som stöds finns i [referenshandboken för regelgenerering för medgivande](./consent-policy-rule-building-reference.md).

![Gränssnittet för principbyggaren för samtycke visar avsnitten Om och sedan med Visa alla markerade.](../images/policies/view-all.png)

Om du väljer **[!UICONTROL View all]** visas dialogrutan **[!UICONTROL Select consent attribute]**. Välj det eller de medgivandeattribut som du vill att den här principen ska kontrollera. I den här dialogrutan kan du också välja **[!UICONTROL Advanced Schema search]** för att välja ett kapslat primitivt fält som ska bedömas som en del av principen. Välj **[!UICONTROL Done]** för att bekräfta dina inställningar.

![Dialogrutan Välj medgivande-attribut med ett attribut markerat.](../images/policies/select-consent-attribute.png)

### Avancerad schemasökning {#advanced-schema-search}

I dialogrutan **[!UICONTROL Select consent attribute]** väljer du **[!UICONTROL Advanced Schema search]** för att öppna dialogrutan **[!UICONTROL Select union schema field]**. I den här vyn väljer du attribut på rotnivå eller kapslade för primitiva fälttyper som sträng, tal, booleskt värde och datum samt behållartyper som objekt, karta och array.

![Klicksökvägen för att navigera i den avancerade schemasökningen.](../images/policies/consent-advanced-schema-search.gif)

#### Fält med fast värde för ett policyvillkor {#fixed-value-fields}

När du väljer ett fält med fast värde som ett principvillkor visas de fördefinierade värdena som definierats i ditt dataschema på panelen [!UICONTROL Selected attributes].

>[!NOTE]
>
>Om ett fält har konfigurerats med en fast uppsättning värden (till exempel som en uppräkning eller annan kontrollerad vokabulär) tillämpar principbyggaren den begränsningen för att se till att villkoren bara utvärderas mot giltiga, standardiserade data.

För att upprätthålla datakvalitet och konsekvens återges dessa värden som valbara kryssrutor i stället för som fritextfält. Den här metoden minskar den manuella valideringen och hjälper er att utvärdera data på ett tillförlitligt sätt.

Om du vill definiera villkoret markerar du kryssrutorna för de värden som du vill att profilen ska utvärdera.

![Dialogrutan Välj unionsschemafält med ett schema-diagramfält och de tillgängliga kryssrutorna för fasta värden är markerade.](../images/policies/select-schema-field.png)

#### Mappa datatypfält för ett principvillkor {#map-data-type-fields}

När du markerar ett primitivt fält som finns i datatypen Map visas ytterligare konfigurationsalternativ på panelen **[!UICONTROL Selected attributes]**. Använd dessa alternativ för att konfigurera godkännandekontroller för flera nycklar utan att behöva använda en separat profil för varje nyckel. Den här konfigurationsmetoden förenklar hanteringen av principer genom att minska antalet principer du måste skapa.

![Avsnittet Samtyckesprofilsmappning är markerat på attributpanelen.](../images/policies/consent-policies-map.png)

##### Konfigurera attribut för kartdatatyp {#configure-map-attributes}

Så här konfigurerar du ett attribut av typen Karta:

Välj ett primitivt fält (till exempel en sträng eller ett tal) som finns i datatypen Map i unionsschemat. Panelen **[!UICONTROL Selected attributes]** uppdateras för att visa ytterligare konfigurationsalternativ för det fältet.

![Uppdaterade attributalternativ för ett primitivt fält som finns i datatypen Map.](../images/policies/select-union-schema-field.png)

Konfigurera hur principen utvärderar kartnycklar på panelen **[!UICONTROL Selected attributes]** genom att markera eller avmarkera kryssrutan **[!UICONTROL Find any matching item]**.

| Alternativ | Åtgärd | Principbeteende |
| --- | --- | --- |
| Kryssrutan **[!UICONTROL Find any matching item]** är **markerad** | Textfältet **[!UICONTROL within]** är inaktiverat. | Principen kontrollerar **alla nycklar** på kartan. Alla nycklar där det kapslade fältet uppfyller värdevillkoret betraktas som en matchning för principen. Detta är användbart när du vill genomdriva global överensstämmelse för dynamiskt keyade attribut. |
| Kryssrutan **[!UICONTROL Find any matching item]** är **omarkerad** | Du måste ange ett specifikt nyckelnamn i textfältet **[!UICONTROL within]**. | Principen kontrollerar bara den mappningsnyckel som anges i fältet **[!UICONTROL within]**. Endast profiler där det kapslade fältet för en viss nyckel uppfyller det definierade värdet matchas. Detta är användbart för principer som har ett specifikt program eller en viss frekvensnyckel som mål (till exempel `frequencyMap.m1`). |

Ange värdet för det valda primitiva fältet som profilen ska utvärdera. Om fälttypen till exempel är `Integer` anger du ett numeriskt värde.

![Sidofältet Markerade attribut med kartkonfigurationsalternativen markerade.](../images/policies/within-option.png)

Välj **[!UICONTROL Select]** för att bekräfta konfigurationen och återgå till principbyggaren.

När du har valt minst ett medgivandeattribut uppdateras panelen **[!UICONTROL Policy properties]** så att det beräknade antalet profiler som ingår i den här principen visas, tillsammans med procentandelen profiler som påverkas i profilarkivet. Det uppskattade antalet profiler uppdateras automatiskt när du ändrar principkonfigurationen.

![Gränssnittet för principbyggaren visar ett konfigurerat villkor med principegenskaperna till höger som visar antalet beräknade kvalificerade profiler.](../images/policies/audience-preview.png)

Om du vill lägga till ytterligare medgivandeattribut väljer du **[!UICONTROL Add result]**. Då skapas en annan regel för att inkludera profiler som baseras på dessa attribut.

![Gränssnittet för principbyggaren för samtycke med Lägg till resultat markerat.](../images/policies/add-result.png)

>[!NOTE]
>
>Om du vill redigera ett befintligt attribut markerar du attributnamnet och väljer sedan pennikonen (![En pennikon.](/help/images/icons/edit.png)). Dialogrutan **[!UICONTROL Select union schema field]** öppnas så att du kan göra ändringar.
>
>![Gränssnittet för principbyggaren för samtycke med attributet för samtycke och redigeringsikonen markerad.](../images/policies/edit-then-attributes.png)

Fortsätt lägga till eller justera villkor och medgivandeattribut tills profilen matchar dina krav. När du är klar anger du ett namn och en (valfri) beskrivning och väljer sedan **[!UICONTROL Save]** för att skapa profilen.

![](../images/policies/name-and-save.png)

Medgivandeprincipen skapas nu och dess status är inställd på [!UICONTROL Disabled] som standard. Om du vill aktivera principen direkt väljer du alternativet **[!UICONTROL Status]** i den högra listen.

![](../images/policies/enable-consent-policy.png)


#### Verifiera policytillämpning

När du har skapat och aktiverat en medgivandeprincip kan du förhandsgranska hur den påverkar de godkända målgrupperna när du aktiverar segment till mål. Mer information finns i avsnittet [utvärdering av principen för samtycke](../enforcement/auto-enforcement.md#consent-policy-evaluation).

## Aktivera eller inaktivera en profil {#enable}

Alla dataanvändningspolicyer (inklusive kärnpolicyer från Adobe) är inaktiverade som standard. För att en enskild princip ska kunna användas måste du manuellt aktivera den principen via API:t eller användargränssnittet.

Du kan aktivera eller inaktivera profiler på fliken **[!UICONTROL Browse]** på arbetsytan i **[!UICONTROL Policies]**. Välj en anpassad profil i listan för att visa informationen till höger. Under **[!UICONTROL Status]** markerar du växlingsknappen för att aktivera eller inaktivera principen.

![](../images/policies/enable-policy.png)

## Visa marknadsföringsaktiviteter {#view-marketing-actions}

På arbetsytan **[!UICONTROL Policies]** väljer du fliken **[!UICONTROL Marketing actions]** för att visa en lista över tillgängliga marknadsföringsåtgärder som definierats av Adobe och din egen organisation.

![](../images/policies/marketing-actions.png)

## Skapa en marknadsföringsåtgärd {#create-marketing-action}

Om du vill skapa en ny anpassad marknadsföringsåtgärd väljer du **[!UICONTROL Create marketing action]** i det övre högra hörnet på fliken **[!UICONTROL Marketing actions]** på arbetsytan i **[!UICONTROL Policies]**.

![](../images/policies/create-marketing-action.png)

Dialogrutan **[!UICONTROL Create marketing action]** visas. Ange ett namn och en beskrivning för marknadsföringsåtgärden och välj sedan **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

Den nyligen skapade åtgärden visas på fliken **[!UICONTROL Marketing actions]**. Du kan nu använda marknadsföringsåtgärden när du [skapar nya dataanvändningsprinciper](#create-policy).

![](../images/policies/created-marketing-action.png)

## Redigera eller ta bort en marknadsföringsåtgärd {#edit-delete-marketing-action}

>[!NOTE]
>
>Endast anpassade marknadsföringsåtgärder som definieras av din organisation kan redigeras. Marknadsföringsåtgärder som definieras av Adobe kan inte ändras eller tas bort.

På arbetsytan **[!UICONTROL Policies]** väljer du fliken **[!UICONTROL Marketing actions]** för att visa en lista över tillgängliga marknadsföringsåtgärder som definierats av Adobe och din egen organisation. Välj en anpassad marknadsföringsåtgärd i listan och använd sedan fälten i den högra delen för att redigera information om marknadsföringsåtgärden.

![](../images/policies/edit-marketing-action.png)

Om marknadsföringsåtgärden inte används av någon befintlig användarprofil kan du ta bort den genom att välja **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Om du försöker ta bort en marknadsföringsåtgärd som används av en befintlig princip visas ett felmeddelande som anger att borttagningsförsöket misslyckades.

![](../images/policies/delete-marketing-action.png)

## Nästa steg

Det här dokumentet innehåller en översikt över hur du hanterar dataanvändningsprinciper i användargränssnittet för [!DNL Experience Platform]. Anvisningar om hur du hanterar principer med [!DNL Policy Service API] finns i [utvecklarhandboken](../api/getting-started.md). Mer information om hur du tillämpar dataanvändningsprinciper finns i [efterlevnadsöversikten](../enforcement/overview.md).

I följande video visas hur du arbetar med användarprofiler i användargränssnittet i [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
