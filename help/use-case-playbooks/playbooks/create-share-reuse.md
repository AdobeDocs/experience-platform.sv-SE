---
solution: Experience Platform
title: Skapa, dela och återanvända spelningsboksinstanser
description: Lär dig hur du skapar, delar och återanvänder spelningsboksinstanser för att få fram ett marknadsföringsexempel.
role: User, Developer
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: c4be3864c680a569166d53f18ec0ee28a52c9ea7
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Skapa, dela och återanvända spelningsboksinstanser

Om du vill använda en spelbok går du till **[!UICONTROL Use Case Playbooks]>[!UICONTROL Playbooks]**. Bläddra och använd de olika sök- och filtreringsalternativen på sidan för att välja och komma igång med en viss spelbok.

## Skapa en spelningsboksinstans {#create-playbook-instance}

>[!CONTEXTUALHELP]
>id="platform_playbooks_create"
>title="Skapa instans"
>abstract="Generera en lista över resurser som resor, målgrupper, scheman eller destinationer som ska användas under resan eller aktiveringsscenarier."

Innan du skapar en spelboksinstans bör du utforska de tillgängliga spelböckerna för att [hitta rätt spelbok för dig](/help/use-case-playbooks/playbooks/discover.md). När du är redo att fortsätta med en spelbok och skapa en instans väljer du **[!UICONTROL Create Instance]** för att fortsätta med spelboken och generera tekniska resurser.

![Skapa en instans av en spelningsbok.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Den här åtgärden genererar flera resurser som du kan använda för att uppnå det användningsfall som beskrivs i spelboken.

![Spelboksvy över genererade resurser när de har aktiverats.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Använd konfigurationskontrollerna för att redigera instansnamn och beskrivningar {#edit-instance-metadata}

När du har skapat en instans baserad på en spelningsbok kan du anpassa den så att den skiljer sig från andra instanser som skapats från samma spelningsbok. Välj konfigurationskontrollen enligt nedan. Redigera namn, beskrivning och anteckningar och välj **[!UICONTROL Save]** när du är klar.

![Redigera namn och beskrivning för en instans.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Förstå de genererade tillgångarna {#understand-assets}

>[!IMPORTANT]
>
>Du behöver inte oroa dig! Det här är ett säkert utrymme att experimentera och du kan inte knäcka någonting. Det finns inga data som är associerade med de resurser du skapar. Du måste först importera data för att uppnå användningsexemplen.

Det är viktigt att förstå att de genererade resurserna skiljer sig åt beroende på vilket användningsfall du aktiverar:

* Olika resurser genereras för olika typer av spelböcker. Dessa resurser skapas specifikt för det användningsfall som uppnås via spelboken. En spelningsbok genererar till exempel ett schema, en målgrupp, en resa och meddelanden. En annan spelningsbok genererar ett schema, en målgrupp och ett mål som data ska aktiveras till.
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
>När objekt har genererats kan du fortsätta att testa dem i utvecklingssandlådorna genom att lägga till data. Du kan testa resurserna så länge du vill i utvecklingssandlådan och du kan replikera resurslogiken (målgruppsdefinitioner, resor, scheman och så vidare) i produktionssandlådan när du är klar. Du kan gå till utvecklingssandlådan och sedan till produktionssandlådan med [funktioner för datainlärning](/help/use-case-playbooks/playbooks/data-awareness.md).

## Återanvänd spelningsböcker {#reuse-playbooks}

Genom att skapa flera instanser av samma spelningsbok kan du implementera samma användningsfall senare, utan att ändra informationen om den tidigare implementeringen av användningsexemplet.

## Dela spelboken och de genererade resurserna med andra teammedlemmar {#share-playbook}

Du kan dela den genererade instansen och resurserna med andra teammedlemmar. Om du vill göra det kopierar du URL-länken från webbläsaren och delar den med ditt team för att ge dem en översikt över de genererade resurserna.

![URL-adressen är markerad i en fallspelningsboksvy.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Videogenomgång av hela uppspelningsprocessen

I den här videon får du lära dig hur du identifierar, skapar, publicerar och felsöker instanser av en Use Case Playbook från början till slut, samt hur du kopierar resurser som genererats av spelboken till andra sandlådor som har konfigurerats i organisationen.

>[!VIDEO](https://video.tv.adobe.com/v/3427058/?learn=on)

## Nästa steg {#next-steps}

Genom att läsa den här guiden och den som handlar om att hitta rätt spelbok för dig, vet du nu hur du tolkar de olika avsnitten i en spelbok och hur du använder de resurser som genereras när du har skapat en instans av en spelbok.

Sedan kan du bläddra i katalogen för spelböcker för att hitta rätt spelbok för ditt användningssätt och läsa [felsökningsguide](/help/use-case-playbooks/playbooks/troubleshooting.md) om du stöter på några problem.
