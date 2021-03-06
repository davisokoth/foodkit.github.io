# Foodkit Backend Coding Task

hello@ginja.co.th

It should take you only a couple of hours to come up with your solution. You can use any language and framework (or *no* framework), but your submission should have clear instructions on how to set up and run your API server.

You should also include 1-2 paragraphs explaining your approach. Keep in mind that there are many possible solutions, some of which are better than others.

## Somchai's Motorbike Taxi Service ##

Somchai runs a motorbike taxi company and wants to create a mobile app so his customers can conveniently book rides in advance and know the fare before getting on the bike. He types "build mobile app" into Google and discovers he needs to build an API to manage the business logic and data persistence for his app.

The first API endpoint he will need is a "quotation" endpoint. This will take the pickup and drop-off location from the user and return a price estimate for the journey.

Somchai realises that he can only service a small area of Bangkok, as he only has drivers in some suburbs. He takes out a map of Bangkok and draws a rectangle around the area he believes his riders can accept jobs from.

(map)

If the user tries to specify a pickup or drop-off location outside of this rectangle, Somchai's riders cannot service it, so the API will return an error state.

As an experienced former motorbike taxi rider himself, Somchai knows the fare charged will depend on the distance. He decides for simplicity he'll just use the straightline distance between the pickup and drop-off location, and calculate the price based on a set per-kilometre fee.

For the purpose of this exercise, you should build the "quotation" endpoint. Your API will need to be configurable with the following settings:

* Delivery boundary (2 x lat,lng pairs, which are the top-left and bottom-right points demarking the serviceable area rectangle)
* Per kilometer cost

The quotation endpoint should accept a payload of the format:

```
POST api/quotation
{
  "from": {"lat": 0.0, "lng": 0.0},
  "to": {"lat": 0.0, "lng": 0.0}
}
```

If either the "from" or "to" location are outside of the service area, the API should return an error state with some message explaining the failure. If the "from" and "to" location are both within the service area, the API should respond as follows:

```
200 OK
{
  "from": {"lat": 0.0, "lng": 0.0},
  "to": {"lat": 0.0, "lng": 0.0},
  "distance": 1.2,
  "cost": 80.0
}
```

## Follow up questions ##

* What challenges are there with calculating in/out of service area?
* How did you calculate the distance? Are there any problems with this approach? How could you do it differently?
* Can you think of a way to group and cache quotations for similar pickup and drop-off locations? Eg. Two users in the same office building might send requests with very similar (but slightly different) lat,lng pairs.
