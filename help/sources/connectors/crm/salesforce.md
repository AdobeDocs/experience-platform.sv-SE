---
title: Salesforce Source Connector - översikt
description: Lär dig hur du ansluter Salesforce till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: d8d9303e358c66c4cd891d6bf59a801c09a95f8e
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>Du kan nu använda källan [!DNL Salesforce] när du kör Adobe Experience Platform på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).

>[!WARNING]
>
>Grundläggande autentisering för källan [!DNL Salesforce] kommer att bli inaktuell i januari 2026. Du måste flytta till autentiseringen för OAuth 2-klientautentiseringsuppgifter för att kunna fortsätta använda källan och hämta data från ditt [!DNL Salesforce]-konto till Experience Platform.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från ett CRM-system från tredje part. Stöd för CRM-providers omfattar [!DNL Salesforce].

## Konfigurera din [!DNL Salesforce]-källa för Experience Platform på Azure {#azure}

Följ stegen nedan för att lära dig hur du kan konfigurera ditt [!DNL Salesforce]-konto för Experience Platform på Azure.

### IP-adressen tillåtelselista för anslutning till Azure

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform på Azure. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Läs sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md) om du vill ha mer information.

>[!BEGINTABS]

>[!TAB VA7]

- `40.70.226.96/28`
- `40.70.226.32/28`
- `52.232.229.255`
- `52.232.229.253`
- `40.70.226.144/28`
- `40.70.226.64/28`
- `40.70.225.240/28`
- `40.70.225.224/28`
- `40.70.224.64/29`
- `40.70.226.80/28`
- `40.70.226.176/28`
- `52.232.229.230`
- `40.70.226.128/28`
- `40.70.226.0/28`
- `40.70.226.16/28`
- `52.138.119.167`
- `40.70.226.160/28`
- `40.70.226.192/28`
- `40.70.226.48/28`
- `20.96.243.176`
- `40.70.226.112/28`
- `40.70.226.208/28`

>[!TAB NLD2]

- `40.74.4.144/28`
- `40.74.3.176/28`
- `40.74.5.128/28`
- `40.74.4.176/28`
- `40.74.6.112/28`
- `40.74.7.128/28`
- `40.74.6.144/28`
- `51.105.144.81`
- `52.142.236.87`
- `40.74.6.80/28`
- `20.101.246.9`
- `40.74.7.208/28`
- `40.74.6.128/28`
- `40.74.7.176/28`
- `51.124.70.4`
- `40.74.7.144/28`
- `108.141.12.47`
- `20.50.23.153`
- `51.144.184.248/29`
- `40.74.7.160/28`
- `40.74.7.192/28`
- `51.105.144.1`
- `40.74.4.160/28`
- `40.74.6.96/28`

>[!TAB AUS5]

- `20.43.111.32/28`
- `20.43.110.144/28`
- `20.53.111.113`
- `20.227.32.175`
- `20.43.110.96/28`
- `20.43.110.64/28`
- `20.193.56.144/28`
- `20.43.110.192/28`
- `20.43.97.95`
- `20.43.111.16/28`
- `20.43.110.128/28`
- `20.40.185.111`
- `20.193.56.160/28`
- `20.43.110.112/28`
- `40.82.220.111`
- `20.43.111.0/28`
- `20.193.38.208/28`
- `20.43.110.80/28`
- `20.43.110.176/28`
- `20.43.110.48/28`
- `20.193.36.37`
- `20.43.110.208/28`
- `20.43.110.224/28`
- `20.43.110.160/28`
- `20.40.185.225`
- `20.43.110.240/28`
- `20.193.56.128/28`
- `20.40.185.185`

>[!TAB CAN2]

- `20.116.159.48/28`
- `20.116.159.144/28`
- `20.116.159.96/28`
- `20.220.243.238`
- `20.116.159.80/28`
- `20.116.159.32/28`
- `20.151.241.138`
- `4.172.28.20`
- `20.151.241.124`
- `20.116.248.0/28`
- `20.116.155.128/28`
- `20.116.159.64/28`
- `20.116.159.192/28`
- `20.116.159.176/28`
- `20.116.175.240/28`
- `20.116.248.16/28`
- `20.116.158.240/28`
- `20.116.159.112/28`
- `20.151.240.247`
- `20.151.241.173`
- `20.116.159.128/28`
- `20.116.159.160/28`
- `20.116.159.0/28`
- `20.104.5.248`
- `20.116.175.224/28`
- `20.116.159.208/28`
- `20.116.159.224/28`

>[!TAB GBR9]

- `20.162.155.16/28`
- `20.162.154.96/28`
- `20.26.64.0/28`
- `20.26.64.96/28`
- `20.162.154.64/28`
- `20.108.200.27`
- `20.162.154.80/28`
- `20.162.153.192/28`
- `20.108.200.61`
- `20.162.154.48/28`
- `20.162.154.192/28`
- `20.162.154.0/28`
- `20.26.64.16/28`
- `20.162.154.112/28`
- `20.162.153.32/28`
- `20.254.80.141`
- `20.162.153.208/28`
- `20.108.203.20`
- `20.26.64.48/28`
- `20.162.154.240/28`
- `20.162.154.208/28`
- `20.162.154.160/28`
- `20.108.205.182`
- `20.108.202.198`
- `20.162.154.32/28`
- `20.162.153.16/28`

>[!TAB IND2]

- `4.188.92.84`
- `4.224.5.224/28`
- `4.224.7.32/28`
- `4.188.92.87`
- `4.188.89.92`
- `4.224.5.112/28`
- `4.224.6.80/28`
- `4.224.144.224/28`
- `4.224.144.240/28`
- `4.224.6.96/28`
- `4.188.89.255`
- `4.188.94.32/28`
- `4.224.5.96/28`
- `4.224.6.64/28`
- `4.224.7.48/28`
- `4.224.5.208/28`
- `4.188.90.65`
- `4.224.6.16/28`
- `4.224.6.0/28`
- `4.224.5.192/28`
- `4.224.7.16/28`
- `4.188.90.67`
- `4.188.90.17`
- `4.188.94.48/28`
- `4.224.6.112/28`
- `4.224.5.240/28`
- `4.224.7.0/28`

>[!ENDTABS]

### Fältmappning från [!DNL Salesforce] till XDM

Om du vill upprätta en källanslutning mellan [!DNL Salesforce] och Experience Platform måste [!DNL Salesforce] källdatafälten mappas till rätt mål-XDM-fält innan de hämtas till Experience Platform.

Mer information om fältmappningsregler mellan [!DNL Salesforce]-datamängder och Experience Platform finns i följande:

- [Kontakter](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Konton](../adobe-applications/mapping/salesforce.md#account)
- [Möjligheter](../adobe-applications/mapping/salesforce.md#opportunity)
- [Kontaktroller för affärsmöjlighet](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Kampanjer](../adobe-applications/mapping/salesforce.md#campaign)
- [Kampanjmedlemmar](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Kontaktrelation för konto](../adobe-applications/mapping/salesforce.md#account-contact-relation)

### Konfigurera det automatiska genereringsverktyget för namnutrymmet [!DNL Salesforce] och schemat

Om du vill använda källan [!DNL Salesforce] som en del av [!DNL B2B-CDP] måste du först konfigurera ett [!DNL Postman]-verktyg för att automatiskt generera [!DNL Salesforce] namnutrymmen och scheman. Följande dokumentation innehåller ytterligare information om hur du konfigurerar verktyget [!DNL Postman]:

- Du kan hämta samlingen och miljön för automatisk generering av namnområde och scheman från den här [GitHub-databasen](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Information om hur du använder Experience Platform API:er, inklusive information om hur du samlar in värden för obligatoriska huvuden och läser API-anrop från exempel, finns i guiden [Komma igång med Experience Platform API:er](../../../landing/api-guide.md).
- Mer information om hur du genererar autentiseringsuppgifter för Experience Platform API:er finns i självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md).
- Information om hur du konfigurerar [!DNL Postman] för Experience Platform API:er finns i självstudiekursen [Konfigurera utvecklarkonsol och [!DNL Postman]](../../../landing/postman.md).

Med en Experience Platform-utvecklarkonsol och [!DNL Postman] konfigurerad kan du nu börja använda lämpliga miljövärden i din [!DNL Postman] -miljö.

+++Visa den variabla tabellstödlinjen

Följande tabell innehåller exempelvärden samt ytterligare information om hur du fyller i din [!DNL Postman]-miljö:

| Variabel | Beskrivning | Exempel |
| --- | --- | --- |
| `CLIENT_SECRET` | En unik identifierare som används för att generera `{ACCESS_TOKEN}`. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) är en autentiseringsuppgift som används för att generera {ACCESS_TOKEN}. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du genererar `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | En unik identifierare som används för att autentisera anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Med avseende på [!DNL Marketo] är det här värdet fast och alltid inställt på: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Behållaren `global` innehåller alla standardklasser som tillhandahålls av Adobe- och Experience Platform-partners, schemafältgrupper, datatyper och scheman. Med avseende på [!DNL Marketo] är det här värdet fast och ställs alltid in på `global`. | `global` |
| `PRIVATE_KEY` | En autentiseringsuppgift som används för att autentisera din [!DNL Postman]-instans till Experience Platform API:er. Se självstudiekursen om hur du konfigurerar utvecklarkonsolen och [konfigurerar utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | En autentiseringsuppgift som används för att integrera med Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) utgör ramverket för autentisering till Adobes tjänster. Med avseende på [!DNL Marketo] är det här värdet fast och alltid inställt på: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen [Konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din `{ORG_ID}`-information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Namnet på den virtuella sandlådepartition som du använder. | `prod` |
| `TENANT_ID` | Ett ID som används för att se till att de resurser du skapar namnges korrekt och finns i din organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | URL-slutpunkten som du gör API-anrop till. Det här värdet är fast och är alltid inställt på: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | Unikt ID för ditt [!DNL Marketo]-konto. I självstudiekursen om [autentisering av din [!DNL Marketo] instans](../adobe-applications/marketo/marketo-auth.md) finns mer information om hur du hämtar din `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | Organisations-ID för ditt [!DNL Salesforce]-konto. Se följande [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&type=1&mode=1) för mer information om hur du skaffar ditt [!DNL Salesforce] organisations-ID. | `00D4W000000FgYJUA0` |
| `has_abm` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

+++

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
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).

Följ stegen nedan för att lära dig hur du kan konfigurera ditt [!DNL Salesforce]-konto för Experience Platform på Amazon Web Services (AWS).

### Förhandskrav

Om du vill ansluta ditt [!DNL Salesforce]-konto till Experience Platform i en AWS-region måste du ha följande:

- Ett [!DNL Salesforce]-konto med API-åtkomst.
- A [!DNL Salesforce Connected App] som du sedan kan använda för att aktivera JWT_BEARER OAuth-flöde.
- Nödvändiga behörigheter i [!DNL Salesforce] för att komma åt data.

### IP-adressen tillåtelselista för anslutning till AWS

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform på AWS. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform på AWS](../../ip-address-allow-list.md).

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
7. Överför filen cert.pem som skapades tidigare.

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

### Anslut [!DNL Salesforce] till Experience Platform med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce] till Experience Platform med API:er eller användargränssnittet:

- [Anslut Salesforce till Experience Platform med API:t för Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)

### Anslut [!DNL Salesforce] till Experience Platform med användargränssnittet

- [Skapa en Salesforce-källanslutning i användargränssnittet](../../tutorials/ui/create/crm/salesforce.md)
- [Skapa ett dataflöde för en CRM-anslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)