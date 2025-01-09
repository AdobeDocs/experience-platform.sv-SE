---
title: Salesforce Source Connector - översikt
description: Lär dig hur du ansluter Salesforce till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: ee659ded9701132b12d5b93672b4c958e9720028
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 0%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>Du kan nu använda källan [!DNL Salesforce] när du kör Adobe Experience Platform på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](../../../landing/multi-cloud.md).


Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från ett CRM-system från tredje part. Stöd för CRM-providers omfattar [!DNL Salesforce].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Fältmappning från [!DNL Salesforce] till XDM

Om du vill upprätta en källanslutning mellan [!DNL Salesforce] och plattformen måste [!DNL Salesforce]-källdatafälten mappas till rätt mål-XDM-fält innan de hämtas till plattformen.

Mer information om fältmappningsregler mellan [!DNL Salesforce]-datamängder och plattformen finns i följande:

- [Kontakter](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Konton](../adobe-applications/mapping/salesforce.md#account)
- [Möjligheter](../adobe-applications/mapping/salesforce.md#opportunity)
- [Kontaktroller för affärsmöjlighet](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Kampanjer](../adobe-applications/mapping/salesforce.md#campaign)
- [Kampanjmedlemmar](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Kontaktrelation för konto](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Konfigurera det automatiska genereringsverktyget för namnutrymmet [!DNL Salesforce] och schemat

Om du vill använda källan [!DNL Salesforce] som en del av [!DNL B2B-CDP] måste du först konfigurera ett [!DNL Postman]-verktyg för att automatiskt generera [!DNL Salesforce] namnutrymmen och scheman. Följande dokumentation innehåller ytterligare information om hur du konfigurerar verktyget [!DNL Postman]:

- Du kan hämta samlingen och miljön för automatisk generering av namnområde och scheman från den här [GitHub-databasen](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Information om hur du använder plattforms-API:er, inklusive information om hur du samlar in värden för obligatoriska huvuden och läser exempel-API-anrop, finns i guiden [Komma igång med plattforms-API:er](../../../landing/api-guide.md).
- Mer information om hur du genererar autentiseringsuppgifter för plattforms-API:er finns i självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md).
- Information om hur du konfigurerar [!DNL Postman] för plattforms-API:er finns i självstudiekursen [Konfigurera utvecklarkonsol och [!DNL Postman]](../../../landing/postman.md).

Med en plattformsutvecklarkonsol och [!DNL Postman] konfigurerad kan du nu börja använda lämpliga miljövärden i din [!DNL Postman] -miljö.

Följande tabell innehåller exempelvärden samt ytterligare information om hur du fyller i din [!DNL Postman]-miljö:

| Variabel | Beskrivning | Exempel |
| --- | --- | --- |
| `CLIENT_SECRET` | En unik identifierare som används för att generera `{ACCESS_TOKEN}`. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) är en autentiseringsuppgift som används för att generera {ACCESS_TOKEN}. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du genererar `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | En unik identifierare som används för att autentisera anrop till API:er för Experience Platform. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Med avseende på [!DNL Marketo] är det här värdet fast och alltid inställt på: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Behållaren `global` innehåller alla klasser, schemafältgrupper, datatyper och scheman som tillhandahålls av Adobe och Experience Platform-partner. Med avseende på [!DNL Marketo] är det här värdet fast och ställs alltid in på `global`. | `global` |
| `PRIVATE_KEY` | En autentiseringsuppgift som används för att autentisera din [!DNL Postman]-instans till API:er för Experience Platform. Se självstudiekursen om hur du konfigurerar utvecklarkonsolen och [konfigurerar utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | En autentiseringsuppgift som används för att integrera med Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) utgör ramverket för autentisering till Adobes tjänster. Med avseende på [!DNL Marketo] är det här värdet fast och alltid inställt på: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen [Konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din `{ORG_ID}`-information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Namnet på den virtuella sandlådepartition som du använder. | `prod` |
| `TENANT_ID` | Ett ID som används för att se till att de resurser du skapar namnges korrekt och finns i din organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | URL-slutpunkten som du gör API-anrop till. Det här värdet är fast och är alltid inställt på: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | Unikt ID för ditt [!DNL Marketo]-konto. I självstudiekursen om [autentisering av din [!DNL Marketo] instans](../adobe-applications/marketo/marketo-auth.md) finns mer information om hur du hämtar din `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | Organisations-ID för ditt [!DNL Salesforce]-konto. Se följande [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) för mer information om hur du skaffar ditt [!DNL Salesforce] organisations-ID. | `00D4W000000FgYJUA0` |
| `has_abm` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Kör skripten

När din [!DNL Postman]-samling och miljö är konfigurerad kan du nu köra skriptet via gränssnittet [!DNL Postman].

I gränssnittet [!DNL Postman] väljer du rotmappen för verktyget för autogenerering och sedan **[!DNL Run]** i den övre rubriken.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

Gränssnittet [!DNL Runner] visas. Se till att alla kryssrutor är markerade och välj sedan **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

En lyckad begäran skapar B2B-namnutrymmen och scheman enligt betaspecifikationerna.

## Konfigurera din [!DNL Salesforce]-källa för Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller för implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](../../../landing/multi-cloud.md).

Följ stegen nedan för att lära dig hur du kan konfigurera ditt [!DNL Salesforce]-konto för Experience Platform på Amazon Web Services (AWS).

### Förhandskrav

Om du vill ansluta ditt [!DNL Salesforce]-konto till Experience Platform i en AWS-region måste du ha följande:

- Ett [!DNL Salesforce]-konto med API-åtkomst.
- A [!DNL Salesforce Connected App] som du sedan kan använda för att aktivera JWT_BEARER OAuth-flöde.
- Nödvändiga behörigheter i [!DNL Salesforce] för att komma åt data.

Du måste också lägga till följande IP-adresser i tillåtelselista för att kunna ansluta ditt [!DNL Salesforce]-konto till Experience Platform på Amazon Web Services (AWS):

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

### Skapa en [!DNL Salesforce Connected App]

Använd först följande för att skapa PEM-filer med certifikat/nyckelpar.

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. Välj inställningar (![Inställningsikonen på kontrollpanelen [!DNL Salesforce].](/help/images/icons/settings.png)) och välj sedan **[!DNL Setup]**.
2. Navigera till [!DNL App Manager] och välj sedan **[!DNL New Connection App]**.
3. Ange ett namn för appen och låt resten av fälten fyllas i automatiskt.
4. Aktivera rutan för [!DNL Enable OAuth Settings].
5. Ange en återanrops-URL. Eftersom detta inte kommer att användas för JWT kan du använda `https://localhost`.
6. Aktivera rutan för [!DNL Use Digital Signatures].
7. Överför filen cert.perm som skapades tidigare.

#### Lägg till nödvändiga behörigheter

Lägg till följande behörigheter:

1. Hantera användardata via API:er (api)
2. Åtkomst till anpassade behörigheter (custom_permissions)
3. Öppna URL-tjänsten för identitet (id, profil, e-post, adress, telefon)
4. Åtkomst till unika identifierare (openID)
5. Utför begäranden när som helst (refresh_token, offline_access)

När du har lagt till dina behörigheter måste du aktivera rutan för **[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]**.

Välj sedan **[!DNL Save]**, **[!DNL Continue]** och sedan **[!DNL Manage Customer Details]**. Använd panelen med konsumentinformation för att hämta följande:

- **Konsumentnyckel**: Du kommer senare att använda den här konsumentnyckeln som ditt klient-ID när du autentiserar ditt [!DNL Salesforce]-konto för Experience Platform.
- **Konsumenthemlighet**: Du kommer senare att använda den här konsumenthemligheten som ditt klient-ID när du autentiserar ditt [!DNL Salesforce]-konto för Experience Platform.

### Auktorisera din [!DNL Salesforce]-användare till den anslutna appen

Följ stegen nedan för att få behörighet att använda den anslutna appen:

1. Navigera till **[!DNL Manage Connected Apps]**.
2. Välj **[!DNL Edit]**.
3. Konfigurera **[!DNL Permitted Users]** som **[!DNL Admin approved users are pre-authorized]** och välj sedan **[!DNL Save]**.
4. Navigera till **[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]**.
5. Redigera den profil som är kopplad till användaren.
6. Navigera till **[!DNL Connected App Access]** och markera sedan appen som du skapade i ett tidigare steg.

### Generera JWT Bearer-token

Följ stegen nedan för att generera din JWT Bearer-token.

#### Konvertera nyckelpar till pkcs12

Om du vill generera en JWT Bärartoken måste du först använda följande kommando för att konvertera ditt certifikat/nyckelpar till pkcs12-format. Under det här steget måste du även **ange ett exportlösenord** när du uppmanas till det.

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### Skapa java-nyckelbehållare baserat på pkcs12

Använd sedan följande kommando för att skapa en java-nyckelbehållare baserad på de pkcs12 som du just genererade. Under det här steget måste du även ange ett **lösenord för målnyckelbehållare** när du uppmanas till det. Dessutom måste du ange det tidigare exportlösenordet som källnyckelbehållarlösenord.

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### Bekräfta att ditt keystroke.jks innehåller ett jwtcert-alias

Använd sedan följande kommando för att bekräfta att `keystroke.jks` innehåller ett `jwtcert`-alias. Under det här steget uppmanas du att ange lösenordet för målnyckelbehållaren som skapades i det föregående steget.

```shell
keytool -keystore keystore.jks -list
```

#### Generera signerad token

Använd slutligen Java-klassens JWTExample nedan för att generera din signerade token.

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| Egenskap | Konfigurationer |
| --- | --- |
| `claimArray[0]` | Uppdatera `claimArray[0]` med ditt klient-ID. |
| `claimArray[1]` | Uppdatera `claimArray[1]` med användarnamnet [!DNL Salesforce] som är auktoriserat för appen. |
| `claimArray[2]` | Uppdatera `claimArray[2]` med din [!DNL Salesforce]-inloggnings-URL. |
| `claimArray[3]` | Uppdatera `claimArray[3]` med ett förfallodatum som är formaterat i millisekunder sedan epoktiden. `3660624000000` är till exempel 12-31-2085. |
| `/path/to/keystore` | Ersätt `/path/to/keystore` med rätt sökväg till din keystore.jks |
| `keystorepassword` | Ersätt `keystorepassword` med lösenordet för målnyckelbehållaren. |
| `privatekeypassword` | Ersätt `privatekeypassword` med ditt källnyckellösenord. |

## Nästa steg

När du har slutfört kravkonfigurationen för ditt [!DNL Salesforce]-konto kan du fortsätta att ansluta ditt [!DNL Salesforce]-konto till Experience Platform och importera dina CRM-data. Läs dokumentationen nedan för mer information:

### Anslut [!DNL Salesforce] till plattformen med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce] till plattformen med API:er eller användargränssnittet:

- [Skapa en Salesforce-basanslutning med API:t för Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)

### Anslut [!DNL Salesforce] till plattformen med användargränssnittet

- [Skapa en Salesforce-källanslutning i användargränssnittet](../../tutorials/ui/create/crm/salesforce.md)
- [Skapa ett dataflöde för en CRM-anslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)