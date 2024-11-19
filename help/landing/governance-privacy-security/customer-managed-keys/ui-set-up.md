---
title: Konfigurera och konfigurera kundhanterade nycklar med hjälp av plattformsgränssnittet
description: Lär dig hur du konfigurerar din CMK-app med din Azure-klient och skickar ditt krypteringsnyckel-ID till Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Konfigurera och konfigurera kundhanterade nycklar med hjälp av plattformsgränssnittet

Det här dokumentet beskriver processen för att aktivera funktionen för kundhanterade nycklar (CMK) i plattformen med användargränssnittet. Instruktioner om hur du slutför den här processen med API:t finns i [API CMK-inställningsdokumentet](./api-set-up.md).

## Förhandskrav

Om du vill visa och gå till avsnittet [!UICONTROL Encryption] i Adobe Experience Platform måste du ha skapat en roll och tilldelat behörigheten [!UICONTROL Manage Customer Managed Key] till den rollen. Alla användare som har behörigheten [!UICONTROL Manage Customer Managed Key] kan aktivera CMK för sin organisation.

Mer information om hur du tilldelar roller och behörigheter i Experience Platform finns i [Konfigurera behörigheter](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Om du vill aktivera CMK måste [[!DNL Azure] nyckelvalvet konfigureras](./azure-key-vault-config.md) med följande inställningar:

* [Aktivera rensningsskydd](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Aktivera mjuk borttagning](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurera åtkomst med  [!DNL Azure] rollbaserad åtkomstkontroll](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Konfigurera ett  [!DNL Azure] nyckelvalv](./azure-key-vault-config.md)

## Konfigurera CMK-appen {#register-app}

När du har konfigurerat nyckelvalvet är nästa steg att registrera CMK-programmet som ska länka till din [!DNL Azure]-klient.

### Komma igång

Om du vill visa kontrollpanelen [!UICONTROL Encryption configurations] väljer du **[!UICONTROL Encryption]** under rubriken [!UICONTROL Administration] i den vänstra navigeringssidlisten.

![Kontrollpanelen för krypteringskonfiguration med kryptering och kortet för kundhanterade nycklar är markerat.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Välj **[!UICONTROL Configure]** för att öppna vyn [!UICONTROL Customer Managed Keys configuration]. Den här arbetsytan innehåller alla värden som krävs för att slutföra stegen som beskrivs nedan och utföra integreringen med Azure Key-valvet.

### Kopiera autentiserings-URL {#copy-authentication-url}

Om du vill starta registreringsprocessen kopierar du URL:en för programautentisering för din organisation från vyn [!UICONTROL Customer Managed Keys configuration] och klistrar in den i din [!DNL Azure] miljö **[!DNL Key Vault Crypto Service Encryption User]**. Information om hur du [tilldelar en roll](#assign-to-role) finns i nästa avsnitt.

Välj kopieringsikonen (![Kopieringsikonen.](/help/images/icons/copy.png)) av [!UICONTROL Application authentication url].

![Vyn [!UICONTROL Customer Managed Keys configuration] med URL:en för programautentisering är markerad.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Kopiera och klistra in [!UICONTROL Application authentication url] i en webbläsare för att öppna en autentiseringsdialogruta. Välj **[!DNL Accept]** om du vill lägga till CMK-programtjänstens huvudnamn i din [!DNL Azure]-innehavare. Bekräftelse av autentiseringen omdirigerar dig till landningssidan för Experience Cloud.

![En dialogruta för Microsoft-behörighetsbegäran med [!UICONTROL Accept] markerad.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Om du har flera [!DNL Microsoft Azure]-prenumerationer kan du ansluta din Platform-instans till fel nyckelvalv. I det här fallet måste du byta ut `common`-avsnittet i URL:en för programautentisering för CMK-katalog-ID:t.<br>Kopiera CMK-katalog-ID från sidan Portal settings, Directories, and Subscriptions (Portal-inställningar, Kataloger och Prenumerationer) i [!DNL Microsoft Azure] programmet<br>![Sidan [!DNL Microsoft Azure] Application Portal settings, Directories and Subscriptions (Programportalinställningar, kataloger och prenumerationer) med katalog-ID markerat.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Klistra sedan in den i webbläsarens adressfält.<br>![En webbläsarsida i Google med avsnittet &quot;common&quot; i URL:en för programautentisering markerad.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Tilldela CMK-appen till en roll {#assign-to-role}

När autentiseringsprocessen är slutförd går du tillbaka till [!DNL Azure]-nyckelvalvet och väljer **[!DNL Access control]** i den vänstra navigeringen. Här väljer du **[!DNL Add]** följt av **[!DNL Add role assignment]**.

![Kontrollpanelen [!DNL Microsoft Azure] med [!DNL Add] och [!DNL Add role assignment] markerade.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

På nästa skärm får du en uppmaning om att välja en roll för uppdraget. Välj **[!DNL Key Vault Crypto Service Encryption User]** innan du väljer **[!DNL Next]** för att fortsätta.

>[!NOTE]
>
>Om du har nivån [!DNL Managed-HSM Key Vault] måste du välja användarrollen **[!DNL Managed HSM Crypto Service Encryption User]**.

![Kontrollpanelen [!DNL Microsoft Azure] med [!DNL Key Vault Crypto Service Encryption User] markerad.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

På nästa skärm väljer du **[!DNL Select members]** för att öppna en dialogruta i den högra listen. Använd sökfältet för att hitta tjänstens huvudnamn för CMK-programmet och markera det i listan. När du är klar väljer du **[!DNL Save]**.

>[!NOTE]
>
>Om du inte kan hitta ditt program i listan har ditt huvudnamn inte godkänts i din klientorganisation. Om du vill vara säker på att du har rätt behörigheter kan du samarbeta med [!DNL Azure]-administratören eller -representanten.

Du kan verifiera programmet genom att jämföra [!UICONTROL Application ID] som finns i vyn [!UICONTROL Customer Managed Keys configuration] med [!DNL Application ID] som finns i programöversikten för [!DNL Microsoft Azure].

![Vyn [!UICONTROL Customer Managed Keys configuration] med [!UICONTROL Application ID] markerad.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

All information som krävs för att verifiera Azure-verktygen ingår i plattformens användargränssnitt. Den här detaljnivån tillhandahålls så många användare som vill använda andra Azure-verktyg för att förbättra sina möjligheter att övervaka och logga dessa program åtkomst till deras nyckelvalv. Att förstå dessa identifierare är avgörande för det ändamålet och för att hjälpa Adobes tjänster att komma åt nyckeln.

## Aktivera krypteringsnyckelkonfigurationen i Experience Platform {#send-to-adobe}

När du har installerat CMK-appen på [!DNL Azure] kan du skicka krypteringsnyckelns identifierare till Adobe. Välj **[!DNL Keys]** i den vänstra navigeringen, följt av namnet på nyckeln som du vill skicka.

![Microsoft Azure-instrumentpanelen med objektet [!DNL Keys] och nyckelnamnet markerat.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Välj den senaste versionen av nyckeln så visas informationssidan. Här kan du välja att konfigurera tillåtna åtgärder för nyckeln.

>[!IMPORTANT]
>
>De åtgärder som minst krävs för nyckeln är behörigheterna **[!DNL Wrap Key]** och **[!DNL Unwrap Key]**. Du kan inkludera [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] och [!DNL Verify] om du vill.

Fältet **[!UICONTROL Key Identifier]** visar URI-identifieraren för nyckeln. Kopiera det här URI-värdet för användning i nästa steg.

![Nyckelinformation för Microsoft Azure-instrumentpanelen med avsnitten [!DNL Permitted operations] och kopieringsnyckel markerade.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

När du har fått [!DNL Key vault URI] går du tillbaka till vyn [!UICONTROL Customer Managed Keys configuration] och anger en beskrivning **[!UICONTROL Configuration name]**. Lägg sedan till [!DNL Key Identifier] från sidan med Azure-nyckeldetaljer i **[!UICONTROL Key vault key identifier]** och välj **[!UICONTROL  Save]**.

![Vyn [!UICONTROL Customer Managed Keys configuration] med avsnitten [!UICONTROL Configuration name] och [!UICONTROL Key vault key identifier] markerade.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Du återgår till [!UICONTROL Encryption configurations dashboard]. Status för konfigurationen [!UICONTROL Customer Managed Keys] visas som [!UICONTROL Processing].

![Kontrollpanelen [!UICONTROL Encryption configurations] med [!UICONTROL Processing] markerad på [!UICONTROL Customer Managed Keys]-kortet.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Verifiera konfigurationens status {#check-status}

Bearbetningen kan ta lång tid. Om du vill kontrollera statusen för konfigurationen går du tillbaka till vyn [!UICONTROL Customer Managed Keys configuration] och rullar ned till [!UICONTROL Configuration status]. Förloppsindikatorn har avancerat till steg ett av tre och förklarar att systemet validerar att plattformen har åtkomst till nyckel- och nyckelvalvet.

Det finns fyra möjliga statusvärden för CMK-konfigurationen. De är följande:

* Steg 1: Verifierar att plattformen har åtkomst till nyckel- och nyckelvalvet.
* Steg 2: Nyckelvalvet och nyckelnamnet läggs till i alla datalager i organisationen.
* Steg 3: Nyckelvalvet och nyckelnamnet har lagts till i datalagret.
* `FAILED`: Ett problem har uppstått, huvudsakligen relaterat till nyckeln, nyckelvalvet eller konfigurationen av multi-tenant-appar.

## Nästa steg

Genom att utföra ovanstående steg har du aktiverat CMK för din organisation. Data som är inkapslade i primära datalager krypteras och dekrypteras nu med nycklarna i [!DNL Azure]-nyckelvalvet.
