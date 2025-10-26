# GET /v1beta1/flights

## Overview

The **one-way flights endpoint** returns flight data for a single trip between two airports.  
You can retrieve all available flights, or filter to get the **cheapest** or **best** option based on multiple factors.

---

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| **GET** | `/v1beta1/flights/{from}/{to}/{date}/{num_adults}/{num_kids}/{num_inf}/{cabin_class}` | Returns detailed information about one-way flights, including price, duration, layovers, and other flight details. |
| **GET** | `/v1beta1/flights/{from}/{to}/{date}/{num_adults}/{num_kids}/{num_inf}/{cabin_class}?param=cheapest` | Returns the cheapest available one-way flight for the given inputs. |
| **GET** | `/v1beta1/flights/{from}/{to}/{date}/{num_adults}/{num_kids}/{num_inf}/{cabin_class}?param=best` | Returns the best-scored one-way flight based on a combination of price, number of layovers, and average layover time. |

---

## Path Parameters

| Parameter | Type | Description | Example |
|------------|------|-------------|----------|
| **from** | string | IATA code of the departure airport | `JFK` |
| **to** | string | IATA code of the destination airport | `LAX` |
| **date** | string | Flight date in `YYYY-MM-DD` format | `2025-12-21` |
| **num_adults** | integer | Number of adult passengers | `1` |
| **num_kids** | integer | Number of child passengers | `0` |
| **num_inf** | integer | Number of infant passengers | `0` |
| **cabin_class** | string | Cabin class for the flight. One of: `Economy`, `Premium_Economy`, `Business`, `First` | `Economy` |

---

## Query Parameters

| Parameter | Description | Example |
|------------|-------------|----------|
| **cheapest** | Returns only the cheapest one-way flight available for the given inputs. | `?param=cheapest` |
| **best** | Returns the best-scored one-way flight based on a balanced evaluation of price, layovers, and layover times. | `?param=best` |

---

## Examples

Partial example response for `v1beta1/flights/JFK/NRT/2025-10-23/1/0/0/Economy`:
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
        "alternative_origins": [],
        "destination": 14788,
        "alternative_destinations": [],
        "date": "2025-10-23"
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
      "id": "12712-2510230930--32444-2-14788-2510251120",
      "itinerary_token": "H4sIAAAAAAAA_2XMSwrCMBSFYWKpJjeCUoTWDiToJAiF9iY3j44ci93_GgQX4TO14ug_Z_LBjcEAADwSOWopFK_tvCHva8mvqzVUpRJ6tx_PUjfHeWPQWovPUjR9huhP7DzjDC4wIQoJosPgnG_JJq9STOfJ26pcH368R3tmPtoAU2HkQgixFklYfDGpN39Y1kV8c3dTj3wy7wAAAA==",
      "leg_ids": [
        "12712-2510230930--32444-2-14788-2510251120"
      ],
      "pricing_options": [
        {
          "id": "xwCjC0SBPSsz",
          "agent_ids": [
            "oojo"
          ],
          "price": {
            "amount": 811.96,
            "update_status": "current",
            "last_updated": "2025-09-13T09:54:26",
            "quote_age": 64
          },
          "unpriced_type": "",
          "items": [
            {
              "agent_id": "oojo",
              "url": "/transport_deeplink/4.0/US/en-GB/USD/oojo/1/12712.14788.2025-10-23/air/trava/flights?itinerary=flight|-32444|227|12712|2025-10-23T09:30|16216|2025-10-23T12:45|375|-|-|-;flight|-32444|3|16216|2025-10-24T01:05|17075|2025-10-25T05:35|810|-|-|-;flight|-32444|192|17075|2025-10-25T07:00|14788|2025-10-25T11:20|200|-|-|-&carriers=-32444&operators=-32593;-32444;-32444&passengers=1&channel=website&cabin_class=economy&fps_session_id=b2645942-9526-4356-b6fe-64d1d2e51938&ticket_price=811.96&is_npt=false&is_multipart=false&client_id=skyscanner_website&q_ids=H4sIAAAAAAAA_-OS4mLJz8_KF2LmWJEsxcxxpFih4cHT42xGTAqMAP5HVsocAAAA|2586879230578014412|2&q_sources=JACQUARD&commercial_filters=false&q_datetime_utc=2025-09-13T09:54:26&pqid=true&fare_type=base_fare",
              "segment_ids": [
                "12712-16216-2510230930-2510231245--32444",
                "16216-17075-2510240105-2510250535--32444",
                "17075-14788-2510250700-2510251120--32444"
              ],
              "price": {
                "amount": 811.96,
                "update_status": "current",
                "last_updated": "2025-09-13T09:54:26",
                "quote_age": 64
              },
              "booking_proposition": "PBOOK",
              "transfer_protection": "",
              "max_redirect_age": 10,
              "fares": [
                {
                  "segment_id": "12712-16216-2510230930-2510231245--32444"
                },
                {
                  "segment_id": "16216-17075-2510240105-2510250535--32444"
                },
                {
                  "segment_id": "17075-14788-2510250700-2510251120--32444"
                }
              ],
              "opaque_id": "-1165616559",
              "booking_metadata": {
                "metadata_set": "",
                "signature": ""
              },
              "ticket_attributes": [],
              "flight_attributes": [],
              "discount_category": "DISCOUNT_CATEGORY_UNSPECIFIED",
              "marketing_carrier_ids": [
                -32444
              ]
            }
          ],
          "transfer_type": "MANAGED",
          "score": 2.56741,
          "pricing_option_fare": {
            "attribute_labels": [],
            "leg_details": {},
            "brand_names": [],
            "added_attribute_labels": []
          },
          "pricing_option_fare_type": "BASE_FARE"
        },
        {
          "id": "d54XgSwPOJRu",
          "agent_ids": [
            "cair"
          ],
          "price": {
            "update_status": "current",
            "last_updated": ""
          },
          "unpriced_type": "partner_not_selected",
          "items": [
            {
              "agent_id": "cair",
              "url": "/transport_deeplink/4.0/US/en-GB/USD/cair/1/12712.14788.2025-10-23/air/airli/flights_np?itinerary=flight|-32444|227|12712|2025-10-23T09:30|16216|2025-10-23T12:45|375|-|-|-;flight|-32444|3|16216|2025-10-24T01:05|17075|2025-10-25T05:35|810|-|-|-;flight|-32444|192|17075|2025-10-25T07:00|14788|2025-10-25T11:20|200|-|-|-&carriers=-32444&operators=-32593;-32444;-32444&passengers=1&channel=website&cabin_class=economy&fps_session_id=b2645942-9526-4356-b6fe-64d1d2e51938&is_npt=false&is_multipart=false&client_id=skyscanner_website&pqid=false&fare_type=base_fare",
              "segment_ids": [
                "12712-16216-2510230930-2510231245--32444",
                "16216-17075-2510240105-2510250535--32444",
                "17075-14788-2510250700-2510251120--32444"
              ],
              "price": {
                "update_status": "current",
                "last_updated": ""
              },
              "booking_proposition": "PBOOK",
              "transfer_protection": "",
              "max_redirect_age": 10,
              "fares": [],
              "opaque_id": "-220745125",
              "booking_metadata": {
                "metadata_set": "",
                "signature": ""
              },
              "ticket_attributes": [],
              "flight_attributes": [],
              "discount_category": "DISCOUNT_CATEGORY_UNSPECIFIED",
              "marketing_carrier_ids": [
                -32444
              ]
            }
          ],
          "transfer_type": "MANAGED",
          "pricing_option_fare": {
            "attribute_labels": [],
            "leg_details": {},
            "brand_names": [],
            "added_attribute_labels": []
          },
          "pricing_option_fare_type": "BASE_FARE"
        }
      ],
      "score": 2.56356,
      "cheapest_price": {
        "amount": 811.96,
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


Example response for `v1beta1/flights/JFK/NRT/2025-10-23/1/0/0/Economy?param=cheapest`:
```json
{
    "price": "475.00",
    "url": "skyscanner.com/transport_deeplink/4.0/US/en-GB/USD/skyp/1/12712.14788.2025-10-23/air/trava/flights?itinerary=flight|-32289|3237|12712|2025-10-23T06:59|13411|2025-10-23T09:34|335|-|-|-;flight|-32289|3291|13411|2025-10-23T10:50|13416|2025-10-23T12:14|84|-|-|-;flight|-30816|23|13416|2025-10-24T10:25|14788|2025-10-25T14:10|705|-|X|-&carriers=-32289,-30816&operators=-32289;-32289;-30816&passengers=1&channel=website&cabin_class=economy&fps_session_id=b2645942-9526-4356-b6fe-64d1d2e51938&ticket_price=475.00&is_npt=false&is_multipart=false&client_id=skyscanner_website&q_ids=H4sIAAAAAAAA_-OS4mIpzq4sEGLmWJEsxcxxpFih4cHT42xGTAqMAHJBFJkcAAAA|-551467528571022490|2&q_sources=JACQUARD&commercial_filters=false&q_datetime_utc=2025-09-13T06:47:57&transfer_protection=protected&pqid=true&fare_type=base_fare"
}
```

Example response for `v1beta1/flights/JFK/NRT/2025-10-23/1/0/0/Economy?param=best`:
```json
{
    "arrival": "2025-10-25 14:10:00 +0000 UTC",
    "avgLayoversDuration": "8h25m30s",
    "departure": "2025-10-23 13:01:00 +0000 UTC",
    "numOfLayovers": "2",
    "price": "481.00",
    "score": "0.8124",
    "url": "skyscanner.com/transport_deeplink/4.0/US/en-GB/USD/skyp/1/12712.14788.2025-10-23/air/trava/flights?itinerary=flight|-32289|4731|12712|2025-10-23T13:01|9596|2025-10-23T15:38|157|-|-|-;flight|-32289|4547|9596|2025-10-23T19:48|13416|2025-10-23T21:44|296|-|-|-;flight|-30816|23|13416|2025-10-24T10:25|14788|2025-10-25T14:10|705|-|X|-&carriers=-32289,-30816&operators=-32289;-32289;-30816&passengers=1&channel=website&cabin_class=economy&fps_session_id=b2645942-9526-4356-b6fe-64d1d2e51938&ticket_price=481.00&is_npt=false&is_multipart=false&client_id=skyscanner_website&q_ids=H4sIAAAAAAAA_-OS4mIpzq4sEGLmWJEsxcxxpFih4cHT42xGTAqMAHJBFJkcAAAA|-1960961887345880697|2&q_sources=JACQUARD&commercial_filters=false&q_datetime_utc=2025-09-13T06:47:57&transfer_protection=protected&pqid=true&fare_type=base_fare"
}
```
