---
title: Visa Insight SQL
description: Visa SQL bakom din profil, målgrupp, destination och anpassade insikter och kör frågan på begäran via Frågeredigeraren.
exl-id: fd728926-c113-4593-92b1-916a02d09d41
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Visa SQL-insikter

Använd [!UICONTROL View SQL] om du vill visa SQL bakom din profil, målgrupp, mål och anpassade insikter och köra frågan på begäran via Frågeredigeraren. Hämta inspiration från SQL av över 40 befintliga insikter för att skapa nya frågor som bygger på unika insikter från plattformsdata baserat på era affärsbehov.

## Navigera till översikten över kontrollpanelen {#navigate-to-overview}

Om du vill öppna den valda instrumentpanelen väljer du antingen **[!UICONTROL Profiles]**, **[!UICONTROL Audiences]**, eller **[!UICONTROL Destinations]** från vänster navigering. Nästa val **[!UICONTROL Overview]** på flikalternativen om arbetsytan inte visas automatiskt.

Du kan också välja **[!UICONTROL Dashboards]** från vänster navigering följt av namnet på din anpassade kontrollpanel. Översikten över den användardefinierade kontrollpanelen visas.

![Experience Platform-gränssnittet med [!UICONTROL Profiles], [!UICONTROL Audiences], [!UICONTROL Destinations]och [!UICONTROL Dashboards] markerad.](./images/view-sql/dashboard-navigation.png)

## Visa växlingsknappen för SQL {#toggle}

Det finns en växlingsknapp i översikten över kontrollpanelerna Profil, Målgrupp, Mål och Användardefinierad för att aktivera eller inaktivera funktionen.

>[!NOTE]
>
>Om du aktiverar [!UICONTROL View SQL] kan du inte ändra globala filter och widgetnivåfilter förrän du inaktiverar funktionen.

![The [!UICONTROL View SQL] växla markerat.](./images/view-sql/view-sql-toggle.png)

Aktivera växlingsknappen som ska visas [!UICONTROL View SQL] text på varje enskild insikt.

![En insikt med [!UICONTROL View SQL] markerad.](./images/view-sql/insight-view-sql.png)

Välj **[!UICONTROL View SQL]** för att öppna en dialogruta som innehåller widgetens SQL.

## SQL-dialogruta {#sql-dialog}

En dialogruta visas som innehåller titeln på insikten och SQL-koden som genererar den.

>[!TIP]
>
>Du kan kopiera hela SQL-satsen till Urklipp genom att välja kopieringsikonen (![Kopieringsikonen.](./images/view-sql/copy-icon.png)) i dialogrutans övre högra hörn.

![En insiktsdialogruta med SQL-satsen markerad.](./images/view-sql/sql-dialog.png)

Välj **[!UICONTROL Run SQL]** för att öppna frågeredigeraren med frågan är ifylld i förväg.

![En insiktsdialog med [!UICONTROL Run SQL] markerad.](./images/view-sql/run-sql.png)

## Redigera befintlig SQL {#edit-sql}

Frågeredigeraren visas. Nu kan du redigera satsen och fråga dina plattformsdata på ett sätt som bättre passar dina rapporteringsbehov. Spara den nya frågemallen med ett lämpligt namn.

![Frågeredigeraren med vald information som SQL är förifyllt.](./images/view-sql/edit-sql.png)

## Nästa steg

När du har läst det här dokumentet kan du nu förstå hur du får åtkomst till SQL för att få information antingen i standardkontrollpanelerna eller i en användardefinierad kontrollpanel. Om du inte redan har gjort det bör du läsa [Real-time Customer Data Platform Insights - datamodelldokument](./data-models/cdp-insights-data-model-b2c.md). Det dokumentet innehåller insikter om hur du anpassar SQL-mallar för Real-Time CDP-rapporter som är skräddarsydda efter dina marknadsförings- och KPI-behov.
