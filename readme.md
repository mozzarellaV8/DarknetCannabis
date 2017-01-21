# Black Market Cannabis Analysis

Logistic Regression Classification model to predict cannabis quality on darknet markets.


## Motivations

In times of political uncertainty, what can be learned from something that is inherently uncertain? 

As legalized/de-criminalized use of cannabis grows, darknet markets might serve as a proto-model of how marijuana e-commerce can be conducted. Conversely, as policies have begun to change under a new presidential administration, darknet markets might grow as a primary means for clients to acquire cannabis. 

Is it possible to make reasonable estimates on the quality of cannabis offered on darknet markets? 
How does darknet cannabis compare to other markets in terms of price? What other factors might influence quality? How do location, asking price, bitcoin-USD exchange rate, and textual features contribute to quality? 

## On Darknet Markets

**Client feedback plays a central role for inferring the reputability of a darknet vendor, and by extension, the quality of the product. There is incentive for both vendor and client for honest feedback to be submitted.**

Darknet markets face issues that largely have been resolved in clearnet e-commerce - stability, trust in products and payment processes. The trade-off is anonymity, which provides the freedom to buy and sell products outside the law. 

Because of these issues, client feedback plays an important role in vendor reputability. A vendor without a history of good client feeback would generally appear as a risk to any potential client. With anonymity also comes the potential for scams - be it a vendor disappearing with payment without delivering, the client doing the same, or the market simply disappearing overnight. To address this the first two issues, different payment options emerged:

- FE, or finalize early - a client agrees to pay in advance for any product ordered. This method poses significant risk for the client, and generally can only be enforced by vendors with _very_ strong reputations - long transaction histories with total positive feedback.

- Escrow - where a third party arbiter (generally the market themselves) holds client payment in escrow until the product is delivered. Generally, this has been seen as the most 'trustworthy' method of doing business, where risk is spread to both client and vendor.

_a broad overview of Categories, Subcategories, and Locations:_

![catmap01](http://pi.mozzarella.website/BMC/EDA-CatMap.png)
 

# The Data

The data comes courtesy of [Black Market Archives](http://www.gwern.net/Black-market%20archives), specifically raw crawls of HTML pages on the market Agora from January 2014 through July 2015. Data was extracted using `rvest` across a series of directories, culminating in a single bound dataframe comprising approximately 2.3 million observations of 11 variables. 

## Variables Provided

- date 
- URL  
- vendor  
- product listing - _resembles Craigslist headlines_
- price in Bitcoin
- category, subcategory, and sub-subcategory of product
- origin location - _where a vendor is shipping from_
- shipping destinations - _where a vendor is willing to ship to_
- client feedback
- vendor bio - _in progress_
- vendor verification* - _in progress_ - binary - _a vendor will either be registered, or will have the added bonus of being vouched for on another darknet market._

## Variables Derived

- price in USD - _via daily BTC-USD exchange rate_
- feedback score - assigned ordinal values, as feedback is left on a 0-5 scale along with description.

**Text Features**

Given the importance of feedback, these are features to be derived from 3 possible textual fields: product listing, product description, client feedback, and vendor bio. The goal is to create quantitative variables that might provide reasonable metrics for cannabis quality. 

- word count 
- word frequency
- sentiment scores
- TF-IDF

The high level category _Cannabis_ is divided into 5 subcategories: _weed_, _synthetics_, _seeds_, _hash_, _edibles_, and _concentrates_. Can a topic model be fit to observe textual trends or features within these finer grain categories? 

**Variables Added: Price Indices**

The reason behind comparing cannabis prices to the High Times index is to see if price might be a factor in darknet transactions. Gold and oil prices were added to test the idea of cannabis as a commodity. 

- THMQ - High Times monthly survey of marijuana prices per ounce: overall index, Kind, Mids, Schwag
- corresponding price for ounce of gold
- corresponding price for barrel of WTI crude oil 
- price for barrel of Brent crude oil
- US retail electricy prices - _in progress_


