![Arcadier](https://theme.zdassets.com/theme_assets/2008942/9566e69f67b1ee67fdfbcd79b1e580bdbbc98874.svg "Arcadier")

## How to Use API calls to Checkout a Bespoke item

This guide is intended to assist users on the generic process of using our API calls to Checkout a Bespoke item. Make sure to pay close attention to all minor details as all the information you give and receive can be sensitive. The slightest change in detail can change the entire order of your checkout. Please take note that this document will be using Postman to call APIs, therefore your method of calling APIs may be different. All body paragraphs sent for API calls will be in JSON.

<img width="1433" alt="pre" src="https://user-images.githubusercontent.com/6611854/60698351-7f4cfd80-9f21-11e9-8400-02b392d36492.png">

-----------------------------------------------------------------------------------------------------------------------------

## Pre-Checkout - Add Item to Cart

### For Buyers Only

**_Variables_**

The first step to checking out a Bespoke item would be adding that specific item to your cart. The necessary information that you need before calling the Pre-Checkout API would be:
 * {{your-marketplace} → Your marketplace domain
 * {{buyerID}} → the Buyer’s (your) user ID
 * {{buyertoken}} → the Buyer’s (your) token
 * The Item’s ID
	* Note that if an Item has any variance, this ID should be the ID of the specific variant of your item, NOT the 	generic item ID itself
 * Shipping Method’s ID
	* You can simply call another API “Get Shipping Methods” to obtain the ID
 	* If you do not have one, you can also call another API “Create a shipping Method” to create one

-----------------------------------------------------------------------------------------------------------------------------

**_Headers_**

For the authorization, you will need your Buyer’s token and allocate Authorization with the value as “Bearer {{buyertoken}}”. 

<img width="1262" alt="1 header" src="https://user-images.githubusercontent.com/6611854/60698352-81af5780-9f21-11e9-9736-88f1d6d6fe83.png">

-----------------------------------------------------------------------------------------------------------------------------

**_Body_**

The Body of your API call should follow the following structure:
 * ItemDetail
	 * ID: (The Item’s ID)
 * Quantity: Number of items you want
 * CartItemType: “delivery”
 * ShippingMethod
	 * ID: (Shipping Method’s ID)
Please follow the illustration below with your own information.

<img width="1266" alt="1body" src="https://user-images.githubusercontent.com/6611854/60698354-81af5780-9f21-11e9-8f8b-e19e3b2de679.png">

-----------------------------------------------------------------------------------------------------------------------------

**_URL_**

In order to call the actual API, you have to use the URL 
_https://{{your-marketplace}}.arcadier.io/api/v2/users/{{buyerID}}/carts_
Respectively, this is where you will place your marketplace domain and buyer’s user ID. 

-----------------------------------------------------------------------------------------------------------------------------

**_Response_**

The Response from the API Call will contain a lot of information regarding the addition of the item to your cart. However, please take note of the **Cart Item ID**, which should be the first ID variable you see.

<img width="1261" alt="1response" src="https://user-images.githubusercontent.com/6611854/60698356-8247ee00-9f21-11e9-88c7-2e952e096fe6.png">

-----------------------------------------------------------------------------------------------------------------------------

## Checkout - Generate Invoice and Orders from Cart

### For Buyers Only

**_Variables_**

After adding the item to your cart, it makes chronological sense for the next step to be checking out the cart. To do so, you will need the following variables:
 * {{your-marketplace} → Your marketplace domain
 * {{buyerID}} → the Buyer’s (your) user ID
 * {{buyertoken}} → the Buyer’s (your) token
 * The Cart Item ID
	 * This is the ID that you should have gotten from the previous API call (Pre-Checkout)

-----------------------------------------------------------------------------------------------------------------------------

**_Headers_**

-----------------------------------------------------------------------------------------------------------------------------

**_Body_**

-----------------------------------------------------------------------------------------------------------------------------

**_URL_**

-----------------------------------------------------------------------------------------------------------------------------

**_Response_**

-----------------------------------------------------------------------------------------------------------------------------

## Post-Checkout - Edit Order Details

### For Merchants Only, to Update Orders on their side after Receiving Money

**_Variables_**

After receiving a response from the payment gateway API, take note of the following variables as the next step is the post-checkout API to edit your order details:
 * {{your-marketplace} → Your marketplace domain
 * {{merchantID}} → the Merchant’s user ID
 * {{merchanttoken}} → the authorization token of the Merchant
 * The Order ID
	 * This is the ID that you should have gotten from the previous API call (Checkout)
 * The Address ID
	 * This is the ID of the Buyer’s address
	 * You can simply call another API “User Address” to obtain the ID

-----------------------------------------------------------------------------------------------------------------------------

**_Headers_**

-----------------------------------------------------------------------------------------------------------------------------

**_Body_**

The Body of your API call should follow the following structure:
 * FulfilmentStatus: “Acknowledged” if the item has not reached the buyer yet
	 * “Delivered” if the item has reached the buyer
 * PaymentStatus: “Paid” if the buyer has paid
	 * “Acknowledged” if the buyer has ordered and the seller has seen the order
	 * “Processing” if the payment is being processed
	 * “Waiting for Payment” if the buyer has ordered and use cash on delivery payments
	 * “Pending” if awaiting payment
	 * “Failed” if payment failed
	 * “Refunded” if payment was refunded
 * Balance: Set to the amount of money you have NOT received yet for the item
	 * For example, if the item cost $100 but you have received $40, this value should be 60
 * DeliveryToAddress
	 * ID: The Address ID
 * CartItemType: “delivery”
Please follow the illustration below with your own information

-----------------------------------------------------------------------------------------------------------------------------

**_URL_**

-----------------------------------------------------------------------------------------------------------------------------

**_Response_**

-----------------------------------------------------------------------------------------------------------------------------

## Post-Checkout - Update Payments for Invoice Number

### For Admins Only

**_Variables_**

This API call is only for Admins to update payments for the invoice number (may possibly consist of multiple Order IDs). This step requires a lot of the variables from the previous API calls, so please take note of the following variables carefully:
 * {{your-marketplace} → Your marketplace domain
 * {{adminID}} → the Admin’s user ID
 * {{admintoken}} → the authorization token of the Admin
 * The Invoice ID
	 * This is the ID that you should have gotten from the Checkout API call
	 * Keep in mind, this is different than the Order ID
 * Buyer’s user ID
 * Merchant’s user ID
 * The Order ID

-----------------------------------------------------------------------------------------------------------------------------

**_Headers_**

-----------------------------------------------------------------------------------------------------------------------------

**_Body_**

The first few lines of the Body of your API call should follow the following structure:
 * InvoiceNo: The Invoice ID
 * Payer
	 * ID: The Buyer’s user ID
 * Payee
	 * ID: The Merchant’s user ID
 * Order
	 * ID: The Order ID
 * Status: "Success" (read below)

-----------------------------------------------------------------------------------------------------------------------------

**_URL_**

-----------------------------------------------------------------------------------------------------------------------------

**_Response_**

