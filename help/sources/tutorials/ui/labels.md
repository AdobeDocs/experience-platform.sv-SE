---
title: Använda åtkomstetiketter för att hantera användaråtkomst till källfilsflöden i användargränssnittet
description: Lär dig hur du använder användargränssnittet i Experience Platform för att använda åtkomstetiketter och hantera användaråtkomst till källans dataflöden.
hide: true
hidefromtoc: true
source-git-commit: 80fb60abdf33eb2a7ca691a9a48a811c632b34fc
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Använda åtkomstetiketter för att hantera användaråtkomst till källfilsflöden i användargränssnittet

Du kan använda funktionerna som tillhandahålls av [attributbaserad åtkomstkontroll](../../../access-control/abac/overview.md) i Real-Time CDP för att använda etiketter på källdata. Med den här funktionen kan du se till att bara en delmängd av användarna i organisationen får tillgång till specifika källdata.

När du lägger till en åtkomstetikett i ett visst dataflöde kan bara användare som har tillgång till en roll som är tilldelad den etiketten visa och redigera det dataflödet. Om ett källdataflöde inte är markerat med någon etikett, visas det för alla användare som tillhör din organisation. Om du till exempel använder etiketten C12 på ett dataflöde kommer användare som tilldelats en roll som inte har etiketten C12 inte att kunna visa och redigera dataflödet med etiketten C12.

Läs den här guiden om du vill veta mer om hur du använder åtkomstetiketter i källdata med Adobe Experience Platform användargränssnitt.

## Kom igång

Innan du arbetar med åtkomstkontrollsetiketter måste du först bekanta dig med funktionerna i attributbaserad åtkomstkontroll. Mer information finns i följande dokumentation:

* [Attributbaserad åtkomstkontroll - översikt](../../../access-control/abac/overview.md)
* [Attributbaserad åtkomstkontroll från början till slut](../../../access-control/abac/end-to-end-guide.md)
* [Hantera etiketter med hjälp av gränssnittet Behörigheter](../../../access-control/abac/ui/labels.md)
* [Etikettordlista för dataanvändning](../../../data-governance/labels/reference.md)

## Tillämpa åtkomstetiketter på källdataflöden

>[!NOTE]
>
>* Du kan inte använda etiketter i en flödeskörning. Flödeskörningar ärver emellertid alla etiketter som du använder på det överordnade dataflödet.
>
>* Om du inte har åtkomst till ett dataflöde kan du inte heller visa dess motsvarande flödeskörningar.

Om du vill använda åtkomstetiketter på källans dataflöden går du till **[!UICONTROL Sources]** > **[!UICONTROL Dataflows]** och letar upp det dataflöde som du vill uppdatera och begränsar användaråtkomsten till.

Markera sedan ellipsen (`...`) i kolumnen [!UICONTROL Name] och välj **[!UICONTROL Apply access labels]** för att lägga till och hantera etiketter för det valda dataflödet.

![Dataflödssidan i källor med alternativet Använd åtkomstetiketter markerat.](../../images/tutorials/labels/apply_access_labels.png)

Fönstret [!UICONTROL Apply access and data governance labels] visas. I det här fönstret väljer du de etiketter som du vill använda i dataflödet. Du kan också filtrera etiketter efter typ. När du är klar väljer du **[!UICONTROL Save]**.

![Fönstret med etiketter för datastyrning med etiketten C2 markerat.](../../images/tutorials/labels/labels_window.png)

När du har konfigurerat åtkomstetiketter för ditt dataflöde kan inte längre användare som inte har åtkomst till den etiketten hämta dataflödet. Du kan också använda kolumnen [!UICONTROL Access Labels] för att visa etiketter som används i ett visst dataflöde.

## Nästa steg

Du vet nu hur du använder åtkomstetiketter i källans dataflöden. Nu kan du se till att bara en viss grupp användare i organisationen har åtkomst till vissa källdata. Mer information finns i följande dokumentation:

* [Tillämpa åtkomstetiketter på källdataflöden i API](../api/labels.md)
* [Översikt över åtkomstkontroll](../../../access-control/home.md)