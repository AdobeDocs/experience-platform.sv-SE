---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individuell profil;fält;scheman;scheman;identityMap;identity map;identity map;Schema design;map;union schema;union schema
title: Fältgrupp för IdentityMap-schema
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: 43b3b79a4d24fd92c7afbf9ca9c83b0cbf80e2c2
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL IdentityMap] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Fältgruppen innehåller ett enda mappningsfält som innehåller en uppsättning användaridentiteter som angetts av namnutrymmet.

![Ett diagram över [!UICONTROL IdentityMap] schemafältgrupp](../../images/field-groups/identitymap.png)

Se avsnittet om identitetskartor i [grunderna för schemakomposition](../../schema/composition.md#identityMap) om du vill ha mer information om deras användning, inklusive fördelarna och nackdelarna.

**exempel**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Mer information om fältgruppen finns i [fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) i den offentliga XDM-databasen.
