---
title: Konfigurera aviseringar och IP-tillåtelselista för Azure CMK
description: Lär dig hur du tillåtslista Adobe statiska IP-adress i Azure Key Vault och hur Experience Platform-varningar hjälper dig att identifiera och lösa problem med kundhanterad nyckel.
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Konfigurera aviseringar och IP-tillåtelselista för [!DNL Azure] CMK

För att förbättra genomskinligheten tillhandahåller Adobe en [övervakningstjänst](../../../../observability/alerts/ui.md){target="_blank"} som kontrollerar nyckelvalvets åtkomststatus och utlöser varningar om problem uppstår. Dessa varningar hjälper dig att svara snabbt och undvika avbrott i tjänsten. Om du vill aktivera den här tjänsten tillåtslista du Adobe statiska IP-adress.

>[!IMPORTANT]
>
>Om du har inaktiverat åtkomst till offentliga nätverk eller konfigurerat [!DNL Azure]-nyckelvalvet så att bara vissa nätverk tillåts, måste du lägga till en statisk Adobe-IP-adress i tillåtelselista. Utan det kanske du inte får något meddelande om åtkomstproblem som kan påverka Experience Platform-instansen.

## Tillåtslista Adobe statiska IP-adress i [!DNL Azure] nyckelvalv {#add-adobe-static-ip}

Navigera till **[!DNL Azure Key Vault]** > **[!DNL Networking settings]** om du vill aktivera de här aviseringarna samtidigt som du behåller nätverksbegränsningarna. Välj **[!DNL Allow public access from specific virtual networks and IP addresses]** på fliken **[!DNL Firewalls and virtual networks]**.

![[!DNL Azure] Inställningsskärmen för nyckelvalv för nätverk visar var Adobe statiska IP-adress ska läggas till och med alternativet Tillåt åtkomst från markerat.](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Adobe statiska IP-adress

>[!IMPORTANT]
>
>Den statiska IP-adressen som tillhandahålls av Adobe är: `20.88.123.53`.

I avsnittet **[!DNL Firewall]** väljer du sedan **[!DNL Add your current IP address]** och ersätter den med Adobe statiska IP-adress. Alla utgående anslutningar behandlas som produktionsmiljöer, så denna statiska IP-adress måste tillåtslista för att säkerställa oavbruten åtkomst till ditt nyckelvalv i begränsade nätverkskonfigurationer.

>[!NOTE]
>
>När du har lagt till eller uppdaterat den statiska IP-adressen i inställningarna för nyckelvalv för [!DNL Azure] kan det ta upp till 10 minuter innan ändringen börjar gälla. När IP-adressen har lagts till får CMK-appen åtkomst till nyckelvalvet för att verifiera behörigheter.

När du har tillåtslista Adobe statiska IP-adress kan Experience Platform övervaka åtkomsten till ditt nyckelvalv och utlösa varningar om det uppstår problem. Dessa varningar ger tidiga varningar så att du kan agera innan tjänsten påverkas. I nästa avsnitt beskrivs vilka typer av aviseringar du kan få och hur du ska svara.

## Övervaka aviseringar {#monitor-alerts}

Plattformsaviseringar meddelar dig om problem som kan avbryta nyckelåtkomst, till exempel **[!UICONTROL Key access failure]** eller **[!UICONTROL Key disablement]**. Dessa varningar hjälper dig att snabbt identifiera problem som borttagen statisk IP eller en felkonfigurerad brandvägg. Granska brandväggsinställningarna för [!DNL Azure] och lägg till IP-adressen igen om du vill återställa åtkomsten.

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

Prenumerera på Adobe I/O händelsemeddelanden för att få realtidsaviseringar i övervakningsverktygen. Instruktioner finns i [Prenumerera på Adobe I/O-händelsemeddelanden](../../../../observability/alerts/subscribe.md). Du kan även läsa användargränssnittsguiden för [varningar](../../../../observability/alerts/ui.md) för att lära dig hur du visar och hanterar varningar i Experience Platform.

## Nästa steg

Du har nu konfigurerat IP-tillåtelselistning och varningsövervakning för ditt [!DNL Azure]-nyckelvalv. Följ dessa konfigurationsguider när du vill slutföra konfigurationen av kundhanterade nycklar i [!DNL Azure].

- [Konfigurera ett  [!DNL Azure] nyckelvalv](./azure-key-vault-config.md)
- [Använd API:t för att konfigurera CMK](./api-set-up.md)
- [Använd användargränssnittet för att konfigurera CMK](./ui-set-up.md)
