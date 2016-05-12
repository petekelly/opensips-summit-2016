# opensips-summit-2016

If you want to try the demo you will need to change the IP address accordingly in
multiple places in index.html, and also in opensips.cfg.

You will also need to generate your own SSL certificate, this can be done on a debian system using the following commands (also documented in Step 2 here https://wiki.debian.org/Self-Signed_Certificate):

	mkdir -p /etc/ssl/localcerts
	openssl req -new -x509 -days 365 -nodes -out /etc/ssl/localcerts/mycert.pem -keyout /etc/ssl/localcerts/mycert.key
	chmod 600 /etc/ssl/localcerts/mycert*



The repository contains 2 files.

## index.html
A very basic html file which demonstrates loading the sipjs library and creating
some listeners to page clicks.

Its key purposes are to demonstrate:
*  Secure websocket connection to OpenSIPS
*  UA registration to OpenSIPS
*  receiving a call
*  Making a call

There are known bugs, for example you only have a UserAgent available to make a call if you have registered first.


## opensips.cfg
A modified version of the default opensips.cfg. It contains the following changes:

* Loading of proto_wss module
* Loading of tls_mgm module
* Loading of nathelper module
* Loading of rtpengine module
* specification of received_avp for both registrar and nathelper modules
* calls to fix_nated_register() and fix_nated_contact() as needed
* Calls to rtpengine_offer() and rtpengine_answer() for use in PSTN demonstration.
