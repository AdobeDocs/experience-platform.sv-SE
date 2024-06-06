---
title: Edge Delivery View
description: Den här guiden innehåller detaljerad information om Edge Delivery-vyn i Adobe Experience Platform Assurance.
source-git-commit: d6b5894a5c5ba3907a8e6dd0d1864f773dd6325c
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# Edge Delivery View in Assurance

The **[!UICONTROL Edge Delivery]** visa inuti **[!UICONTROL Adobe Experience Platform Assurance]** ger möjlighet att inspektera och validera [!UICONTROL AJO Inbound] leverans av meddelanden till era webb- och mobilappar. Den här vyn är särskilt användbar när du vill felsöka leveransen av [!UICONTROL AJO Inbound] webb- och mobilkampanjer och resor.

## Komma igång

Kontrollera att du har tillgång till följande tjänster innan du fortsätter:

- The [Adobe Experience Platform Data Collection UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Så här installerar du **[!UICONTROL Assurance]** kan du läsa [implementera Assurance-guide](../tutorials/implement-assurance.md).

## Använd försäkring med Edge Delivery

När du har öppnat en **[!UICONTROL Assurance]** -session kan du lägga till **[!UICONTROL Edge Delivery]** visa för **[!UICONTROL Assurance]**. Längst ned på den vänstra panelen väljer du **[!UICONTROL Configure]** för att lägga till **[!UICONTROL Edge Delivery]** visa och **Spara** den.

![Lägg till plugin-programmet genom att välja Konfigurera längst ned till vänster](./images/edge-delivery/add-plugin.png)

När du lagt till väljer du **[!UICONTROL Edge Delivery]** visa i **[!UICONTROL Adobe Journey Optimizer]** för att validera inkommande kantleverans.

![Edge Delivery finns i Adobe Journey Optimizer view group](./images/edge-delivery/ajo-plugins.png)

## Lista över förfrågningar

På vys huvudfönster visas en lista med begäranden om kantleverans. Den här listan innehåller alla [!UICONTROL Inbound AJO] förfrågningar som gjorts till Experience Edge och bearbetats av **[!UICONTROL Inbound Delivery Service]**, inklusive förfrågningar om att ta fram personaliseringsbeslut, samt spåra interaktioner för personaliseringsförslag (som visning, klickning, utlösare eller avvisning).

Begäranden beställs med tidsstämpel, med de senaste förfrågningarna överst. Förutom tidsstämpeln innehåller listan även en kolumn för begärande-ID samt typ av begäran, som kan vara något av följande:

- **[!UICONTROL Experience Delivery]**: En begäran om att hämta personaliseringsbeslut
- **[!UICONTROL Experience Interactions]**: En begäran om att spåra interaktioner för personaliseringsförslag
- **[!UICONTROL Experience Delivery & Interactions]**: En begäran om att få tag på personaliseringsbeslut som även omfattar interaktioner för personaliseringsförslag
- **[!UICONTROL Preview Delivery]**: En begäran om att hämta personaliseringsbeslut för förhandsgranskning

Förfrågningar kan också filtreras genom att du anger en sökterm i sökfältet högst upp i listan. Detta är användbart när du filtrerar efter specifika värden, som ID:n.

![Listan över inkommande begäranden visas i huvudvyn](./images/edge-delivery/request-list.png)

## Detaljerade granskningar

När en begäran har valts i huvudvyn visas detaljerad information om den valda begäran till höger. Den här vyn innehåller följande avsnitt:

### Översikt över begäran

I det här avsnittet finns en översikt på hög nivå över den valda begäran, inklusive [!UICONTROL Organization ID], [!UICONTROL Edge cluster], [!UICONTROL Request ID] och [!UICONTROL Request type], [!UICONTROL Sandbox ID], [!UICONTROL Sandbox name], [!UICONTROL Datastream ID]samt en förteckning över begärandeytor om [!UICONTROL Experience Delivery] förfrågningar.

![I avsnittet Översikt över begäran finns information om begäran på hög nivå](./images/edge-delivery/request-overview.png)

### Profil

I det här avsnittet finns information om profildata som används vid bearbetningen av begäran, inklusive inställningar för identitetskarta, segmentmedlemskap och samtycke.\
The [!UICONTROL Profile] -avsnittet är mycket användbart när du felsöker problem som att leveransen inte fungerar som förväntat på grund av att segmentmedlemskapet saknas eller är försenad eller avanmälningsansvarig.

![I profilavsnittet finns identitetskartan, segmentmedlemskap och inställningar för samtycke](./images/edge-delivery/profile.png)

### Kvalificerade aktiviteter

I det här avsnittet finns en lista med aktiviteter som är kvalificerade för den valda begäran, inklusive aktivitetstyp, ID, ID-namnutrymme, ytor, schema och målgrupper. Mer detaljerad information om aktiviteten finns i [spårning av råkörning](#execution).

![Avsnittet Kvalificerade aktiviteter innehåller information om kvalificerade aktiviteter](./images/edge-delivery/qualified-activities.png)

### Icke-kvalificerade aktiviteter

I det här avsnittet finns en lista över aktiviteter som har uteslutits från att kvalificeras. Förutom aktivitetstyp, ID:n, identitetsnamnutrymmen, ytor, scheman och målgrupper innehåller det här avsnittet även en lista med orsaker till varför aktiviteten var okvalificerad.

![Avsnittet Ej kvalificerade aktiviteter innehåller information om okvalificerad aktivitet och orsaker till uteslutning](./images/edge-delivery/unqualified-activities.png)

### Meddelandeinformation

I det här avsnittet finns detaljerad information om de meddelanden som levererades för den valda begäran. Den innehåller meddelande-ID, fragment, beslutsprofiler, [!UICONTROL Offer Decisioning] parametrar samt meddelandets markeringskontext.

![Avsnitt som innehåller levererad meddelandeinformation som meddelande-ID:n och urvalskontext, fragment, beslutsprofiler och beslutsparametrar](./images/edge-delivery/message-details.png)

### Interaktioner

I det här avsnittet finns detaljerad information om de interaktioner som spårades i den valda begäran. Den innehåller interaktionstypen (under `propositionEventType`), samt tillhörande förslagsmetadata, t.ex. aktivitetsmetadata (under `scopeDetails.activity`) och proposition event-token (in `scopeDetails.characteristics.eventToken`).

![Interaktioner spåras via propositionstoken och associerade aktivitetsmetadata](./images/edge-delivery/interactions.png)

### Raw-spår

I det här avsnittet finns de råa spårningarna för den valda begäran. Den innehåller hela spårningen av begäran, inklusive den faktiska begäran som den togs emot i **[!UICONTROL Inbound Delivery Service]**, körningsspårning och svarsspårning. Detta är användbart för avancerad felsökning, t.ex. leverans som inte fungerar som förväntat på grund av att leveranstjänsten inte är tillgänglig, att data saknas eller är felaktiga, eller för att förstå hela flödet av begärandebearbetning.

#### Begäran

Begäranspårningen innehåller den fullständiga begäran som den togs emot av **[!UICONTROL Inbound Delivery Service]** **[!UICONTROL Konductor]** uppströms Den innehåller begäranderubriker, brödtext och andra metadata. XDM-nyttolasten för begäran kan till exempel granskas i `event.body.xdm` fält.

![Detaljerad begärandeinformation med rubriker och brödtext finns i begärandekalkeringen](./images/edge-delivery/request.png)

#### Körning

Körningsspårningen innehåller den fullständiga spårningen för begäran när den bearbetades av **[!UICONTROL Inbound Delivery Service]**. Den visar körningskontext, aktivitetskvalificering, meddelandeurval och andra bearbetningssteg. Eventuella fel eller varningar som uppstod under bearbetningen av begäran finns i `context.messages` och `context.exceptions` fält. Detaljerad information om aktivitetskvalifikationer finns i `context.qualifiedActivitiesDetailed` och `context.unqualifiedActivitiesDetailed` fält.

![Körningsspårning innehåller körningskontext, aktivitetskvalificering, meddelandeval och annan bearbetningsinformation](./images/edge-delivery/execution.png)

#### Svar

Svarsspårningen innehåller det fullständiga svaret som det returnerades av **[!UICONTROL Inbound Delivery Service]** nedåt till **[!UICONTROL Konductor]**. Den innehåller svarshuvuden, brödtext och andra metadata. Hela svarstexten kan inspekteras genom att meddelandet med ID kopieras `1` till Urklipp med **[!UICONTROL Copy Value]** och klistra in den i ett JSON-visningsprogram.

![Svarsspårningen innehåller den fullständiga svarstexten som returneras nedströms](./images/edge-delivery/response.png)
