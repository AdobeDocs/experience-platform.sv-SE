---
title: Stripe
description: Lär dig hur du importerar betalningsdata från ditt Stripe-konto till Adobe Experience Platform
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# [!DNL Stripe]

Tusentals företag av alla storlekar använder [!DNL Stripe] både online och personligen för att ta emot betalningar, generera nya inkomstkällor och expandera globalt med hjälp av Adobe Experience Platform, Adobe Commerce och [!DNL Magento Open Source].

Använd [!DNL Stripe]-källan i Experience Platform för att importera data som dina kunder har samlat in under inköpsflödet. Använd dessa data när de har importerats för att skapa personaliserade erbjudanden och få bättre affärsinsikter.

>[!TIP]
>
>Om du har frågor om källan [!DNL Stripe] på Experience Platform kan du kontakta [!DNL Stripe] på adobe-partnership<span>@stripe.com.

>[!BEGINSHADEBOX]

**Exempel på användning för [!DNL Stripe] source**

Med ditt företag kan kunder köpa artiklar i din onlinebutik med möjlighet att **köpa nu** och **betala senare** (med [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] eller [!DNL Zip]).

Använd datakällan [!DNL Stripe] för att analysera användningen av alternativen **Köp nu** och **betala senare** och experimentera med personaliserade erbjudanden till dessa kunder. Överväg till exempel att rekommendera tilläggsobjekt för att utöka antalet artiklar i kundvagnen före utcheckning.

>[!ENDSHADEBOX]

Läs dokumentet nedan för information om hur du kan konfigurera [!DNL Stripe]-källkontot, hämta nödvändiga autentiseringsuppgifter och skapa dina scheman.

## Förhandskrav {#prerequisites}

Följande avsnitt innehåller information om den nödvändiga konfiguration som du måste slutföra innan du kan ansluta ditt [!DNL Stripe]-konto till Experience Platform.

### Hämta din åtkomsttoken

* Logga in på [[!DNL Stripe] instrumentpanelen](https://dashboard.stripe.com/login) med din [!DNL Stripe] e-postadress och ditt lösenord.
* Välj [!DNL Developers] på kontrollpanelen **[!DNL API keys for developers]**.
* Under fliken **API-nycklar** väljer du **[!DNL Reveal test key]** för att visa din åtkomsttoken.
* Du kan nu använda den här token som din åtkomsttoken när du ansluter ditt [!DNL Stripe]-konto till Experience Platform med API:t [!DNL Flow Service] eller Experience Platform-gränssnittet.

### Samla in nödvändiga inloggningsuppgifter

Om du vill ansluta ditt [!DNL Stripe]-konto till Experience Platform måste du ange värden för följande autentiseringsuppgifter:

>[!BEGINTABS]

>[!TAB API]

Du måste ange följande autentiseringsuppgifter när du ansluter ditt [!DNL Stripe]-konto med API:t [!DNL Flow Service].

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `accessToken` | Autentiseringstoken för [!DNL Stripe] OAuth 2-uppdateringskod. |
| `connectionSpec.id` | Anslutningens spec-ID för källan [!DNL Stripe]. Detta ID har korrigerats som: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB Gränssnitt]

Du måste ange följande autentiseringsuppgifter när du ansluter ditt [!DNL Stripe]-konto med Experience Platform användargränssnitt.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Åtkomsttoken | Autentiseringstoken för [!DNL Stripe] OAuth 2-uppdateringskod. |

>[!ENDTABS]

Mer information om hur du använder [!DNL Stripe] API:er finns i [[!DNL Stripe] dokumentationen om API-nycklar](https://docs.stripe.com/keys).

### Skapa ett XDM-schema (Experience Data Model)

Källan [!DNL Stripe] stöder inmatning av data från följande resurssökvägar:

* Avgifter
* Prenumerationer
* Återbetalningar
* Saldotransaktioner
* Kunder
* Priser

Du måste skapa ett XDM-schema för att beskriva en datauppsättning, som kan lagra fält och datatyper som ska skickas från [!DNL Stripe] till Experience Platform.

>[!BEGINTABS]

>[!TAB Avgifter]

I [!DNL Stripe] representerar **avgifter** försök att flytta pengar till din [!DNL Stripe]. Läs [[!DNL Stripe] API-guiden för avgifter](https://docs.stripe.com/api/charges) om du vill ha mer information om specifika debiteringsattribut.

+++Markera för att visa Stripe Charge-objektet  

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB Prenumerationer]

I [!DNL Stripe] kan du använda **prenumerationer** för att debitera en kund regelbundet. Läs [[!DNL Stripe] API-guiden för prenumerationer](https://docs.stripe.com/api/subscriptions) om du vill ha mer information om specifika prenumerationsattribut.

+++Markera för att visa Stripe Subscription-objektet

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB Återbetalningar]

I [!DNL Stripe] kan du använda **återbetalningar** om du vill återbetala en avgift som skapats tidigare. Läs [[!DNL Stripe] API-guiden för återbetalningar](https://docs.stripe.com/api/refunds) om du vill ha mer information om specifika återbetalningsattribut.

+++Markera för att visa Stripe Refund-objektet

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB Balansera transaktioner]

I [!DNL Stripe] representerar **saldotransaktioner** rörelsen av medel mellan dina [!DNL Stripe]-konton. Läs [[!DNL Stripe] API-guiden för saldotransaktioner](https://docs.stripe.com/api/balance_transactions) om du vill ha mer information om specifika saldotransaktionsattribut.

+++Markera för att visa Stripe saldotransaktionsobjekt

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB Kunder]

I [!DNL Stripe] representerar **kunder** en viss kund i ditt företag. Mer information om specifika kundattribut finns i [[!DNL Stripe] API-handboken för kunder](https://docs.stripe.com/api/customers) för mer information om specifika kundattribut.

+++Välj det här om du vill visa Stripe kundobjekt

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB Priser]

I [!DNL Stripe] representerar **priser** enhetskostnaden, valutan och den valfria faktureringscykeln för både återkommande och engångsköp av produkter. Läs [[!DNL Stripe] API-guiden för priser](https://docs.stripe.com/api/prices) om du vill ha mer information om specifika prisattribut.

+++Markera för att visa Stripe Price-objektet

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Stripe]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/ui/overview.md).

## Nästa steg

När du har slutfört konfigurationen av din förutsättning kan du fortsätta ansluta och importera dina [!DNL Stripe]-data till Experience Platform. Läs följande guider om du vill veta hur du importerar [!DNL Stripe] betalningsdata till Experience Platform med API:er eller användargränssnittet:

* [Infoga betalningsdata från ditt Stripe-konto till Experience Platform med API:t för Flow Service ](../../tutorials/api/create/payments/stripe.md).
* [Registrera betalningsdata från ditt Stripe-konto till Experience Platform via användargränssnittet](../../tutorials/ui/create/payments/stripe.md).
