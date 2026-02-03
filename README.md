# Application Integration Examples

A collection of practical examples and code samples for integrating modern identity and authentication systems with various application frameworks and languages.

## Overview

This repository accompanies the **Application Integration** article series on [giveexamples.com](https://giveexamples.com), providing production-ready code examples for securing applications with cloud identity providers, particularly MS Entra ID (formerly Azure Active Directory).

## What You'll Find Here

Real-world, reproducible examples demonstrating:

- **OAuth 2.0 & OpenID Connect** integration patterns
- **JWT validation** and claims-based authorization
- **Infrastructure as Code** (Terraform) for identity resource provisioning
- **Multi-language implementations** (Java, Kotlin, Python, Go, TypeScript)
- **Security best practices** for enterprise applications

## Article Series

### Part 1: Authentication
- [Securing a Spring Boot API with MS Entra ID](https://giveexamples.com/application-integration/spring-boot-msentra-authentication/)
    - OAuth 2.0 resource server configuration
    - JWT token validation
    - Terraform-managed app registrations
    - [Code Example →](./spring-boot-oauth2-msentra/)

### Part 2: Authorization (Coming Soon)
- Implementing Role-Based Access Control (RBAC) with MS Entra App Roles
    - Defining custom roles in app registrations
    - Endpoint-level authorization enforcement
    - Role assignment and management

## Repository Structure

```
application-integration/
├── spring-boot-oauth2-msentra/
│   ├── terraform/              # MS Entra app registration
│   ├── src/                    # Spring Boot API source
│   ├── build.gradle
│   └── README.md
│
├── spring-boot-rbac/           # Coming soon: App Roles example
│   └── ...
```

## Prerequisites

Different examples have different requirements. Generally, you'll need:

### For Java/Spring Boot Examples
- Java 25 or later
- Gradle 9.3.0 or later
- An Azure subscription with app registration permissions

### For Infrastructure Setup
- Terraform 1.14.4 or later
- Azure CLI
- Appropriate Azure permissions (Application Developer role or higher)

### For Testing
- cURL, Postman, or similar HTTP client
- Azure CLI for obtaining test tokens

## Getting Started

Each example includes its own README with detailed setup instructions. A typical workflow:

1. **Provision Identity Resources**
   ```bash
   cd spring-boot-oauth2-msentra/terraform
   terraform init
   terraform apply
   ```

2. **Configure Application**
   ```bash
   export AZURE_TENANT_ID="your-tenant-id"
   export AZURE_CLIENT_ID="your-client-id"
   ```

3. **Run Application**
   ```bash
   ./gradlew bootRun
   ```

4. **Test Protected Endpoints**
   ```bash
   TOKEN=$(az account get-access-token --resource api://your-api --query accessToken -o tsv)
   curl -H "Authorization: Bearer $TOKEN" http://localhost:8080/api/secure-data
   ```

## Key Concepts Covered

### Authentication vs Authorization
Examples demonstrate the distinction between:
- **Authentication**: Verifying identity (OAuth 2.0 flows, JWT validation)
- **Authorization**: Enforcing access control (RBAC, claims-based policies)

Read more: [Authentication vs Authorization](https://giveexamples.com/identity-fundamentals/authentication-vs-authorization/)

### OAuth 2.0 Flows
Code examples implement various OAuth 2.0 grant types:
- **Client Credentials**: Service-to-service authentication
- **Authorization Code + PKCE**: User-facing applications
- **On-Behalf-Of (OBO)**: Delegated permissions

Learn more: [OAuth 2.0, OIDC, and SAML](https://giveexamples.com/identity-fundamentals/oauth2-oidc-saml/)

### JWT Token Validation
All examples include proper JWT validation:
- Signature verification using JWKS
- Issuer validation
- Audience validation
- Expiration checking
- Claims extraction

## Security Considerations

These examples prioritize security:

✅ **Do's:**
- Validate all JWT claims (iss, aud, exp)
- Use HTTPS in production
- Store secrets in environment variables or Key Vault
- Implement proper error handling and logging
- Follow principle of least privilege

❌ **Don'ts:**
- Never disable signature verification
- Never accept tokens without audience validation
- Never hardcode credentials
- Never trust token contents without validation
- Never expose unnecessary actuator endpoints

## Contributing

Found an issue or have an improvement? Contributions are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Make your changes with clear commit messages
4. Add tests if applicable
5. Submit a pull request

## Testing

Each example includes:
- Unit tests for core security logic
- Integration tests with mocked identity providers
- Example requests for manual testing

Run tests:
```bash
./gradlew test
```

## Common Issues

### Invalid Token Errors
- Verify tenant ID matches between token issuer and configuration
- Ensure audience claim matches your API identifier URI
- Check token expiration timestamp

### Signature Validation Failures
- Confirm network access to JWKS endpoint
- Verify no proxy issues
- Check system clock synchronization

## Additional Resources

### Official Documentation
- [Microsoft Identity Platform](https://learn.microsoft.com/en-us/entra/identity-platform/)
- [Spring Security OAuth 2.0 Resource Server](https://docs.spring.io/spring-security/reference/servlet/oauth2/resource-server/index.html)
- [Terraform AzureAD Provider](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs)

### Related Blog Articles
- [Token Types and Lifecycle](https://giveexamples.com/identity-fundamentals/token-types-and-lifecycle/)
- [User vs Workload Identities](https://giveexamples.com/identity-fundamentals/user-vs-workload-identities/)

### Tools
- [JWT.io](https://jwt.io) - JWT decoder and debugger
- [Azure AD Token Analyzer](https://jwt.ms) - Microsoft's token inspector

## License

MIT License - See [LICENSE](LICENSE) for details.

## Support

- **Blog**: [giveexamples.com](https://giveexamples.com)
- **Issues**: [GitHub Issues](https://github.com/giveexamples/application-integration/issues)
- **Discussions**: Use the comments section on individual blog articles

## About

This repository is maintained as part of the [giveexamples.com](https://giveexamples.com) blog, which focuses on explaining complex identity and security concepts through practical, production-ready examples.

**Author**: Saeed
**Website**: [giveexamples.com](https://giveexamples.com)

---

*Last updated: February 2026*
