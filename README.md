# Secure-Processing-XXE-Tests-Java
This repository show that the `FEATURE_SECURE_PROCESSING` functionality doesn't provide any security benefit against `XXE` in Java.

# How to Install
- Install via: `mvn clean install`

# How to Run
- Run via `mvn spring-boot:run`. This runs the server on port `8080`

# Prove that `secure-processing` does not prevent XXE
- To show that the `secure-processing` feature does not do anything against `XXE`, we implemented the `POST /xxe-secure-processing-test` route which takes in a parameter called `xmlInput`.
- As an example `XXE payload` that works (regardless of `secure-processing`), you may wanna use `./xxe_payload.xml` (which renders the `/etc/passwd` file)