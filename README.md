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

In order to call the actual API, you have to use the URL https://{{your-marketplace}}.arcadier.io/api/v2/users/{{buyerID}}/carts. Respectively, this is where you will place your marketplace domain and buyer’s user ID. 

-----------------------------------------------------------------------------------------------------------------------------

**_Response_**

The Response from the API Call will contain a lot of information regarding the addition of the item to your cart. However, please take note of the **Cart Item ID**, which should be the first ID variable you see.

<img width="1261" alt="1response" src="https://user-images.githubusercontent.com/6611854/60698356-8247ee00-9f21-11e9-88c7-2e952e096fe6.png">

-----------------------------------------------------------------------------------------------------------------------------

## Checkout - Generate Invoice and Orders from Cart

### For Buyers Only

**_Variables_**

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

-----------------------------------------------------------------------------------------------------------------------------

**_Headers_**

-----------------------------------------------------------------------------------------------------------------------------

**_Body_**

-----------------------------------------------------------------------------------------------------------------------------

**_URL_**

-----------------------------------------------------------------------------------------------------------------------------

**_Response_**

-----------------------------------------------------------------------------------------------------------------------------

## Post-Checkout - Update Payments for Invoice Number

### For Admins Only

**_Variables_**

-----------------------------------------------------------------------------------------------------------------------------

**_Headers_**

-----------------------------------------------------------------------------------------------------------------------------

**_Body_**

-----------------------------------------------------------------------------------------------------------------------------

**_URL_**

-----------------------------------------------------------------------------------------------------------------------------

**_Response_**

