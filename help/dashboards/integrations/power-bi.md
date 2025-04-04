---
title: Power BI rapportmallar för Experience Platform Dashboards
description: Använd rapportmallar för att utforska Experience Platform data med Power BI.
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 0%

---

# Power BI rapportmallar för kontrollpaneler

Med rapportmallsfunktionen i Power BI kan du skapa övertygande rapporter med data från Adobe Experience Platform. Den smidiga installationsprocessen installerar automatiskt standardwidgetar för kundprofil, segmentering och mål i realtid. Installationen kopplar även Power BI till era datamodeller så att ni enkelt kan anpassa och utöka rapportmallarna. Rapporterna kan delas av hela organisationen utan att mottagarna behöver inloggningsuppgifter för din organisation på Experience Platform.

Det här dokumentet innehåller anvisningar om hur du ansluter Adobe Experience Platform till Power BI och använder rapportmallar för att dela viktiga Experience Platform-datainsikter med externa användare.

## Komma igång

Innan du fortsätter med den här självstudiekursen bör du ha god förståelse för [schemakomposition](../../xdm/schema/composition.md) i Experience Platform och hur attribut inkluderas i kundprofilen i realtid via [unionsschemat](../../xdm/schema/composition.md#union).

För att installera Power BI-programintegreringen måste användarna först ha fått följande Experience Platform-behörigheter:

- Hantera frågor
- Hantera sandlådor

Läs dokumentationen för [åtkomstkontrollen](../../access-control/home.md) om du vill lära dig hur du tilldelar dessa behörigheter.

Du måste också ha ett Power BI-konto för att kunna följa den här självstudiekursen. Om du vill skapa ett konto går du till [Power BI hemsida](https://powerbi.microsoft.com/en-us/) och följer registreringsprocessen. Användare för det här Power BI-kontot måste även aktivera inställningen **Skapa arbetsyta** i sina Power BI-inställningar. Den här inställningen finns i klientinställningarna för Power BI administratörsportal. Om ditt konto tillhandahålls av din klientorganisation eller arbetsgivare, kontaktar du respektive administratör för att aktivera den här inställningen.

![Power BI Admin Portal - skapa arbetsyteinställningar.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>För att fliken Kontrollpaneler ska kunna visas i den vänstra navigeringen i Experience Platform användargränssnitt och i vyn Kontrollpanelsinventering måste du ha tillgång till någon av kontrollpanelerna Profil, Segmentering eller Mål som en del av din Experience Platform-licens.

## Installera Power BI programintegrering

I Experience Platform-gränssnittet väljer du **[!UICONTROL Dashboards]** i den vänstra navigeringen för att öppna arbetsytan i [!UICONTROL Dashboards]. Fliken [!UICONTROL Browse] visar en lista över tillgängliga instrumentpanelsvyer. Mer information om hur du visar tillgängliga instrumentpaneler finns i [lagerdokumentationen](../inventory.md).

Välj sedan fliken **[!UICONTROL Integrations]**. Power BI programintegrationssida visas. Här väljer du **[!UICONTROL Install]** för att påbörja installationen.

>[!NOTE]
>
>Knappen [!UICONTROL Install] är inaktiverad om du inte har både behörighet för att hantera frågetjänster och hantera sandlådor.

![Skärmen med information om Power BI med knappen Installera markerad.](../images/power-bi/details-screen.png)

### Ange autentiseringsuppgifter

Det första steget i installationsprocessen är att ange autentiseringsuppgifter som inte upphör att gälla för Power BI-programintegrering. Det finns två tillgängliga alternativ för att tillhandahålla dessa: [[!UICONTROL Create new credentials]](#create-new-credentials) eller [[!UICONTROL Use existing credentials]](#use-existing-credentials). Välj lämplig växel för att fortsätta.

#### Skapa nya autentiseringsuppgifter {#create-new-credentials}

Det finns två obligatoriska fält när nya autentiseringsuppgifter genereras: [!UICONTROL Name] och [!UICONTROL Assigned to]. Fältet [!UICONTROL Assigned to] relaterar till den e-postadress som är associerad med ditt Power BI-konto.

![Power BI genererar ny inloggningsskärm.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>Om du vill skapa autentiseringsuppgifter som inte förfaller måste du ha vissa behörigheter och roller tilldelade. Behörigheterna som krävs är Hantera sandlådor och Hantera integrering av frågetjänster. Rollerna som krävs är Adobe Experience Platform admin- och utvecklarroller. Läs dokumentationen för [åtkomstkontrollen](../../access-control/home.md) om du vill lära dig hur du tilldelar dessa behörigheter.

Mer information om hur du genererar autentiseringsuppgifter för frågetjänsten som inte upphör att gälla finns i handboken [för icke-förfallande autentiseringsuppgifter](../../query-service/ui/credentials.md#non-expiring-credentials).

När du har genererat icke-förfallande autentiseringsuppgifter för första gången hämtas en JSON-fil till den datorn. Den här JSON-filen kan sedan delas med andra användare som autentiseringsuppgifter för att slutföra installationsprocessen.

#### Använd befintliga autentiseringsuppgifter {#use-existing-credentials}

En JSON-autentiseringsfil kan också överföras för att validera. Dessa JSON-filer som innehåller autentiseringsuppgifter som inte upphör att gälla hämtas till den lokala datorn som används när en autentiseringsuppgift som inte upphör att gälla skapas.

>[!IMPORTANT]
>
>Användaren måste ha tilldelats en autentiseringsuppgift för att kunna använda en befintlig referens som inte förfaller. Om användaren inte har tilldelats någon autentiseringsuppgift och inte kan skapa en ny med Adobe Admin Console, kan användaren inte fortsätta med installationsprocessen.

Välj **[!UICONTROL Upload credential file]** och välj sedan den JSON-fil som ska överföras i den dialogruta som visas.

![Skärmen för Power BI-autentiseringsuppgifter med knappen för överföring av autentiseringsfil markerad.](../images/power-bi/upload-credential-file.png)

När du har angett inloggningsuppgifterna som inte förfaller valideras de automatiskt av Experience Platform. Ett bekräftelsemeddelande visas när valideringen har slutförts. Välj **[!UICONTROL Next]** om du vill granska medgivandeavtalet för Power BI-programmet.

![Skärmen för autentiseringsuppgifter som inte förfaller har verifierats med knappen Nästa markerad.](../images/power-bi/successfully-uploaded-credential-file.png)

### Ge medgivande

Medgivande visas. Välj **[!UICONTROL Review consent]** om du vill öppna ett nytt fönster med information om de behörigheter som krävs för att Power BI ska få tillgång till och använda dina data enligt användarvillkoren och sekretesspolicyn.

![Medgivande visas med knappen för godkännande av granskning markerad.](../images/power-bi/provide-consent-display.png)

Välj **[!UICONTROL Accept]** om du vill ge Power BI behörighet att komma åt och använda dina Experience Platform-data.

![Behörighetsbegäran för Power BI.](../images/power-bi/permissions.png)

>[!NOTE]
>
>Om du avslutar installationsprocessen någon gång innan du ger ditt medgivande kommer Power BI-programintegreringen inte att installeras i kontrollpanelernas lager.

När du har gett ditt samtycke installeras rapportmallen automatiskt i Power BI-miljön som en del av installationsprocessen. Power BI använder sedan de icke-förfallande autentiseringsuppgifterna för att få åtkomst till Experience Platform, köra alla SQL-frågor sekventiellt och fylla i rapportmallen med returnerade data.

Välj **[!UICONTROL Finish]** om du vill återgå till instrumentpanelsinventeringen.

![Medgivande visas med knappen Slutför markerad.](../images/power-bi/finish-consent-review.png)

Nu när rapportmallen för Power BI är installerad visas den i listan över tillgängliga instrumentpaneler på fliken [!UICONTROL Browse]. Välj **[!UICONTROL Power BI]** i listan för att navigera till Power BI-miljön.

![Power BI listas i instrumentpanelsinventeringen.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Power BI-administratörer måste se till att användarna har behörighet att visa dessa instrumentpaneler i Power BI-miljön.

## Power BI arbetsyta

Efter inloggning på [Power BI-arbetsytan](https://dxt.powerbi.com) är rapportmallar tillgängliga för alla tjänster som du har åtkomst till. Rapportmallarna innehåller profiler, segment och målkontrollpaneler **endast** om de har motsvarande visningsbehörigheter.

Standardwidgetar från profiler, segment och mål är som standard tillgängliga i Power BI-mallrapporter.

>[!NOTE]
>
>Du måste ha redigeringsbehörighet aktiverad för en viss instrumentpanel för att den instrumentpanelen ska kunna installeras i Power BI-miljön.

![Power BI-profilmallsrapport med Experience Platform standardprofilwidgetar.](../images/power-bi/profile-report-template.png)

När en kontrollpanel har installerats i Power BI visas rapportmallar som standard för alla användare. Om du vill begränsa åtkomsten till rapportmallar måste du inaktivera åtkomsten för användarna i fråga inifrån Power BI-miljön.

## Anpassa Power BI rapportmall

Genom att använda anpassade widgetar kan du lägga till anpassade attribut i din datamodell för att förbättra rapportmallarna från Power BI.

>[!NOTE]
>
>Vilka attribut du kan använda för anpassade widgetar beror på vad som är tillgängligt i unionsschemat. Om du vill lära dig hur du visar och utforskar unionens scheman till förmån för dina anpassade widgetar kan du läsa användargränssnittsguiden för [unionens schema](../../profile/ui/union-schema.md).

### Skapa en anpassad widget

Anpassade widgetar skapas via widgetbiblioteket. En introduktion till funktionen och självstudiekursen [för att skapa en anpassad widget](../customize/custom-widgets.md) finns i [Översikt över widgetbiblioteket](../customize/widget-library.md).

>[!IMPORTANT]
>
>De nya anpassade widgetarna synkroniseras **inte** automatiskt mellan Adobe Experience Platform-kontrollpaneler och Power BI rapportmallar. Alla anpassade widgetar som skapas i Experience Platform-gränssnittet måste återskapas manuellt i Power BI-miljön.

### Återskapa din anpassade widget i Power BI-miljön

När kontrollpanelen har rätt mått och attribut i anpassade widgetar kan du ändra rapportmallen som visas i Power BI-miljön. Mer information om hur du redigerar en rapport via användargränssnittet finns i [Power BI-dokumentationen](https://docs.microsoft.com/en-us/power-bi/).

## Ta bort Power BI programintegrering

Om du vill ta bort instrumentpanelen går du till instrumentpanelens inventering och väljer borttagningsikonen (![borttagningsikonen](/help/images/icons/delete.png)) bredvid instrumentpanelens namn.

>[!NOTE]
>
>Det är bara den användare som har installerat Power BI Dashboard som kan ta bort integreringen från Experience Platform användargränssnitt.

![Fliken Bläddra bland instrumentpaneler på skärmen visas med knappen Bläddra och ikonen Ta bort markerad.](../images/power-bi/delete-power-bi-dashboard.png)

En bekräftelsepover visas. Välj **[!UICONTROL Delete]** för att bekräfta processen.

>[!IMPORTANT]
>
>Om du tar bort Power BI-kontrollpanelen från Experience Platform-gränssnittet tas **inte** rapportmallarna som är tillgängliga i din Power BI-miljö bort. Om du vill ta bort all information som finns i Power BI rapportmallar måste du logga in på ditt Power BI-konto och ta bort rapportmallarna från den miljön. När den tagits bort kan användaren installera om Power BI Dashboard genom att följa samma installationsanvisningar som ovan.

## Nästa steg

Genom att läsa det här dokumentet får du en bättre förståelse för hur Power BI rapportmallar kan integreras i Experience Platform för att dela övertygande datainsikter från era profiler, segment eller målpaneler. Se [översikten över anpassning av kontrollpanelen](../customize/overview.md) om du vill veta mer om hur du anpassar dina kontrollpaneler.
