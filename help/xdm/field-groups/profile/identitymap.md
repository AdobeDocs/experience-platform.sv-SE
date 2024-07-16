---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individuell profil;fält;scheman;scheman;identityMap;identity map;identity map;Schema design;map;union schema;union schema
title: Fältgrupp för IdentityMap-schema
description: Lär dig mer om klassen XDM Individual Profile.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL IdentityMap]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL IdentityMap] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Fältgruppen innehåller ett enda mappningsfält som innehåller en uppsättning användaridentiteter som angetts av namnutrymmet.

![Ett diagram över [!UICONTROL IdentityMap] schemafältgruppen ](../../images/field-groups/identitymap.png)

I avsnittet om identitetskartor i [grunderna för schemakomposition](../../schema/composition.md#identityMap) finns mer information om användningsfall, inklusive fördelar och nackdelar.

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

Mer information om fältgruppen finns i det [fullständiga schemat](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) i den offentliga XDM-databasen.
