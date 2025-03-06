---
title: Ansluta AWS Redshift till Experience Platform med användargränssnittet
description: Lär dig hur du ansluter ett AWS Redshift-konto till Experience Platform med hjälp av källgränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: 8533aa3527bfb74a77f5b15dacf9ecfe622477d5
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---

# Anslut [!DNL AWS Redshift] till Experience Platform med användargränssnittet

>[!IMPORTANT]
>
>Källan [!DNL AWS Redshift] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL AWS Redshift]-konto till Adobe Experience Platform med hjälp av källarbetsytan i användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   - [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL AWS Redshift]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

## Navigera i källkatalogen

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!DNL AWS Redshift]** under kategorin *[!UICONTROL Databases]* och välj sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med källkortet AWS Redshift valt.](../../../../images/tutorials/create/redshift/catalog.png)

## Använd ett befintligt konto {#existing}

Därefter går du till autentiseringssteget i arbetsflödet för källor. Här kan du antingen använda ett befintligt konto eller skapa ett nytt.

Om du vill använda ett befintligt konto väljer du kontot [!DNL AWS Redshift] i kontokatalogen och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Kontokatalogen i källarbetsflödet där befintliga konton finns listas.](../../../../images/tutorials/create/redshift/existing.png)

## Skapa ett nytt konto {#create}

Om du inte har något befintligt konto måste du skapa ett nytt konto genom att ange de autentiseringsuppgifter som motsvarar källan.

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och kan lägga till en beskrivning för ditt konto.

### Anslut till Experience Platform på Azure {#azure}

Om du vill ansluta ditt [!DNL AWS Redshift]-konto till Experience Platform på Azure anger du dina autentiseringsuppgifter i indataformuläret och väljer sedan **([!UICONTROL Connect to source])**.

![Det nya kontogränssnittet för att ansluta AWS Redshift till Experience Platform på Azure.](../../../../images/tutorials/create/redshift/new.png)

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Server | Servernamnet för din [!DNL AWS Redshift]-instans. |
| Port | TCP-porten som en [!DNL AWS Redshift]-server använder för att avlyssna klientanslutningar. |
| Användarnamn | Användarnamnet för kontot som du vill ge åtkomst till. |
| Lösenord | Lösenordet som motsvarar användarkontot. |
| Databas | Databasen [!DNL AWS Redshift] från vilken data ska hämtas. |

Mer information om hur du kommer igång finns i [det här [!DNL AWS Redshift] dokumentet](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Anslut till Experience Platform på AWS {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på AWS Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Om du vill skapa ett nytt [!DNL AWS Redshift]-konto och ansluta till Experience Platform på AWS kontrollerar du att du befinner dig i en VA6-sandlåda, anger nödvändiga autentiseringsuppgifter för autentisering och väljer sedan **[!UICONTROL Connect to source]**.

![Det nya kontogränssnittet för att ansluta AWS Redshift till Experience Platform på AWS.](../../../../images/tutorials/create/redshift/aws-auth.png)

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Server | Servernamnet för din [!DNL AWS Redshift]-instans. |
| Port | TCP-porten som en [!DNL AWS Redshift]-server använder för att avlyssna klientanslutningar. |
| Användarnamn | Användarnamnet för kontot som du vill ge åtkomst till. |
| Lösenord | Lösenordet som motsvarar användarkontot. |
| Databas | Databasen [!DNL AWS Redshift] från vilken data ska hämtas. |
| Schema | Namnet på schemat som är associerat med din [!DNL AWS Redshift]-databas. Du måste se till att användaren som du vill ge databasåtkomst till också har åtkomst till det här schemat. |

Mer information om hur du kommer igång finns i [det här [!DNL AWS Redshift] dokumentet](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning mellan din [!DNL AWS Redshift]-databas och Experience Platform. Du kan nu fortsätta med nästa självstudiekurs och [skapa ett dataflöde för att importera data från din databas till Experience Platform](../../dataflow/databases.md).