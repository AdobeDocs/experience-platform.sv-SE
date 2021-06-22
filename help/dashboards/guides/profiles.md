---
keywords: Experience Platform;profil;kundprofil i realtid;användargränssnitt;anpassning;profilpanel;instrumentpanel
title: Kontrollpanel för profiler
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om kundprofildata i realtid för din organisation.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 0%

---

# [!UICONTROL Profiles] kontrollpanel

Adobe Experience Platform användargränssnitt (UI) tillhandahåller en kontrollpanel där du kan visa viktig information om dina [!DNL Real-time Customer Profile]-data, som de har tagits under en daglig ögonblicksbild. I den här handboken beskrivs hur du kommer åt och arbetar med kontrollpanelen [!UICONTROL Profiles] i användargränssnittet och den innehåller information om de mått som visas på kontrollpanelen.

En översikt över alla profilfunktioner i användargränssnittet i Experience Platform finns i [Användargränssnittshandboken för kundprofiler i realtid](../../profile/ui/user-guide.md).

## Data för kontrollpanel för profil

Kontrollpanelen [!UICONTROL Profiles] visar en ögonblicksbild av attributdata (post) som din organisation har i profilarkivet i Experience Platform. Ögonblicksbilden innehåller inga händelsedata (tidsserier).

Attributdata i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och kontrollpanelen för profiler uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska kontrollpanelen [!UICONTROL Profiles]

Om du vill navigera till kontrollpanelen [!UICONTROL Profiles] i plattformsgränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra listen och sedan fliken **[!UICONTROL Overview]** för att visa kontrollpanelen.

>[!NOTE]
>
>Om din organisation är ny på Platform och ännu inte har aktiva profildatauppsättningar eller sammanslagningsprinciper skapade, visas inte kontrollpanelen [!UICONTROL Profiles]. Istället visar fliken [!UICONTROL Overview] länkar och dokumentation som hjälper dig att komma igång med kundprofilen i realtid.

![](../images/profiles/dashboard-overview.png)

### Ändra kontrollpanelen [!UICONTROL Profiles]

Du kan ändra utseendet på kontrollpanelen [!UICONTROL Profiles] genom att välja **[!UICONTROL Modify dashboard]**. Detta gör att du kan flytta, lägga till och ta bort widgetar från kontrollpanelen samt komma åt [!UICONTROL Widget library] för att utforska tillgängliga widgetar och skapa anpassade widgetar för din organisation.

Mer information finns i [dokumentationen för att ändra kontrollpanelerna](../modify.md) och [widgetbiblioteket](../widget-library.md).

## Sammanfoga profiler

De mätvärden som visas på kontrollpanelen [!UICONTROL Profiles] baseras på sammanslagningsprinciper som tillämpas på dina kundprofildata i realtid. När data samlas in från flera olika källor för att skapa kundprofilen är det möjligt att data innehåller motstridiga värden (en datauppsättning kan till exempel lista en kund som&quot;enkel&quot; medan en annan datauppsättning kan lista kunden som&quot;gift&quot;). Det är huvudsyftet med sammanfogningsprincipen att avgöra vilka data som ska prioriteras och visas som en del av profilen.

Mer information om sammanfogningsprinciper, inklusive hur du skapar, redigerar och deklarerar en standardprincip för sammanfogning för din organisation, får du genom att läsa översikten [över sammanfogningsprinciper](../../profile/merge-policies/overview.md).

Kontrollpanelen väljer automatiskt vilken sammanfogningsprincip som ska visas, men du kan ändra den sammanfogningsprincip som väljs med hjälp av den nedrullningsbara menyn. Om du vill välja en annan sammanfogningsprincip markerar du listrutan bredvid sammanfogningsprincipnamnet och väljer sedan den sammanfogningsprincip som du vill visa.

>[!NOTE]
>
>I listrutan visas endast sammanfogningsprinciper som är relaterade till den enskilda klassen för XDM-profiler, men om din organisation har skapat flera sammanfogningsprinciper kan det innebära att du måste rulla för att kunna visa den fullständiga listan över tillgängliga sammanfogningsprinciper.

![](../images/profiles/select-merge-policy.png)

## Widgetar och mätvärden

Kontrollpanelen består av widgetar, som är skrivskyddade mått som ger viktig information om dina profildata.

Datum och tid för den senaste uppdateringen av en widget visar när den senaste ögonblicksbilden av data togs. Datum och tid för ögonblicksbilden anges i UTC. den inte finns i den enskilda användarens eller IMS-organisationens tidszon.

## Tillgängliga widgetar

Experience Platform tillhandahåller flera widgetar som du kan använda för att visualisera olika mått som relaterar till dina profildata. Välj namnet på en widget nedan om du vill veta mer:

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles count trend]](#profiles-count-trend)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)

### [!UICONTROL Profile count] {#profile-count}

Widgeten **[!UICONTROL Profile count]** visar det totala antalet sammanfogade profiler i profildatalagret när ögonblicksbilden togs. Det här numret är resultatet av att den valda sammanfogningsprincipen tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person.

Mer information om fragment och sammanfogade profiler får du om du börjar med att läsa *profilfragment jämfört med sammanfogade profiler* i [Kundprofilöversikt i realtid](../../profile/home.md).

![](../images/profiles/profile-count.png)

### [!UICONTROL Profiles added] {#profiles-added}

Widgeten **[!UICONTROL Profiles added]** visar det totala antalet sammanfogade profiler som har lagts till i datalagret Profil vid den senaste ögonblicksbilden som togs. Det här numret är resultatet av att den valda sammanfogningsprincipen tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person.

Du kan använda listruteväljaren för att visa de profiler som lagts till under de senaste 30 dagarna, 90 dagarna eller 12 månaderna.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles count trend] {#profiles-count-trend}

Widgeten **[!UICONTROL Profiles count trend]** visar det totala antalet sammanfogade profiler som har lagts till i datalagret Profil dagligen under de senaste 30 dagarna, 90 dagar eller 12 månaderna. Detta nummer uppdateras varje dag som ögonblicksbilden tas, och om du vill importera profiler till Platform kommer antalet profiler inte att visas förrän nästa ögonblicksbild tas.

Antalet tillagda profiler är resultatet av att den valda sammanfogningsprincipen tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person.

![](../images/profiles/profile-count-trend.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

Widgeten **[!UICONTROL Profiles by identity]** visar uppdelningen av identiteter för alla sammanfogade profiler i din profilbutik. Det totala antalet profiler per identitet (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kan vara högre än det totala antalet sammanfogade profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

Mer information om identiteter finns i [Adobe Experience Platform Identity Service-dokumentationen](../../identity-service/home.md).

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Identity overlap] {#identity-overlap}

Widgeten **[!UICONTROL Identity overlap]** visar ett Venndiagram, eller ett uppsättningsdiagram, som visar överlappningen av profiler i din profilbutik som innehåller flera identiteter.

När du har använt listrutemenyerna i widgeten för att markera de identiteter som du vill jämföra, visas cirklar med den relativa storleken för varje identitet. Antalet profiler som innehåller båda namnutrymmena representeras av storleken på överlappningen mellan cirklarna.

Om en kund interagerar med ert varumärke i mer än en kanal kopplas flera identiteter till den enskilda kunden, och därför är det troligt att organisationen har flera profiler som innehåller fragment från mer än en identitet.

Mer information om identiteter finns i [Adobe Experience Platform Identity Service-dokumentationen](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna hitta kontrollpanelen Profiler och förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om hur du arbetar med [!DNL Profile]-data i användargränssnittet för Experience Platform finns i användargränssnittshandboken för [kundprofiler i realtid](../../profile/ui/user-guide.md).
