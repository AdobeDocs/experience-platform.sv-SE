---
title: Data Landing Zone Source
description: Lär dig ansluta Data Landing Zone till Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 1d4dd60180ef2a3cbf6dcd565c2f09dd575716b9
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Den här sidan är specifik för [!DNL Data Landing Zone] *source*-kopplingen i Experience Platform. Information om hur du ansluter till [!DNL Data Landing Zone] *destination*-kopplingen finns på [[!DNL Data Landing Zone] dokumentationssidan för målet](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] är ett [!DNL Azure Blob]-lagringsgränssnitt som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att hämta filer till plattformen. Du har åtkomst till en [!DNL Data Landing Zone]-behållare per sandlåda, och den totala datavolymen för alla behållare är begränsad till den totala datamängden som tillhandahålls med plattformsprodukten och tjänstlicensen. Alla kunder i Experience Platform har etablerats med en [!DNL Data Landing Zone]-behållare per sandlåda. Du kan läsa och skriva filer till behållaren via [!DNL Azure Storage Explorer] eller kommandoradsgränssnittet.

[!DNL Data Landing Zone] har stöd för SAS-baserad autentisering och dess data skyddas med standardsäkerhetsmekanismer för lagring i [!DNL Azure Blob] vid vila och överföring. Med SAS-baserad autentisering kan du få säker åtkomst till din [!DNL Data Landing Zone]-behållare via en offentlig internetanslutning. Du behöver inte göra några nätverksändringar för att komma åt din [!DNL Data Landing Zone]-behållare, vilket innebär att du inte behöver konfigurera några tillåtelselista- eller korsregionsinställningar för ditt nätverk. Experience Platform tillämpar en strikt 7-dagars förfallotid för alla filer och mappar som överförts till en [!DNL Data Landing Zone]-behållare. Alla filer och mappar tas bort efter sju dagar.

## Konfigurera din [!DNL Data Landing Zone]-källa för Experience Platform på Azure {#azure}

Följ stegen nedan för att lära dig hur du kan konfigurera ditt [!DNL Data Landing Zone]-konto för Experience Platform på Azure.

>[!NOTE]
>
>Om du vill komma åt [!DNL Data Landing Zone] från [!DNL Azure Data Factory] måste du skapa en länkad tjänst för [!DNL Data Landing Zone] med hjälp av [ SAS-autentiseringsuppgifterna](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials) som tillhandahålls av Experience Platform. När du har skapat den länkade tjänsten kan du utforska din [!DNL Data Landing Zone] genom att välja behållarsökvägen i stället för standardrotsökvägen.

### Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfiler eller -kataloger.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (som `0x00` till `0x1F`, `\u0081` och så vidare). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

### Hantera innehållet i din Data Landing Zone{#manage-the-contents-of-your-data-landing-zone}

Du kan använda [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) för att hantera innehållet i [!DNL Data Landing Zone]-behållaren.

I användargränssnittet för [!DNL Azure Storage Explorer] väljer du anslutningsikonen i den vänstra navigeringen. Fönstret **Välj resurs** visas med alternativ att ansluta till. Välj **[!DNL Blob container]** om du vill ansluta till [!DNL Data Landing Zone].

![Arbetsytan Välj resurs i Azure Explorer.](../../images/tutorials/create/dlz/select-resource.png)

Välj sedan **URL för delad åtkomstsignatur (SAS)** som anslutningsmetod och välj sedan **Nästa**.

![Den valda anslutningsmetoden i Azure Explorer, med signatur för delad åtkomst vald.](../../images/tutorials/create/dlz/select-connection-method.png)

När du har valt anslutningsmetod måste du sedan ange **visningsnamn** och **[!DNL Blob]behållar-SAS-URL:en** som motsvarar [!DNL Data Landing Zone]-behållaren.

>[!TIP]
>
>Du kan hämta dina [!DNL Data Landing Zone]-autentiseringsuppgifter från källkatalogen i plattformsgränssnittet.

Ange din [!DNL Data Landing Zone] SAS-URL och välj sedan **Nästa**

![Arbetsytan Ange anslutningsinformation i Azure Explorer där visningsnamnet och SAS-URL:en anges.](../../images/tutorials/create/dlz/enter-connection-info.png)

Fönstret **Sammanfattning** visas med en översikt över dina inställningar, inklusive information om din [!DNL Blob]-slutpunkt och behörigheter. Välj **Anslut** när du är klar.

![Sammanfattningsarbetsytan i Azure Explorer som fångar upp inställningarna för din resursanslutning.](../../images/tutorials/create/dlz/summary.png)

En anslutning uppdaterar användargränssnittet för [!DNL Azure Storage Explorer] med behållaren för [!DNL Data Landing Zone].

![Navigeringsarbetsytan för datalandningszon i Azure Explorer.](../../images/tutorials/create/dlz/dlz-user-container.png)

Med din [!DNL Data Landing Zone]-behållare ansluten till [!DNL Azure Storage Explorer] kan du nu börja överföra filer till [!DNL Data Landing Zone]-behållaren. Om du vill överföra väljer du **Överför** och sedan **Överför filer**.

![Arbetsytan för överföring av filer i Azure Explorer.](../../images/tutorials/create/dlz/upload.png)

När du har valt den fil som du vill överföra måste du sedan identifiera den [!DNL Blob]-typ som du vill överföra den som och den målkatalog som du vill använda. När du är klar väljer du **Överför**.

| [!DNL Blob] typer | Beskrivning |
| --- | --- |
| Blockera [!DNL Blob] | Blocket [!DNL Blobs] är optimerat för att överföra stora mängder data på ett effektivt sätt. Block [!DNL Blobs] är standardalternativet för [!DNL Data Landing Zone]. |
| Lägg till [!DNL Blob] | Tillägget [!DNL Blobs] är optimerat för att lägga till data i slutet av filen. |

![Fönstret för överföring av filer i Azure Explorer där de markerade filerna, blobtypen och målkategorin visas.](../../images/tutorials/create/dlz/upload-files.png)

### Överför filer till [!DNL Data Landing Zone] med kommandoradsgränssnittet

Du kan också använda kommandoradsgränssnittet för enheten och få åtkomst till överföringsfiler till [!DNL Data Landing Zone].

### Överföra en fil med Bash

I följande exempel används Bash och cURL för att överföra en fil till en [!DNL Data Landing Zone] med REST API:t [!DNL Azure Blob Storage]:

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### Överföra en fil med Python

I följande exempel används [!DNL Microsoft's] Python v12 SDK för att överföra en fil till en [!DNL Data Landing Zone]:

>[!TIP]
>
>I exemplet nedan används den fullständiga SAS-URI:n för att ansluta till en [!DNL Azure Blob]-behållare, men du kan använda andra metoder och åtgärder för att autentisera. Mer information finns i det här [[!DNL Microsoft] dokumentet om Python v12 SDK](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python).

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### Överför en fil med [!DNL AzCopy]

I följande exempel används verktyget [!DNL Microsoft's] [!DNL AzCopy] för att överföra en fil till en [!DNL Data Landing Zone]:

>[!TIP]
>
>I exemplet nedan används kommandot `copy`, men du kan använda andra kommandon och alternativ för att överföra en fil till [!DNL Data Landing Zone] med hjälp av [!DNL AzCopy]. Mer information finns i det här [[!DNL Microsoft AzCopy] dokumentet](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json).

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Konfigurera din [!DNL Data Landing Zone]-källa för Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller för implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Följ stegen nedan för att lära dig hur du kan konfigurera ditt [!DNL Data Landing Zone]-konto för Experience Platform på Amazon Web Services (AWS).

### Konfigurera AWS CLI och Utföra åtgärder

- Läs guiden [Installera eller uppdatera till den senaste versionen av AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

### Konfigurera AWS CLI med temporära autentiseringsuppgifter

Använd AWS `configure`-kommandot för att konfigurera CLI-programmet med åtkomstnycklar och en sessionstoken.

```shell
aws configure
```

Ange följande värden när du uppmanas att göra det:

- AWS-åtkomstnyckel-ID: `{YOUR_ACCESS_KEY_ID}`
- AWS hemliga åtkomstnyckel: `{YOUR_SECRET_ACCESS_KEY}`
- Standardregionens namn: `{YOUR_REGION}` (till exempel `us-west-2`)
- Standardutdataformat: `json`

Ange sedan sessionstoken:

```shell
aws configure set aws_session_token your-session-token
```

### Arbeta med filer på [!DNL Amazon S3]

>[!BEGINTABS]

>[!TAB Överför en fil till Amazon S3]

Mall:

```shell
aws s3 cp local-file-path s3://bucketName/dlzFolder/remote-file-Name
```

Exempel:

```shell
aws s3 cp example.txt s3://bucketName/dlzFolder/example.txt
```


>[!TAB Hämta en fil från Amazon S3]

Mall:

```shell
aws s3 cp s3://bucketName/dlzFolder/remote-file local-file-path
```

Exempel:

```shell
aws s3 cp s3://bucketName/dlzFolder/example.txt example.txt
```

>[!ENDTABS]

### Använd dina [!DNL Data Landing Zone]-inloggningsuppgifter för att logga in på AWS Console

#### Extrahera dina autentiseringsuppgifter

Först måste du få följande:

- `awsAccessKeyId`
- `awsSecretAccessKey`
- `awsSessionToken`

#### Generera en inloggningstoken

Använd sedan de extraherade inloggningsuppgifterna för att skapa en session och generera en inloggningstoken med AWS Federation-slutpunkten:

```py
import json
import requests
 
# Example DLZ response with credentials
response_json = '''{
    "credentials": {
        "awsAccessKeyId": "your-access-key",
        "awsSecretAccessKey": "your-secret-key",
        "awsSessionToken": "your-session-token"
    }
}'''
 
# Parse credentials
response_data = json.loads(response_json)
aws_access_key_id = response_data['credentials']['awsAccessKeyId']
aws_secret_access_key = response_data['credentials']['awsSecretAccessKey']
aws_session_token = response_data['credentials']['awsSessionToken']
 
# Create session dictionary
session = {
    'sessionId': aws_access_key_id,
    'sessionKey': aws_secret_access_key,
    'sessionToken': aws_session_token
}
 
# Generate the sign-in token
signin_token_url = "https://signin.aws.amazon.com/federation"
signin_token_payload = {
    "Action": "getSigninToken",
    "Session": json.dumps(session)
}
signin_token_response = requests.post(signin_token_url, data=signin_token_payload)
signin_token = signin_token_response.json()['SigninToken']
```

#### Skapa inloggnings-URL:en för AWS Console

När du har en inloggningstoken kan du skapa den URL som loggar dig i AWS Console och pekar direkt till önskad [!DNL Amazon S3]-bucket.

```py
from urllib.parse import quote
 
# Define the S3 bucket and folder path you want to access
bucket_name = "your-bucket-name"
bucket_path = "your-bucket-folder"
 
# Construct the destination URL
destination_url = f"https://s3.console.aws.amazon.com/s3/buckets/{bucket_name}?prefix={bucket_path}/&tab=objects"
 
# Create the final sign-in URL
signin_url = f"https://signin.aws.amazon.com/federation?Action=login&Issuer=YourAppName&Destination={quote(destination_url)}&SigninToken={signin_token}"
 
print(f"Sign-in URL: {signin_url}")
```

#### Åtkomst till AWS Console

Navigera slutligen till den genererade URL:en för att logga in direkt på AWS Console med dina [!DNL Data Landing Zone]-inloggningsuppgifter, som ger åtkomst till en viss mapp i en [!DNL Amazon S3]-bucket. Inloggnings-URL:en tar dig direkt till den mappen och ser till att du bara ser och hanterar tillåtna data.

## Anslut [!DNL Data Landing Zone] till Experience Platform

>[!IMPORTANT]
>
>- Om du vill ansluta till källan måste du ha åtkomstkontrollsbehörigheterna **[!UICONTROL View Sources]** och **[!UICONTROL Manage Sources]**. Mer information finns i [åtkomstkontrollsöversikten](../../../access-control/home.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>
>- Privata länkar stöds för närvarande inte vid anslutning till Experience Platform med [!DNL Data Landing Zone]. De enda metoder som stöds för åtkomst är de metoder som anges [här](#manage-the-contents-of-your-data-landing-zone).

Dokumentationen nedan innehåller information om hur du hämtar data från din [!DNL Data Landing Zone]-behållare till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.

### Använda API:er

- [Skapa en  [!DNL Data Landing Zone] källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Anslut [!DNL Data Landing Zone] till plattformen med användargränssnittet](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)

