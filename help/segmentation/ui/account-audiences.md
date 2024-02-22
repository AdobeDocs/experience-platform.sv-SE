---
title: Målgrupper
description: Lär dig hur du skapar och använder kontomålgrupper för att rikta in kontoprofiler på efterföljande destinationer.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 3c0b7c4eee7c790a8ffae95c05a8db6ba7c3b285
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# Målgrupper

>[!AVAILABILITY]
>
>Kontomålgrupper är bara tillgängliga i [B2B Edition av Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b) och [B2P Edition av Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p).

Med kontosegmentering kan Adobe Experience Platform göra marknadsföringssegmenteringen från personbaserade målgrupper till kontobaserade målgrupper så enkel och sofistikerad som möjligt.

Kontomålgrupper kan användas som indata för kontobaserade destinationer, så att ni kan inrikta er på personer inom dessa konton i underordnade tjänster. Du kan till exempel använda kontobaserade målgrupper för att hämta poster för alla konton som gör **not** ha kontaktuppgifter till alla med titeln Chief Operating Officer (COO) eller Chief Marketing Officer (CMO).

## Terminologi {#terminology}

Innan du börjar med kontomålgrupper bör du granska skillnaderna mellan olika typer av målgrupper:

- **Målgrupper**: En målgrupp är en målgrupp som skapas med **konto** profildata. Kontoprofildata kan användas för att skapa målgrupper som riktar sig till personer i efterföljande konton. Mer information om kontoprofiler finns i [kontoprofilöversikt](../../rtcdp/accounts/account-profile-overview.md).
- **Målgrupper**: En publik är en publik som skapats med **kund** profildata. Kundprofildata kan användas för att skapa målgrupper som riktar sig till företagets kunder. Mer information om kundprofiler finns i [Översikt över kundprofiler i realtid](../../profile/home.md).
- **Potentiella målgrupper**: En potentiell målgrupp är en målgrupp som skapats med **potentiell** profildata. Prospektprofildata kan användas för att skapa målgrupper från oautentiserade användare. Mer information om profiler för potentiella kunder finns i [översikt över potentiella kundprofiler](../../profile/ui/prospect-profile.md).

## Åtkomst {#access}

Om du vill få åtkomst till målgrupper väljer du **[!UICONTROL Audiences]** i **[!UICONTROL Accounts]** -avsnitt.

![Knappen Publiker markeras i avsnittet Konton.](../images/ui/account-audiences/select.png)

The [!UICONTROL Browse] visas, med en lista över alla kontomunkter för organisationen.

![De kontomålgrupper som tillhör organisationen visas.](../images/ui/account-audiences/browse.png)

I den här vyn visas information om målgruppen, inklusive namn, antal profiler, ursprung, livscykelstatus, skapat datum och senaste uppdateringsdatum.

## Skapa målgrupper {#create}

Om du vill skapa en kontopublik väljer du **[!UICONTROL Create audience]** på [!UICONTROL Browse] sida.

![The [!UICONTROL Create audience] knappen markeras på kontomålsidans webbsida.](../images/ui/account-audiences/select-create-audience.png)

Segmentbyggaren visas. Kontoattributen visas i det vänstra navigeringsfältet.

![Segmentbyggaren visas. Observera att bara attributen visas.](../images/ui/account-audiences/segment-builder.png)

När du skapar kontomålgrupper bör du tänka på att händelser listas under **[!UICONTROL People]**, i stället för att vara deras egen flik, eftersom dessa attribut är kopplade till personer.

![Platsen där du söker efter händelser, som finns i [!UICONTROL People] , är markerad.](../images/ui/account-audiences/attributes.png)

Mer information om hur du använder Segment Builder finns i [Användargränssnittsguide för segmentbyggare](./segment-builder.md).

## Aktivera målgrupp {#activate}

>[!NOTE]
>
>Endast ett begränsat antal destinationer har stöd för målgrupper på konton. Kontrollera att den destination som du vill aktivera har stöd för kontomålgrupper innan du fortsätter med den här processen.

När du har skapat din kontopublik kan du aktivera målgruppen för andra tjänster längre fram i kedjan.

Välj den målgrupp som du vill aktivera, följt av **[!UICONTROL Activate to destination]**.

![The [!UICONTROL Activate to destination] knappen markeras på snabbåtgärdsmenyn för den valda målgruppen.](../images/ui/account-audiences/activate.png)

The [!UICONTROL Activate destination] visas. Mer information om aktiveringsprocessen, inklusive destinationer som stöds och information om fältkopplingar finns i [aktivera kontomålgrupper](/help/destinations/ui/activate-account-audiences.md) självstudie.

## Nästa steg {#next-steps}

När du har läst den här guiden får du nu en bättre förståelse för hur du skapar och använder kontomålgrupper i Adobe Experience Platform. Läs mer om hur du använder andra typer av målgrupper i Platform i [Användargränssnittsguide för segmenteringstjänst](./overview.md).

## Bilaga {#appendix}

Följande avsnitt innehåller ytterligare information om kontomaterial.

### Validering av kontosegmentering {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Maximalt uppslagsfönsterfel"
>abstract="Det maximala uppslagsfönstret för Experience Events är 30 dagar."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Största antal kapslade behållardjupfel"
>abstract="Det maximala djupet för kapslade behållare är **5**. Det betyder att du **inte** har fler än fem kapslade behållare när du skapar din målgrupp."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Högsta regelbeloppsfel"
>abstract="Det högsta antalet regler i en enskild behållare är **5**. Det betyder att du **inte** har mer än fem regler i en och samma behållare när du skapar din målgrupp."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Största korsenhetsbeloppsfel"
>abstract="Det högsta antalet korsentiteter som kan användas inom en enskild målgrupp är **5**. En korsenhet är när du ändrar mellan olika enheter inom målgruppen. Du kan till exempel gå från ett konto till en person till en marknadsföringslista."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Fel för anpassad entitet"
>abstract="Anpassade entiteter **not** tillåtna."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="Ogiltigt B2B-entitetsfel"
>abstract="Endast följande B2B-enheter får användas: `_xdm.context.account`, `_xdm.content.opportunity`, `_xdm.context.profile`, `_xdm.context.experienceevent`, `_xdm.context.account-person`, `_xdm.classes.opportunity-person`, `_xdm.classes.marketing-list-member`, `_xdm.classes.marketing-list`, `_xdm.context.campaign-member`och `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="Fel med högsta värden"
>abstract="Det högsta antalet värden som kan kontrolleras för ett enskilt fält är **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="inSegment-händelsefel"
>abstract="inSegment-händelser är **not** tillåtna."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="inSegment-händelsefel"
>abstract="inSegment-händelser är **not** tillåtna."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Sekventiellt händelsefel"
>abstract="Sekventiella händelser är **not** tillåtna."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Egenskapsfel av typen Map"
>abstract="Karttypegenskaper är **not** tillåtna."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Största antal kapslade entitetsdjupfel"
>abstract="Det maximala djupet för kapslade arrayer är **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Högsta antal kapslade objekt-fel"
>abstract="Högsta tillåtna antal kapslade objekt är **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Begränsningsöverträdelse"
>abstract="Publiken bryter mot en begränsning. Läs det länkade dokumentet för mer information."

När ni använder kontomålgrupper är målgruppen **måste** följer följande begränsningar:

>[!NOTE]
>
>I följande lista visas **standard** begränsningar för kontomålgrupper. Dessa värden **kan** ändras beroende på inställningarna som implementeras av organisationens administratör.

- Det maximala uppslagsfönstret för Experience Events är **30 dagar**.
- Det maximala djupet för kapslade behållare är **5**.
   - Det betyder att du **inte** har fler än fem kapslade behållare när du skapar din målgrupp.
- Det högsta antalet regler i en enskild behållare är **5**.
   - Detta innebär att er målgrupp **inte** har mer än fem regler som sätter er målgrupp i botten.
- Det högsta antalet korsentiteter som kan användas är **5**.
   - En korsenhet är när du ändrar mellan olika enheter inom målgruppen. Du kan till exempel gå från ett konto till en person till en marknadsföringslista.
- Anpassade entiteter **inte** användas.
- Det högsta antalet värden som kan kontrolleras för ett enskilt fält är **50**.
   - Om du till exempel har fältet&quot;Ortnamn&quot; kan du kontrollera det värdet mot 50 stadsnamn.
- Målgrupper **inte** use `inSegment` händelser.
- Målgrupper **inte** använda sekventiella händelser.
- Målgrupper **inte** använd kartor.
- Det maximala djupet för kapslade arrayer är **5**.
- Det högsta antalet kapslade objekt är **10**.
