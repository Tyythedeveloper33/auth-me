
Here’s a set of API documentation for an e-commerce store based on your SleepInn example. This includes user authentication and authorization routes, as well as some additional routes relevant to the e-commerce context such as product management, cart operations, and order management.

ECommerceStore
Database Schema Design

API Documentation
USER AUTHENTICATION/AUTHORIZATION
All Endpoints that Require Authentication
Endpoints that require a current user to be logged in.

Request: Endpoints that require authentication.
Error Response: Require Authentication
Status Code: 401
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "message": "Authentication required"
}
All Endpoints that Require Proper Authorization
Endpoints that require authentication and the current user does not have the correct role(s) or permission(s).

Request: Endpoints that require proper authorization.
Error Response: Require Proper Authorization
Status Code: 403
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "message": "Forbidden"
}
Get the Current User
Returns the information about the current user that is logged in.

Require Authentication: true

Request

Method: GET
Route Path: /api/session
Body: None
Successful Response when there is a logged-in user

Status Code: 200
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "user": {
    "id": 1,
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@gmail.com",
    "username": "JohnSmith"
  }
}
Successful Response when there is no logged-in user

Status Code: 200
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "user": null
}
PRODUCT MANAGEMENT
Get All Products
Retrieves a list of all products.

Require Authentication: false

Request

Method: GET
Route Path: /api/products
Body: None
Successful Response

Status Code: 200
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "products": [
    {
      "product_id": 1,
      "name": "Product 1",
      "description": "Description of product 1",
      "price": 19.99,
      "category_id": 2,
      "attributes": [
        {"attribute_name": "Size", "attribute_value": "L"}
      ]
    },
    ...
  ]
}
Get Product by ID
Retrieves detailed information about a specific product.

Require Authentication: false

Request

Method: GET
Route Path: /api/products/{product_id}
Body: None
Successful Response

Status Code: 200
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "product": {
    "product_id": 1,
    "name": "Product 1",
    "description": "Description of product 1",
    "price": 19.99,
    "category_id": 2,
    "attributes": [
      {"attribute_name": "Size", "attribute_value": "L"}
    ]
  }
}
CART OPERATIONS
Get Cart
Retrieves the cart of the current user.

Require Authentication: true

Request

Method: GET
Route Path: /api/carts
Body: None
Successful Response

Status Code: 200
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "cart": {
    "cart_id": 1,
    "items": [
      {
        "cart_item_id": 1,
        "product_id": 1,
        "quantity": 2
      },
      ...
    ]
  }
}
Add Item to Cart
Adds an item to the cart of the current user.

Require Authentication: true

Request

Method: POST
Route Path: /api/carts/items
Body:
json
Copy code
{
  "product_id": 1,
  "quantity": 2
}
Successful Response

Status Code: 201
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "message": "Item added to cart",
  "cart_item_id": 1
}
ORDER MANAGEMENT
Create Order
Creates a new order from the current user's cart.

Require Authentication: true

Request

Method: POST
Route Path: /api/orders
Body:
json
Copy code
{
  "shipping_address": "123 Shipping St, City, State, ZIP",
  "billing_address": "123 Billing St, City, State, ZIP"
}
Successful Response

Status Code: 201
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "message": "Order created successfully",
  "order_id": 1
}
Get Order by ID
Retrieves details about a specific order.

Require Authentication: true

Request

Method: GET
Route Path: /api/orders/{order_id}
Body: None
Successful Response

Status Code: 200
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "order": {
    "order_id": 1,
    "user_id": 1,
    "order_date": "2024-09-05T12:34:56Z",
    "total_amount": 39.98,
    "status": "Pending",
    "shipping_address": "123 Shipping St, City, State, ZIP",
    "billing_address": "123 Billing St, City, State, ZIP",
    "items": [
      {
        "order_item_id": 1,
        "product_id": 1,
        "quantity": 2,
        "price": 19.99
      }
    ]
  }
}
REVIEWS
Submit a Review
Allows a user to submit a review for a product.

Require Authentication: true

Request

Method: POST
Route Path: /api/reviews
Body:
json
Copy code
{
  "product_id": 1,
  "rating": 4.5,
  "comment": "Great product!"
}
Successful Response

Status Code: 201
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "message": "Review submitted successfully",
  "review_id": 1
}
Get Reviews for a Product
Retrieves reviews for a specific product.

Require Authentication: false

Request

Method: GET
Route Path: /api/products/{product_id}/reviews
Body: None
Successful Response

Status Code: 200
Headers:
Content-Type: application/json
Body:
json
Copy code
{
  "reviews": [
    {
      "review_id": 1,
      "user_id": 1,
      "rating": 4.5,
      "comment": "Great product!",
      "created_at": "2024-09-05T12:34:56Z"
    }
  ]
}
