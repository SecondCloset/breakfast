# Overview
Data fetching in the rails API is built into a repository layer, which handles making the request to the third party platform, as well as serializing the response. This section will provide a breakdown of the tools used to fetch Shopify data and how to use these tools.

In all the below examples, shop is an `::Integration::Shopify::Shop` record.

## Orders
### Find all orders on a store
```ruby
  ::Integration::Shopify::OrderRepository.all(shop)
```

### Finding a specific order by Shopify ID
```ruby
  ::Integration::Shopify::OrderRepository.find(shop, shopify_order_id)
```

The Shopify order ID is the first section of the `external_order_id` of a `::Fulfillment::Order`.

### Finding a specific order by Shopify order number
```ruby
  ::Integration::Shopify::OrderRepository.all(shop, params: { name: shopify_order_number, status: :any })
```

## Products
### Find all products on a store
```ruby
  ::Integration::Shopify::ProductRepository.all(shop)
```

### Finding a specific product by Shopify ID
```ruby
  ::Integration::Shopify::ProductRepository.find(shop, shopify_product_id)
```

The Shopify product can be found on the join model `::Integration::Shopify::ShopProduct`.
*Note that this uses the Shopify **product** ID rather than the variant ID*

## Customers
### Find all customers on a store
```ruby
  ::Integration::Shopify::CustomerRepository.all(shop)
```

### Finding a specific customer by Shopify ID
```ruby
  ::Integration::Shopify::CustomerRepository.find(shop, shopify_customer_id)
```

## Locations
### Find all locations on a store
```ruby
  ::Integration::Shopify::LocationRepository.all(shop)
```

## Fulfillments
### Finding a specific fulfillment by Shopify ID
```ruby
  ::Integration::Shopify::ShipmentRepository.find(shop, shopify_order_id, shopify_fulfillment_id)
```

The Shopify order ID is the first section of the `external_order_id` of a `::Fulfillment::Order`.
The Shopify fulfillment ID is the first section of the `external_shipment_id` of a `::Logistics::Shipment`.
