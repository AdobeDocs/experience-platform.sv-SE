---
title: Oracle Eloqua (V2) Source - översikt
description: Lär dig ansluta Oracle Eloqua till Adobe Experience Platform.
last-substantial-update: 2025-02-02T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 0%

---

# Översikt över källan [!DNL Oracle Eloqua] (V2)

>[!IMPORTANT]
>
>Den ursprungliga källan [[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md) har tagits bort från januari 2026. Det finns inga tillgängliga migreringar för den här inaktuella källan och du måste implementera dina data igen med den nya [!DNL Oracle Eloqua] (V2)-källan.

[!DNL Oracle Eloqua] är en kraftfull automatiseringsplattform för marknadsföring i enterpriseklass som utformats för att hjälpa organisationer, främst inom B2B-området, att automatisera och personalisera den komplexa processen att hantera leads och samordna köparresor. Det fungerar som ett centralt nav där marknadsföringsteamen kan definiera, driftsätta och mäta avancerade kampanjer i flera digitala kanaler, vilket garanterar att potentiella kunder får rätt innehåll i precis den stund de är mest engagerade. Objekten som stöds för förtäring via [!DNL Eloqua] är **Kontakter**, **Konton**, **Kampanjer** och **Aktiviteter**. När det första intaget är slutfört importeras ändrade data enligt en schemalagd stegvis process.

Du kan använda källan [!DNL Eloqua] för att ansluta ditt [!DNL Eloqua]-konto till Adobe Experience Platform. Läs dokumentationen nedan för att lära dig hur du kommer igång.

## Använd exempel på exempel {#use-case-examples}

Nedan finns en tabell över de marknadsföringsobjekt som stöds av integreringen [!DNL Eloqua] (V2) med Adobe Experience Platform. För varje objekt hittar du en beskrivning tillsammans med exempel på användningsexempel som visar hur integrering av [!DNL Eloqua]-data med Real-Time CDP kan öka marknadsföringseffektiviteten och kampanjresultaten.

| Objekt | Beskrivning | Använd exempel på exempel |
| --- | --- | --- |
| Kontakter | Importera kontaktdata (till exempel namn, e-post, telefonnummer, befattning) till Real-Time CDP för att skapa detaljerade, enhetliga kundprofiler som sammanför alla interaktioner och engagemang med varje enskild kontakt. | **Kampanjoptimering:** Genom att integrera kontaktdata från [!DNL Eloqua] kan marknadsföringsteamet identifiera potentiella kunder med hög prioritet baserat på senaste aktiviteter som e-postöppningar, formulärinlämning och händelseregistreringar. Real-Time CDP ger en helhetsbild av varje kontakts beteende över e-post, webbplatser och andra kontaktytor, så att marknadsföringsteamen kan skräddarsy kampanjer och optimera meddelanden för bättre engagemang och konvertering. |
| Konton | Importera data på kontonivå (t.ex. företagsnamn, bransch, företagsstorlek, intäkt, plats) för att skapa kontobaserade marknadsföringsstrategier i Real-Time CDP, och gör det möjligt för teamet att inrikta sig på och engagera rätt organisationer med relevanta meddelanden. | **ABM-kampanjer:** Genom att integrera kontodata från [!DNL Eloqua] kan du skapa riktade ABM-kampanjer. Ett programvaruföretag kan till exempel använda kontouppgifterna för att segmentera och skicka anpassade e-postkampanjer till beslutsfattare på företag inom finanssektorn, för att marknadsföra nya lösningar som är anpassade efter deras bransch. |
| Kampanjer | Lägg in kampanjdata (som kampanjnamn, typer, mål, resultatvärden som öppna frekvenser, CTR) i Real-Time CDP för att spåra och optimera kampanjresultat i flera kanaler. Använd dessa data för att mäta ROI och förfina era strategier. | **Flerkanalsattribuering:** Om [!DNL Eloqua] skickar kampanjdata till Real-Time CDP kan marknadsföringsteamen visa resultatet för kampanjer i olika kanaler (e-post, sociala medier, annonser osv.), attribuera konverteringar till rätt kontaktpunkter och förfina framtida strategier baserat på den insikten. |
| Aktiviteter | Ingest activity data (t.ex. öppning av e-post, klickningar, webbplatsbesök, inskickade formulär, webbinarier-närvaro) för att spåra beteenden och kontakter i realtid i olika kanaler, vilket skapar möjligheter för personaliserat engagemang i realtid. | **Realtidstjänst:** Genom att integrera aktivitetsdata från [!DNL Eloqua] kan Real-Time CDP utlösa personaliserade e-postmeddelanden eller meddelanden till säljarna när en kontakt interagerar med innehåll (som att hämta ett whitepaper eller klicka på en e-postlänk), vilket ger snabb uppföljning och bättre konverteringsmöjligheter. |

{style="table-layout:auto"}

## Förhandskrav {#prerequisites}

I avsnitten nedan finns information om vilka krav som måste uppfyllas innan du kan ansluta källan till Experience Platform.

### Konfigurera autentiseringsprogram

Följ stegen nedan för att lära dig hur du konfigurerar ditt [!DNL Eloqua]-konto och ansluter till Experience Platform med grundläggande autentisering.

Logga in på din [!DNL Eloqua]-instans som administratör (eller som en användare som har behörighet att skapa användare, säkerhetsgrupper och appar) för att komma igång.

![Min Eloqua-instrumentpanel.](../../images/tutorials/create/eloqua/admin.png)

Navigera till **Inställningar** > **Plattformstillägg** > **App Cloud Developer** > **Skapa app**. Ange information om din app, inklusive dess namn, beskrivning, ikon och OAuth-återanrops-URL. Välj **Spara** när du är klar.

![Panelen App Developer och knappen Create App (Skapa app) på Eloqua-kontrollpanelen.](../../images/tutorials/create/eloqua/create-app.png)

| Egenskap | Beskrivning |
| --- | --- |
| Namn | Namnet på din app. |
| Beskrivning | En kort beskrivning av appen. |
| Ikon | Ikonens URL. |
| URL för OAuth-återanrop | Den URL som användare ska omdirigeras till efter att appen har installerats och autentiserats med [!DNL Eloqua]. |

![Skapa-appfönstret i Eloqua.](../../images/tutorials/create/eloqua/new-app.png)

När appen har skapats navigerar du till [!DNL Authentication to Eloqua] och hämtar **klient-ID** och **klienthemlighet** från den nya appen. Dessa värden används senare vid anslutning till Experience Platform.

![Klient-ID och klienthemlighet i Eloqua.](../../images/tutorials/create/eloqua/credentials.png)

Med säkerhetsgrupper kan administratörer styra vilken åtkomstnivå användare har till resurser, funktioner, gränssnitt och så vidare. Om du vill skapa en säkerhetsgrupp går du till **Inställningar** > **Användare**. Välj sedan fliken **Grupp** på den vänstra panelen och välj sedan **Skapa ny säkerhetsgrupp**.

![Kontrollpanelen för användarhantering i Eloqua.](../../images/tutorials/create/eloqua/user-management.png)

Använd fönstret **[!DNL Security Group Overview]** för att ange ett namn och en akronym för din säkerhetsgrupp. Navigera till [!DNL Action Permissions] och lägg till API-behörigheten [!DNL Consume] från listan och välj **Spara**.

![Översiktsfönstret för säkerhetsgruppen i Eloqua.](../../images/tutorials/create/eloqua/security-group-overview.png)

![Urvalsfönstret för API:t &#x200B;](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>API:t [!DNL Consume] är en nödvändig behörighet, men du kan lägga till fler behörigheter beroende på hur du använder appen.

Om du vill importera kampanjdata navigerar du till gränssnittet **Redigera användare** och lägger till [!DNL Guided Campaigns] i den valda säkerhetsgruppen.

![Säkerhetsgruppen med guidade kampanjer har lagts till.](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

Du kan även skapa ytterligare en användare och lägga till användaren i en säkerhetsgrupp. Mer information finns i [!DNL Eloqua]-dokumentationen om hur du [skapar en användare](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm) och [tilldelar en användare till en säkerhetsgrupp](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm).

### Samla in nödvändiga inloggningsuppgifter

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta [!DNL Eloqua] till Experience Platform.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Klient-ID | Den offentligt exponerade identifierare som används av [!DNL Eloqua] för att identifiera ditt konto vid auktorisering till Experience Platform. |
| Klienthemlighet | Den konfidentiella nyckeln som bara är känd för klientprogrammet och auktoriseringsservern. Den här nyckeln krävs vid sidan av klient-ID för att ditt konto ska kunna autentiseras. |
| Användarnamn | Användarnamnet som är associerat med ditt [!DNL Eloqua]-konto. Detta används för att verifiera och auktorisera din åtkomst. Användarnamnet följer formatet för `CompanyName\Username`. |
| Lösenord | Lösenordet som är kopplat till ditt [!DNL Eloqua]-konto. Tillsammans med ditt användarnamn ger det åtkomst till din Eloqua-miljö. |
| Basslutpunkt | Prefixet för din autentiseringsbas-URI för [!DNL Eloqua]. Basslutpunkten ska inte innehålla `http://` eller `https://` vid autentisering. |

## Mappningsguide för [!DNL Eloqua]

>[!NOTE]
>
>Följande deltafält används internt för inkrementell datainläsning:
>
>- **Kontakter:** `C_DateModified`
>- **Konton:** `M_DateModified`
>- **Aktivitet:** `CreatedAt`
>- **Egna objekt:** `UpdatedAt`
>- **Kampanj:** `updatedAt`

I följande tabeller finns detaljerade mappningar mellan [!DNL Eloqua]-källfält och deras motsvarande XDM-målfält (Experience Data Model) i Experience Platform. Varje rad visar transformeringslogiken, om fältet är oföränderligt, och ger dig ytterligare information som hjälper dig förstå hur dina [!DNL Eloqua]-data kommer att importeras och struktureras i Experience Platform.

### Konton

| Eloqua Source Column | XDM-målsökväg | Anteckningar |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | Det här fältet är alltid inställt på det fasta värdet &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `M_CompanyName` | accountName | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountScore | |
| `M_Account_Type1` | accountType | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Kopplingen kan inte identifiera ditt CRM-instans-ID automatiskt. Du måste ersätta `${CRM_INSTANCE_ID}` manuellt med ditt faktiska instans-ID för CRM, antingen ditt instans-ID för Salesforce eller Dynamics. Om det finns `M_SFDCAccountID` vid importen genereras den externa nyckeln med det värdet och tillägget `\@CRM_INSTANCE_ID.Salesforce` läggs till. Om fältet är tomt kommer kopplingen att använda `M_MSCRMAccountID` och lägga till `\@CRM_INSTANCE_ID.Dynamics` i stället. Om båda fälten är tomma ställs fältet in på null. |

{style="table-layout:auto"}

### Aktiviteter

| Eloqua Source Column | XDM-målsökväg | Anteckningar |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | Det här fältet är alltid inställt på det fasta värdet &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | Baserat på ActivityType fylls motsvarande Experience Platform eventType-värde i. För ExternalActivities finns ingen eventType i Experience Platform. Du kan ändra den här mappningen för att hantera fler typer. |
| `ActivityDate` | tidsstämpel | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### Kampanjer

| Eloqua Source Column | XDM-målsökväg | Anteckningar |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | Det här fältet är alltid inställt på det fasta värdet &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `name` | campaignName | |
| `endAt` | campaignEndDate | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignStatus | |
| `campaignType` | campaignType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### Kontakter

| Eloqua Source Column | XDM-målsökväg | Anteckningar |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | Det här fältet är alltid inställt på det fasta värdet &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | `SOURCE_INSTANCE_ID` ersätts automatiskt av kopplingen. |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | Om instansen [!DNL Eloqua] synkroniseras med Salesforce ska du behålla mappningen. Annars tar du bort den. Kopplingen kan inte identifiera CRM_INSTANCE_ID, så du måste ersätta ${CRM_INSTANCE_ID} med ditt synkroniserade Salesforce-instans-ID. Samma mappning gäller för personComponents och extSourceSystemAudit, så behåll båda. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | Om instansen [!DNL Eloqua] synkroniseras med Dynamics ska du behålla mappningen. Annars tar du bort den. Kopplingen kan inte identifiera CRM_INSTANCE_ID, så du måste ersätta ${CRM_INSTANCE_ID} med ditt synkroniserade Dynamics-instans-ID. Samma mappning gäller för personComponents och extSourceSystemAudit, så behåll båda. |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | Om instansen [!DNL Eloqua] synkroniseras med Salesforce ska du behålla mappningen. Annars tar du bort den. Kopplingen kan inte identifiera CRM_INSTANCE_ID, så du måste ersätta ${CRM_INSTANCE_ID} med ditt synkroniserade Salesforce-instans-ID. Samma mappning gäller för personComponents och extSourceSystemAudit, så behåll båda. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Om instansen [!DNL Eloqua] synkroniseras med Dynamics ska du behålla mappningen. Annars tar du bort den. Kopplingen kan inte identifiera CRM_INSTANCE_ID, så du måste ersätta ${CRM_INSTANCE_ID} med ditt synkroniserade Dynamics-instans-ID. Samma mappning gäller för personComponents och extSourceSystemAudit, så behåll båda. |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | Kopplingen kan inte identifiera CRM_INSTANCE_ID, så du måste ersätta ${CRM_INSTANCE_ID} med ditt synkroniserade CRM-instans-ID, antingen Salesforce instans-ID eller Dynamics-instans-ID. Samma mappning gäller både b2b.accountKey och personComponents.sourceAccountKey, så behåll båda. |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | Kopplingen kan inte identifiera CRM_INSTANCE_ID, så du måste ersätta ${CRM_INSTANCE_ID} med ditt synkroniserade CRM-instans-ID, antingen Salesforce instans-ID eller Dynamics-instans-ID. Samma mappning gäller både b2b.accountKey och personComponents.sourceAccountKey, så behåll båda. |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### Referens för mappning av aktivitetstyp

| Eloqua ActivityType | XDM eventType |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | skicka som |

{style="table-layout:auto"}

### Variabelplatshållare

Mappningsmallarna använder följande variabelplatshållare som ersätts när ett dataflöde körs:

| Platshållare | Beskrivning | Användning |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | Unikt ID för Eloqua-källinstansen | Används i källnycklar |
| `${CRM_INSTANCE_ID}` | Unikt ID för CRM-system (Salesforce/Dynamics) | Används i externa nycklar |

## Anslut [!DNL Eloqua] till Experience Platform

Fortsätt med att konfigurera [!DNL Eloqua]-källanslutningen i Experience Platform. En steg-för-steg-guide om hur du konfigurerar anslutningen via användargränssnittet finns i [självstudiekursen här](../../tutorials/ui/create/marketing-automation/eloqua.md). Läs den här självstudiekursen om du vill lära dig att ansluta ditt [!DNL Eloqua]-konto, välja data, mappningsfält, schemalägga ingivelser och övervaka dina dataflöden.

