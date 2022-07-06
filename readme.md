## Reactive Microservices with Spring WebFlux and Spring Cloud
Project  showing how to use Spring WebFlux together with Spring Cloud projects in order to provide such mechanisms like service discovery, load balancing or API gateway for reactive microservices built on top of Spring Boot.

___
$ docker run -d --name mongo -p 27017:27017 mongo

Finally, after running gateway-service, and other (all) services we may add some test data.

$ curl --header "Content-Type: application/json" --request POST --data '{"firstName": "John","lastName": "Scott","age": 30}' http://localhost:8090/customer
{"id": "5aec1debfa656c0b38b952b4","firstName": "John","lastName": "Scott","age": 30,"accounts": null}
$ curl --header "Content-Type: application/json" --request POST --data '{"number": "1234567890","amount": 5000,"customerId": "5aec1debfa656c0b38b952b4"}' http://localhost:8090/account
{"id": "5aec1e86fa656c11d4c655fb","number": "1234567892","customerId": "5aec1debfa656c0b38b952b4","amount": 5000}
$ curl --header "Content-Type: application/json" --request POST --data '{"number": "1234567891","amount": 12000,"customerId": "5aec1debfa656c0b38b952b4"}' http://localhost:8090/account
{"id": "5aec1e91fa656c11d4c655fc","number": "1234567892","customerId": "5aec1debfa656c0b38b952b4","amount": 12000}
$ curl --header "Content-Type: application/json" --request POST --data '{"number": "1234567892","amount": 2000,"customerId": "5aec1debfa656c0b38b952b4"}' http://localhost:8090/account
{"id": "5aec1e99fa656c11d4c655fd","number": "1234567892","customerId": "5aec1debfa656c0b38b952b4","amount": 2000}

To test inter-service communication just call endpoint GET /customer/{id}/with-accounts on gateway-service. 
It forwards the request to customer-service, and then customer-service calls endpoint exposed by account-service using reactive WebClient.

