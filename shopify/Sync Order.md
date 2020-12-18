# Overview
This section will guide you through how to resync shopify orders via `rails` console. This guide is based on the implementation of `app/workers/integrations/shopify/webhooks/orders_create_or_update_job.rb`

### 1. Get Fulfillment Order
```ruby
fo = Fulfillment::Order.find('xxxx')
```
### 2. Get Shopify Shop
```ruby
# please beware that some clients have multiple shops
shop = fo.organization.integration_shopify_shops.first
```

### 3. Get Shopify Order
```ruby
order = Integration::Shopify::OrderRepository.find(shop, `external_order_id`)
or
order = Integration::Shopify::OrderRepository.all(shop, params: { name: `external_order_number`, status: :any })
```

### 4. Collect products and customer details
```ruby
# collection products and customer data through API (we do not use data from webhook)
products = Integration::Shopify::ProductRepository.all(shop, params: {
    ids: order.line_items.map(&:product_id).uniq.join(',')
})
customer = Integration::Shopify::CustomerRepository.find(shop, order.customer.id)
```

### 5. Initiate Shopify order sync
```ruby
# initiate order sync
result = Integrations::Shopify::SyncShop.call(
    shop: shop,
    user: shop.organization.users.first,
    organization: shop.organization,
    shopify_orders: [order],
    shopify_products: products,
    shopify_customers: [customer],
    skip_external_system_notification: true,
    send_sync_result_email: false
);nil
```

### 6. Result
```ruby
# If any error occurs, sendgrid email will be fired with error messages
# you can explicitly check the result
result.success?
```