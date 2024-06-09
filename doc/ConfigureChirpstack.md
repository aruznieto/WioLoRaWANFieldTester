# Configure device in the Chirpstack for Helium Network

Please see (Configure for Helium Network)[ConfigureHelium.md] documentation.

# Configure device in the Chirpstack Standalone

This have a limitation: Chirpstack use API integration for downlink request. My backend doesn't support API Key management and I don't want to store your API Keys. As a consequence, this configuration mode is not supported. 

You can connect WioLoRaWanFieldTester to Chiprstack, it will work, but you wont get most of the value coming from the downlink. So you will have to create your own backend.
