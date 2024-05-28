
## eBay’s RESTful APIs

Yet another reason for using eBay’s API service is its transition from traditional API services to REST-based APIs. This shift is so profound that it alone justifies using this service. 

There are many reasons why REST-based APIs are superior to traditional services:

- **Scalability:** REST APIs are stateless, making them highly scalable and capable of handling large volumes of requests efficiently.
   
- **Atomicity of Calls:** Each API call in a RESTful system is atomic, meaning it is complete and self-contained. This simplifies error handling and ensures consistent interactions.

- **Flexibility:** REST APIs are flexible, allowing for multiple types of calls and data formats. They can adapt and evolve without breaking existing integrations.

- **Performance:** REST APIs leverage HTTP caching mechanisms, reducing server load and improving response times, leading to better overall performance.

## Sandbox Mode
Unfortunately, eBay's production API keys cannot be granted to developer simply because they want to work on a personal project, and will only be granted to companies or individuals under strict contract and monetary promise. However, eBay's generously has created and maintained a rich sandbox environment that allows developers to work/test on a simulated eBay website with all the same API's (for free)! Due to the large amount of quality item postings on sandbox eBay, this means developing this project in this environment hardly comes with any downsides!

### Signing Up to be a Developer
Signing up with eBay's developer program to access their sandbox APIs is simple and only takes a day for verification. Follow this link to sign up for API access (it's free!): [eBay Developer Program](https://developer.ebay.com/develop/get-started)

## The Right API: Buy APIs -> Browse API
With so many APIs to choose from, which one should we use? The goal is to obtain as much information about as many items as possible with minimal effort. eBay's Browse API (from the home developer page go to APIs -> RESTful APIs -> Buy APIs -> Browse API) provides the one golden call we'll need to collect tons of high-quality data: the **search** call.

Example Call Request Using search:
https://api.sandbox.ebay.com/buy/browse/v1/item_summary/search?q=watch&limit=3

Respective Output Example:
`{"itemId": "v1|110554920324|0", "title": "Szanto Heritage Aviator Watches, Black Dial, Tan Strap, Gun Gray, One : SZ 2757", "leafCategoryIds": ["31387"], "categories": [{"categoryId": "31387", "categoryName": "Wristwatches"}, {"categoryId": "281", "categoryName": "Jewelry & Watches"}, {"categoryId": "260324", "categoryName": "Watches, Parts & Accessories"}, {"categoryId": "260325", "categoryName": "Watches"}], "price": {"value": "225.00", "currency": "USD"}, "itemHref": "https://api.sandbox.ebay.com/buy/browse/v1/item/v1%7C110554920324%7C0", "seller": {"feedbackScore": 500}, "condition": "New with tags", "conditionId": "1000", "shippingOptions": [{"shippingCostType": "FIXED", "shippingCost": {"value": "0.00", "currency": "USD"}}], "buyingOptions": ["FIXED_PRICE", "BEST_OFFER"], "itemWebUrl": "http://www.sandbox.ebay.com/itm/Szanto-Heritage-Aviator-Watches-Black-Dial-Tan-Strap-Gun-Gray-One-SZ-2757-/110554920324?hash=item19bd963584:i:110554920324", "itemLocation": {"city": "Northbrook", "postalCode": "600**", "country": "US"}, "adultOnly": false, "legacyItemId": "110554920324", "availableCoupons": false, "itemCreationDate": "2024-05-02T20:25:40.000Z", ...`

## Selenium and the Description Parsing Issue
You may have noticed a very crucial detail of this output is missing, the items description we had hoped for. While in eBay's documentation it states that one of the keys called "shortDescriptions" should be returned holding short text descriptioin of the item, this wasn't the case, atleast not for virtually any sandbox items.  


## Setup

### Install External Libraries
- `selenium`
- `requests`