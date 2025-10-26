# GET /v1beta1/flights/round-trip

## Overview

The **round-trip flights endpoint** returns flight data for a complete round-trip journey between two airports.  
You can retrieve all flight options, or filter to get the **cheapest** or **best** (based on price and layovers) results.

---

## Endpoints

| Method | Path                                                                                                                                                      | Description |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| **GET** | `/v1beta1/flights/round-trip/{from}/{to}/{departure_date}/{arrival_date}/{num_adults}/{num_kids}/{num_inf}/{cabin_class}` | Returns detailed information about round-trip flights, including price, duration, layovers, and other flight details. |
| **GET** | `/v1beta1/flights/round-trip/{from}/{to}/{departure_date}/{arrival_date}/{num_adults}/{num_kids}/{num_inf}/{cabin_class}?param=cheapest` | Returns the cheapest available round-trip flight for the given inputs. |
| **GET** | `/v1beta1/flights/round-trip/{from}/{to}/{departure_date}/{arrival_date}/{num_adults}/{num_kids}/{num_inf}/{cabin_class}?param=best` | Returns the best-scored round-trip flight based on a combination of price, number of layovers, and average layover time. |

---

## Path Parameters

| Parameter | Type | Description | Example |
|------------|------|-------------|----------|
| **from** | string | IATA code of the departure airport | `JFK` |
| **to** | string | IATA code of the destination airport | `NRT` |
| **departure_date** | string | Outbound flight date in `YYYY-MM-DD` format | `2025-12-21` |
| **arrival_date** | string | Return flight date in `YYYY-MM-DD` format | `2025-12-28` |
| **num_adults** | integer | Number of adult passengers | `1` |
| **num_kids** | integer | Number of child passengers | `0` |
| **num_inf** | integer | Number of infant passengers | `0` |
| **cabin_class** | string | Cabin class for the flight. One of: `Economy`, `Premium_Economy`, `Business`, `First` | `Economy` |

---

## Query Parameters

| Parameter | Description | Example |
|------------|-------------|----------|
| **cheapest** | Returns only the cheapest round-trip flight available for the given inputs. | `?param=cheapest` |
| **best** | Returns the best-scored round-trip flight based on a balanced evaluation of price, layovers, and layover times. | `?param=best` |

---

## Examples


Partial example response for `v1beta1/flights/round-trip/JFK/NRT/2025-10-23/2025-10-30/1/0/0/Economy`:

```json
{
  "query": {
    "market": "US",
    "currency": "USD",
    "locale": "en-GB",
    "adults": 1,
    "child_ages": [],
    "cabin_class": "economy",
    "legs": [
      {
        "origin": 12712,
        "destination": 14788,
        "date": "2025-10-23"
      },
      {
        "origin": 14788,
        "destination": 12712,
        "date": "2025-10-30"
      }
    ],
    "children": 0,
    "infants": 0
  },
  "context": {
    "request_id": "",
    "session_id": "b2645942-9526-4356-b6fe-64d1d2e51938"
  },
  "itineraries": [
    {
      "id": "12712-2510230930--32444-2-14788-2510251120__14788-3010251435--32444-2-12712-3010251930",
      "itinerary_token": "H4sIAAAAAAAA_9XLSwrCMBSFYWKpJjeCUoTW...",
      "leg_ids": [
        "12712-2510230930--32444-2-14788-2510251120",
        "14788-3010251435--32444-2-12712-3010251930"
      ],
      "pricing_options": [
        {
          "id": "xwCjC0SBPSsz",
          "agent_ids": ["oojo"],
          "price": {
            "amount": 1452.80,
            "update_status": "current",
            "last_updated": "2025-09-13T09:54:26",
            "quote_age": 64
          },
          "items": [
            {
              "agent_id": "oojo",
              "url": "/transport_deeplink/4.0/US/en-GB/USD/oojo/1/12712.14788.2025-10-23,14788.12712.2025-10-30/air/trava/flights?...",
              "segment_ids": [
                "12712-16216-2510230930-2510231245--32444",
                "16216-14788-2510240105-2510251120--32444",
                "14788-16216-3010251435-3010251740--32444",
                "16216-12712-3010251915-3010251930--32444"
              ],
              "price": {
                "amount": 1452.80,
                "update_status": "current",
                "last_updated": "2025-09-13T09:54:26",
                "quote_age": 64
              },
              "booking_proposition": "PBOOK",
              "fares": [
                { "segment_id": "12712-16216-2510230930-2510231245--32444" },
                { "segment_id": "16216-14788-2510240105-2510251120--32444" },
                { "segment_id": "14788-16216-3010251435-3010251740--32444" },
                { "segment_id": "16216-12712-3010251915-3010251930--32444" }
              ],
              "marketing_carrier_ids": [-32444]
            }
          ],
          "transfer_type": "MANAGED",
          "score": 3.8124,
          "pricing_option_fare_type": "BASE_FARE"
        },
        {
          "id": "d54XgSwPOJRu",
          "agent_ids": ["cair"],
          "price": {
            "update_status": "current",
            "last_updated": ""
          },
          "unpriced_type": "partner_not_selected"
        }
      ],
      "score": 3.81,
      "cheapest_price": {
        "amount": 1452.80,
        "update_status": "current",
        "last_updated": "2025-09-13T09:54:26",
        "quote_age": 64
      },
      "pricing_options_count": 2,
      "has_linked_pricing_options": false
    }
  ]
}

```

Partial example response for `v1beta1/flights/JFK/NRT/2025-10-23/1/0/0/Economy`:

Example response for `v1beta1/flights/round-trip/JFK/NRT/2026-04-10/2026-04-13/1/0/0/Economy?param=cheapest`:
```json
{
    "price": "475.00",
    "url": "skyscanner.com/transport_deeplink/4.0/US/en-GB/USD/skyp/1/12712.14788.2025-10-23/air/trava/flights?itinerary=flight|-32289|3237|12712|2025-10-23T06:59|13411|2025-10-23T09:34|335|-|-|-;flight|-32289|3291|13411|2025-10-23T10:50|13416|2025-10-23T12:14|84|-|-|-;flight|-30816|23|13416|2025-10-24T10:25|14788|2025-10-25T14:10|705|-|X|-&carriers=-32289,-30816&operators=-32289;-32289;-30816&passengers=1&channel=website&cabin_class=economy&fps_session_id=b2645942-9526-4356-b6fe-64d1d2e51938&ticket_price=475.00&is_npt=false&is_multipart=false&client_id=skyscanner_website&q_ids=H4sIAAAAAAAA_-OS4mIpzq4sEGLmWJEsxcxxpFih4cHT42xGTAqMAHJBFJkcAAAA|-551467528571022490|2&q_sources=JACQUARD&commercial_filters=false&q_datetime_utc=2025-09-13T06:47:57&transfer_protection=protected&pqid=true&fare_type=base_fare"
}
```

Example response for `v1beta1/flights/round-trip/JFK/NRT/2026-04-10/2026-04-13/1/0/0/Economy?param=best`:

```json
{
    "arrival":"2026-04-13T09:05:00Z",
    "avgLayoversDuration":"1h5m0s",
    "departure":"2026-04-10T09:55:00Z",
    "numOfLayovers":"1",
    "price":"1135.09",
    "score":"0.6337",
    "url":"https://skyscanner.com/transport_deeplink/4.0/US/en-GB/USD/dela/2/13554.12712.2026-04-10,12712.13554.2026-04-12/air/airli/flights?itinerary=flight|-32385|9596|13554|2026-04-10T09:55|9451|2026-04-10T12:20|85|UY58DBLA|E|BASIC-ECONOMY;flight|-32385|9348|9451|2026-04-10T13:25|12712|2026-04-10T15:25|480|UY58DBLA|E|BASIC-ECONOMY,flight|-32385|5923|12712|2026-04-12T21:00|13554|2026-04-13T09:05|425|VY9EDBLA|E|BASIC-ECONOMY\u0026carriers=-32385\u0026operators=-32132;-32132,-31697\u0026passengers=1\u0026channel=website\u0026cabin_class=economy\u0026fps_session_id=3b5d8704-5786-432c-9902-a40d0d6905fb\u0026ticket_price=1135.09\u0026is_npt=false\u0026is_multipart=false\u0026client_id=skyscanner_website\u0026q_ids=H4sIAAAAAAAA_-NS4GJJSc1JFGLm-JQpxcyxIlmh4feDc2waDQdfn2MzYlJgBABurHFtIgAAAA|-6230831681541745832|2\u0026q_sources=JACQUARD\u0026commercial_filters=false\u0026q_datetime_utc=2025-10-01T19:00:53\u0026pqid=false\u0026fare_type=base_fare"
}
```