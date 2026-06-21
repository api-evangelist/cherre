# Cherre GraphQL API

Cherre is a real-estate data-integration and property-intelligence platform. It ingests
public records, third-party vendor feeds, and customer-proprietary data, standardizes and
resolves them against a real-estate knowledge graph, and serves the connected result back
through a **single GraphQL API** built on [Hasura](https://hasura.io/case-studies/cherre/).
A client asks for exactly the objects and fields it needs and Cherre joins, filters, and
aggregates them server-side, returning a JSON response.

**Endpoint:** `https://api.cherre.com/graphql` (representative; access is provisioned per
customer via Cherre's Developer Portal / Core API at `app.cherre.com/core-api`)
**Transport:** HTTP `POST` of a GraphQL document
**Authentication:** OAuth 2.0 client-credentials → `Bearer <access_token>` in the
`Authorization` header (see Auth below)
**Documentation:** <https://cherre.com/products/platform/>

- Platform: <https://cherre.com/products/platform/>
- Connections marketplace: <https://cherre.com/marketplace-connections/>
- Hasura case study: <https://hasura.io/case-studies/cherre/>
- GitHub: <https://github.com/cherreco>

> **Note on accuracy.** Cherre's full GraphQL schema is exposed to authenticated customers
> through their Developer Portal and is not published as a public, versioned SDL. The schema
> in [`cherre-schema.graphql`](./cherre-schema.graphql) is a **representative** model of the
> documented capabilities (resolved property, tax assessor, recorder/deeds, mortgage/lien,
> owner, parcel-boundary, and connected datasets; PostGIS spatial filtering; aggregations).
> Exact type, field, and table names depend on a customer's licensed datasets and the data
> model version they are mapped to.

---

## Authentication

Cherre's API is access-controlled. Obtain a bearer access token via the OAuth 2.0
client-credentials grant, then send it on every GraphQL request:

```bash
# 1. Exchange client credentials for a bearer token
curl -X POST https://api.cherre.com/oauth/token \
  -H "Content-Type: application/json" \
  -d '{
    "grant_type": "client_credentials",
    "client_id": "YOUR_CLIENT_ID",
    "client_secret": "YOUR_CLIENT_SECRET"
  }'

# 2. Call the GraphQL endpoint with the token
curl -X POST https://api.cherre.com/graphql \
  -H "Authorization: Bearer $CHERRE_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query":"{ tax_assessor(limit: 1) { tax_assessor_id assessed_value_total } }"}'
```

---

## Type inventory

### Scalars
| Scalar | Purpose |
|--------|---------|
| `bigint` | 64-bit identifiers and large counts |
| `numeric` | Currency amounts, areas, and valuations |
| `date` | Calendar dates (assessment, recording, sale) |
| `timestamptz` | ISO-8601 timestamps |
| `geometry` | PostGIS geometry (parcel / building boundaries, points) |
| `jsonb` | Arbitrary structured JSON payloads |

### Core dataset object types
- `tax_assessor` — resolved tax assessor / assessment record: assessed and market values,
  land and improvement valuations, exemptions, lot and building characteristics.
- `recorder` — recorder document: deeds, transfers, and document detail with dates and parties.
- `recorder_mortgage` — mortgage / lien record: lender, loan amount, term, and recording detail.
- `property` — resolved property entity joining characteristics, valuation, and location.
- `owner` — resolved owner / entity with name, mailing address, and entity relationships.
- `parcel_boundary` — parcel and building boundary geometry for spatial queries.
- `usa_demographics` — community and demographic attributes by geography.
- `connection_dataset` — a connected third-party marketplace or customer-proprietary dataset
  joined to the knowledge graph.

Each dataset exposes a matching `*_aggregate` type for `count`, `sum`, `avg`, `min`, and
`max` over numeric fields, and supports `where`, `order_by`, `limit`, and `offset` arguments
in the Hasura style.

---

## Query examples

### Look up a property's tax assessor record

```graphql
query {
  tax_assessor(
    where: { fips_code: { _eq: "36061" }, situs_zip_code: { _eq: "10001" } }
    limit: 25
  ) {
    tax_assessor_id
    assessed_value_total
    market_value_total
    land_use_code
    year_built
    gross_sq_ft
  }
}
```

### Recorder deeds and mortgages connected to a parcel

```graphql
query {
  recorder(
    where: { fips_code: { _eq: "06037" }, document_recorded_date: { _gte: "2024-01-01" } }
    order_by: { document_recorded_date: desc }
    limit: 50
  ) {
    recorder_id
    document_type
    document_recorded_date
    document_amount
    grantor_name
    grantee_name
    mortgages {
      lender_name
      mortgage_amount
      mortgage_due_date
    }
  }
}
```

### Spatial query — properties within a custom market boundary (PostGIS)

```graphql
query($area: geometry!) {
  parcel_boundary(
    where: { geom: { _st_contains: $area } }
    limit: 500
  ) {
    cherre_parcel_id
    geom
    tax_assessor {
      assessed_value_total
      land_use_code
    }
  }
}
```

### Aggregate assessed value across a ZIP code

```graphql
query {
  tax_assessor_aggregate(
    where: { situs_zip_code: { _eq: "33139" } }
  ) {
    aggregate {
      count
      sum { assessed_value_total }
      avg { assessed_value_total }
    }
  }
}
```

### Resolve an owner and their connected holdings

```graphql
query {
  owner(where: { owner_name: { _ilike: "%acme holdings%" } }, limit: 10) {
    cherre_owner_id
    owner_name
    mailing_address
    properties {
      cherre_property_id
      tax_assessor { assessed_value_total }
    }
  }
}
```
