---
solution: Experience Platform
title: Så här får du och beviljar behörigheter för Experience Platform-kontrollpaneler
type: Documentation
description: Ge användare möjlighet att visa, redigera och uppdatera kontrollpaneler i Experience Platform med Adobe Admin Console.
source-git-commit: 36aaccddeb207e22a22d5124ec8592ac8dddf8bc
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---


# Åtkomstbehörigheter för kontrollpaneler

Om du vill att användare ska kunna visa, redigera och uppdatera kontrollpaneler måste du först aktivera behörigheter. I Adobe Experience Platform tillhandahålls åtkomstkontroll via Adobe Admin Console. Den här funktionen utnyttjar produktprofiler i [!DNL Admin Console], som länkar användare med behörigheter och sandlådor.

Det här dokumentet innehåller en sammanfattning av hur du ger åtkomst till specifika instrumentpanelsbehörigheter i Admin Console. Detaljerad information om hur du får och tilldelar åtkomstbehörigheter finns i [översikten över åtkomstkontroll](../access-control/home.md).

>[!NOTE]
>
>Om du vill konfigurera åtkomstkontroll för [!DNL Experience Platform] måste du ha administratörsbehörighet för en organisation som har en [!DNL Experience Platform]-produktintegrering. Mer information finns i Adobe Help Center-artikeln [administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html).

## Tillgängliga behörigheter {#available-permissions}

Det finns två huvudbehörigheter som krävs för att komma åt instrumentpaneler i Experience Platform. Dessa behörigheter är:

* **Visa kontrollpanel för licensanvändning**: Den här behörigheten ger skrivskyddad åtkomst till kontrollpanelen för licensanvändning i användargränssnittet i Experience Platform.
* **Hantera standardinstrumentpaneler**: Med den här behörigheten kan användare lägga till anpassade attribut som ännu inte finns i data warehouse.

Följande steg visar hur du lägger till dessa behörigheter med Admin Console.

## Välj produktprofiler

Om du vill ge användare åtkomst till kontrollpaneler i Experience Platform börjar du med att logga in på [Adobe Admin Console](https://adminconsole.adobe.com) och välja **Produkter** i den översta navigeringen.

![](images/admin-console/admin-console-overview.png)

Välj **Adobe Experience Platform** i listrutan Experience Cloud i den vänstra navigeringsrutan eller från korten i *Alla produkter och tjänster*. På Adobe Experience Platform produktsida väljer du den produktprofil som du vill lägga till kontrollpanelsbehörigheterna i eller väljer **Ny profil** för att skapa en ny produktprofil.

![](images/admin-console/products.png)

Den valda produktprofilen öppnas och visar de användare som är associerade med den produktprofilen. Om du vill hantera behörigheter för produktprofilen väljer du **Behörigheter**.

![](images/admin-console/product-users.png)

## Lägg till/redigera behörigheter

På fliken **Behörigheter** visas alla tillgängliga behörigheter för produktprofilen. Leta reda på raden **Kontrollpaneler** och observera att det för närvarande står &quot;0 av 2 inkluderade&quot;, vilket betyder att det inte finns några kontrollpanelsbehörigheter aktiverade för produktprofilen.

Om du vill redigera kontrollpanelens behörigheter väljer du **Redigera** på kontrollpanelsraden.

![](images/admin-console/product-permissions.png)

Dialogrutan **Redigera behörigheter** öppnas med tillgängliga behörighetsobjekt och inkluderade behörighetsobjekt. Du kan markera plustecknet (`+`) bredvid behörigheten att lägga till det eller välja **+ Lägg till alla** om du vill lägga till alla behörigheter samtidigt.

Beskrivningar av behörigheter finns i [tillgängliga behörigheter](#available-permissions)-avsnittet tidigare i det här dokumentet.

>[!NOTE]
>
>Du behöver inte aktivera alla behörigheter för alla användare. Beroende på din organisations struktur kanske du vill skapa separata produktprofiler för vissa användare och bevilja begränsad åtkomst (t.ex. skrivskyddad).

När behörigheter har lagts till väljer du **Spara** för att återgå till produktprofilen.

![](images/admin-console/dashboard-permissions.png)

När du återgår till produktprofilen kan du verifiera att behörigheterna har lagts till genom att bekräfta att raden **Kontrollpaneler** visar &quot;2 av 2 inkluderade&quot;.

![](images/admin-console/product-permissions-included.png)

## Nästa steg

Nu när du har lagt till åtkomstbehörigheter till kontrollpaneler kan användare i organisationen börja visa kontrollpaneler i användargränssnittet för Experience Platform och utföra andra åtgärder baserat på de behörigheter som du har tilldelat.