# SMART DEALS

**A Local Online Marketplace for Buying & Selling with Bids**

---

## Overview

**SMART DEALS** is a community-driven online marketplace where users can:

- Post items for sale (`Products`)
- Place bids on items (`Bids`)
- Negotiate prices through bidding
- Mark items as `sold` or keep them `pending`

> _ — think of it as your neighborhood OLX or Craigslist with a bidding system._

---

## Tech Stack

| Layer    | Technology                    |
| -------- | ----------------------------- |
| Frontend | React / HTML+CSS+JS           |
| Backend  | Node.js + Express             |
| Database | MongoDB (NoSQL)               |
| Auth     | Firebase-based Authentication |
| API      | RESTful                       |

---

## Database Collections

### 1. `Products` Collection (Product Listings)

| Field            | Type         | Description                  |
| ---------------- | ------------ | ---------------------------- |
| `_id`            | ObjectId     | Auto-generated ID            |
| `title`          | String       | Item name                    |
| `price_min`      | Number       | Minimum acceptable price     |
| `price_max`      | Number       | Maximum asking price         |
| `email`          | String       | Seller's email               |
| `category`       | String       | e.g., Electronics, Furniture |
| `created_at`     | ISODate      | Timestamp of posting         |
| `image`          | String (URL) | Item photo                   |
| `status`         | String       | `pending` / `sold`           |
| `location`       | String       | City or area                 |
| `seller_image`   | String (URL) | Seller profile pic           |
| `seller_name`    | String       | Seller’s full name           |
| `condition`      | String       | `fresh` / `used`             |
| `usage`          | String       | e.g., "6 months old"         |
| `description`    | String       | Full details                 |
| `seller_contact` | String       | Phone or contact             |

---

### 2. `Bids` Collection (Buyer Offers)

| Field           | Type         | Description             |
| --------------- | ------------ | ----------------------- |
| `_id`           | ObjectId     | Unique bid ID           |
| `product`       | ObjectId     | Reference to `Products._id` |
| `buyer_image`   | String (URL) | Buyer’s profile pic     |
| `buyer_name`    | String       | Buyer’s name            |
| `buyer_contact` | String       | Buyer’s phone           |
| `buyer_email`   | String       | Buyer’s email           |
| `bid_price`     | Number       | Offer amount            |
| `status`        | String       | `pending` / `confirmed` |

---

## API Endpoints

### **Products Endpoints**

| Method   | Endpoint                       | Description                        |
| -------- | ------------------------------ | ---------------------------------- |
| `GET`    | `/products?email=user@example.com` | Get all ads (or filter by seller)  |
| `GET`    | `/products/:id`                    | Get single ad                      |
| `POST`   | `/products`                        | Create new ad                      |
| `PUT`    | `/products/:id`                    | Update ad                          |
| `DELETE` | `/products/:id`                    | Delete ad                          |
| `PATCH`  | `/products/status/:text`           | Change status: `sold` or `pending` |

---

### **Bids Endpoints**

| Method   | Endpoint            | Description                                 |
| -------- | ------------------- | ------------------------------------------- |
| `GET`    | `/bids/:email`      | Get all bids by user                        |
| `POST`   | `/bids`             | Place a new bid                             |
| `DELETE` | `/bids/:id`         | Delete a bid                                |
| `DELETE` | `/bids/product/:id` | Delete **all bids** for a product           |
| `PATCH`  | `/bids/status/:id`  | Update bid status (`confirmed` / `pending`) |

---

## Frontend Pages

| Page             | Purpose                         |
| ---------------- | ------------------------------- |
| **Home**         | Show all active ads             |
| **Register**     | User signup                     |
| **Login**        | User login                      |
| **All-Products**     | Browse all listings             |
| **My-Products**      | View & manage your posted items |
| **My Bids**      | View bids you've placed         |
| **Products Details** | View item + place bid           |
| **Post Products**    | Create new listing              |
| **Update Products**  | Edit your ad                    |
| **Error Page**   | 404 / error handling            |

---

## User Flow Example

```text
1. Seller posts: "iPhone 13 - Used - $500-$550"
   → POST /products

2. Buyer 1 bids $510
   → POST /bids

3. Buyer 2 bids $530
   → POST /bids

4. Seller accepts Buyer 2
   → PATCH /bids/status/{bidId} → "confirmed"
   → PATCH /products/status/sold

5. System deletes other bids
   → DELETE /bids/product/{addId}
```

---

---

## License

MIT © SMART DEALS

---

> **Start dealing locally. Post. Bid. Sell.**  
> _Built for the community, by the community._

---

**SMART DEALS** – _Where every deal feels like home._
