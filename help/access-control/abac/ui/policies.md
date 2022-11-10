---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;attributbaserad åtkomstkontroll;ABAC
title: Attributbaserad åtkomstkontroll Skapa en profil
description: Det här dokumentet innehåller information om hur du hanterar profiler via gränssnittet Behörigheter i Adobe Experience Cloud
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 1a755fa5480e036bde50617f01440cfabbaf64c2
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# Hantera profiler

Profiler är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Profiler kan antingen vara lokala eller globala och kan åsidosätta andra profiler.

## Skapa en ny princip

Om du vill skapa en ny profil väljer du **[!UICONTROL Policies]** i sidlisten och välj **[!UICONTROL Create Policy]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

The **[!UICONTROL Create a new policy]** visas där du uppmanas att ange ett namn och en valfri beskrivning. När du är klar väljer du **[!UICONTROL Confirm]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Använd listrutepilen för att välja om du vill **Tillåt åtkomst till** (![flac-allow-access-to](../../images/flac-ui/flac-permit-access-to.png)) en resurs eller **Neka åtkomst till** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) en resurs.

Välj sedan den resurs som du vill inkludera i principen med listrutan och sökåtkomsttypen, läs eller skriv.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Använd sedan listrutepilen för att välja det villkor som du vill tillämpa på profilen, **Följande är sant** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) eller **Följande är false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Markera plusikonen för att **Lägg till matchningsuttryck** eller **Lägg till uttrycksgrupp** för resursen.

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Använd listrutan för att välja **Resurs**.

![flash-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

I listrutan väljer du **Matchar**.

![flac-policy-match-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Välj sedan typ av etikett (**[!UICONTROL Core label]** eller **[!UICONTROL Custom label]**) för att matcha etiketten som tilldelats användaren i roller.

![flash-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Slutligen väljer du **Sandbox** som du vill att principvillkoren ska gälla för med hjälp av listrutan.

![flash-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Välj **Lägg till resurs** för att lägga till fler resurser. När du är klar väljer du **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Den nya principen har skapats och du omdirigeras till **[!UICONTROL Policies]** där du ser den nya profilen i listan.

![sparad med flac-policy](../../images/flac-ui/flac-policy-saved.png)

## Redigera en profil

Om du vill redigera en befintlig profil väljer du den i dialogrutan **[!UICONTROL Policies]** -fliken. Du kan också använda filteralternativet för att filtrera resultatet och hitta profilen som du vill redigera.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Välj sedan ellipsen (`…`) bredvid profilnamnet och en listruta med kontroller för att redigera, inaktivera, ta bort eller duplicera rollen. Välj Redigera i listrutan.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

Skärmen för principbehörigheter visas. Gör uppdateringarna och välj sedan **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Principen har uppdaterats och du omdirigeras till **[!UICONTROL Policies]** -fliken.

## Duplicera en princip

Om du vill duplicera en befintlig princip väljer du den i dialogrutan **[!UICONTROL Policies]** -fliken. Du kan också använda filteralternativet för att filtrera resultatet och hitta profilen som du vill redigera.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Välj sedan ellipsen (`…`) bredvid ett profilnamn och en listruta innehåller kontroller för att redigera, inaktivera, ta bort eller duplicera rollen. Välj Duplicera i listrutan.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

The **[!UICONTROL Duplicate policy]** visas och du uppmanas att bekräfta dupliceringen.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Den nya profilen visas i listan som en kopia av originalet på **[!UICONTROL Policies]** -fliken.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Ta bort en profil

Om du vill ta bort en befintlig princip väljer du den i dialogrutan **[!UICONTROL Policies]** -fliken. Du kan också använda filteralternativet för att filtrera resultatet och hitta profilen som du vill ta bort.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Välj sedan ellipsen (`…`) bredvid ett profilnamn och en listruta innehåller kontroller för att redigera, inaktivera, ta bort eller duplicera rollen. Välj Ta bort i listrutan.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

The **[!UICONTROL Delete user policy]** visas och du uppmanas att bekräfta borttagningen.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

Du kommer tillbaka till **[!UICONTROL policies]** och en bekräftelse på borttagningen visas.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Aktivera en profil

Om du vill aktivera en befintlig princip väljer du den i dialogrutan **[!UICONTROL Policies]** -fliken. Du kan också använda filteralternativet för att filtrera resultatet och hitta profilen som du vill ta bort.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Välj sedan ellipsen (`…`) bredvid ett profilnamn och en listruta med kontroller för att redigera, aktivera, ta bort eller duplicera rollen. Välj Aktivera i listrutan.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

The **[!UICONTROL Activate user policy]** visas och du uppmanas att bekräfta aktiveringen.

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

Du kommer tillbaka till **[!UICONTROL policies]** och en bekräftelse på aktiveringen visas. Policystatusen visas som aktiv.

![flash-policy-activated](../../images/flac-ui/flac-policy-activated.png)

## Nästa steg

När du har skapat en ny profil kan du fortsätta till nästa steg i [hantera behörigheter för en roll](permissions.md).
