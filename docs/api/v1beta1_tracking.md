# GET /v1beta1/tracking

## Overview

The **flight tracking endpoint** provides real-time or scheduled tracking information for a specific flight.  
You can retrieve full flight details or focus on delay information (departure and arrival).

---

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| **GET** | `/v1beta1/tracking/{num}/{airline}/{date}` | Tracks a specific flight by its flight number, airline code, and date. Returns detailed information including departure, arrival, aircraft type, and current flight status. |
| **GET** | `/v1beta1/tracking/{num}/{airline}/{date}?param=delay` | Returns departure and arrival delay times in minutes. A negative delay means the flight departed or arrived earlier than scheduled. |

---

## Path Parameters

| Parameter | Type | Description | Example |
|------------|------|-------------|----------|
| **num** | string | Flight number (numeric part only) | `33` |
| **airline** | string | Airline IATA code | `DL` |
| **date** | string | Flight date in `YYYYMMDD` format | `20251024` |

---

## Query Parameters

| Parameter | Description | Example |
|------------|-------------|----------|
| **delay** | Returns only delay-related data (departure and arrival delays in minutes). | `?param=delay` |

---

## Examples

Example response for `v1beta1/tracking/33/DL/20231024`:
```json
[
    {
        "departure": {
            "airport": "Heathrow",
            "airportCity": "London",
            "airportCode": "LHR",
            "airportCountryCode": "GB",
            "airportSlug": "LHR-London-UK-(Heathrow)",
            "departureDateTime": "2023-10-24T14:37:00+01:00",
            "estimatedTime": null,
            "gate": "31",
            "offGroundTime": "14:37, Oct 24",
            "outGateTime": null,
            "scheduledTime": "13:55, Oct 24",
            "terminal": "3"
        }
    },
    {
        "arrival": {
            "airport": "Hartsfield Atlanta Intl",
            "airportCity": "Atlanta",
            "airportCode": "ATL",
            "airportCountryCode": "US",
            "airportSlug": "ATL-Atlanta-GA",
            "arrivalDateTime": "2023-10-24T18:05:00-04:00",
            "baggage": null,
            "estimatedTime": null,
            "gate": "F12",
            "inGateTime": "18:05, Oct 24",
            "onGroundTime": null,
            "scheduledTime": "18:30, Oct 24",
            "terminal": "I",
            "timeRemaining": null
        }
    },
    {
        "aircraft": {
            "code": "764",
            "id": 68,
            "name": "Boeing 767-400"
        }
    },
    {
        "status": "Arrived"
    }
]
```

Example response for `v1beta1/tracking/33/DL/20231024?param=delay`:
```json
{
    "arrDelay": -25,
    "depDelay": 42
}
```
