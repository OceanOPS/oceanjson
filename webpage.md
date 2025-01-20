# Understanding Our Ocean Data Standards

In operational oceanography, sharing data effectively is essential to improving our understanding of the ocean. To achieve this, OceanOPS is introducing a standardized JSON format for platform metadata and data. This initiative will ensure data is easily shared, validated, and used by the global oceanographic community. This page explains the purpose, technology, and examples of our approach, designed for both technical and non-technical users.

---

## Why We Need a Standardized Format

Our initiative addresses three specific needs:

### 1. **Submitting Metadata to OceanOPS (Input)**
Agencies and organizations worldwide submit metadata to OceanOPS to describe their platforms, such as floats or buoys. Ensuring this metadata is accurate, complete, and consistent is critical for:
- Maintaining data quality.
- Reducing errors during ingestion.
- Simplifying the validation process.

### 2. **Retrieving Metadata from OceanOPS (Output)**
OceanOPS makes this metadata available via APIs for use in:
- AMRIT applications.
- OceanOPS applications.
- Other organizations' systems and dashboards.

By standardizing the output format, we ensure:
- Interoperability with other tools and applications.
- Easy integration into workflows across the community.

### 3. **Exposing Metadata for Discovery (Harvesting)**
To enhance global collaboration, we expose our metadata for harvesting by initiatives like the Ocean Data Information System (ODIS). This ensures:
- Discoverability of data across platforms.
- Traceability of metadata origins, providing acknowledgement and transparency about where the data came from and how it has been processed.

---

## The Technology Behind Our Standard

To meet these needs, we use two complementary technologies: **JSON Schema** and **JSON-LD**. Together, they provide both structure and semantic meaning to our data.

### JSON Schema
JSON Schema is a powerful tool that:
- Defines the structure of data.
- Ensures data is valid and complete by enforcing rules (e.g., required fields, valid formats).
- Supports interoperability by creating a clear and consistent blueprint for data.

**Example Use Case:**
When an organization submits metadata about a buoy, JSON Schema ensures fields like `platform_id` and `name` are correctly filled out and properly formatted.

### JSON-LD
JSON-LD (Linked Data) adds semantic meaning to our data, enabling it to be easily understood and linked to other datasets. Key features include:
- **@context:** Provides mappings to standard vocabularies (e.g., Schema.org, PROV).
- **@type:** Identifies the type of data (e.g., Platform, Sensor).
- **@id:** Provides unique identifiers for resources, making them discoverable globally.

**Example Use Case:**
Exposing metadata to ODIS with JSON-LD enables machines to understand the relationships between platforms, sensors, and their origins, improving discoverability.

---

## The JSON Schema
Here is the JSON Schema we use to validate and structure our data:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "@context": {
      "type": "string",
      "format": "uri",
      "description": "The JSON-LD context defining namespaces and mappings."
    },
    "@type": {
      "type": "string",
      "enum": ["Platform", "Sensor"],
      "description": "The type of entity being described."
    },
    "@id": {
      "type": "string",
      "format": "uri",
      "description": "A globally unique identifier for the resource."
    },
    "platform_id": {
      "type": "string",
      "description": "The unique identifier for the platform."
    },
    "name": {
      "type": "string",
      "description": "The name of the platform."
    }
  },
  "required": ["@context", "@type", "@id", "platform_id"]
}
```

---

## Examples in Action
Here are examples of how this schema is used for different purposes:

### 1. **Input (Metadata Submission)**
This example shows how an organization submits metadata:

```json
{
  "@context": "https://ocean-ops.org/oceanjson/schema/context.jsonld",
  "@type": "Platform",
  "@id": "https://ocean-ops.org/api/data/oceanjson/platforms/12345",
  "platform_id": "12345",
  "name": "Dzaoudzi Buoy 12345"
}
```

### 2. **Output (API Response)**
This example illustrates how metadata is retrieved from the OceanOPS API:

```json
{
  "@context": "https://ocean-ops.org/oceanjson/schema/context.jsonld",
  "@type": "Platform",
  "@id": "https://ocean-ops.org/api/data/oceanjson/platforms/12345",
  "platform_id": "12345",
  "name": "Dzaoudzi Buoy 12345",
  "sensors": [
    {
      "@type": "Sensor",
      "@id": "https://oceanops.org/sensors/67890",
      "name": "CTD Sensor"
    }
  ],
  "traceability": {
    "source": "Submitted by Institute A",
    "ingestion_date": "2025-01-15T12:00:00Z",
    "prov:wasGeneratedBy": "OceanOPS ingestion pipeline"
  }
}
```

### 3. **Exposure (Harvesting/ODIS)**
This example demonstrates metadata exposed for discovery:

```json
{
  "@context": "https://ocean-ops.org/oceanjson/schema/context.jsonld",
  "@type": "Platform",
  "@id": "https://ocean-ops.org/api/data/oceanjson/platforms/12345",
  "platform_id": "12345",
  "name": "Dzaoudzi Buoy 12345",
  "traceability": {
    "source": "Submitted by Institute A",
    "ingestion_date": "2025-01-15T12:00:00Z",
    "prov:wasDerivedFrom": [
      {
        "@id": "https://institute-a.org/metadata/rv-endeavour",
        "name": "Original Metadata from Institute A"
      }
    ]
  },
  "links": {
    "related": [
      {
        "@id": "https://bodc.ac.uk/platforms/12345",
        "description": "BODC record for this platform"
      }
    ]
  }
}
```

---

## Conclusion

By adopting a standardized JSON format, OceanOPS aims to enhance data sharing, quality, and discoverability. Using JSON Schema for validation and JSON-LD for semantic enrichment ensures our data is robust, interoperable, and future-proof. We invite all stakeholders to collaborate with us in implementing this standard to improve the global oceanographic data ecosystem.

