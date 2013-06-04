QR code Scan
============

QR Code format
--------------
QR code scanner will read qr codes produced by OMTrak.  The code will have the following formatter

    https://secure.omtrak.com/:project_slug/locations/:id

For example:

    https://secure.omtrak.com/test-project/locations/3234

The url representation is used so if people scan with any barcode scanner they can visit a valid website and get information about the product.

For the app we can read the last block :id to obtain ids for location.  
For example, we can split the string using "/" as delimiter and get the last block of text and parse it into an int.

Scan QR Code
------------

The app uses QR code in three places

* Location Filter
* Edit Defect -> Location selector
* New Defect -> Location selector

In each place, a Locatio Selector is presented to the user.  In the Location Selector user can tap on the camera icon
to present the scan view.  User can then scan the QR code which return a string that conforms
to the QR code format.  The app then parse the string and select the location accordingly.

