# FTN Partner Webhooks Documentation

# Introduction

Webhooks allow us to notify your application when specific events occur. This enables you to build more interactive and responsive integrations. Below are the details for the webhooks available that you need to implement on your system.

# Table of Contents

1. [Webhooks Setup](#webhooks-setup)
2. [Available Webhooks](#available-webhooks)
    - [Ticket Hold](#ticket-hold)
    - [Ticket Release](#ticket-release)
    - [Listing Update](#listing-update)
    - [Order Update](#order-update)
    - [Order Fulfillment](#order-fulfillment)
3. [Contact Us](#contact-us)

# Webhooks Setup

To start receiving webhooks from the FTN, follow these steps:
  - **Register Your Endpoints**: Supply your webhook URLs to receive data from FTN.
  - **Ensure Endpoint Availability**: Make sure your endpoints are operational and consistently return a 200 status code.
  - **Payload Delivery**: All webhook payloads are sent via POST requests.

# Available Webhooks

## Ticket Hold

### Introduction

The `ticket.hold` webhook is triggered when a ticket hold is successfully created. This webhook provides you with detailed information about the ticket hold.

### Payload

```json
{
    "event": "ticket.hold",
    "data": [
        {
            "listing_id": "274832",
            "quantity_held": 1
        },
        {
            "listing_id": "274836",
            "quantity_held": 5
        }
    ]
}
```

[Table of Contents](#table-of-contents)

## Ticket Release

### Introduction

The `ticket.release` webhook is triggered when a previously held ticket is released. This webhook provides you with detailed information about the ticket release.

### Payload

```json
{
    "event": "ticket.release",
    "data": [
        {
            "listing_id": "274836",
            "quantity_released": 5,
            "quantity_available": 2
        },
        {
            "listing_id": "274835",
            "quantity_released": 2,
            "quantity_available": 1
        }
    ]
}
```

[Table of Contents](#table-of-contents)

## Listing Update

### Introduction

The `listing.update` webhook is triggered when there is an update to a listing. This webhook provides detailed information about the updated listing, including listing id, updated quantity, price, and any other relevant details.

### Payload
```json
{
    "event": "listing.update",
    "data": {
        "listing_id": 324694,
        "category": {
            "category_id": "3497",
            "category_name": "Central Longside Lower ",
            "description": "Central Longside Lower ",
            "seating_type": "block",
            "seating_blocks": "N1409;N1408;N1407;N1406;N1405;N2409;N2405;S126;S125;S124;S123"
        },
        "quantity": 3,
        "held_quantity": 0,
        "price": 2,
        "booking_fee": 0.6,
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
        "description": "Central Longside Lower ",
        "note": "",
        "fans_side": "",
        "block": [],
        "row": [],
        "image_point_of_view": "",
        "extra_note_hospitality": "",
        "instant_download": "",
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
```

[Table of Contents](#table-of-contents)

## Order Update

### Introduction

The `order.update` webhook is triggered whenever there is an update to an order's status. This webhook provides information about the updated order, including its status, customer details, and any other relevant information.

### Payload

```json
{
    "event": "order.update",
    "data": {
        "id": "1215843",
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
        "attendees": [
            {
                "index": 1,
                "birthdate": "10-07-2024",
                "fullname": "Test Tester",
                "passport": "1111111111111",
                "nationality": "American Samoa",
                "city_of_birth": "Test City",
                "province_of_birth": "Not in USA and Canada"
            }
        ]
    }
}
```
[Table of Contents](#table-of-contents)

## Order Fulfillment

### Introduction

The `order.fulfillment` webhook is triggered when an order is fulfilled. This webhook provides ticket files associated or links with the order, which are uploaded in base64 format. The `fulfillment_status` is marked as 'Completed' once all files/evidence are provided.

### Payload

1. Fulfill ticket files: Tickets are delivered as file (pdf or image).
```json
{
    "event": "order.fulfillment",
    "data": {
        "order_id": "1215850",
        "fulfillment_type": "file",
        "fulfillment_status": "Completed",
        "files": [
            {
                "file_name": "ticket_1.pdf",
                "file_content_base64": "JVBERi0xLjQKJ...<base64 encoded content>...=="
            },
            {
                "file_name": "ticket_2.pdf",
                "file_content_base64": "JVBERi0xLjQKJ...<base64 encoded content>...=="
            }
        ]
    }
}
```

2. Fulfill ticket links: Tickets are delivered as mobile links.
```json
{
    "event": "order.fulfillment",
    "data": {
        "order_id": "1215850",
        "fulfillment_type": "link",
        "fulfillment_status": "Completed",
        "links": [
            "https://link1.com",
            "https://link2.com"
        ]
    }
}
```
  
3. Fulfill evidence: Provide documentation or proof of ticket delivery.
```json

{
    "event": "order.fulfillment",
    "data": {
        "order_id": "1215850",
        "fulfillment_type": "evidence",
        "fulfillment_status": "Completed",
        "files": [
            {
                "file_name": "evidence_1.pdf",
                "file_content_base64": "JVBERi0xLjQKJ...<base64 encoded content>...=="
            },
            {
                "file_name": "evidence_2.pdf",
                "file_content_base64": "JVBERi0xLjQKJ...<base64 encoded content>...=="
            }
        ]
    }
}
```

[Table of Contents](#table-of-contents)

# Contact Us

If you have any questions or need further assistance, please contact our support team at support@footballticketnet.com.
