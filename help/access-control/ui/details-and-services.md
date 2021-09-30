---
keywords: Experience Platform;hem;populära ämnen;produktprofil
solution: Experience Platform
title: Hantera detaljer och ytterligare tjänster för en produktprofil
topic-legacy: user guide
description: Det här dokumentet innehåller de steg som krävs för att hantera information och ytterligare tjänster för en produktprofil i Adobe Admin Console. Du kan konfigurera information om en profil och få tillgång till ytterligare tjänster på menyn Profilinställningar.
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: 6228f499a42e61583abd1f7ff1e1af1fb90640c6
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Hantera information och ytterligare tjänster för en produktprofil

Du kan konfigurera en profils information och åtkomst till ytterligare tjänster från **[!UICONTROL Profile Settings]**-menyn. Du öppnar menyn genom att välja **[!UICONTROL Settings]** på sidan **[!UICONTROL Product Profile]**.

![inställningar](../images/settings.png)

Menyn **[!UICONTROL Edit product profile]** visas med början på fliken **[!UICONTROL Edit profile details]**. På den här fliken kan du ange och redigera profilens namn och beskrivning. Du kan också ändra visningsnamnet och e-postmeddelandeinställningarna för ditt konto.

![edit-product-profile](../images/edit-product-profile.png)

Välj **[!UICONTROL Next]** för att komma åt sidan **[!UICONTROL Enable services]**.

Med menyn **[!UICONTROL Enable services]** kan du ändra en profils åtkomst till ytterligare [!DNL Platform]-tjänster som ursprungligen konfigurerades när profilen skapades. Beroende på din [!DNL Platform]-prenumeration kan dessa tjänster omfatta:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- [!DNL Real-Time Customer Data Platform] UI (endast för CDP i realtid)
- B2B-gränssnitt

Klicka på växlingsknappen till höger om en viss tjänst för att aktivera eller inaktivera den. Du kan också markera kryssrutan **[!UICONTROL All on]** om du vill aktivera eller inaktivera alla listade tjänster.

När du är klar väljer du **[!UICONTROL Save]**.

![enable-services](../images/enable-services.png)

Kunder som är berättigade till B2B- eller B2P-versionen har tillgång till B2B-gränssnittet. B2B-gränssnittet kan etableras för användare via [!UICONTROL Enable services menu]. Markera växlingsknappen bredvid [!UICONTROL B2B UI] för att aktivera tjänsten för en viss produktprofil och välj sedan **[!UICONTROL Save]**.

Med användargränssnittet för B2B kan användare visa B2B-arbetsflöden för att hantera konton och affärsmöjligheter samt skapa B2B-relaterade segment.

![enable-b2b](../images/enable-b2b.png)