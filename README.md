# Cherre (cherre)

Cherre is a real-estate data-integration and property-intelligence platform that connects, cleans, and resolves public, third-party, and proprietary real-estate datasets - property characteristics, tax and assessments, recorder and deeds, owners, parcel boundaries, and connected portfolio data - and serves them back through a single GraphQL API built on Hasura.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cherre/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cherre/refs/heads/main/apis.yml)

## Tags

- Real Estate
- Property Intelligence
- Data Integration
- Knowledge Graph
- GraphQL

## Timestamps

- **Created:** 2026-06-21
- **Modified:** 2026-06-21

## APIs

### Cherre Property API

Resolved property records - characteristics, valuations, building and unit attributes - queried over Cherre's single GraphQL API with joins, filters, aggregations, and PostGIS geospatial operations across connected datasets.

- **Human URL:** [https://cherre.com/products/platform/](https://cherre.com/products/platform/)
- **Base URL:** `https://api.cherre.com/graphql`

#### Tags

- Property
- Real Estate
- GraphQL

#### Properties

- [Documentation](https://cherre.com/products/platform/)
- [GraphQL](graphql/cherre-graphql.md) — [GraphQL](https://graphql.org)
- [OpenAPI](openapi/cherre-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cherre.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cherre.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cherre Tax Assessor API

County tax assessor and assessment data - assessed and market values, land and improvement valuations, exemptions, and assessment history - resolved to Cherre's standard property model and queryable via GraphQL.

- **Human URL:** [https://cherre.com/products/platform/](https://cherre.com/products/platform/)
- **Base URL:** `https://api.cherre.com/graphql`

#### Tags

- Tax Assessor
- Assessments
- GraphQL

#### Properties

- [Documentation](https://cherre.com/products/platform/)
- [GraphQL](graphql/cherre-graphql.md) — [GraphQL](https://graphql.org)
- [OpenAPI](openapi/cherre-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cherre.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cherre.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cherre Recorder API

Recorder, deeds, transactions, mortgages, and liens - sales and transfer history, lenders, loan amounts, and document detail - connected to parcels and owners through the Cherre knowledge graph.

- **Human URL:** [https://cherre.com/products/platform/](https://cherre.com/products/platform/)
- **Base URL:** `https://api.cherre.com/graphql`

#### Tags

- Recorder
- Deeds
- Mortgages
- GraphQL

#### Properties

- [Documentation](https://cherre.com/products/platform/)
- [GraphQL](graphql/cherre-graphql.md) — [GraphQL](https://graphql.org)
- [OpenAPI](openapi/cherre-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cherre.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cherre.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cherre Owner & Parcel API

Resolved owners and entity relationships plus parcel and building boundary geometries, with PostGIS spatial queries (contains, intersects, point lookups) for custom market areas over the GraphQL API.

- **Human URL:** [https://cherre.com/products/platform/](https://cherre.com/products/platform/)
- **Base URL:** `https://api.cherre.com/graphql`

#### Tags

- Owner
- Parcel
- Boundaries
- GraphQL

#### Properties

- [Documentation](https://cherre.com/products/platform/)
- [GraphQL](graphql/cherre-graphql.md) — [GraphQL](https://graphql.org)
- [OpenAPI](openapi/cherre-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cherre.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cherre.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cherre Connections API

Connected third-party marketplace datasets and a customer's own proprietary and portfolio data, joined to the resolved knowledge graph and exposed through the same unified GraphQL surface for cross-dataset queries.

- **Human URL:** [https://cherre.com/marketplace-connections/](https://cherre.com/marketplace-connections/)
- **Base URL:** `https://api.cherre.com/graphql`

#### Tags

- Connections
- Marketplace
- Proprietary Data
- GraphQL

#### Properties

- [Documentation](https://cherre.com/marketplace-connections/)
- [GraphQL](graphql/cherre-graphql.md) — [GraphQL](https://graphql.org)
- [OpenAPI](openapi/cherre-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cherre.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cherre.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/cherreco)
- [LinkedIn](https://www.linkedin.com/company/cherre)
- [Website](https://www.cherre.com)
- [Documentation](https://cherre.com/products/platform/)
- [Plans](plans/cherre-plans-pricing.yml)
- [Rate Limits](rate-limits/cherre-rate-limits.yml)
- [Fin Ops](finops/cherre-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
