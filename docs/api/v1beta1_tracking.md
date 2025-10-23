# GET /v1beta1/tracking

| Method | Path                                    | Description                      |
|--------|-----------------------------------------|----------------------------------|
| GET    | `/v1beta1/tracking/{num}/{airline}/{date}` | Tracks a specific flight by flight number, airline code, and date. Returns detailed information including departure, arrival, aircraft, and status. |
| GET    |`/v1beta1/tracking/{num}/{airline}/{date}?param=delay`| Returns departure and arrival delay in minutes. If negative, plane departed/arrived earlier than in schedule. |

Path Parameters:

* num: Flight number (e.g. 33)
* airline: Airline IATA code (e.g. DL)
* date: Flight date in YYYYMMDD format (e.g. 20231024)

Query Parameters:

* delay

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
