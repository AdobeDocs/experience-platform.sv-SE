---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Översikt över namnområde för identitet

Identitetsnamnutrymmen är en komponent i [identitetstjänsten](./home.md) som fungerar som indikatorer för det sammanhang som en identitet relateras till. De skiljer till exempel på värdet&quot;name<span>@email.com&quot; som e-postadress eller&quot;443522&quot; som ett numeriskt CRM-ID.

## Komma igång

Att arbeta med identitetsnamnutrymmen kräver förståelse för de olika Adobe Experience Platform-tjänsterna som är inblandade. Innan du börjar arbeta med namnutrymmen bör du läsa dokumentationen för följande tjänster:

- [Kundprofil](../profile/home.md)i realtid: Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
- [Identitetstjänst](./home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
- [Integritetstjänst](../privacy-service/home.md): Identitetsnamnutrymmen används för att uppfylla den allmänna dataskyddsförordningen (GDPR), där GDPR-begäranden kan göras i förhållande till ett namnutrymme.

## Identitetsnamnutrymmen

En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme. När postdata matchas mellan profilfragment, som när kundprofilen i realtid sammanfogar profildata, måste både identitetsvärdet och namnutrymmet matcha.

Två profilfragment kan till exempel innehålla olika primära ID:n, men de delar samma värde för namnutrymmet&quot;E-post&quot;. Därför kan Platform se att dessa fragment faktiskt är samma individ och sammanför data i identitetsdiagrammet för den enskilda personen.

![](images/identity-service-stitching.png)

### Identitetstyper

Data kan identifieras av flera olika identitetstyper. Identitetstypen anges när identitetsnamnutrymmet skapas och kontrollerar om data bevaras i identitetsdiagrammet och eventuella specialinstruktioner för hur data ska hanteras.

Följande identitetstyper är tillgängliga inom Platform:

| Identitetstyp | Beskrivning |
| --- | --- |
| Cookie | Dessa identiteter är viktiga för expansion och utgör huvuddelen av identitetsdiagrammet. Av naturen sjunker de dock snabbt och förlorar sitt värde över tiden. Borttagning av cookies hanteras särskilt i identitetsdiagrammet. |
| Flera enheter | Detta visar att identitetstjänsten bör betrakta detta som en stark personidentifierare och därmed bevara den för alltid. Exempel är inloggnings-ID, CRM-ID, lojalitets-ID osv. |
| Enhet | Inkluderar IDFA, GAID och andra IOT ID:n. Dessa kan delas av människor i hushåll. |
| E-post | Identiteter av den här typen omfattar personligt identifierbar information (PII). Detta är en indikation till identitetstjänsten för att hantera värdet känsligt. |
| Mobil | Identiteter av den här typen är PII. Detta är en indikation till identitetstjänsten för att hantera värdet känsligt. |
| Icke-människor | Används för att lagra identifierare som behöver namnutrymmen, men som inte är kopplade till ett personkluster. Dessa identifierare filtreras sedan från identitetsdiagrammet. Möjliga användningsexempel är data om produkter, organisationer, butiker osv. (Till exempel en produkt-SKU.) |
| Telefon | Identiteter av den här typen är PII. Detta är en indikation till identitetstjänsten för att hantera värdet känsligt. |

### Standardnamnutrymmen

Adobe Experience Platform innehåller flera identitetsnamnutrymmen som är tillgängliga för alla organisationer. Dessa kallas standardnamnutrymmen och visas med identitetstjänstens API eller med hjälp av plattformens användargränssnitt.

Om du vill visa standardnamnutrymmen i användargränssnittet klickar du på **Identiteter** i den vänstra listen och sedan på fliken *Bläddra* . Alla identitetsnamnutrymmen som är tillgängliga för din organisation visas, men de med &quot;Standard&quot; som &quot;Ägare&quot; är standardnamnutrymmena från Adobe.

Du kan sedan klicka på ett av namnutrymmena för att visa information.

![](./images/standard-namespace-detail.png)

## Hantera namnutrymmen för din organisation

Beroende på dina organisationsdata och användningsfall kan du behöva anpassade namnutrymmen.

De här är synliga i användargränssnittet som namnutrymmen med&quot;Egen&quot; som&quot;Ägare&quot;. Du kan skapa anpassade namnutrymmen med hjälp av ID-tjänstens API eller via användargränssnittet.

Om du vill skapa ett anpassat namnutrymme med användargränssnittet klickar du på **Skapa ID-namnutrymme**, fyller i dialogrutan och klickar på **Skapa**.

Namnutrymmen som du definierar är privata för din organisation och kräver en unik identitetssymbol (eller kod) om du använder API:t) för att kunna skapas.

![](./images/create-identity-namespace.png)

På samma sätt som för standardnamnutrymmen kan du klicka på ett anpassat namnutrymme på fliken *Bläddra* för att visa information. Med ett anpassat namnutrymme kan du även redigera dess visningsnamn och beskrivning i informationsområdet.

>[!NOTE] När ett namnutrymme har skapats kan det inte tas bort och dess&quot;identitetssymbol&quot; (eller&quot;kod&quot; i API) och&quot;typ&quot; kan inte ändras.

## Namnutrymmen i identitetsdata

Om du anger namnutrymmet för en identitet beror på vilken metod du använder för att ange identitetsdata. Mer information om att tillhandahålla data om identitetsuppgifter finns i avsnittet om [att tillhandahålla identitetsdata](./home.md#supplying-identity-data-to-identity-service) i översikten över identitetstjänsten.
