# Configure device in the Helium console

This describes the different steps to configure the device on the [Helium](https://www.helium.com) network.

## Join Helium console (Chirpstack)


### create an account on helium console

Skip if you already have an account.

You can create and account on one for the Helium - Chiprstack console, the one I'm operating is [Helium-IoT.xyz](https://console.helium-iot.xyz). 

<img src="../img/HeliumChirp-register-1.png" alt="Helium account creation" width="500"/>

Click on "No account? signup!" button and complete the following registration form:

<img src="../img/HeliumChirp-register-2.png" alt="Helium registration form" width="500"/>

Enter your email, set a password, type a tenant name, thi is a name you want to give to your tenant, it can be like *MyWio*. Leave Coupon code empty. Read and eventually accept the service term & use and click on **register**. You will get an email to confirm your registration and being able to connect to the console.

### create a device profile

Chirpstack uses *Device Profile* for the setup of a group of devices.

<img src="../img/HeliumChirp-devprofile-1.png" alt="Helium device profile creation" width="500"/>

Depending on the zone where you are, you need to change the **Region** field to match your region. If your device is going to be in different Region, you can declare multiple device profile with a similar name with region as a prefix like the following. If you are not moving from a region to another, just make a single  device profile.

<img src="../img/HeliumChirp-devprofile-3.png" alt="Helium device profile creation" width="500"/>

Make sure your device profile is OTAA:

<img src="../img/HeliumChirp-devprofile-2.png" alt="Helium device profile creation" width="500"/>


### create an application

In the left menu, click on application, then on the **add application** button on the top left.

<img src="../img/HeliumChirp-application-1.png" alt="Helium application creation" width="500"/>

Now, you need to create an Integration for this application, click on **Integartion** tab and select **HTTP** by clikong on the pensil icon. Then enter the following content:

<img src="../img/HeliumChirp-application-2.png" alt="Helium application creation" width="500"/>

### Add your device

Now, in the application, you can create a device by clicking on **Add Device** button and fill the form. You can generate the Dvice EUI an Join EUI (App EUI on Wio).

<img src="../img/HeliumChirp-device-1.png" alt="Helium device creation" width="500"/>

After submiting, you will need to generate an Application Key:

<img src="../img/HeliumChirp-device-2.png" alt="Helium device creation" width="500"/>

### Increase the number of purchased packets

In the top bar, click on **Tenant details** to increase the *Max copy* parameter. This is configuring the number of copies of a frame coming from different hotspots. You can set any value from 1 to 50. Cost will be higher with value, information visible on the WioFieldTester will be also higher with a higher value.

<img src="../img/HeliumChirp-tenant-1.png" alt="Helium device creation" width="500"/>



## Join Helium console ( Legacy, not any more viable )

Skip if you already have an account on helium console.

You need to create an account on the [Helium console](https://console.helium.com). This is free and you get 10.000 Data Credit (DC) for the registration. This is large enough to start for a couple of month to year of device use. You can later buy extra DC, 100.000 DC correspond to $1.

Once you have your account created, you can register your device. We are going to create a Label: this is basically a group of devices where common settings apply. Then we will create a Device to get the required credentials to identify the device. This device will be attached to the label.

Then we are going to create an integration with WioLoRaWANFieldTester backend. As explained in [How it works](HowItWorks.md) page, this allows the device to receives computed informations from the network and automatically report the coordinated to the [helium mapper](https://mappers.helium.com)

## Create a Label

From the Helium console dashboard, click on the **+** icon and select **Add label**

<img src="../img/HNTv2_Create_a_label_from_console.png" alt="Helium label creation" width="500"/>

Then, enter a *Label* name and **Save** it.

<img src="../img/HNTv2_Create_a_WioTester_label.png" alt="Helium label creation details" width="500"/>

## Create a Device

From the Helium console dashboard, click on the **+** icon and select **Add device**

<img src="../img/HNTv2_Create_a_device_from_console.png" alt="Helium device creation" width="500"/>

Then, enter a **Name** and Search the **Label** you created previously to make the attachment. You need to click on the Label name once displayed to add it in the form field. Then Save.

<img src="../img/HNTv2_Create_a_device_WioTester.png" alt="Helium device creation details" width="500"/>

Here you can see the device credential. There is no need to save them during this step, we will later see how to get and use them to setup the device.

## Create the Integration

From the Helium console dashboard, click on the **+** icon and select **Add integration**

<img src="../img/HNTv2_Create_an_integration_from_console.png" alt="Helium Add Integration" width="500"/>

The integration is **HTTP** type, it means the data will be redirected to a custom URL. You can get details on this in the [How it works](HowItWorks.md) page.

<img src="../img/HNTv2_Create_an_integration_type_http.png" alt="Helium Integration type HTTP" width="500"/>

Now you need to setup the integration by entering the target endpoint. Ensure the type is **POST** and enter as Endpoint URL: 
```
https://dev.disk91.com/fieldtester/helium/v3
```
At the end of the form, enter a name of your choice for this integration and click on **Add Integration**

<img src="../img/HNTv2_Create_an_integration_type_http_details.png" alt="Helium Integration HTTP details" width="500"/>

## Create a flow to link the Integration with the Label

We need to create a link between the Label and the Integration. Thanks to this, the Helium router will know that any data coming from one of the devices of the given Label will need to be transferred to the custom backend on dev.disk91.com.

From the console Dashboard, click on **Flow** to access the setup page.

<img src="../img/HNTv2_Create_a_flow_from_console.png" alt="Helium flow creation" width="500"/>

From the flow page, click on **Nodes** to extend the object's panel, then select **Labels** tab and drag & drop the Label you created previously to the flow page background.

<img src="../img/HNTv2_Create_a_flow_add_label.png" alt="Helium add a label in a flow" width="500"/>

Then you can select the **Integrations** tab and drag & drop your previously created integration to the flow page background.

<img src="../img/HNTv2_Create_a_flow_add_integration.png" alt="Helium add an integration in a flow" width="500"/>

Now, you need to link the Label to the Integration, for doing this, click on the Label connector (circle on the right of the Label) and drag your mouse to the Integration connector (on its left). It should be like the picture above.

<img src="../img/HNTv2_Create_a_flow_add_link.png" alt="Helium flow link label to integration" width="500"/>

## Configure the Label to buy all the replicate packets

Basically on Helium network, even if all the Hotspots around receives the Data, only one of them is basically bought by the Router to one of the Hotspot. This is because, one single frame is enough if you are only interested by the data transported. 
If you want to obtain more informations about the local network like the list of hotspot having received the message, you need to ask the router to buy more replicates of that frame coming from different Hotspots. Thanks to this, we will be able to display on the device a range of signal straight and the number of hotspot having received the message.
As a consequence, each message processed will cost 1DC each (plus ack cost). 
If you want to preserve your DC spend you can limit the number of messages bought by router.

You also need to know that currently the router, most of the time, only returns 1 message, even if many other exists. It is still under investigation by Helium.

To configure the number of packets to be bought, you need first to create a **Multiple Packets** configuration.
Give it a name and select the number of packets (replicates) you want to buy as a maximum. Then create this configuration.

<img src="../img/HNTv2_Create_a_multipacket_config.png" alt="Helium multi-packets configuration" width="500"/>

Now we need to associate this configuration to the Label on the **Flow** page

<img src="../img/HNTv2_Create_a_flow_from_console.png" alt="Helium flow creation" width="500"/>

Then click on the **Label** displayed on the Flow background page to edit its setting. Select the **Packets** tab and in this page, enable the corresponding **Multi-packets** configuration.

<img src="../img/HNTv2_Create_a_multipacket_config_affect.png" alt="Helium Label multi-packets association" width="500"/>

After doing this, you need to **Save** the flow settings.

<img src="../img/HNTv2_Create_a_multipacket_config_save.png" alt="Helium Flow save" width="500"/>


## Next steps

Go back to [installation page](SETUP.md) to continue the configuration


