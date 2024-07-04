# FTN Partner API Documentation

Before integrating with the FTN Partner API, you must contact us to become a partner. Once approved, you'll gain access to our resources to configure your API integration with our system.

# Table of Contents

1. [Authentication](#authentication)
2. [Feed Endpoints](#feed-endpoints)
   - [Tournaments](#tournaments)
   - [Teams](#teams)
   - [Venues](#venues)
   - [Events](#events)
   - [Listings](#listings)
3. [Ticket Endpoints](#ticket-endpoints)
   - [Ticket Detail](#ticket-detail)
   - [Hold Tickets](#hold-tickets)
   - [Update Tickets](#update-tickets)
   - [Release Tickets](#release-tickets)
4. [Order Endpoints](#order-endpoints)
   - [Add New Order](#add-new-order)
   - [Update Order](#update-order)
5. [Error Codes](#error-codes)
6. [Contact](#contact)
7. [License](#license)

# Authentication

To successfully access the FTN Partner API, you must provide a valid hash key as a query parameter in your request, along with your registered email and current timestamp.

### Example Request

```php
{{ftn_domain}}/reseller/api/order/update?u=your@email.com&s=44b777745ad5ca4fc9dba0f6d081706fb57bf940c61&ts=1719394313
```
- u: Your registered email on our system.
- s: Hash key
- ts: Current server timestamp.

### How to build hash key

The hash key is generated by hashing a concatenated string of your email, action, timestamp, and secret key.

Example in PHP

```php
$hash_key = hash('sha256', "$email-$action-$timestamp-$secret");
```
- email: Your registered email
- action: Current API endpoint being called.
- timestamp: Current server timestamp (should match the s parameter).
- secret: Secret key provided during account registration.

[Table of Contents](#table-of-contents)

# Feed Endpoints

### Tournaments

- **Endpoint:** `/reseller/api/feed/tournaments`
- **Method:** `GET`
- **Description:** Search for tournaments.
- **Request Params:**
  - `name: Search tournaments by name (optional)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": [
        {
            "tournament_id": "2725",
            "name": "Euro 2024"
        },
        {
            "tournament_id": "2274",
            "name": "Europa Conference League"
        },
        {
            "tournament_id": "209",
            "name": "Europa League"
        }
    ],
    "total": 2
}
```

[Table of Contents](#table-of-contents)

### Teams

- **Endpoint:** `/reseller/api/feed/teams`
- **Method:** `GET`
- **Description:** Search for teams.
- **Request Params:**
  - `name: Search teams by name (optional)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": [
        {
            "team_id": "2309",
            "name": " Barcelona Legends"
        },
        {
            "team_id": "2836",
            "name": " FC Swift Hesperange"
        },
        {
            "team_id": "139",
            "name": "1. FC Koln"
        }
    ],
    "total": 3
}
```

[Table of Contents](#table-of-contents)

### Venues

- **Endpoint:** `/reseller/api/feed/venues`
- **Method:** `GET`
- **Description:** Search for venues.
- **Request Params:**
  - `name: Search venues by name (optional)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": [
        {
            "venue_id": "274",
            "venue_name": "Farum Park",
            "capacity": "10300",
            "categories": [
                {
                    "category_id": "302",
                    "name": "Best Available",
                    "blocks": "",
                    "sub_categories": []
                },
                {
                    "category_id": "320",
                    "name": "Category 2:",
                    "blocks": "",
                    "sub_categories": []
                }
            ]
        }
    ],
    "total": 1
}
```

[Table of Contents](#table-of-contents)

### Events

- **Endpoint:** `/reseller/api/feed/events`
- **Method:** `GET`
- **Description:** Search for events.
- **Request Params:**
  - `event_name: Search events by name (optional)`
  - `id: Search event by id (optional)`
  - `from_date: Search by date (optiontal)`
  - `to_date: Search by date (optional)`
  - `home_team_name: Search by home team (optional)`
  - `away_team_name: Search by away team (optional)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": [
        {
            "id": "95920",
            "name": "Manchester United vs Brentford",
            "date": "2023-10-07 19:00:00",
            "min_price": {
                "price": "2.00",
                "currency_code": "GBP"
            },
            "venue": {
                "venue_id": "2",
                "venue_name": "Old Trafford",
                "venue_city_name": "Manchester",
                "venue_country_name": "United Kingdom",
                "categories": [
                    {
                        "category_id": "6",
                        "name": "Away Section :",
                        "blocks": "0E132,0E232,0E231,0E230",
                        "sub_categories": []
                    },
                    {
                        "category_id": "49",
                        "name": "Salford Suite:",
                        "blocks": "",
                        "sub_categories": []
                    }
                ]
            },
            "tour": {
                "id": "4",
                "name": "Premier League",
                "nice_name": "English Barclays Premier League",
            },
            "team1": {
                "id": "3",
                "name": "Manchester United",
                "t1_nice_name": "Man United"
            },
            "team2": {
                "id": "539",
                "name": "Brentford",
                "t2_nice_name": "Brentford FC"
            }
        }
    ],
    "total": 1
}
```

[Table of Contents](#table-of-contents)

### Listings

- **Endpoint:** `/reseller/api/feed/listings`
- **Method:** `GET`
- **Description:** Search for listings.
- **Request Params:**
  - `event_id: Event id (required)`
  - `listing_id: Search by listing id (optional)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": [
        {
            "listing_id": 324132,
            "category": {
                "category_id": "3493",
                "category_name": "Longside Lower Level ",
                "description": "Longside Lower Level ",
                "seating_type": "block",
                "seating_blocks": "N1413;N1411;N1410;N1404;N1403;N1401;N2413;N2412;N2411;N2410;N2404;N2403;N2402;N2401;S128;S127;S229;S228;S227;S122;S121;WL0;W212;W211;W210"
            },
            "quantity": 3,
            "held_quantity": 0,
            "price": 234,
            "booking_fee": 74.88,
            "currency_code": "GBP",
            "activated": 1,
            "type": "Electronic Tickets",
            "split_type": "ANY",
            "splits": [
                1,
                2,
                3
            ],
            "view_type": "Tickets With a Clear View",
            "is_singles": false,
            "description": "Longside Lower Level ",
            "note": "",
            "fans_side": "",
            "block": [],
            "row": [],
            "image_point_of_view": "",
            "extra_note_hospitality": "",
            "instant_download": "link",
            "fee_for_quantities": {
                "1-2": 45,
                "3-4": 65,
                "5-10": 85,
                "11-15": 105,
                "16-20": 155,
                "20-inf": 195
            }
        }
    ],
    "total": 1
}
```

[Table of Contents](#table-of-contents)

# Ticket Endpoints

### Ticket Detail

- **Endpoint:** `/reseller/api/ticket/listing`
- **Method:** `GET`
- **Description:** Get listing information (with event details).
- **Request Params:**
  - `listing_id: Id of listing (required)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": {
        "id": "95920",
        "name": "Manchester United vs Brentford",
        "date": "2023-10-07 19:00:00",
        "min_price": {
            "price": "2.00",
            "currency_code": "GBP"
        },
        "venue": {
            "venue_id": "2",
            "venue_name": "Old Trafford",
            "venue_city_name": "Manchester",
            "venue_country_name": "United Kingdom",
            "categories": [
                {
                    "category_id": "6",
                    "name": "Away Section :",
                    "blocks": "0E132,0E232,0E231,0E230",
                    "sub_categories": []
                },
                {
                    "category_id": "49",
                    "name": "Salford Suite:",
                    "blocks": "",
                    "sub_categories": []
                }
            ]
        },
        "tour": {
            "id": "4",
            "name": "Premier League",
            "nice_name": "English Barclays Premier League",
        },
        "team1": {
            "id": "3",
            "name": "Manchester United",
            "t1_nice_name": "Man United"
        },
        "team2": {
            "id": "539",
            "name": "Brentford",
            "t2_nice_name": "Brentford FC"
        },
        "fans_sides": [],
        "listing_info": {
            "listing_id": 324132,
            "category": {
                "category_id": "3493",
                "category_name": "Longside Lower Level ",
                "description": "Longside Lower Level ",
                "seating_type": "block",
                "seating_blocks": "N1413;N1411;N1410;N1404;N1403;N1401;N2413;N2412;N2411;N2410;N2404;N2403;N2402;N2401;S128;S127;S229;S228;S227;S122;S121;WL0;W212;W211;W210"
            },
            "quantity": 3,
            "held_quantity": 0,
            "price": 234,
            "booking_fee": 74.88,
            "currency_code": "GBP",
            "activated": 1,
            "type": "Electronic Tickets",
            "split_type": "ANY",
            "splits": [
                1,
                2,
                3
            ],
            "view_type": "Tickets With a Clear View",
            "is_singles": false,
            "description": "Longside Lower Level ",
            "note": "",
            "fans_side": "",
            "block": [],
            "row": [],
            "image_point_of_view": "",
            "extra_note_hospitality": "",
            "instant_download": "link",
            "fee_for_quantities": {
                "1-2": 45,
                "3-4": 65,
                "5-10": 85,
                "11-15": 105,
                "16-20": 155,
                "20-inf": 195
            }
        }
    }
}
```

[Table of Contents](#table-of-contents)


### Hold Tickets

- **Endpoint:** `/reseller/api/ticket/hold`
- **Method:** `GET`
- **Description:** Get hold tickets for adding order.
- **Request Params:**
  - `listing_id: Id of listing (required)`
  - `quantity: The quantity of tickets (required)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": {
        "hold_id": "9",
        "held_quantity": 1,
        "quantity_available": 2
    }
}
```

[Table of Contents](#table-of-contents)

### Update Tickets

- **Endpoint:** `/reseller/api/ticket/hold/update`
- **Method:** `GET`
- **Description:** Update the hold quantity of a ticket.
- **Request Params:**
  - `hold_id: Id of the hold ticket (required)`
  - `quantity: The quantity of ticket holds to update (required).`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": {
        "hold_id": "9",
        "held_quantity": "3",
        "quantity_available": 0
    }
}
```

[Table of Contents](#table-of-contents)

### Release Tickets

- **Endpoint:** `/reseller/api/ticket/release`
- **Method:** `GET`
- **Description:** Release hold ticket.
- **Request Params:**
  - `hold_id: Id of the hold ticket (required)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": {
        "status": true
    }
}
```

# Order Endpoints


### Add New Order

- **Endpoint:** `/reseller/api/order/add`
- **Method:** `POST`
- **Description:** Add new order.
- **Post Params:**
  - `hold_id: The id of the hold ticket (required)`
  - `ticket[listing_id]: The id of listing (required)`
  - `ticket[quantity]: The order quantity (required)`
  - `ticket[price]: The price of ticket (required)`
  - `ticket[block]: The price of ticket (optional)`
  - `ticket[row]: The price of ticket (optional)`
  - `customer[first_name]: Customer's first name (required)`
  - `customer[last_name]: Customer's last name (required)`
  - `customer[email]: Customer's email (required)`
  - `customer[phone]: Customer's phone (required)`
  - `customer[country]: Customer's country (optional)`
  - `customer[state]: Customer's state (optional)`
  - `customer[city]: Customer's city (optional)`
  - `customer[address]: Customer's address (optional)`
  - `customer[postal_code]: Customer's postal_code (optional)`
  - `order_status: Order Status (required). Should be New/Paid`
  - `currency: Currency, it should be the same as event (required)`
  - `date_time: Purchase date, the date in ISO-8601 UTC Format (required)`
  - `total_amount: The order's total value (required)`
  - `note: Order note (optional)`
- **Response:**
```json
{
    "isSuccessful": true,
    "data": {
        "id": "1215850",
        "date_time": "2024-07-10T15:30:00+00:00",
        "quantity": 1,
        "ticket_type": "Electronic Tickets",
        "currency": "EUR",
        "sub_total": 133.99,
        "booking_fee": 49866.01,
        "grand_total": 50000,
        "status": "Paid",
        "customer": {
            "first_name": "Test",
            "last_name": "Tester",
            "email": "admin@google.com",
            "phone": "0123456789",
            "postal_code": null,
            "city": null,
            "state": null,
            "country": null,
            "address": null
        },
        "event": {
            "event_id": "98454",
            "event_name": "FC Barcelona vs Atletico Madrid",
            "event_date": "2024-07-11T14:00:00+00:00",
            "home_team": "FC Barcelona",
            "away_team": "Atletico Madrid",
            "location": "Wanda Metropolitano, Madrid, Spain"
        },
        "ticket": {
            "listing_id": "274836",
            "category_name": "Category 3",
            "description": "<ul><li>Long Side Upper Tier Tickets.</li><li>Seating in Pairs Guaranteed</li><li>Tickets With a Clear View</li></ul>",
            "fans_side": "FC Barcelona Fans"
        },
        "attendees": []
    }
}
```

[Table of Contents](#table-of-contents)

### Update Order

- **Endpoint:** `/reseller/api/order/update`
- **Method:** `GET`
- **Description:** Update existing order's status.
- **Request Params:**
  - `order_id: Id of the order (required)`
  - `order_status: New status of the order (required). Accept: Paid/Cancelled`
- **Response:** Order object or error message

[Table of Contents](#table-of-contents)
