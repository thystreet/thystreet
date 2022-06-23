# Getting started

The following tutorial is a hello world equivalent of using tools provided by [Thy Street](https://thystreet.com).

![](<.gitbook/assets/image (2).png>)

{% embed url="https://www.youtube.com/watch?v=lNZUh9FUR38" %}

## About Device:

For keeping it simple, the setup that we will be using is following:

* **Hardware:** ESP32 devkit v1 module.
* **Software**: Arduino using platform.io
* **MQTT:** Any MQTT server available public

{% hint style="info" %}
This guide majorly focuses on how you can set up a simple workflow for your device using Thy Street APIs. If you are interested in how to set up your environment, please check out Platform.io[ official documentation.](https://docs.platformio.org/en/latest/frameworks/arduino.html)
{% endhint %}

After a simple google search, we found [HiveMQ](https://www.hivemq.com/mqtt-cloud-broker/) provides a free MQTT broker in their basic plan.Set up your details and get your MQTT credentials. We will be using the following details for the rest of this tutorial:

* **Username:** USER\_ID
* **Password:** DEVICE\_PASSWORD
* **Hostname:** example.hivemq.cloud

{% hint style="info" %}
Please understand we are in no way associated with HiveMQ., and this is not any sponsored post. The decision to select HiveMQ was purely random.
{% endhint %}

{% hint style="info" %}
You can download the stater code from [github](https://github.com/thystreet/esp32-blink-example). Starter code is in `starter` branch.
{% endhint %}

## Dashboard Actions

* Login into the dashboard.
* [Enable payment](accounts/payment.md) (it takes up to 48 business hours to create your account in the payment gateway.)
* [Add a new device](devices/create-device.md).
* [Create a tariff card](tariff-manager/edittariff.md) with below details:
  * **Currency:** INR
  * Add an entry in the tariff card with the following details:
    * **Name:** blink
    * **Title:** Fresh LED blinks
    * **Minimum Value:** 0
    * **Maximum Value:** 10
    * **Increment:** 1
    * **Price:** 10
    * **Tax1** rate in percentage **8**
* Create a [custom adapter](devices/webhook/custom-adapter.md) to convert our HTTP webhook data to MQTT Arduino data, use the MQTT credentials created above.

## Client Integration

* Get the [API credentials](accounts/account-settings/api-credentials.md) from your account page.
* Add [Thy Street client SDK](https://platformio.org/lib/show/12370/thystreet/installation) in your platform io project.

#### Add authentication.

```cpp
#include "DeviceApi.h"

...

const char *apiKey = "Thy Street API Key";
const char *apiSecret = "Thy Street API secret";


Tiny::DeviceApi api;
void setup()
{
    ...
    
    api.setAuthorization(apiKey, apiSecret);
    
    ...
}
```

#### Generate new token and set device status to available

```cpp
void setup()
{
...

auto tokenResponse = api.generateToken();
Serial.println(resp.obj.c_str());

Tiny::DeviceStatusDto dto;
dto.setAvailable(true);
dto.setDeviceId("device-id");
auto resp = api.setStatus(dto);
Serial.println(resp.code);
Serial.println(resp.obj.c_str());
...
}
```

#### Update your MQTT listener loop

```cpp
// Mark the order status as confirmed
// Blink the LED 8 times
// Generate the token again for the next customer 
// Mark order status as completed.
```

As a last step, make the device public. (This is a paid action and will ask for a [subscription](https://thystreet.com/pricing)).

Upload the code on your esp32 and start the device. Navigate to the device's page, select 3 led blinks, click on pay. Once you enter the code and make the payment, the onboard led should blink three times.

{% hint style="info" %}
Help your customers by adding [FAQs](frequently-asked-questions/what-are-faqs.md), and support information for your device.
{% endhint %}

Download and print the device's QR code, install your device and enjoy your sales on the [payment gateway's dashboard](https://dashboard.razorpay.com).

{% hint style="info" %}
When sharing your device installation over social media, please don't forget to tag us.

If you have a device idea feel free to discuss with the [community](https://github.com/thystreet/thystreet/discussions/categories/ideas)
{% endhint %}
