# Cored Onsite Payment Gateway (Cofred Credit Debit card and Mobile Money)
With Cofred, Credit/Debit card and Mobile Money options on single page to make payment.

Cofred onsite payment can be used to receive payments from Cofred, Credit/Debit Cards and Mobile Money on your website and all options will show on same time. In which user can choose whichever medium they want to make payment.

Follow the details below to implement Cofred payment button on your website.

You will need to set javascript parameters and load a Cofred Javascript library

Load Cofred library like this in your page

<script src="https://cofredpay.com/sdk/cofredall.js"></script>

https://cofredpay.com/sdk/cofredall.js is the Javascript library url.

# Required Javacript variables-

1) cfd_merchantid - Your Cofred merchant ID here.
2) cfd_accesstoken - Your Cofred access token here.
3) amount - Add amount you want to debit using the API.
4) item_name - Your Item name.
5) currency - Pass currency you want to charge user (Supported currencies GHS, NGN, USD, KES, UGX, TZS)
6) merchant_ref - Your transaction reference number to identify transaction in callbacks.
7) notify_url - Here you need to pass url where you want to receive callbacks of each transactions.
8) success_url - Pass url to redirect after payment success.
9) cancel_url - Pass url to redirect in case of payment cancellations.

# Load button at your place

You can load Cofred payment button whereever you need. You just need to add below code where you need the payment button

<div id="cofred-button-container"></div>

Or load "cofred-button-container" in your ID of any HTML tags.

# Process to receive callback

Callback is sent by POST method in Json format.

Callback sample

{
 "status":"SUCCESS",
 "merchant_ref":"HUSD34UEDFJ",
 "amount":"1000",
 "currency":2,
 "symbol":'GHS', // Sent transacted currency symbol
 "txn_reference":"HFYUERIEROI"
}

To validate callback use the process below - 

We send encrypted form of your Cofred Secret Key and Access Tokens in header of callback.

Validation code sample

$seccode=strtoupper(md5("COFRED SECRET KEY HERE")); // Coded with callback check
$accesstoken=strtoupper(md5("COFRED ACCESS TOKEN HERE")); // Coded with callback check
$header_seccode=$_SERVER["HTTP_SECRETCODE"]; // Sent with response in Header
$header_accesstoken=$_SERVER["HTTP_ACCESSTOKEN"]; // Sent with response in Header

if($seccode != $header_seccode) { return false; }

if($accesstoken != $header_accesstoken) { return false; }
