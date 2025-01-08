---
title: Så här använder du Amazon Web Services nyckelhanteringstjänst för Adobe Experience Platform datakryptering
description: Lär dig hur du använder Amazon Web Services nyckelhanteringstjänst för att konfigurera dina krypteringsnycklar för data som lagras i Adobe Experience Platform.
role: Developer, Admin, User
hide: true
hidefromtoc: true
source-git-commit: 7c37ce72eecbcbc9e49aa4135a21ef4649d9bfa5
workflow-type: tm+mt
source-wordcount: '2623'
ht-degree: 0%

---

# Så här använder du Amazon Web Services nyckelhanteringstjänst för Adobe Experience Platform-datakryptering

>[!AVAILABILITY]
>
>Detta dokument gäller för implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>[Kundhanterade nycklar](../customer-managed-keys/overview.md) (CMK) på AWS stöds för sköld för skydd av privatlivet och säkerheten, men är inte tillgängliga för hälso- och sjukvårdsskölden. CMK på Azure stöds både för Privacy och Security Shield samt för Healthcare Shield.

Använd den här guiden för att skydda dina data med Amazon Web Services (AWS) Key Management Service (KMS) genom att skapa, hantera och styra krypteringsnycklar för Adobe Experience Platform. Integrationen förenklar regelefterlevnaden, effektiviserar verksamheten genom automatisering och eliminerar behovet av att underhålla en egen nyckelhanteringsinfrastruktur.

Instruktioner för Customer Journey Analytics finns i [Customer Journey Analytics CMK-dokumentationen](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-privacy/cmk)

>[!IMPORTANT]
>
>Adobe Experience Platform krypterar vilande data som standard med systemhanterade nycklar. Genom att aktivera CMK (Customer Managed Keys) får du full kontroll över datasäkerheten. Den här ändringen går dock inte att ångra, men när CMK har aktiverats går det inte att återställa till systemhanterade nycklar. Du ansvarar för att hantera dina nycklar på ett säkert sätt för att säkerställa oavbruten åtkomst till dina data och förhindra eventuell otillgänglighet.

Den här guiden beskriver processen att skapa och hantera krypteringsnycklar i AWS KMS för att skydda data i Experience Platform.

## Förhandskrav {#prerequisites}

Innan du fortsätter med det här dokumentet bör du ha god förståelse för följande viktiga begrepp och funktioner:

- **AWS nyckelhanteringstjänst (KMS)**: Förstå grunderna i AWS KMS, inklusive hur du skapar, hanterar och roterar krypteringsnycklar. Mer information finns i den [officiella KMS-dokumentationen](https://docs.aws.amazon.com/kms/).
- **IAM-principer (Identity and Access Management) i AWS**: IAM är en tjänst som gör att du kan hantera åtkomst till AWS tjänster och resurser på ett säkert sätt. Använd IAM för att:
   - Definiera vilka användare, grupper och roller som har åtkomst till specifika resurser.
   - Ange vilka åtgärder som användare tillåts eller nekas att utföra.
   - Implementera detaljerad åtkomstkontroll genom att tilldela behörigheter med IAM-principer.
Mer information finns i [IAM-reglerna för den officiella dokumentationen för AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- **Datasäkerhet i Experience Platform**: Upptäck hur Platform säkerställer datasäkerhet och integrerar med externa tjänster som AWS KMS för kryptering. Plattformen skyddar data med HTTPS TLS v1.2 för överföring, molnkryptering i vila, isolerad lagring samt anpassningsbara autentiserings- och krypteringsalternativ. Mer information om hur dina data skyddas finns i [styrnings-, sekretess- och säkerhetsöversikten](../overview.md) eller i dokumentet om [datakryptering i plattformen](../encryption.md).
- **AWS Management Console**: Ett centralt nav där du kan komma åt och hantera alla dina AWS-tjänster från ett webbaserat program. Använd sökfältet för att snabbt hitta verktyg, kontrollera meddelanden, hantera ditt konto och din fakturering samt anpassa inställningarna. Mer information finns i den [officiella dokumentationen för AWS-hanteringskonsolen](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html).

## Kom igång {#get-started}

Den här guiden kräver att du redan har tillgång till ett Amazon Web Services-konto och åtkomst till hanteringskonsolen. Följ stegen nedan för att komma igång:

1. **Verifiera behörigheter**: Kontrollera att du har de AWS Identity and Access Management-behörigheter (IAM) som krävs för att skapa, hantera och använda krypteringsnycklar i KMS. Så här verifierar du dina behörigheter:
   1. Gå till [IAM-principsimulatorn](https://policysim.aws.amazon.com/).
   1. Välj ditt användarkonto eller din roll.
   1. Simulera KMS-åtgärder som `kms:CreateKey` eller `kms:Encrypt`.
Om simuleringen returnerar ett fel, eller om du är osäker på din behörighet, kan du kontakta AWS-administratören för att få hjälp.

1. **Kontrollera din AWS-kontokonfiguration**: Bekräfta att ditt AWS-konto är aktiverat för att använda AWS KMS-tjänster. KMS-åtkomst är aktiverat som standard för de flesta konton, men du kan granska kontoinställningarna genom att gå till [AWS Management Console](https://aws.amazon.com/console/). Mer information finns i [Utvecklarhandboken för AWS Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html).

1. **Välj en region som stöds**: AWS KMS är tillgängligt i vissa regioner. Kontrollera att du arbetar i en region där KMS stöds. Du kan visa en fullständig lista över regioner som stöds i [AWS KMS-slutpunkts- och kvotlistan](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

### Navigera till AWS KMS för att starta nyckelkonfigurationen

>[!IMPORTANT]
>
>Säkerställ säker lagring, åtkomst och tillgänglighet för krypteringsnycklarna. Du ansvarar för att hantera dina nycklar och förhindra avbrott i plattformsåtgärder.

Om du vill börja konfigurera och hantera krypteringsnyckeln loggar du in på ditt AWS-konto och går till AWS nyckelhanteringstjänst (KMS). Från AWS Management Console och välj **Nyckelhanteringstjänst (KMS)** på menyn Tjänster.

![Listrutan Sök i AWS Management Console med nyckelhanteringstjänsten markerad.](../../images/governance-privacy-security/key-management-service/navigate-to-kms.png)

## Skapa en ny nyckel {#create-a-key}

Arbetsytan [!DNL Key Management Service (KMS)] visas. Välj **[!DNL Create a key]**.

![Arbetsytan för nyckelhanteringstjänsten med Skapa en nyckel markerad.](../../images/governance-privacy-security/key-management-service/create-a-key.png)

## Konfigurera nyckelinställningar {#configure-key}

Arbetsflödet [!DNL Configure Key] visas. Som standard är nyckeltypen inställd på **[!DNL Symmetric]** och nyckelanvändningen är inställd på **[!DNL Encrypt and Decrypt]**. Se till att de här alternativen är markerade innan du fortsätter.

![Stega ett av alternativen i Konfigurera nyckelarbetsflödet med Grundläggande alternativ för Symmetrisk och Kryptera och dekryptera markerade.](../../images/governance-privacy-security/key-management-service/configure-key-basic-options.png)

Expandera listrutan **[!DNL Advanced options]**. Du rekommenderas att använda alternativet **[!DNL KMS]**, som gör att AWS kan skapa och hantera nyckelmaterial. Alternativet **[!DNL KMS]** är markerat som standard.

>[!NOTE]
>
>Om du redan har en befintlig nyckel kan du importera externt nyckelmaterial eller använda nyckelbehållaren för AWS [!DNL CloudHSM]. Dessa alternativ omfattas inte av detta dokuments tillämpningsområde.

Välj sedan inställningen [!DNL Regionality] som anger nyckelns regionomfång. Välj **[!DNL Single-Region key]** följt av **[!DNL Next]** för att fortsätta till steg två.

>[!IMPORTANT]
>
>AWS tillämpar regionsbegränsningar för KMS-nycklar. Den här regionbegränsningen innebär att nyckeln måste finnas i samma region som ditt Adobe-konto. Adobe har bara åtkomst till KMS-nycklar som finns i kontots region. Kontrollera att det område du väljer matchar regionen för ditt single-tenant-konto i Adobe.

![Stega ett av de avancerade alternativen i Konfigurera nyckelarbetsflöde med AWS-regionen, KMS och Enstaka region markerade.](../../images/governance-privacy-security/key-management-service/configure-key-advanced-options.png)

## Märk upp och tagga nyckeln {#add-labels-and-tags-to-key}

Den andra [!DNL Add labels]-fasen av arbetsflödet visas. Här konfigurerar du fälten [!DNL Alias] och [!DNL Tags] så att du kan hantera och hitta din krypteringsnyckel från AWS KMS-konsolen.

Ange en beskrivande etikett för nyckeln i indatafältet **[!DNL Alias]**. Aliaset fungerar som en användarvänlig identifierare som snabbt hittar nyckeln med sökfältet i AWS KMS-konsolen. För att undvika missförstånd väljer du ett beskrivande namn som återspeglar syftet med nyckeln, till exempel&quot;Adobe-Platform-Key&quot; eller&quot;Customer-Encryption-Key&quot;. Du kan även inkludera en beskrivning av nyckeln om nyckelaliaset inte räcker till för att beskriva dess syfte.

Tilldela slutligen metadata till nyckeln genom att lägga till nyckelvärdepar i avsnittet [!DNL Tags]. Det här steget är valfritt, men du bör lägga till taggar för att kategorisera och filtrera AWS-resurser för enklare hantering. Om din organisation till exempel använder flera Adobe-relaterade resurser kan du tagga dem med&quot;Adobe&quot; eller&quot;Experience-Platform&quot;. Det här extra steget gör det enkelt att söka efter och hantera alla associerade resurser i AWS Management Console. Välj **[!DNL Add tag]** för att påbörja processen.

<!-- I do not have an AWS account with which to document the Add tag process as yet. -->

När du är nöjd med dina inställningar väljer du **[!DNL Next]** för att fortsätta med arbetsflödet.

![Steg två av Konfigurera nyckelarbetsflödet med Alias, Beskrivning, Taggar och Nästa markerat.](../../images/governance-privacy-security/key-management-service/add-labels.png)

## Definiera administrativa nyckelbehörigheter {#define-key-admins}

Steg tre av arbetsflödet för att skapa nycklar visas. För att säkerställa säker och kontrollerad åtkomst kan du välja vilken av IAM-användarna och rollerna som kan hantera nyckeln. Det finns två alternativ i det här skedet, [!DNL Key administrators] och [!DNL Key deletion]. I avsnittet **[!DNL Key administrators]** markerar du en eller flera kryssrutor bredvid namnet på en användare, eller roll, som du vill ge administratörsbehörighet för den här nyckeln.

>[!NOTE]
>
>Du kan inte skapa administratörer i det här skedet av arbetsflödet.

I avsnittet **[!DNL Key deletion]** aktiverar du kryssrutan så att nyckeladministratörer kan ta bort den här nyckeln. Om du inte markerar kryssrutan tillåts inte administrativa användare att utföra den åtgärden.

Välj **[!DNL Next]** om du vill fortsätta med arbetsflödet.

![Steg för Definiera administratörsbehörighet för nyckel i arbetsflödet, med kryssrutor och nästa markerade.](../../images/governance-privacy-security/key-management-service/define-key-admins.png)

## Bevilja åtkomst för nyckelanvändare {#assign-key-users}

I steg fyra av arbetsflödet kan du [!DNL Define key usage permissions]. I listan **[!DNL Key users]** markerar du kryssrutorna för alla IAM-användare och roller som du vill ha behörighet att använda den här nyckeln.

Från den här vyn kan du även [!DNL Add another AWS account], men du bör inte lägga till andra AWS-konton. Om du lägger till ett annat konto kan det medföra risker och komplicera behörighetshanteringen för krypterings- och dekrypteringsåtgärder. Genom att behålla nyckeln som är kopplad till ett enda AWS-konto kan Adobe säkerställa säker integrering med AWS KMS, minimera riskerna och säkerställa tillförlitlig drift.

Välj **[!DNL Next]** om du vill fortsätta med arbetsflödet.

![Ställa in nyckelanvändningsbehörighet i arbetsflödet, med kryssrutor och nästa markerade.](../../images/governance-privacy-security/key-management-service/define-key-users.png)

## Granska nyckelkonfiguration {#review}

Granskningssteget för nyckelkonfigurationen visas. Verifiera nyckelinformationen i avsnitten [!DNL Key configuration] och [!DNL Alias and description].

>[!NOTE]
>
>Se till att nyckelregionen är densamma som AWS-kontot.

![Granskningsfasen av arbetsflödet med nyckelkonfigurationen och alias- och beskrivningsavsnitten markerade.](../../images/governance-privacy-security/key-management-service/review-key-configuration-details.png)

### Uppdatera nyckelprincipen för att integrera nyckeln med Experience Platform

Redigera sedan JSON i avsnittet **[!DNL Key Policy]** för att integrera nyckeln med Experience Platform. En standardnyckelprincip ser ut ungefär som JSON nedan.

<!-- The AWS ID below is fake. Q) Can I refer to it simply as AWS_ACCOUNT_ID ? Is that suitable? -->

```JSON
{
  "Id": "key-consolepolicy-3",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Enable IAM User Permissions",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123464903283:root" // this is a mock AWS Principal ID, your ID will differ
      },
      "Action": "kms:*",
      "Resource": "*"
    }
  ]
}
```

I exemplet ovan kan alla resurser (`"Resource": "*"`) i samma konto (`Principal.AWS`) komma åt den här nyckeln. Principen tillåter att andra tjänster på samma konto använder nyckeln för kryptering och dekryptering. Tjänsterna har bara behörighet för det här kontot.

Ge ditt Platform single tenant-konto åtkomst till den här nyckeln genom att lägga till nya satser i den här principen. Du kan hämta JSON-principen från användargränssnittet för plattformen och använda den på din AWS KMS-nyckel för att länka den till plattformen på ett säkert sätt.

Navigera till plattformsgränssnittet. Välj **[!UICONTROL Encryption]** i avsnittet **[!UICONTROL Administration]** i den vänstra navigeringslisten. Arbetsytan [!UICONTROL Encryption Configuration] visas. Välj sedan **[!UICONTROL Configure]** i [!UICONTROL Customer Managed Keys]-kortet.

![Arbetsytan Konfiguration av plattformskryptering med Konfigurera är markerad på kundkortet för hanterade nycklar.](../../images/governance-privacy-security/key-management-service/encryption-configuration.png)

[!UICONTROL Customer Managed Keys configuration] visas. Välj kopieringsikonen (![En kopieringsikon).](../../../images/icons/copy.png)) om du vill kopiera CMK KMS-principen till Urklipp. Ett grönt popup-meddelande bekräftar att principen kopierades.

![Konfigurationen för kundhanterade nycklar med CMK KMS-principen visas och kopieringsikonen är markerad.](../../images/governance-privacy-security/key-management-service/copy-cmk-policy.png)

<!-- This part of the workflow was in contention at the time of the demo.  -->

Gå sedan tillbaka till AWS KMS-arbetsytan och uppdatera nyckelprincipen som visas nedan.

![Granskningssteget i arbetsflödet med den uppdaterade principen och Slutför markerat.](../../images/governance-privacy-security/key-management-service/updated-cmk-policy.png)

Lägg till de fyra programsatserna från arbetsytan [!UICONTROL Platform Encryption Configuration] i standardprincipen enligt nedan: `Enable IAM User Permissions`, `CJA Flow IAM User Permissions`, `CJA Integrity IAM User Permissions`, `CJA Oberon IAM User Permissions`.

```json
{
    "Version": "2012-10-17",
    "Id": "key-consolepolicy",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::975049898882:root" // this is a mock AWS Principal ID, your ID will differ
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "975049898882" // this is a mock AWS Principal ID, your ID will differ
                }
            }
        },
        {
            "Sid": "CJA Flow IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::767397686373:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "767397686373"
                }
            }
        },
        {
            "Sid": "CJA Integrity IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::730335345392:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "730335345392"
                }
            }
        },
        {
            "Sid": "CJA Oberon IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::891377157113:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "891377157113"
                }
            }
        }
    ]
}
```



Välj **[!DNL Finish]** om du vill bekräfta din nyckelinformation med den uppdaterade profilen och skapa nyckeln. Nyckeln och principen har nu konfigurerats med totalt fem satser så att ditt AWS-konto kan kommunicera med ditt Experience Platform-konto. Effekten är omedelbar.

Den uppdaterade [!DNL Customer managed keys]-arbetsytan i AWS [!DNL Key Management Service] visas.

### Lägg till information om AWS krypteringsnyckel till plattformen

Om du sedan vill aktivera kryptering lägger du till nyckelns ARN (Amazon Resource Name) på plattformen [!UICONTROL Customer Managed Keys configuration]. I avsnittet [!DNL Customer Managed Keys] i AWS väljer du alias för den nya nyckeln i listan i [!DNL Key Management Service].

![Arbetsytan för kundhanterade nycklar i AWS KMS med det nya nyckelaliaset markerat.](../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

Information om nyckeln visas. Allt i AWS har ett ARN (Amazon Resource Name) som
är en unik identifierare som används för att ange resurser för olika AWS-tjänster. Det följer ett standardiserat format: `arn:partition:service:region:account-id:resource`.

Välj kopieringsikonen om du vill kopiera ARN. En bekräftelsedialogruta visas.

![Nyckelinformation om kundhanterad nyckel för AWS KMS med ARN markerad.](../../images/governance-privacy-security/key-management-service/keys-details-arn.png)

Gå tillbaka till användargränssnittet för plattformen [!UICONTROL Customer Managed Keys configuration]. I avsnittet **[!UICONTROL Add AWS encryption key details]** lägger du till en **[!UICONTROL Configuration name]** och den **[!UICONTROL KMS key ARN]** du kopierade från AWS-gränssnittet.

![Arbetsytan Konfiguration av plattformskryptering med konfigurationsnamnet och KMS-nyckeln ARN markeras i avsnittet Lägg till information om krypteringsnyckel för AWS.](../../images/governance-privacy-security/key-management-service/add-encryption-key-details.png)

Välj sedan **[!UICONTROL SAVE]** för att skicka konfigurationsnamnet, KMS-nyckeln ARN, och börja validera nyckeln.

![Arbetsytan Konfiguration av plattformskryptering med Spara markerad.](../../images/governance-privacy-security/key-management-service/save.png)

Du återgår till arbetsytan [!UICONTROL Encryption Configurations]. Status för krypteringskonfigurationen visas längst ned på kortet **[!UICONTROL Customer Managed Keys]**.

![Arbetsytan Krypteringskonfigurationer i plattformsgränssnittet med bearbetning är markerad på kundens hanterade nyckelkort.](../../images/governance-privacy-security/key-management-service/configuration-status.png)

När nyckeln har validerats läggs nyckelvalvet-ID:n till i datavjön och profildatastores för alla sandlådor.

>[!NOTE]
>
>Hur länge processen varar beror på datastorleken. Vanligtvis slutförs processen på mindre än 24 timmar. Varje sandlåda uppdateras vanligtvis på två till tre minuter.

## Återkallning av nyckel {#key-revocation}

>[!IMPORTANT]
>
>Förstå konsekvenserna av återkallande av nyckelord för program längre fram i kedjan innan du återkallar en åtkomst.

Här följer några viktiga saker att tänka på när du återkallar en nyckel:

- Om du återkallar eller inaktiverar nyckeln blir plattformsdata otillgängliga. Denna åtgärd är irreversibel och bör utföras med försiktighet.
- Tänk på spridningstidslinjerna när åtkomst till krypteringsnycklar återkallas. Primära datalager blir oåtkomliga inom några minuter till 24 timmar. Cachelagrade eller tillfälliga datalager blir oåtkomliga inom sju dagar.

Om du vill återkalla en tangent går du till arbetsytan i AWS KMS. I avsnittet **[!DNL Customer managed keys]** visas alla tillgängliga nycklar för ditt AWS-konto. Välj alias för nyckeln i listan.

![Arbetsytan för kundhanterade nycklar i AWS KMS med det nya nyckelaliaset markerat.](../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

Information om nyckeln visas. Om du vill inaktivera nyckeln väljer du **[!DNL Key actions]** och sedan **[!DNL Disable]** i listrutan.

![Information om din AWS-nyckel i AWS KMS-gränssnittet med Key actions och Disable markerat.](../../images/governance-privacy-security/key-management-service/disable-key.png)

En bekräftelsedialogruta visas. Välj **[!DNL Disable key]** för att bekräfta ditt val. Effekten av att inaktivera nyckeln bör återspeglas i plattformsapplikationer och användargränssnittet inom ungefär fem minuter.

>[!NOTE]
>
>När du har inaktiverat nyckeln kan du aktivera den igen med samma metod som beskrivs ovan om du skulle behöva göra det. Det här alternativet är tillgängligt i listrutan **[!DNL Key actions]**.

![Dialogrutan Inaktivera tangent med inaktiveringstangenten markerad.](../../images/governance-privacy-security/key-management-service/disable-key-dialog.png)

Om nyckeln används för andra tjänster kan du även ta bort åtkomsten för Experience Platform direkt från nyckelprincipen. Välj **[!UICONTROL Edit]** i avsnittet **[!DNL Key Policy]**.

![Detaljdelen av AWS-nyckeln med Redigera markerat i nyckelprincipavsnittet.](../../images/governance-privacy-security/key-management-service/edit-key-policy.png)

Sidan **[!DNL Edit key policy]** visas. Markera och ta bort den principsats som kopierats från plattformsgränssnittet för att ta bort behörigheten för appen Kundhanterade nycklar. Välj sedan **[!DNL Save changes]** för att slutföra processen.

![Arbetsytan Redigera nyckelprincip på AWS med JSON-objektet för satsen och Spara ändringar markerade.](../../images/governance-privacy-security/key-management-service/delete-statement-and-save-changes.png)

## Nyckelrotation {#key-rotation}

AWS erbjuder automatisk tangentrotation på begäran. För att minska risken för nyckelkompromisser eller uppfylla säkerhetskraven kan du automatiskt generera nya krypteringsnycklar vid behov eller med regelbundna intervall. Schemalägg automatisk tangentrotation för att begränsa nyckelns livslängd och kontrollera att tangenten inte kan användas efter rotation om den är komprometterad. Moderna krypteringsalgoritmer är mycket säkra, men nyckelrotation är en viktig åtgärd för att uppfylla säkerhetskraven och visar att de bästa säkerhetsmetoderna följs.

### Automatisk tangentrotation {#automatic-key-rotation}

Automatisk tangentrotation är inaktiverat som standard. Om du vill schemalägga automatisk tangentrotation från KMS-arbetsytan väljer du fliken **[!DNL Key rotation]** följt av **[!DNL Edit]** i **[!DNL Automatic key rotation section]** .

![Informationsdelen för AWS-nyckeln med nyckelrotation och redigering markerade.](../../images/governance-privacy-security/key-management-service/key-rotation.png)

Arbetsytan **[!DNL Edit automatic key rotation]** visas. Här väljer du alternativknappen för att aktivera eller inaktivera automatisk tangentrotation. Använd sedan textinmatningsfältet eller listrutan för att välja en tidsperiod för tangentrotationen. Välj **[!DNL Save]** för att bekräfta dina inställningar och återgå till arbetsytan med nyckelinformation.

>[!NOTE]
>
>Den minsta tangentrotationsperioden är 90 dagar och den högsta är 2 560 dagar.

![Arbetsytan Redigera automatisk tangentrotation med rotationsperioden och Spara markerad.](../../images/governance-privacy-security/key-management-service/automatic-key-rotation.png)

### Rotation av on demand-tangenten {#on-demand-key-rotation}

Om den aktuella nyckeln är komprometterad väljer du **[!DNL Rotate Now]** för att rotera den omedelbart. AWS tillåter endast tio on-demand-rotationer. Använd en schemalagd nyckelrotation såvida inte säkerheten redan har komprometterats.

![Informationsdelen i AWS-nyckeln med Rotera nu markerat.](../../images/governance-privacy-security/key-management-service/on-demand-key-rotation.png)

## Nästa steg

När du har läst det här dokumentet har du lärt dig att skapa, konfigurera och hantera krypteringsnycklar i AWS KMS för användning med Adobe Experience Platform. Som ett nästa steg bör du överväga att granska organisationens säkerhets- och efterlevnadspolicyer för att säkerställa korrekt hantering, som schemalagd nyckelrotation och säker nyckellagring.
