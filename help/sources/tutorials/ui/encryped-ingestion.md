---
title: Infoga krypterade data i källanvändargränssnittet i Workspace
description: Lär dig hur du importerar krypterade data i källans arbetsyta.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Infoga krypterade data i källans användargränssnitt

>[!AVAILABILITY]
>
>Stöd för krypterad datainmatning i källans användargränssnitt finns i betaversion och kanske inte är tillgängligt för din organisation. Funktionen och dokumentationen kan komma att ändras.

Du kan importera krypterade datafiler och mappar till Adobe Experience Platform med hjälp av batchkällor i molnet. Med krypterad datainmatning kan ni utnyttja asymmetriska krypteringsmekanismer för att på ett säkert sätt överföra batchdata till Experience Platform. För närvarande stöds PGP och GPG för asymmetrisk kryptering.

Den här funktionen är tillgänglig för följande källor:

* [Amazon S3]
* [Azure-blob]
* [Azure Data Lake Storage Gen2]
* [Azure-fillagring]
* [Datalandningszon]
* [FTP]
* [Google Cloud-lagring]
* [HDFS]
* [Oraclena objektlagring]
* [SFTP]

Läs den här guiden och lär dig hur du kan importera krypterade data med batchkällor i molnet med hjälp av användargränssnittet.

## Kom igång

Det kan vara bra att ha en förståelse för följande funktioner och koncept i Experience Platform innan du arbetar med krypterad datainmatning i användargränssnittet:

* [Källor](../../home.md): Använd källor i Experience Platform för att importera data från ett Adobe-program eller en datakälla från en tredje part.
* [Dataflöden](../../../dataflows/home.md): Dataflöden är representationer av datajobb som flyttar data mellan Experience Platform. Du kan använda källarbetsytan för att skapa dataflöden som importerar data från en viss källa till Experience Platform.
* [Sandlådor](../../../sandboxes/home.md): Använd sandlådor i Experience Platform för att skapa virtuella partitioner mellan dina Experience Platform-instanser och skapa miljöer som är dedikerade till utveckling eller produktion.

### Kontur på hög nivå

1. Skapa ett krypteringsnyckelpar med hjälp av källarbetsytan i användargränssnittet i Experience Platform. Du kan också skapa nyckelpar för signaturverifiering för att ge ytterligare ett säkerhetslager till dina krypterade data.
2. Använd den offentliga nyckeln för att kryptera dina data.
3. Placera dina krypterade data i din molnlagringsleverantör. Under det här steget måste du också se till att du har en exempelfil som kan användas som referens för att mappa dina källdata till ett XDM-schema (Experience Data Model).
4. Importera krypterade data till Experience Platform genom att skapa en källanslutning.
5. När du skapar din källanslutning anger du det nyckel-ID som motsvarar den offentliga nyckel som du använde för att kryptera dina data. Om du även använde teckenverifieringsnyckelparet måste du även ange det ID för signaturverifieringsnyckel som motsvarar dina krypterade data.
6. Fortsätt till stegen för att skapa dataflödet.

## Skapa ett krypteringsnyckelpar {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID för krypteringsnyckel"
>abstract="Ange det krypteringsnyckel-ID som motsvarar den krypteringsnyckel som användes för att kryptera källdata."

* Navigera till källarbetsytan i plattformsgränssnittet och välj sedan [!UICONTROL Key Pairs] i det övre sidhuvudet.
* Du dirigeras till en sida som visar en lista över befintliga krypteringsnyckelpar i organisationen. Den här sidan innehåller information om en viss nyckels titel, ID, typ, krypteringsalgoritm, förfallodatum och status. Om du vill skapa ett nytt nyckelpar väljer du **[!UICONTROL Create Key]**.
* Välj sedan den nyckeltyp som du vill skapa. Om du vill skapa en krypteringsnyckel väljer du **[!UICONTROL Encryption Key]** och anger sedan en titel och en lösenfras för din krypteringsnyckel. Lösenfrasen är ytterligare ett skyddslager för dina krypteringsnycklar. När lösenordet skapas lagrar Experience Platform den i ett annat säkert valv än den offentliga nyckeln. Du måste ange en sträng som inte är tom som lösenfras.

### Skapa en signaturverifieringsnyckel {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="ID för signaturverifieringsnyckel"
>abstract="Ange det ID för signaturverifieringsnyckel som motsvarar dina signerade, krypterade källdata."

## Importera krypterade data {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Är filen krypterad?"
>abstract="Välj det här alternativet om du vill importera en fil som redan är krypterad."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Välj exempelfil"
>abstract="Du måste importera en exempelfil när du importerar krypterade data för att kunna skapa en mappning."


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
