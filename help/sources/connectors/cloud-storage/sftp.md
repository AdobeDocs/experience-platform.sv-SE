---
keywords: Experience Platform;hem;populära ämnen;SFTP;sftp
solution: Experience Platform
title: SFTP Source Connector - översikt
description: Lär dig hur du ansluter en SFTP-server till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: 52c1c8e6bc332bd6ee579cad52a7343007615efd
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# SFTP-anslutning

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Läs det här dokumentet om du behöver utföra nödvändiga steg för att kunna ansluta ditt [!DNL SFTP]-konto till Experience Platform.

>[!TIP]
>
>Du måste inaktivera interaktiv tangentbordsautentisering i SFTP-serverkonfigurationen innan du ansluter. Om du inaktiverar inställningen kan du ange lösenord manuellt, i stället för att skriva in dem via en tjänst eller ett program.

## Förhandskrav {#prerequisites}

I det här avsnittet finns information om nödvändiga steg som du måste slutföra för att kunna ansluta [!DNL SFTP]-källan till Experience Platform.

### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

### Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

* Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
* Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
* Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
* Följande tecken tillåts inte: `" \ / : | < > * ?`.
* Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

### Konfigurera en Base64-kodad privat OpenSSH-nyckel för [!DNL SFTP]

Källan [!DNL SFTP] stöder autentisering med [!DNL Base64]-kodad privat nyckel för OpenSSH. Se stegen nedan för mer information om hur du skapar den Base64-kodade privata OpenSSH-nyckeln och ansluter [!DNL SFTP] till plattformen.

>[!BEGINTABS]

>[!TAB Windows]

### [!DNL Windows] användare

Om du använder en [!DNL Windows]-dator öppnar du menyn **Start** och väljer sedan **Inställningar** .

![inställningar](../../images/tutorials/create/sftp/settings.png)

Välj **Appar** på menyn **Inställningar** som visas.

![appar](../../images/tutorials/create/sftp/apps.png)

Välj sedan **Valfria funktioner**.

![valfria funktioner](../../images/tutorials/create/sftp/optional-features.png)

En lista över valfria funktioner visas. Om **OpenSSH-klienten** redan är förinstallerad på datorn inkluderas den i listan **Installerade funktioner** under **Valfria funktioner**.

![open-ssh](../../images/tutorials/create/sftp/open-ssh.png)

Om den inte är installerad väljer du **Installera**, öppnar **[!DNL Powershell]** och kör följande kommando för att generera din privata nyckel:

```shell
PS C:\Users\lucy> ssh-keygen -t rsa -m pem
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\lucy/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\lucy/.ssh/id_rsa.
Your public key has been saved in C:\Users\lucy/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:osJ6Lg0TqK8nekNQyZGMoYwfyxNc+Wh0hYBtBylXuGk lucy@LAPTOP-FUJT1JEC
The key's randomart image is:
+---[RSA 3072]----+
|.=.*+B.o.        |
|=.O.O +          |
|+o+= B           |
|+o +E .          |
|.o=o  . S        |
|+... . .         |
| *o .            |
|o.B.             |
|=O..             |
+----[SHA256]-----+
```

Kör sedan följande kommando när du anger sökvägen till den privata nyckeln för att koda den privata nyckeln i [!DNL Base64]:

```shell
C:\Users\lucy> [convert]::ToBase64String((Get-Content -path "C:\Users\lucy\.ssh\id_rsa" -Encoding byte)) > C:\Users\lucy\.ssh\id_rsa_base64
```

Ovanstående kommando sparar den [!DNL Base64]-kodade privata nyckeln i den sökväg du angav. Du kan sedan använda den privata nyckeln för att autentisera till [!DNL SFTP] och ansluta till plattformen.

>[!TAB Mac]

### [!DNL Mac] användare

Om du använder en [!DNL Mac] öppnar du **Terminal** och kör följande kommando för att generera den privata nyckeln (i det här fallet sparas den privata nyckeln i `/Documents/id_rsa`):

```shell
ssh-keygen -t rsa -m pem -f ~/Documents/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/vrana/Documents/id_rsa.
Your public key has been saved in /Users/vrana/Documents/id_rsa.pub.
The key fingerprint is:
SHA256:s49PCaO4a0Ee8I7OOeSyhQAGc+pSUQnRii9+5S7pp1M vrana@vrana-macOS
The key's randomart image is:
+---[RSA 2048]----+
|o ==..           |
|.+..o            |
|oo.+             |
|=.. +            |
|oo = .  S        |
|+.+ +E . = .     |
|o*..*.. . o      |
|.o*=.+   +       |
|.oo=Oo  ..o      |
+----[SHA256]-----+
```

Kör sedan följande kommando för att koda den privata nyckeln i [!DNL Base64]:

```shell
base64 ~/Documents/id_rsa > ~/Documents/id_rsa_base64
 
 
# Print Content of base64 encoded file
cat ~/Documents/id_rsa_base64
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUJGd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFRRUF0cWFYczlXOUF1ZmtWazUwSXpwNXNLTDlOMU9VYklaYXVxbVM0Q0ZaenI1NjNxUGFuN244CmFxZWdvQTlCZnVnWDJsTVpGSFl5elEzbnp6NXdXMkdZa1hkdjFjakd0elVyNyt1NnBUeWRneGxrOGRXZWZsSzBpUlpYWW4KVFRwS0E5c2xXaHhjTXg3R2x5ejdGeDhWSzI3MmdNSzNqY1d1Q0VIU3lLSFR5SFFwekw0MEVKbGZJY1RGR1h1dW1LQjI5SwpEakhwT1grSDdGcG5Gd1pabTA4Uzc2UHJveTVaMndFalcyd1lYcTlyUDFhL0E4ejFoM1ZLdllzcG53c2tCcHFQSkQ1V3haCjczZ3M2OG9sVllIdnhWajNjS3ZsRlFqQlVFNWRNUnB2M0I5QWZ0SWlrYmNJeUNDaXV3UnJmbHk5eVNPQ2VlSEc0Z2tUcGwKL3V4YXNOT0h1d0FBQThqNnF6R1YrcXN4bFFBQUFBZHpjMmd0Y25OaEFBQUJBUUMycHBlejFiMEM1K1JXVG5Rak9ubXdvdgowM1U1UnNobHE2cVpMZ0lWbk92bnJlbzlxZnVmeHFwNkNnRDBGKzZCZmFVeGtVZGpMTkRlZlBQbkJiWVppUmQyL1Z5TWEzCk5TdnY2N3FsUEoyREdXVHgxWjUrVXJTSkZsZGlkTk9rb0QyeVZhSEZ3ekhzYVhMUHNYSHhVcmJ2YUF3cmVOeGE0SVFkTEkKb2RQSWRDbk12alFRbVY4aHhNVVplNjZZb0hiMG9PTWVrNWY0ZnNXbWNYQmxtYlR4THZvK3VqTGxuYkFTTmJiQmhlcjJzLwpWcjhEelBXSGRVcTlpeW1mQ3lRR21vOGtQbGJGbnZlQ3pyeWlWVmdlL0ZXUGR3cStVVkNNRlFUbDB4R20vY0gwQiswaUtSCnR3aklJS0s3Qkd0K1hMM0pJNEo1NGNiaUNST21YKzdGcXcwNGU3QUFBQUF3RUFBUUFBQVFBcGs0WllzMENSRnNRTk9WS0sKYWxjazlCVDdzUlRLRjFNenhrSGVydmpJYk9kL0lvRXpkcHlVa28rbm41RmpGK1hHRnNCUXZnOFdTaUlJTk1oU3BNYWI1agpvWXlka2gvd0ovWElOaDlZaE5QVXlURi9NNkFnMkNYd21KS2RxN1VKWjZyNjloV3V0VVN6U05QbkVYWTZLc29GeVUwTEFvCko0OHJMT1pMZldtMHFhWDBLNUgzNmJPaHFXSWJwMDNoZk94eno5M0MrSDM5MFJkRkp4bzJVZ0FVY3UvdHREb0REVldBdmEKVkVyMWEzak9LenVHbThrK21WeXpPZERjVFY4ckZIT0pwRnRBU3l6Q24yVld1MjV0TWtrcGRPRjNKcVdMZHdOY3loeG1URApXZGVDNWh4V0Fiano0WDZ5WXpHcFcwTmptVkFoWUVVZGNBSVlXWWM3OGEvQkFBQUFnRm8wakl4aGhwZkJ6QjF6b09FMDJBClpjTC9hcUNuYysrdmJ1a2V0aFg5Zzhlb0xQMTQyeUgzdlpLczl3c1RtbVVsZ0prZURaN2hUcklwOGY2eEwzdDRlMXByY1kKb2ZLd0gwckNGOTFyaldPbGZOUmxEempoR1NTTEVMczZoNlNzMEdBQXE2Z0ZQTVF2dTB4TDlQUTlGQ21YZVVKazJpRm1MWgpEWWJGc0NyVUxEQUFBQWdRRGF0a1pMamJaSTBFM0ZuY2dTOVF5Y3lVWmtkZ1dVNjBQcG9ud3BMQXdUdHRpOG1EQXE5cHYwClEvUlk1WE9UeGF3VXNHa0tYMjNtV1BYR0grdUlBSzhrelVVM2dGM1dRWGVkTWw4NHVCVFZCTEtUdStvVVAvZmIvMEE0dE0KSE9BSythbXZPMkZuYzFiSmVwd05USTE2cjZXWk9sZWV2ZklJQVpXcEgxVVpIdkVRQUFBSUVBMWNwcStDNUVXSFJwbnVPZQpiNHE4T0tKTlJhSUxIRUN6U0twWlFpZDFhRmJYWlVKUXpIQU85YzhINVZMcjBNUjFkcW1ORkNja2ZsZzI2Y3BEUEl3TjBYCm5HMFBxcmhKbXp0U3ZQZ3NGdkNPallncXF6U0RYUjkxd1JQTEN5cU8zcGMyM2kzZnp2WkhtMGhIdWdoNVJqV0loUlFZVkwKZUpDWHRqM08vY3p1SWdzQUFBQVJkbkpoYm1GQWRuSmhibUV0YldGalQxTUJBZz09Ci0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

När den [!DNL Base64]-kodade privata nyckeln har sparats i den mapp du angav, måste du lägga till innehållet i filen med den offentliga nyckeln på en ny rad i de [!DNL SFTP] värdauktoriserade nycklarna. Kör följande kommando på kommandoraden:

```shell
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

Du kan kontrollera om den offentliga nyckeln har lagts till korrekt genom att köra följande på kommandoraden:

```shell
more ~/.ssh/authorized_keys
```

>[!ENDTABS]

### Samla in nödvändiga inloggningsuppgifter {#credentials}

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta [!DNL SFTP]-servern till Experience Platform.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Ange lämpliga värden för följande autentiseringsuppgifter för att autentisera [!DNL SFTP]-servern med grundläggande autentisering.

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är associerad med [!DNL SFTP]-servern. |
| `port` | Serverporten [!DNL SFTP] som du ansluter till. Om det inte anges används standardvärdet `22`. |
| `username` | Användarnamnet med åtkomst till din [!DNL SFTP]-server. |
| `password` | Lösenordet för din [!DNL SFTP]-server. |
| `maxConcurrentConnections` | Med den här parametern kan du ange en maxgräns för hur många samtidiga anslutningar som plattformen skapar vid anslutning till SFTP-servern. Du måste ange att det här värdet ska vara mindre än gränsen som anges av SFTP. **Obs!** När den här inställningen är aktiverad för ett befintligt SFTP-konto påverkas bara framtida dataflöden och inte befintliga dataflöden. |
| `folderPath` | Sökvägen till mappen som du vill ge åtkomst till. [!DNL SFTP]-källan kan du ange mappsökvägen för att ange användaråtkomst till den undermapp som du väljer. |
| `disableChunking` | Under datainmatningen kan källan [!DNL SFTP] hämta fillängden först, dela upp filen i flera delar och sedan läsa dem parallellt. Du kan aktivera eller inaktivera det här värdet för att ange om [!DNL SFTP]-servern kan hämta fillängder eller läsa data från en viss förskjutning. |
| `connectionSpec.id` | (Endast API) Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer som relaterar till att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL SFTP] är: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

>[!TAB SSH-autentisering med offentlig nyckel]

Ange lämpliga värden för följande autentiseringsuppgifter för att autentisera [!DNL SFTP]-servern med autentisering med offentlig nyckel för SSH.

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är associerad med [!DNL SFTP]-servern. |
| `port` | Serverporten [!DNL SFTP] som du ansluter till. Om det inte anges används standardvärdet `22`. |
| `username` | Användarnamnet med åtkomst till din [!DNL SFTP]-server. |
| `password` | Lösenordet för din [!DNL SFTP]-server. |
| `privateKeyContent` | Base64-kodat innehåll för privat SSH-nyckel. Typen av OpenSSH-nyckel måste klassificeras som antingen RSA eller DSA. |
| `passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |
| `maxConcurrentConnections` | Med den här parametern kan du ange en maxgräns för hur många samtidiga anslutningar som plattformen skapar vid anslutning till SFTP-servern. Du måste ange att det här värdet ska vara mindre än gränsen som anges av SFTP. **Obs!** När den här inställningen är aktiverad för ett befintligt SFTP-konto påverkas bara framtida dataflöden och inte befintliga dataflöden. |
| `folderPath` | Sökvägen till mappen som du vill ge åtkomst till. [!DNL SFTP]-källan kan du ange mappsökvägen för att ange användaråtkomst till den undermapp som du väljer. |
| `disableChunking` | Under datainmatningen kan källan [!DNL SFTP] hämta fillängden först, dela upp filen i flera delar och sedan läsa dem parallellt. Du kan aktivera eller inaktivera det här värdet för att ange om [!DNL SFTP]-servern kan hämta fillängder eller läsa data från en viss förskjutning. |
| `connectionSpec.id` | (Endast API) Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer som relaterar till att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL SFTP] är: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

>[!ENDTABS]

## Anslut SFTP till Experience Platform

Dokumentationen nedan innehåller information om hur du ansluter en SFTP-server till Experience Platform med hjälp av API:er eller användargränssnittet:

### Använda API:er

* [Skapa en SFTP-basanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/sftp.md)
* [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
* [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

* [Skapa en SFTP-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/sftp.md)
* [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
