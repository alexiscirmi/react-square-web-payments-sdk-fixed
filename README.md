# react-square-web-payments-sdk-fixed

`react-square-web-payments-sdk` lets you easily create PCI-compliant inputs to accept payments online with the Square Payments API. It supports the following payment methods: credit and debit cards, ACH bank transfers, Apple Pay, Google Pay, and Gift Cards.

This version fixes a types export bug.

## Install

##### NPM

```shell
npm install react-square-web-payments-sdk-fixed
```

##### Yarn

```shell
yarn add react-square-web-payments-sdk-fixed
```

## Usage

```tsx
// Dependencies
import * as React from 'react';
import { CreditCard, PaymentForm } from 'react-square-web-payments-sdk';

const MyPaymentForm = () => (
  <PaymentForm
    /**
     * Identifies the calling form with a verified application ID generated from
     * the Square Application Dashboard.
     */
    applicationId="sq0idp-Y0QZQ-Xx-Xx-Xx-Xx"
    /**
     * Invoked when payment form receives the result of a tokenize generation
     * request. The result will be a valid credit card or wallet token, or an error.
     */
    cardTokenizeResponseReceived={(token, buyer) => {
      console.info({ token, buyer });
    }}
    /**
     * This function enable the Strong Customer Authentication (SCA) flow
     *
     * We strongly recommend use this function to verify the buyer and reduce
     * the chance of fraudulent transactions.
     */
    createVerificationDetails={() => ({
      amount: '1.00',
      /* collected from the buyer */
      billingContact: {
        addressLines: ['123 Main Street', 'Apartment 1'],
        familyName: 'Doe',
        givenName: 'John',
        countryCode: 'GB',
        city: 'London',
      },
      currencyCode: 'GBP',
      intent: 'CHARGE',
    })}
    /**
     * Identifies the location of the merchant that is taking the payment.
     * Obtained from the Square Application Dashboard - Locations tab.
     */
    locationId="LID"
  >
    <CreditCard />
  </PaymentForm>
);

export default MyPaymentForm;
```
