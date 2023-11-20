# Idempotency

Idempotency in REST APIs means that if the same request happens more than once, it will not cause any effect in our application.
For example, a POST request is suppose to create new resources in the API. So, every POST that an API receives will create a new resource or trigger something in the application. Let's suppose a POST request is sent twice due to some retry error or due to a client mistake. In this scenario, is expected that only one resource is created, not two.

By default, the following HTTP methods are idempotents:
- GET
- OPTIONS
- PUT
- DELETE
- HEAD
- TRACE

They are idempotents because it doesn't matter how many times they are executed. They will always return the same value, I mean, they will not change the state of the application beyonds what is expected. For example, if a GET is executed more than once, there is no problem, because it will not duplicate the resources or change their state. The result will be always the same.
The same for the DELETE. If a DELETE method is executed more than once against a resource, the response may be different, but the resource had already been deleted in the first request, so it will not cause any damage to the system.

Differently from these HTTP methods, we have the ones that are not idempotents:

- POST
- PATCH

If a POST is executed more than once, the same resource will be duplicated in the API.

## Solutions for idempotency

### Unique Request Identifier
The Unique Request Identifier is a commonly approach used by some organizations to add idempotency to its API in POST and PATCH request methods. 

This approach consists of a client generating a unique identifier (UUID for example) and attaching it to the request header, in a key defined in the contract of the API.
The API then, will store this key alongside with the request body. Usually this keep stored for 24 hours, but there is no rule about that. So, if a new request with the same identifier reaches the API, the same result will be returned with a 500 status code (or the status code that better suites your needs).

Stripe uses this approach by accepting a [IDEMPOTENCY-KEY in the request header](https://stripe.com/docs/api/idempotent_requests).