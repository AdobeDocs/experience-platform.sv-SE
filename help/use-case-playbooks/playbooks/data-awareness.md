---
solution: Experience Platform
title: Översikt över datainsikt i Use Case Playbooks
description: Lär dig hur du snabbar upp time to value genom att kopiera resurserna som genereras i den sista inspirerande sandlådan till andra sandlådor.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Publish spelboksgenererade resurser till andra sandlådor {#publish-to-other-sandboxes}

Använd fallspelsböcker är marknadsföringsmallar som utformats för att generera resurser som målgrupper, scheman eller resor för vanliga användningsfall inom marknadsföring. Du kan testa de resurser som skapas av spelböcker i den inspirerande sandlådan och när du är klar kan du importera resurserna till andra utvecklingssandlådor för ytterligare testning med de data som du har tillgängliga i dessa sandlådor. När du är nöjd med testningen kan du sedan flytta resurserna från utvecklingssandlådor till produktionssandlådor.

I vissa fall kan du dock redan ha konfigurerat egna scheman, fält och fältgrupper i andra utvecklingssandlådor. Detta kan göra att vissa resurser som genereras av ärendemallar, som resor, inte är kompatibla med dina data. Läs den här självstudiekursen om du vill veta hur du använder funktioner för att öka medvetenheten om data för att bättre anpassa och komplettera de genererade resurserna med dina befintliga resurser.

## Förhandskrav {#prerequisites}

Innan du läser den här självstudiekursen bläddrar du bland de [tillgängliga fallspelningsboksmallarna](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) och [skapar en instans](/help/use-case-playbooks/playbooks/create-share-reuse.md) av en önskad spelningsbok.

När du skapar en instans genereras en uppsättning resurser som resor, segment, scheman och meddelanden i den inspirerande sandlådan. Läs vidare för att lära dig hur du kan kopiera dessa resurser till andra sandlådor.

### Skapa och publicera ett paket {#create-publish-package}

>[!NOTE]
>
> Du kan bara importera paket till andra utvecklingssandlådor. När du har gjort alla nödvändiga ändringar eller uppdateringar kan du importera resurserna eller paketen från dessa utvecklingssandlådor till produktion. Du kan inte importera direkt från sandlådan Använd fallspelningsböcker till produktion.

1. Om du vill importera objekt från den inspirerande sandlådan till en annan sandlåda bläddrar du till önskad instans av en fallspelningsbok och väljer **[!UICONTROL Publish to a different sandbox]** för att exportera artefakterna som ett paket.

   ![GIF som visar olika instanser av användningsfall](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. När du har valt knappen **[!UICONTROL Publish to a different sandbox]** visas ett modalt värde. Fyll i namnet och den valfria beskrivningen och välj **[!UICONTROL Create]**. I det här steget paketeras de genererade resurserna i ett paket som kan importeras till en annan sandlåda.

   ![Ett modalt sätt att skapa ett paket](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Navigera till sidan **Sandlådor** i den vänstra navigeringen och välj fliken **Paket** , sök efter ditt paket och publicera det. Om du vill publicera ett paket som är i utkastläge följer du stegen i [sandlådeverktygets](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish)-dokument.

   ![Paketet i utkastläge eller opublicerat läge](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Paketet publiceras](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. När publiceringen är klar visas en **+**-knapp aktiverad bredvid namnet på paketbläddringssidan.

   ![Fliken Paket på sidan Sandlådor](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Paketet kan inte importeras medan det fortfarande är i utkastläge, så öppna paketdetaljsidan och publicera paketet.

5. Välj kontrollen **+** och starta arbetsflödet för att importera resurserna som genereras av fallspelningsboken till **[!UICONTROL Target sandbox]**. Markera en målsandlåda och bekräfta det paketnamn som du vill importera med listrutan. Lägg till jobbinformation som jobbnamn och jobbbeskrivning innan du fortsätter till nästa steg.

   ![Starta importarbetsflöde, välj mål, bekräfta paket, lägg till jobbinformation.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. I steget **[!UICONTROL View dependencies]** kan du mappa scheman och kopiera andra resurser från den inspirerande sandlådan till målsandlådan. Knappen **[!UICONTROL Finish]** är inaktiverad tills du mappar varje schema.

   ![Mappa scheman i steget Visa beroenden, aktivera knappen Slutför.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Kartscheman {#map-schemas}

1. Mappa det första schemat. I dialogrutan för schemamappning visas en listruta där du kan välja målschema. Om källschemat är ett profilschema finns det inga andra målschemaalternativ förutom det [enskilda unionsprofilschemat](/help/xdm/classes/individual-profile.md). Du kan se automatiskt genererade mappningsrekommendationer mellan Source-data och målfält när sidan visas första gången. Du kan redigera mappningarna genom att markera målfältet och sedan välja ett nytt fält. Om du ändrar de föreslagna mappningarna kan du använda knappen **Validera** för att validera de nya mappningarna och visa eventuella fel som kan vara länkade till de nya mappningarna. Välj **Spara** när mappningen är klar.

   ![Dialogrutan för schemamappning med en listruta där du kan välja ett målschema.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Fortsätt mappa alla fält i scheman. Om schemat är ett [händelseschema](/help/xdm/classes/experienceevent.md) visas en listruta där du kan visa alla händelsescheman i målsandlådan.

   ![Välj ett målschema i listrutan](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Välj ett schema från tillgängliga scheman i **målsandlådan**.

   ![Välj ett schema](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Slutför mappningen och välj **Spara**.

   ![Spara mappning](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. När du har mappat alla fält i scheman väljer du **Slutför** för att slutföra importarbetsflödet.

   ![Slutför flödet](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Du kan inte ändra några resurser förutom scheman, eftersom det här är en inspirerande sandlåda, men de visas som beroende av paketet.

### Importstatus {#import-status}

1. Du omdirigeras automatiskt till sidan [**Importer**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) där du kan se importförloppet.

   ![Sidan visar importförloppet](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. När paketet importeras skapas resurserna i paketet i målsandlådan. När de är klara refererar de till de fält som du mappade under importprocessen. Processen är nu klar och resurserna från den inspirerande sandlådan finns nu också i din målsandlåda så att du kan testa dem.

   ![Genererade resurser i målsandlådan](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur du använder fallspelningsböcker tillsammans med [sandlådeverktyg](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) för att skapa körbara resor som refererar till dina scheman. Läs mer om de vanliga [användningsfallen för Real-Time CDP](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
