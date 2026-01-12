# rest-demo

A small Spring Boot example that exposes a simple in-memory Cloud Vendor REST API.

## Summary

This project demonstrates a minimal Spring Boot REST service that manages a `CloudVendor` model. It is intended as a learning/example project — the controller currently stores a single `CloudVendor` instance in memory (no database).

## Prerequisites

- Java 17+ (or the JDK version configured for the project)
- Maven 3.6+

## Build and run

From the project root run:

```bash
mvn clean package
mvn spring-boot:run
```

Or run the produced jar:

```bash
java -jar target/*.jar
```

On Windows PowerShell the same commands work; prefix with `.
` if running scripts (e.g. `.\mvnw.cmd spring-boot:run`) when using the included wrapper.

## API

Base path: `/cloudvendor`

- GET `/cloudvendor/{vendorId}`
  - Returns the stored `CloudVendor` object. (Note: current implementation ignores the path variable and returns the single in-memory instance.)

- POST `/cloudvendor`
  - Create a new `CloudVendor`. Request body: JSON. Example:

```json
{
  "vendorId": "C1",
  "vendorName": "Vendor 1",
  "vendorAddress": "Address One",
  "vendorPhoneNumber": "00001"
}
```

- PUT `/cloudvendor`
  - Update the stored `CloudVendor`. Request body: same JSON shape as POST.

- DELETE `/cloudvendor/{vendorId}`
  - Delete the stored `CloudVendor`. (Current implementation ignores the path variable and clears the in-memory object.)

### Example curl commands

Create:

```bash
curl -X POST http://localhost:8080/cloudvendor \
  -H "Content-Type: application/json" \
  -d '{"vendorId":"C1","vendorName":"Vendor 1","vendorAddress":"Address One","vendorPhoneNumber":"00001"}'
```

Get:

```bash
curl http://localhost:8080/cloudvendor/C1
```

Update:

```bash
curl -X PUT http://localhost:8080/cloudvendor \
  -H "Content-Type: application/json" \
  -d '{"vendorId":"C1","vendorName":"Vendor 1 Updated","vendorAddress":"New Address","vendorPhoneNumber":"00002"}'
```

Delete:

```bash
curl -X DELETE http://localhost:8080/cloudvendor/C1
```

## Notes & next steps

- The controller in `src/main/java/com/example/rest_demo/controller/CloudVendorAPIService.java` currently keeps a single `CloudVendor` in memory and does not use the request path variables. For production or realistic testing you should:
  - Add `@PathVariable` annotations to the `GET` and `DELETE` methods and use the variable.
  - Persist data with a database (JPA/H2/Postgres) or at least a concurrent map for multiple vendors.
  - Add validation and error handling.

## Tests

Run the tests with:

```bash
mvn test
```

## Contributing

PRs and issues are welcome. Keep changes small and focused; add tests for new functionality.

## License

This repository does not include a license file. Add a `LICENSE` if you wish to make the project open-source.
