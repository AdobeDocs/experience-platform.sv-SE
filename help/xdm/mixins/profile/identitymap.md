---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individuell profil;fält;scheman;scheman;identityMap;identity map;identity map;Schema design;map;union schema;union schema
solution: Experience Platform
title: IdentityMap Mixin
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] blanda

>[!NOTE]
>
>Namnen på flera blandningar har ändrats. Mer information finns i dokumentet om [uppdateringar av blandnamn](../name-updates.md).

[!UICONTROL IdentityMap] är en standardblandning för  [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). MixIn innehåller ett enda kartfält som innehåller en uppsättning användaridentiteter som skrivs med namnutrymme.

>[!WARNING]
>
>Fältet `IdentityMap` uppdateras automatiskt av systemet när identitetsdata importeras. Om du vill använda det här fältet för [Kundprofil för realtid](../../../profile/home.md) ska du inte försöka uppdatera fältets innehåll manuellt i dataåtgärderna.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Mer information om hur de används finns i avsnittet om identitetskartor i [grunderna för schemakomposition](../../schema/composition.md#identityMap).