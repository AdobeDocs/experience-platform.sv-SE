---
solution: Experience Platform
title: Användargränssnittsguide för spelböcker
description: Lär dig hur du använder användargränssnittet i Experience Platform för att visa och aktivera spelböcker.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---


# (Beta) Så här aktiverar och återanvänder du en spelbok

>[!AVAILABILITY]
>
>Den här funktionen finns för närvarande i betaversionen och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Om du vill använda en spelbok går du till **[!UICONTROL Use Case Playbooks]>[!UICONTROL Playbooks]**. Bläddra och använd de olika sök- och filtreringsalternativen på sidan för att välja och komma igång med en viss spelbok.

## Söka och filtrera {#search-and-filter}

Använd sökfönstret och filtren som finns på sidan för att hitta rätt spelbok för ditt användningssätt.

Du kan till exempel filtrera spelböcker som du kan använda baserat på den fas i marknadsföringstratten som du vill ha som mål - konvertering, engagemang eller lojalitet. Du kan även filtrera de spelböcker som visas efter den bransch du befinner dig i eller det produktberättigande som du har tillgång till - Adobe Journey Optimizer eller CDP i realtid.

![Filtrera spelböcker efter marknadsföringstratt, bransch eller produkt](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

Du kan också använda sökfunktionen för att hitta rätt spelbok. Nedan visas ett exempel på hur du kan hitta en spelbok som hjälper dig att interagera med användare som kanske har övergett sin kundvagn.

![Engagera med användare som kanske har övergett sin kundvagn.](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

Eller så kan du filtrera de tillgängliga spelböckerna efter de kanaler som du tänker använda för att nå dina kunder, vilket visas nedan:

![Filtrera efter kanal](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

Experimentera med filter och sökalternativ och hitta rätt spelbok för dig.

## Visa spelbok och generera resurser {#view-playbook-generate-assets}

Innan du slutför en spelbok och skapar instanser av den bör du kontrollera att den passar dina behov. För att du bättre ska förstå vilka användningsområden de omfattar innehåller alla spelböcker avsnitten som listas nedan. När du är redo att fortsätta och generera resurser väljer du **[!UICONTROL Create Instance]**.

### Mindmap {#mindmap}

Använd mindmap-avsnittet i en spelbok för att förstå de steg i arbetsflödet som spelboken kan hjälpa dig att lösa. Visualisera flödet av hur alla genererade objekt kan hjälpa dig att uppnå användningsfallet, utifrån den personlighet som är vald i användningsfallet.

Mindmap börjar med en definition av vem som nås i användarresan och beskriver i varje steg om något levereras av Adobe, som ett nytt meddelande eller en påminnelse, eller om det är något som målpersonen gjorde som utlöser nästa meddelande eller händelse.

![Playbook mindmap selected.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### Sammanfattning {#summary}

Inspect sammanfattningsavsnittet för att förstå vilka resurser som genereras när du skapar instanser från spelboken. Resurserna som genereras för varje spelningsbok är anpassade efter användningsfallet som spelningsboken aktiverar. Hämta mer information nedan om alla objekt i sammanfattningsavsnittet.

| Objekt | Beskrivning |
---------|----------|
| **[!UICONTROL Target audience]** | Beskriver de profiler som du vill nå genom den här användningsfallsspelboken. |
| **[!UICONTROL Marketing Channels]** | Beskriver de kanaler som används för att nå de profiler som spelboken riktar sig till. |
| **[!UICONTROL Technical assets]** | En lista med tekniska resurser som genereras när du har skapat instanser av spelboken. De genererade resurserna skiljer sig åt i spelboken, beroende på användningsfallet. Vissa spelböcker kan generera scheman, segment och resor. Andra kan generera destinationer. Se [Förstå genererade tillgångar](#understand-assets) nedan för mer information om hur du kan använda och återanvända de genererade resurserna. |

{style="table-layout:auto"}

![Spelbokssammanfattning markerad](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### Instanser {#instances}

Bläddra ned till avsnittet med instanser för att få en översikt över de instanser av den här spelboken som du eller medlemmar i ditt team redan har skapat. Du kan använda olika kontroller för att sortera och filtrera de förekomster som visas, t.ex. för att endast visa de som du har skapat. Du kan även se olika information om varje instans enligt nedan.

| Objekt | Beskrivning |
|---------|----------|
| **[!UICONTROL Name]** | Namnet på instansen baserat på spelningsboken. Du kan anpassa namnet och beskrivningen för en instans. Läs avsnittet nedan [redigera instansmetadata](#edit-instance-metadata) för mer information. |
| **[!UICONTROL Status]** | Anger instansens status. A **[!UICONTROL submitted]** -instansen är klar att användas. |
| **[!UICONTROL Created]** | Anger när instansen skapades. |
| **[!UICONTROL Created By]** | Anger vem som skapade instansen. |
| **[!UICONTROL Last Modified]** | Anger när instansen senast ändrades. |

{style="table-layout:auto"}

![Playbook-instansen är markerad.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## Aktivera spelningsboken {#enable-playbook}

När du är redo att fortsätta med en spelbok och skapa en instans väljer du **[!UICONTROL Create Instance]** för att fortsätta med spelboken och generera tekniska resurser.

![Skapa en instans av en spelningsbok.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Den här åtgärden genererar flera resurser som du kan använda för att uppnå det användningsfall som beskrivs i spelboken.

![Spelboksvy över genererade resurser när de har aktiverats.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Använd konfigurationskontrollerna för att redigera instansnamn och beskrivningar {#edit-instance-metadata}

När du har skapat en instans baserad på en spelningsbok kan du anpassa den så att den skiljer sig från andra instanser som skapats från samma spelningsbok. Välj konfigurationskontrollen enligt nedan. Redigera namn, beskrivning och anteckningar och välj **[!UICONTROL Save]** när du är klar.

![Redigera namn och beskrivning för en instans.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Förstå genererade tillgångar {#understand-assets}

>[!IMPORTANT]
>
>Du behöver inte oroa dig! Det här är ett säkert utrymme att experimentera och du kan inte knäcka någonting. Det finns inga data som är associerade med de resurser du skapar. Du måste först importera data för att uppnå användningsexemplen.

Det är viktigt att förstå att de genererade resurserna skiljer sig åt beroende på vilket användningsfall du aktiverar:

* Olika resurser genereras för olika typer av spelböcker. Dessa resurser skapas specifikt för det användningsfall som uppnås via spelboken. En spelningsbok genererar till exempel ett schema, ett segment, en resa och meddelanden. En annan spelningsbok genererar ett schema, ett segment och ett mål som data ska aktiveras till.
* Resurserna skiljer sig åt mellan spelböcker. För **[!UICONTROL Send A Birthday Message To Guests]** spelbok, målgruppen som skapas har regeln `birthday=today AND year=any`.

Så här illustrerar du ett exempel för **[!UICONTROL Abandoned Cart: Merchandise]** spelbok, kan du se att en viss resa skapas som innehåller de meddelanden som har skapats för det här användningsfallet.

![Resan skapad från fallspelsbok.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Använda och redigera genererade resurser {#use-and-edit-assets}

När du utforskar de resurser som genereras när du har skapat en instans av en spelbok kan du redigera alla resurser som skapas.

Om du eller någon i ditt team skapar en annan instans av spelboken behålls de redigerade resurserna och nya resurser skapas för den nya instansen av spelboken.

Beteendet som beskrivs ovan gäller för alla resurser som skapas, förutom scheman. När det gäller scheman skapas inga nya scheman när en ny instans av en spelningsbok skapas, så du kommer att använda det redigerade schemat från en annan instans av spelningsboken i den nyligen skapade instansen.

>[!TIP]
>
>Testa i utvecklingssandlådan och gå till produktion när det är klart.
>
>När objekt har genererats kan du fortsätta att testa dem i utvecklingssandlådorna genom att lägga till data. Du kan testa resurserna så länge du vill i utvecklingssandlådan och du kan replikera resurslogiken (segmentdefinitioner, resor, scheman och så vidare) i produktionssandlådan när du är klar.

### Återanvänd spelningsböcker {#reuse-playbooks}

Genom att skapa flera instanser av samma spelningsbok kan du implementera samma användningsfall senare, utan att ändra informationen om den tidigare implementeringen av användningsexemplet.

### Dela spelboken och de genererade resurserna med andra teammedlemmar {#share-playbook}

Du kan dela den genererade instansen och resurserna med andra teammedlemmar. Om du vill göra det kopierar du URL-länken från webbläsaren och delar den med ditt team för att ge dem en översikt över de genererade resurserna.

![URL-adressen är markerad i en fallspelningsboksvy.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Nästa steg {#next-steps}

Genom att läsa den här gränssnittshandboken kan du nu tolka de olika avsnitten i en spelbok och hur du använder de resurser som genereras när du har skapat en instans av en spelbok. Därefter kan du bläddra i katalogen med spelböcker för att hitta rätt spelbok för ditt användningsfall och läsa felsökningsguiden om du råkar ut för några fel.