---
title: getPayflowLinkToken query | Commerce Web APIs
---

# getPayflowLinkToken query

The `getPayflowLinkToken` query retrieves PayPal payment credentials for a PayPal Payflow transaction. You must run this query after you [set the payment method](../../cart/mutations/set-payment-method.md) and [place the order](../../cart/mutations/place-order.md).

See [Paypal Payflow Link payment method](../../../payment-methods/payflow-link.md) for detailed information about the workflow of PayPal Payflow Link transactions.

## Syntax

`getPayflowLinkToken(input: PayflowLinkTokenInput): PayflowLinkToken`

## Example

The following example requests a token in a Payflow Link transaction.

**Request:**

```graphql
{
  getPayflowLinkToken(input: {cart_id: "123"}) {
    secure_token
    secure_token_id
    mode
    paypal_url
  }
}
```

**Response:**

```json
{
    "data": {
        "getPayflowLinkToken": {
            "secure_token": "<token-value>",
            "secure_token_id": "<token-value-id>",
            "mode": "TEST",
            "paypal_url": "https://pilot-payflowlink.paypal.com"
        }
    }
}
```

## Input attributes

### PayflowLinkTokenInput

The `PayflowLinkTokenInput` object defines the attributes required to receive a Payflow Link token from PayPal.

Attribute |  Data Type | Description
--- | --- | ---
`cart_id` | String! | The unique ID that identifies the customer's cart

## Output attributes

### PayflowLinkToken

The `PayflowLinkToken` object contains a token returned by PayPal and a set of URLs that allow the buyer to authorize payment and adjust checkout details.

Attribute |  Data Type | Description
--- | --- | ---
`mode` | `PayflowLinkMode` | The mode for the Payflow Link payment. Must be `LIVE` (actual transaction) or `TEST` (sandbox transaction)
`paypal_url` | String | The PayPal URL used for requesting a Payflow form
`secure_token` | String | Secure token generated by PayPal
`secure_token_id` | String | Secure token ID generated by PayPal

## Errors

Error | Description
--- | ---
`No such entity with cartId` | An invalid `cartId` was provided
