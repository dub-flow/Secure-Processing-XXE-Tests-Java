# Secure-Processing  XXE Tests (Java)

This repository show that the `FEATURE_SECURE_PROCESSING` functionality isn't guaranteed to provide protection against `XXE` in Java. It does, however, prevent the `Billion Laughs Attack`.

For our PoC, we use `DocumentBuilderFactory` and configure it with `setFeature("http://javax.xml.XMLConstants/feature/secure-processing", true);`. Still, our `XXE` payload works.

# How to Install

- Install via: `mvn clean install`.

# How to Run

- Run via `mvn spring-boot:run`. This runs the server on port `8080`.

# Prove that `secure-processing` does not prevent XXE

- To show that the `secure-processing` feature does not do anything against `XXE`, we implemented the `POST /xxe-secure-processing-test` route which takes in a parameter called `xmlInput`.
- As a proof of concept to show that `secure-processing` doesn't protect against `XXE`, you can use the example from `./xxe_payload.xml` (which renders the `/etc/passwd` file). For this, run the following `POST` request:
```
POST /xxe-secure-processing-test HTTP/1.1
<redacted for brevity>
Content-Type: application/x-www-form-urlencoded
Content-Length: 134

inputXml=<%3fxml+version%3d"1.0"%3f><!DOCTYPE+book+[<!ENTITY+xxe+SYSTEM+'file%3a///etc/passwd'>]><book><title>%26xxe%3b</title></book>
```
