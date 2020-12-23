- [Overview](#overview)
- [Shopify Entities](#shopify-entities)
  * [Products](#products)
  * [Inventory Items](#inventory-items)
  * [Orders](#orders)
  * [Customers](#customers)
  * [Locations](#locations)
  * [Fulfillments](#fulfillments)
- [Internal References to Shopify](#internal-references-to-shopify)
  * [Shops](#shops)
  * [Orders](#orders-1)
  * [Shipments](#shipments)
  * [Products](#products-1)

# Overview
This section breaks down the relevant entities on Shopify's side and how they relate to entities in our system.

# Shopify Entities
## Products
Products on Shopify are very similar to the products in our system. Each product is composed of multiple variants (for example a t-shirt might be broken up into multiple variants for different colors). Each product in our system should map directly to a variant if connected to Shopify.

https://shopify.dev/docs/admin-api/rest/reference/products

## Inventory Items
Inventory items are Shopify's way of certain additional information for their own products. It has a 1 to 1 relationship with Shopify's variants. Our system does not directly make use of these entities in any meaningful way. They are simply additional data for a given variant.

https://shopify.dev/docs/admin-api/rest/reference/inventory/inventoryitem

## Orders
Shopify's orders are a 1 to 1 mapping to orders in our system. Orders contain line items which are Shopify's version of our order items. The customer as well as the shipping address of the order is used to generate our order's customer and address for internal orders. Fulfillments on the order are Shopify's version of shipments in our system. Fulfillment statuses are auto set by Shopify and cannot be set by us unless we integrate with them in a way similar to ShipBob. Refunds on order items are represented in our system as removed items.

https://shopify.dev/docs/admin-api/rest/reference/orders/order

## Customers
Customer information used by us to generate internal customer/address data.

https://shopify.dev/docs/admin-api/rest/reference/customers/customer

## Locations
Shopify's locations represent a place where a store's physical inventory can be kept. This is used by Shopify to determine where their fulfillments are sourced from. When generating a fulfillment on a Shopify order, it is required for our application to specify the location where the shipment is sourced from. By default, our application takes the entire list of a store's locations and uses the first one to generate fulfillments. The client can create locations on their store that are named `Second Closet` or `Second Closet - {Facility}` and our system will use those locations instead. Our system is also able to specify a single location to use when pushing up fulfillments to Shopify through organization configurations. Shopify products must be tracked at a location in order for us to generate a fulfillment from that specific location. Location related errors include `None of the items are stocked at the new location.` and `All line items must be stocked at the same location.`.

https://shopify.dev/docs/admin-api/rest/reference/inventory/location

## Fulfillments
Shopify fulfillments are equivalent to our internal shipments. We do not have the ability to control the state of a fulfillment. Any fulfillment on Shopify's side is automatically considered to be completed. A fulfillment can contain tracking information supplied by our application.

https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillment

# Internal References to Shopify

## Shops
An organization can be connected to multiple Shopify stores through the relationship: `::Account::Organization 1->n ::Integration::Shopify::Shop`. The shop is the main way our application fetches data and communicates with Shopify.

## Orders
A fulfillment order is connected to Shopify if its `platform` field is `shopify`. The order will have an `external_order_id` with format `{Shopify order ID}___{::Integration::Shopify::Shop ID}`.

## Shipments
A fulfillment order is connected to Shopify if its external (fulfillment) order's  `platform` field is `shopify`. The shipment will have an `external_shipment_id` with format `{Shopify fulfillment ID}___{::Integration::Shopify::Shop ID}`.

## Products
A fulfillment product is linked to shopify products through the join model `{::Integration::Shopify::ShopProduct}`.

This join model contains 3 main pieces of Shopify data:
1. Shopify's product ID
2. Shopify's variant ID
3. Shopify's SKU

When an order syncs into our system, this join model is used to determine which products to use for the order.