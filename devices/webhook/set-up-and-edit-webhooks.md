---
description: You can set up and edit webhook  from the Thy Street Dashboard.
---

# Set Up and Edit Webhooks

### Prerequisites

Before you begin, get access to the [Thy Street Dashboard](https://thystreet.com/dashboard) by creating an [account](https://thystreet.com/register); make sure you have gone through:

{% content-ref url="../create-device.md" %}
[create-device.md](../create-device.md)
{% endcontent-ref %}

{% content-ref url="../../accounts/account-settings/api-credentials.md" %}
[api-credentials.md](../../accounts/account-settings/api-credentials.md)
{% endcontent-ref %}

## Set up Webhooks

1. Login into the [Thy Street Dashboard](https://thystreet.com/dashboard) and navigate to the [Devices](https://thystreet.com/devices) page.
2. Search and click on your device card.
3. Under the **Details** section, hover on **Integration** and Click on  ![](../../.gitbook/assets/edit.svg)icon.
4. In the  **Device Integration** pop-up page
   1. &#x20;Enter the URL where you want to receive the webhook payload when an event is triggered. We recommend using an HTTPS URL. You can use other protocols by writing your own [custom adapter](custom-adapter.md).&#x20;
   2. Enter a **Secret** for the endpoint. The secret is used to validate that the webhook is from Thy Street. Learn more about [how to validate and test webhooks](validate-and-test-webhooks.md).&#x20;
   3. Click on **Save Endpoint** to save changes.

{% hint style="info" %}
**Webhook URLs**\
****Webhooks can only be delivered to public URLs.
{% endhint %}

{% hint style="warning" %}
All webhook responses must return a status code in the range of 2XX within a window of 6 seconds. If we receive response codes other than this or the request times out, it is considered a failure.
{% endhint %}

{% hint style="info" %}
#### Secret for Webhooks

* When setting up the Webhooks, you will be asked to specify a secret. Using this secret, you can validate that the webhook is from Thy Street. The **Secret** should never be exposed publicly.
* The webhook secret doesn't need to be the API key provided for your account.
{% endhint %}

## Edit a Webhook

You can edit your webhook to replace the webhook URL and modify the secret.

To edit webhooks:

1. Log into the [Thy Street Dashboard](https://thystreet.com/dashboard) and navigate to your **Device** page
2. Under the **Details** section, hover on your webhook link and click on  ![](../../.gitbook/assets/edit.svg)
3.  The **Device Integration** pop-up page is displayed. You can modify the following:

    * Webhook URL
    * Secret


4. Click on **Save Endpoint** to save changes.

{% hint style="info" %}
#### Next Steps

You should validate and test your webhooks before you go live.
{% endhint %}

{% content-ref url="validate-and-test-webhooks.md" %}
[validate-and-test-webhooks.md](validate-and-test-webhooks.md)
{% endcontent-ref %}





