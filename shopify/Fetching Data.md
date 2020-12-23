- [Overview](#overview)
  * [Orders](#orders)
    + [Find all orders on a store](#find-all-orders-on-a-store)
    + [Finding a specific order by Shopify ID](#finding-a-specific-order-by-shopify-id)
    + [Finding a specific order by Shopify order number](#finding-a-specific-order-by-shopify-order-number)
    + [Printing line items of an order](#printing-line-items-of-an-order)
    + [Printing refunded line items of an order](#printing-refunded-line-items-of-an-order)
    + [Printing fulfillments (shipments) of an order](#printing-fulfillments--shipments--of-an-order)
  * [Products](#products)
    + [Find all products on a store](#find-all-products-on-a-store)
    + [Finding a specific product by Shopify ID](#finding-a-specific-product-by-shopify-id)
  * [Customers](#customers)
    + [Find all customers on a store](#find-all-customers-on-a-store)
    + [Finding a specific customer by Shopify ID](#finding-a-specific-customer-by-shopify-id)
  * [Locations](#locations)
    + [Find all locations on a store](#find-all-locations-on-a-store)
  * [Fulfillments](#fulfillments)
    + [Finding a specific fulfillment by Shopify ID](#finding-a-specific-fulfillment-by-shopify-id)


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

e.g. `2229492875367___84b4a67e-0f38-11ea-b786-9775e313c04f`, `2229492875367` is shopify order ID.

### Finding a specific order by Shopify order number
```ruby
  ::Integration::Shopify::OrderRepository.all(shop, params: { name: shopify_order_number, status: 'any' })
```

e.g. External order number `#118082`. Parameters would be `params: { name: '118082', status: 'any' }`

### Printing line items of an order
```ruby
  irb(main):165:0> order.line_items.each { |i| print [i.sku, i.name, i.variant_id, i.quantity, i.fulfillable_quantity]; puts };nil
  ["PTS-3PC-TWIN-PINSTRIPE", "Sheet Set - PINSTRIPE / Twin XL"]
  ["PFS-4PC-FULL-PINSTRIPE", "Sheet Set - PINSTRIPE / Full/Double"]
  ["PQS-4PC-QUEEN-PINSTRIPE", "Sheet Set - PINSTRIPE / Queen"]
  => nil
```

* __quantity__: total purchased quantity including refunds and shipped
* __fulfillable_quantity__: quantity available for fulfillment (excluding refunds and shipped)

### Printing refunded line items of an order
```ruby
  irb(main):166:0> order.refunds.map(&:refund_line_items).flatten.map(&:line_item).each { |i| print [i.sku, i.name, i.variant_id, i.quantity]; puts };nil
  ["PTS-3PC-TWIN-PINSTRIPE", "PINSTRIPE / Twin XL"]
  ["PFS-4PC-FULL-PINSTRIPE", "PINSTRIPE / Full/Double"]
  => nil
```

### Printing fulfillments (shipments) of an order
```ruby
  irb(main):173:0> order.shipments.map(&:line_items).flatten.map { |i| print [i.sku, i.name, i.variant_id, i.quantity]; puts };nil
  ["Return Label BC to ON", "48MP WiFi Touchscreen Kids Digital Camera + HD Video Camcorder 2 in 1 (Model K) - Model K - Zippy"]
  => nil
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
