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
            "total_quantity": 2,
            "held_quantity": 1
        },
        {
            "listing_id": "274836",
            "total_quantity": 8,
            "held_quantity": 5
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
            "total_quantity": 5,
            "held_quantity": 2
        },
        {
            "listing_id": "274835",
            "total_quantity": 2,
            "held_quantity": 1
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
        "event_id": 95920,
        "venue_id": 2,
        "tournament_id": 4,
        "listing_id": 324129,
        "category": {
            "category_id": "95",
            "category_name": "Executive Private Boxes :",
            "description": "Luxury Padded Seating Directly Outside Your Box.",
            "seating_type": "block",
            "seating_blocks": "Seat-Box"
        },
        "is_singles": false,
        "quantity": 20,
        "held_quantity": 0,
        "activated": 1,
        "type": "Electronic Tickets",
        "price_details": {
            "currency": "GBP",
            "price": 20000,
            "booking_fee": 6400,
            "fee_for_quantities": {
                "1-2": 45,
                "3-4": 65,
                "5-10": 85,
                "11-15": 105,
                "16-20": 155,
                "20-inf": 195
            }
        },
        "seat_details": {
            "block": "Bock 1",
            "row": "Row 1",
            "view_type": "Please Note - Tickets With a Restricted View",
            "image_point_of_view": "",
            "extra_note_hospitality": "Good hospitality boxes"
        },
        "split": {
            "split_type": "PAIRS",
            "splits": [
                2,
                4,
                6,
                8,
                10,
                12,
                14,
                16,
                18,
                20
            ]
        },
        "description": "Luxury Padded Seating Directly Outside Your Box.",
        "note": "",
        "fans_side": "",
        "instant_download": ""
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
        "order_id": "1215843",
        "date_time": "2024-07-10T15:30:00+00:00",
        "ticket_type": "Electronic Tickets",
        "currency": "EUR",
        "quantity": 1,
        "price": 150,
        "sub_total": 150,
        "booking_fee": 50,
        "grand_total": 200,
        "status": "Paid",
        "customer": {
            "first_name": "Test",
            "last_name": "Tester",
            "email": "example@email.com",
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
                "birthdate": "10-07-1985",
                "fullname": "Test Tester",
                "passport": "1234567890",
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

The `order.fulfillment` webhook is triggered when an order is fulfilled. This webhook provides ticket files or links associated with the order, which are uploaded in base64 format. The `fulfillment_status` is marked as 'Completed' once all files/evidence are provided.

### Payload

1. Fulfill ticket files: Tickets are delivered as file (pdf or image).
```json
{
    "event": "order.fulfillment",
    "data": [
         {
            "order_id": "1215850",
            "delivery_status": "e-Ticket Sent",  //See Delivery Status for more details
            "fulfillment_status": "Completed",   //See Fulfillment Status for more details
            "tickets": [
                "files": [
                    "JVBERi0xLjQKJ...<base64 encoded content>...==",
                    "JVBERi0xLjQKJ...<base64 encoded content>...=="
                ]
            ],
            "instructions": [
                "JVBERi0xLjQKJ...<base64 encoded content>...=="
            ]
        }
    ]
}
```

2. Fulfill ticket links: Tickets are delivered as general links.
```json
{
    "event": "order.fulfillment",
    "data": [
         {
            "order_id": "1215850",
            "delivery_status": "e-Ticket Sent",  //See Delivery Status for more details
            "fulfillment_status": "Completed",   //See Fulfillment Status for more details
            "tickets": [
                "links": [
                    "https://ticket.com/ticket-1.jpg",
                    "https://ticket.com/ticket-2.jpg",
                ]
            ],
            "instructions": [
                "JVBERi0xLjQKJ...<base64 encoded content>...=="
            ]
        }
    ]
}
```

3. Fulfill mobile links: Tickets are delivered as mobile links.
```json
{
    "event": "order.fulfillment",
    "data": [
         {
            "order_id": "1215850",
            "delivery_status": "e-Ticket Sent",  //See Delivery Status for more details
            "fulfillment_status": "Completed",   //See Fulfillment Status for more details
            "tickets": [
                "mobile_links": [
                    [
                        "ios": "https://ticket.com/ticket-1.ios.jpg",
                        "android": "https://ticket.com/ticket-1.android.jpg",
                    ]
                ]
            ],
            "instructions": [
                "JVBERi0xLjQKJ...<base64 encoded content>...=="
            ]
        }
    ]
}
```
4. Fulfill evidence: Provide documentation or proof of ticket delivery.
```json

{
    "event": "order.fulfillment",
    "data": [
         {
            "order_id": "1215850",
            "delivery_status": "e-Ticket Sent",  //See Delivery Status for more details
            "fulfillment_status": "Completed",   //See Fulfillment Status for more details
            "evidences": [
                "JVBERi0xLjQKJ...<base64 encoded content>...=="
            ]
        }
    ]
}
```

### Delivery Status
1. The delivery_status parameter indicates the current status of the ticket delivery process. This status informs whether the tickets have been sent to the customer and what stage the delivery is in.
2. Possible Values:
    - "None": Indicates no delivery status has been assigned.
    - "Details Sent": Details of the order or tickets have been sent to the customer.
    - "Posting Problems": There were issues encountered while posting the tickets.
    - "Posted": Tickets have been posted to the customer.
    - "Hand Delivery": Tickets will be delivered by hand.
    - "Pick Up Point": Tickets are available for pick-up at a designated location.
    - "e-Ticket": Tickets are electronic tickets.
    - "Tickets Collected": Tickets have been collected by the customer.
    - "Mobile Tickets": Tickets are delivered as mobile tickets.
    - "e-Ticket Sent": Indicates that the electronic ticket has been successfully sent to the customer.
    - "e-Ticket Emailed": Electronic tickets have been emailed to the customer.
    - "Mobile Tickets Sent": Mobile tickets have been sent to the customer.
    - "Mobile links sent": Links to mobile tickets have been sent to the customer.
    - "e-Ticket Downloaded": The customer has downloaded the electronic ticket.
    - "Mobile Tickets Delivered": Mobile tickets have been delivered to the customer.
    - "Mobile Links Downloaded": The customer has downloaded the mobile ticket links.
    - "Box Office Collection": Tickets are available for collection at the box office.
    - "Delivered": Tickets have been delivered to the customer.
    - "Order Sent": The entire order has been sent to the customer.

### Fulfillment Status
1. The fulfillment_status parameter represents the overall completion status of the order fulfillment process. It signifies whether all necessary steps and requirements for fulfilling the order have been met.
2. Possible Values:
    - "InComplete": Indicates that the order fulfillment process is incomplete. Necessary steps or materials are still outstanding.
    - "Partial": Indicates that the order fulfillment process is partially complete. Some, but not all, tickets or required materials have been delivered.
    - "Completed": Indicates that the order fulfillment process is entirely complete. This includes the successful delivery of all tickets and any other required materials or evidence.


[Table of Contents](#table-of-contents)

# Contact Us

If you have any questions or need further assistance, please contact our support team at support@footballticketnet.com.
