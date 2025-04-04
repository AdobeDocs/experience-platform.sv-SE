---
title: Handbok för hela datastyrningen
description: Följ hela processen för att tillämpa begränsningar för användning av data för fält och datauppsättningar i Adobe Experience Platform.
exl-id: f18ae032-027a-4c97-868b-e04753237c81
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 0%

---

# Handbok för datastyrning från början till slut

För att kunna styra vilka marknadsföringsåtgärder som kan utföras på vissa datauppsättningar och fält i Adobe Experience Platform måste du ställa in följande:

1. [Använd etiketter](#labels) på schemafält eller hela datauppsättningar, vars användning du vill begränsa.
1. [Konfigurera och aktivera datastyrningsprinciper](#policy) som avgör vilka typer av märkta data som kan användas för vissa marknadsföringsåtgärder.
1. [Använd marknadsföringsåtgärder på dina mål](#destinations) för att ange vilka principer som gäller för data som skickas till dessa mål.

När du är klar med konfigureringen av etiketter, styrningsprinciper och marknadsföringsåtgärder kan du [testa din policytillämpning](#test) för att kontrollera att den fungerar som förväntat.

Den här guiden går igenom hela processen med att konfigurera och verkställa en datastyrningspolicy i Experience Platform användargränssnitt. Mer detaljerad information om funktionerna som används i den här handboken finns i översiktsdokumentationen för följande ämnen:

* [Adobe Experience Platform datastyrning](./home.md)
* [Dataanvändningsetiketter](./labels/overview.md)
* [Dataanvändningspolicyer](./policies/overview.md)
* [Politiska åtgärder](./enforcement/overview.md)

>[!NOTE]
>
>Den här guiden fokuserar på hur du ställer in och tillämpar regler för hur data används eller aktiveras i Experience Platform. Om du försöker begränsa **åtkomsten** till själva data för vissa Experience Platform-användare i din organisation läser du i handboken från början till slut om [attributbaserad åtkomstkontroll](../access-control/abac/end-to-end-guide.md) i stället. Attributbaserad åtkomstkontroll använder också etiketter och principer, men för ett annat användningssätt än för datastyrning.

## Använd etiketter {#labels}

>[!IMPORTANT]
>
>Etiketter kan inte längre användas på enskilda fält på datauppsättningsnivå. Det här arbetsflödet har ersatts med etiketter på schemanivå. Du kan dock fortfarande märka en hel datauppsättning med etiketter. Etiketter som tidigare använts på enskilda datauppsättningsfält stöds fortfarande i Experience Platform-gränssnittet fram till den 31 maj 2024. För att etiketterna ska vara enhetliga i alla scheman måste du migrera alla etiketter som tidigare har kopplats till fält på datauppsättningsnivå till schemanivån under det kommande året. Mer information om hur du gör detta finns i avsnittet [migrera tidigare använda etiketter](#migrate-labels).

Du kan [använda etiketter i ett schema](#schema-labels) så att alla datauppsättningar som är baserade på det schemat ärver samma etiketter. På så sätt kan ni hantera etiketterna för datastyrning, samtycke och åtkomstkontroll på ett och samma ställe. Genom att tillämpa begränsningar för dataanvändning på schemanivå sprids effekten nedåt till alla datauppsättningar som baseras på det schemat. Etiketter som används på schemafältnivå stöder användningsfall för datastyrning och kan identifieras på arbetsytan för datauppsättningar [!UICONTROL Data Governance] under kolumnen [!UICONTROL Field Name] som skrivskyddade etiketter.

Om det finns en specifik datauppsättning som du vill använda begränsningar för dataanvändning på, kan du [använda etiketter direkt på den datauppsättningen](#dataset-labels) eller specifika fält i den datauppsättningen.

Du kan också [använda etiketter i schemat](#schema-labels) så att alla datauppsättningar som är baserade på schemat ärver samma etiketter.

>[!NOTE]
>
>Mer information om de olika etiketterna för dataanvändning och deras avsedda användning finns i [etiketten för dataanvändning](./labels/reference.md). Om de tillgängliga kärnetiketterna inte täcker alla dina önskade användningsfall kan du [definiera egna anpassade etiketter](./labels/user-guide.md#manage-custom-labels) också.

### Tillämpa etiketter på en hel datauppsättning {#dataset-labels}

Välj **[!UICONTROL Datasets]** i den vänstra navigeringen och markera sedan namnet på datauppsättningen som du vill använda etiketter på. Du kan också använda sökfältet för att begränsa listan med visade datauppsättningar.

![Fliken Bläddra i arbetsytan Datauppsättningar med datauppsättningar och en datauppsättningsrad markerad.](./images/e2e/select-dataset.png)

Informationsvyn för datauppsättningen visas. Välj fliken **[!UICONTROL Data governance]** om du vill visa en lista över datauppsättningens fält och eventuella etiketter som redan har tillämpats på dem. Markera pennikonen om du vill redigera datauppsättningsrubrikerna.

![Fliken Datastyrning för lojalitetsmedlemsdatauppsättningen med pennikonen markerad.](./images/e2e/edit-dataset-labels.png)

Dialogrutan [!UICONTROL Edit governance labels] visas. Välj lämplig styrningsetikett och välj **[!UICONTROL Save]**.

![Dialogrutan Redigera styrningsetiketter med kryssrutan Etikett och Spara markerad.](./images/e2e/edit-dataset-governance-labels.png)

### Tillämpa etiketter på ett schema {#schema-labels}

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen och välj sedan det schema som du vill lägga till etiketter i från listan.

>[!TIP]
>
>Om du är osäker på vilket schema som gäller för en viss datauppsättning väljer du **[!UICONTROL Datasets]** i den vänstra navigeringen och sedan länken under kolumnen **[!UICONTROL Schema]** för den önskade datauppsättningen. Markera schemanamnet i den port som visas för att öppna schemat i Schemaredigeraren.
>
>![Bild som visar en länk till en datamängds schema](./images/e2e/schema-from-dataset.png)

Schemats struktur visas i Schemaredigeraren. Här väljer du fliken **[!UICONTROL Labels]** för att visa en listvy över schemats fält och de etiketter som redan har tillämpats på dem. Markera kryssrutorna intill de fält som du vill lägga till etiketter i och markera sedan **[!UICONTROL Apply access and data governance labels]** i den högra listen.

![Fliken Etiketter på arbetsytan Schema med ett enda schemafält markerat och etiketterna Använd åtkomst och datastyrning markerade.](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>Om du vill lägga till etiketter i alla fält i schemat väljer du pennikonen på den översta raden.
>
>![Bild som visar pennikonen som väljs i vyn Schemaetiketter](./images/e2e/label-whole-schema.png)

Dialogrutan [!UICONTROL Apply access and data governance labels] visas. Markera etiketterna som du vill använda i det valda schemafältet. När du är klar väljer du **[!UICONTROL Save]**.

![Dialogrutan Använd åtkomst- och datastyrningsetiketter visar flera etiketter som läggs till i ett schemafält.](./images/e2e/save-schema-labels.png)

Följ stegen ovan för att tillämpa etiketter på olika fält (eller olika scheman) efter behov. När du är klar kan du fortsätta till nästa steg i [Aktivera datastyrningsprinciper](#policy).

### Migrera etiketter som tidigare använts på datauppsättningsnivå {#migrate-labels}

Välj **[!UICONTROL Dataset]** i den vänstra navigeringen och markera sedan namnet på datauppsättningen som du vill migrera etiketter från. Du kan också använda sökfältet för att begränsa listan med visade datauppsättningar.

![Fliken Bläddra på arbetsytan Datauppsättningar med datauppsättningen Förtroendemedlemmar markerad.](./images/e2e/select-dataset.png)

Informationsvyn för datauppsättningen visas. Välj fliken **[!UICONTROL Data governance]** om du vill visa en lista över datauppsättningens fält och eventuella etiketter som redan har tillämpats på dem. Markera ikonen för att avbryta bredvid etiketter som du vill ta bort från ett fält. En bekräftelsedialogruta visas. Välj [!UICONTROL Remove label] för att bekräfta dina val.

![Fliken Datastyrning på arbetsytan Datauppsättningar med en etikett för ett fält som är markerat för borttagning.](./images/e2e/remove-label.png)

När du har tagit bort etiketten från datauppsättningsfältet går du till Schemaredigeraren och lägger till etiketten i schemat. Instruktioner om hur du gör detta finns i avsnittet [om att använda etiketter i ett schema](#schema-labels).

>[!TIP]
>
>Du kan välja schemanamnet i den högra listen, följt av länken i dialogrutan som visas för att navigera till rätt schema.
>![Fliken Datastyrning på arbetsytan Datauppsättningar med schemanamnet i sidofältet och dialoglänken markerade.](./images/e2e/navigate-to-schema.png)

När du har migrerat de nödvändiga etiketterna kontrollerar du att rätt [datastyrningsprinciper är aktiverade](#policy).

## Aktivera policyer för datastyrning {#policy}

När du har använt etiketter på dina scheman och/eller datauppsättningar kan du skapa regler för datastyrning som begränsar de marknadsföringsåtgärder som vissa etiketter kan användas för.

Välj **[!UICONTROL Policies]** i den vänstra navigeringen om du vill visa en lista över kärnprinciper som har definierats av Adobe samt eventuella egna principer som tidigare har skapats av din organisation.

Varje etikett har en tillhörande grundprincip som, när den är aktiverad, tillämpar lämpliga aktiveringsbegränsningar på alla data som innehåller etiketten. Om du vill aktivera en huvudprincip markerar du den i listan och väljer sedan **[!UICONTROL Policy status]** till **[!UICONTROL Enabled]**.

![Bild som visar att en huvudprincip är aktiverad i användargränssnittet](./images/e2e/enable-core-policy.png)

Om de tillgängliga grundreglerna inte täcker alla dina användningsfall (till exempel när du använder anpassade etiketter som du har definierat under din organisation) kan du definiera en anpassad profil i stället. Välj **[!UICONTROL Create policy]** på arbetsytan **[!UICONTROL Policies]**.

![Bild som visar knappen [!UICONTROL Create policy] som markeras i användargränssnittet ](./images/e2e/create-policy.png)

En pover visas och du uppmanas att välja vilken typ av profil du vill skapa. Välj **[!UICONTROL Data governance policy]** och sedan **[!UICONTROL Continue]**.

![Bild som visar det [!UICONTROL Data governance policy]-alternativ som markeras](./images/e2e/governance-policy.png)

Ange **[!UICONTROL Name]** och valfritt **[!UICONTROL Description]** för principen på nästa skärm. I tabellen nedan markerar du de etiketter som du vill att profilen ska kontrollera. Detta är med andra ord de etiketter som policyn kommer att förhindra från att användas för de marknadsföringsåtgärder som du anger i nästa steg.

Om du markerar flera etiketter kan du använda alternativen i den högra listen för att avgöra om alla etiketter måste finnas för att principen ska kunna tillämpa användningsbegränsningar, eller om bara en av etiketterna behöver finnas. När du är klar väljer du **[!UICONTROL Next]**.

![Bild som visar principens grundläggande konfiguration i gränssnittet](./images/e2e/configure-policy.png)

På nästa skärm väljer du de marknadsföringsåtgärder som den här principen ska begränsa de etiketter som du tidigare valt från att användas. Välj **[!UICONTROL Next]** om du vill fortsätta.

![Bild som visar en marknadsföringsåtgärd som tilldelas en princip i användargränssnittet](./images/e2e/select-marketing-action.png)

I den sista skärmen visas en sammanfattning av principens detaljer och de åtgärder som den kommer att begränsa för vilka etiketter. Välj **[!UICONTROL Finish]** om du vill skapa profilen.

![Bild som visar att konfigurationen av principen har bekräftats i användargränssnittet](./images/e2e/confirm-policy.png)

Principen har skapats, men är inställd på [!UICONTROL Disabled] som standard. Välj profilen i listan och ställ in **[!UICONTROL Policy status]** på **[!UICONTROL Enabled]** för att aktivera principen.

![Bild som visar den skapade principen som aktiveras i användargränssnittet](./images/e2e/enable-created-policy.png)

Följ stegen ovan för att skapa och aktivera de profiler du behöver innan du går vidare till nästa steg.

## Hantera marknadsföringsåtgärder för destinationer {#destinations}

För att dina aktiverade profiler ska kunna avgöra vilka data som kan aktiveras för ett mål måste du tilldela specifika marknadsföringsåtgärder till det målet.

Ta till exempel en aktiverad princip som förhindrar att data som innehåller etiketten `C2` används för marknadsföringsåtgärden [!UICONTROL Export to Third Party]. När data aktiveras till ett mål kontrollerar profilen vilka marknadsföringsåtgärder som finns på målet. Om det finns [!UICONTROL Export to Third Party], och du försöker aktivera data med en `C2`-etikett, uppstår en principöverträdelse. Om [!UICONTROL Export to Third Party] inte finns används inte principen för målet och data med `C2`-etiketter kan aktiveras fritt.

När [ansluter ett mål i användargränssnittet](../destinations/ui/connect-destination.md) kan du med hjälp av steget **[!UICONTROL Governance]** i arbetsflödet välja de marknadsföringsåtgärder som gäller för det här målet, vilket i slutändan avgör vilka datastyrningsprinciper som används för målet.

![Bild som visar de marknadsföringsåtgärder som väljs för ett mål](./images/e2e/destination-marketing-actions.png)

## Testa policytillämpning {#test}

När ni har märkt era data, aktiverade datastyrningsprinciper och tilldelat era destinationer marknadsföringsåtgärder kan ni testa om era policyer används som förväntat.

Om du ställer in allt korrekt, när du försöker aktivera data som begränsas av dina regler, nekas aktiveringen automatiskt och ett meddelande om policyöverträdelse visas med detaljerad information om vad som orsakade överträdelsen.

Mer information om hur du tolkar meddelanden om policyöverträdelser finns i dokumentet om [automatisk policytillämpning](./enforcement/auto-enforcement.md).

## Nästa steg

I den här guiden beskrivs de steg som krävs för att konfigurera och tillämpa policyer för datastyrning i era aktiveringsarbetsflöden. Mer detaljerad information om komponenterna för datastyrning i den här handboken finns i följande dokumentation:

* [Dataanvändningsetiketter](./labels/overview.md)
* [Dataanvändningspolicyer](./policies/overview.md)
* [Politiska åtgärder](./enforcement/overview.md)
