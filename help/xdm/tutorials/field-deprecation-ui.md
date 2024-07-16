---
title: Undertrycka ett XDM-fält i användargränssnittet
description: Lär dig hur du ersätter XDM-fält (Experience Data Model) med Schemaredigeraren i Experience Platform.
exl-id: f4c5f58a-5190-47d7-8bfc-b33ed238bf25
source-git-commit: 4fa98df9dcc296ba7cb141cb22df116524a0eb0c
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Ta bort ett XDM-fält i användargränssnittet

Experience Data Model (XDM) ger er flexibiliteten att hantera er datamodell när era affärsbehov ändras genom att ta bort schemafält efter att data har inhämtats. Oönskade fält kan vara inaktuella för att ta bort dem från användargränssnittsvyn och även dölja dem för användargränssnitten längre ned. En kryssruta i Schemaredigeraren gör det enkelt att visa inaktuella fält och, om det behövs, även ta bort inaktuella.

Eftersom inaktuella fält döljs för användargränssnittet som standard effektiviserar detta ditt schema i Schemaredigeraren och förhindrar att oönskade fält läggs till i underordnade beroenden som segmentbyggaren, resedesignern och så vidare. Borttagning av fält är också bakåtkompatibelt. Andra system som använder inaktuella fält, som målgrupper och frågor, fortsätter att utvärdera dem som de är avsedda. Om ett inaktuellt fält används i en befintlig målgrupp behandlas det normalt, vilket innebär att fältet visas som förväntat i arbetsytan i Segment Builder eller utvärderas baserat på data som är tillgängliga i de inaktuella fälten. Detta är en fast ändring som inte påverkar befintliga dataflöden negativt.

>[!NOTE]
>
>Innan data hämtas till ett schema kan du ta bort onödiga fältgrupper. Mer information finns i dokumentationen om [hur du tar bort en fältgrupp från ett schema](../ui/resources/schemas.md#remove-fields).

När data har importerats till ditt schema kan du inte längre ta bort fält från schemat utan att göra brytningsändringar. I det här fallet kan du ta bort ett oönskat fält i ett schema eller en anpassad resurs med [Schemaredigeraren](./create-schema-ui.md) eller [API:t för schemaregister](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

I det här dokumentet beskrivs hur du ersätter fält för olika XDM-resurser med Schemaredigeraren i användargränssnittet i Experience Platform. Anvisningar om hur du tar bort ett XDM-fält med API:t finns i självstudiekursen om hur du [tar bort ett XDM-fält med API:t för schemaregister](./field-deprecation-api.md).

## Föråldrade ett fält {#deprecate}

Om du vill ta bort ett anpassat fält går du till Schemaredigeraren för det schema som du vill redigera. Markera det fält som du vill ta bort från [!UICONTROL Structure]-delen av arbetsytan, följt av **[!UICONTROL Deprecate]** från [!UICONTROL Field Properties].

![Schemaredigeraren med ett fält markerat och undertryckt.](../images/tutorials/field-deprecation/deprecate-single-field.png)

En dialogruta visas där du kan bekräfta dina val och meddela dig att fältet kommer att tas bort från användargränssnittsvyn i unionsschemat och döljas för användargränssnitten längre fram. Välj **[!UICONTROL Confirm]** om du vill slutföra åtgärden.

![Dialogrutan Föråldrat med Bekräfta markerat.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

Fältet har nu tagits bort från gränssnittsvyn.

>[!NOTE]
>
>När det är föråldrat visas inte längre inaktuella användargränssnitt, som kontrollpaneler för segment, Customer Journey Analytics och Adobe Journey Optimizer, som en del av arbetsflödet. Det underordnade användargränssnittet har dock möjlighet att visa borttagna fält om det behövs och fortsätta att behandla det borttagna fältet som vanligt. Mer information finns i respektive dokumentation. Frågor och målgrupper som använder det borttagna fältet fortsätter att fungera som förväntat.

## Visa inaktuella fält {#show-deprecated}

Om du vill visa tidigare inaktuella fält navigerar du till det relevanta schemat i Schemaredigeraren. Markera kryssrutan **[!UICONTROL Show deprecated fields]** i avsnittet [!UICONTROL Composition] på arbetsytan.

Det borttagna fältet visas nu i gränssnittsvyn. Välj **[!UICONTROL Save]** för att bekräfta dina inställningar.

![Schemaredigeraren med ett fält markerat, Visa inaktuella fält och Spara markerat.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Föråldrade fält {#undeprecate-fields}

Om du vill ångra ett inaktuellt fält [visar du det inaktuella fältet](#show-deprecated) enligt beskrivningen ovan och väljer sedan det inaktuella fältet i redigerarens [!UICONTROL Structure] -avsnitt. Välj sedan **[!UICONTROL Undeprecate]** i sidofältet [!UICONTROL Field properties] följt av **[!UICONTROL Save]**.

![Schemaredigeraren med det borttagna fältet, Undeprecate och Save markerade.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

Dialogrutan [!UICONTROL Undeprecate field] visas. Bekräfta dina ändringar genom att välja **[!UICONTROL Confirm]**.

![Dialogrutan [!UICONTROL Undeprecate field] med Bekräfta markerad.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

Fältet visas nu som standard i användargränssnittsvyn och även i senare användargränssnitt. Nu kan du välja att ersätta fältet.

## Nästa steg

I det här dokumentet beskrivs hur XDM-fält skrivs ut med hjälp av gränssnittet i Schemaredigeraren. Mer information om hur du konfigurerar fält för anpassade resurser finns i guiden [definierar XDM-fält i API](./custom-fields-api.md). Mer information om hur du hanterar beskrivningar finns i [slutpunktshandboken för beskrivningar](../api/descriptors.md).
