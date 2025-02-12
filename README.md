# OceanJSON

An integrated GOOS metadata JSON schema based on the <a target="_blank" href="https://www.ocean-ops.org/docs/">OceanMeta</a> metadata standard.

## Goals

Facilitate integration and ensure seamless metadata exchange between nodes.

## Entities

The format is broken down into Key Entities (Mission, Platform, Ship, Cruise, Contact, Site, Observation, Telecom, Status, Agency, ..) each with their own schema.

These are based on the classes, or groups of classes within the OceanMeta ontology.

We include for each schema and it's fields the the codes and types from the OceanMeta MCD. 

The keywords oceanMetaCode and oceanMetaType are used for this.

These won't affect validation but provide valuable context, with the following benefits:
- Traceability: Users can cross-reference these codes with OceanMeta documentation for more details.
- Documentation Automation: You could auto-generate schema documentation from these codes.
- Validation Support: Developers can build custom tools to check if data aligns with both JSON Schema and MCD standards.

## Examples

In /examples directory, find sample JSON files showing how a complete JSON document would look like.

It will eventually be possible to simply fetch a platform sample array from the OceanOPS API in OceanJSON format:

https://www.ocean-ops.org/api/data/oceanjson/platforms?fields=ref,status

!! WARNING !! THE API DELIVERS A DEPRECATED TEST VERSION OF OceanJSON !

## Property Key Naming Standard 

Property keys will all be based on the OceanMeta names that should all be identified with their respective code and definition.

## OceanJSON Validator

There will be an online tool where you can test that you JSON is valid OceanJSON.


