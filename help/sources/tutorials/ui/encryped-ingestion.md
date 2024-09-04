---
title: Infoga krypterade data i källanvändargränssnittet i Workspace
description: Lär dig hur du importerar krypterade data i källans arbetsyta.
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Infoga krypterade data i källans användargränssnitt

Läs den här guiden och lär dig hur du kan importera krypterade data till Adobe Experience Platform med molnlagringskällor för batchdata.

## Förhandskrav

* Kryptera data

## Importera krypterade data {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Är filen krypterad?"
>abstract="Välj det här alternativet om du vill importera en fil som redan är krypterad."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Välj exempelfil"
>abstract="Du måste importera en exempelfil när du importerar krypterade data för att kunna skapa en mappning."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID för krypteringsnyckel"
>abstract="Ange det krypteringsnyckel-ID som motsvarar den krypteringsnyckel som användes för att kryptera källdata."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="ID för signaturverifieringsnyckel"
>abstract="Ange det ID för signaturverifieringsnyckel som motsvarar dina signerade, krypterade källdata."

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
