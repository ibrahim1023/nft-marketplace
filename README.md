# NFT-Marketplace

## Overview

The marketplace module provides an on-chain decentralized marketplace for listing and purchasing assets within the Aptos ecosystem. It enables users to list objects for sale at a fixed price and allows buyers to purchase them securely.

This module is designed for efficiency and security, leveraging the Aptos object model and smart_vector for dynamic data management. However, for optimal performance in production, off-chain indexers should be used for tracking sellers and listings instead of storing them on-chain.

## Features

Listing Assets: Sellers can list their assets for a fixed price.

Fixed Price Purchase: Buyers can purchase listed assets outright at a specified price.

Escrow Mechanism: Items are held in escrow until purchase completion.

Marketplace Management: Keeps track of sellers and their listings.

## Module Structure

### Data Structures

`MarketplaceSigner`: Governs access to the marketplace functionalities.

`Sellers`: Stores the list of active sellers.

`Listing`: Represents a listed object available for purchase.

`FixedPriceListing<CoinType>`: Associates a listing with a fixed price.

`SellerListings`: Tracks all listings created by a seller.

### Constants

`APP_OBJECT_SEED`: Seed for marketplace initialization.

`ENO_LISTING`: Error code for missing listing.

`ENO_SELLER`: Error code for missing seller.

### Entry Functions

`list_with_fixed_price<CoinType>(seller, object, price)`

Lists an object for sale at a fixed price.

`purchase<CoinType>(purchaser, object)`

Purchases an item listed at a fixed price. Transfers ownership of the object and deposits the payment into the seller’s account.

### Internal Functions

`list_with_fixed_price_internal<CoinType>(seller, object, price)`

Internal function for listing an item, ensuring proper struct initialization and storage updates.

### View Functions

`price<CoinType>(object) -> option<u64>`

Retrieves the price of a listed item.

`listing(object) -> (object::Object<object::ObjectCore>, address)`

Returns the listed object and the seller’s address.

`get_seller_listings(seller) -> vector<address>`

Retrieves all listings of a given seller.

`get_sellers() -> vector<address>`

Retrieves all active sellers in the marketplace.

## Setup and Initialization

To compile

```
aptos move compile --move-2
```

## Unit Tests

The module includes a comprehensive test suite under test_marketplace:

`test_fixed_price`: Ensures a listing can be created and purchased successfully.

`test_not_enough_coin_fixed_price`: Tests failure when a buyer has insufficient funds.

`test_no_listing`: Tests failure when attempting to purchase a nonexistent listing.

### Running Tests

To run the test suite, use the following command:

```
aptos move test
```
