# OceanJSON

An integrated GOOS metadata JSON schema based on the <a target="_blank" href="https://www.ocean-ops.org/docs/">OceanMeta</a> metadata standard.

## Goals

Facilitate integration and ensure seamless metadata exchange between nodes.

## Entities

The format is broken down into Key Entities (Mission, Platform, Ship, Cruise, Contact, Site, Observation, Telecom, Status, Agency, ..) each with their own schema.

## Validation

JSON Schema files for each key entity in /schemas directory.

## Examples

In /examples directory, find sample JSON files showing how a complete JSON document would look like.

It will eventually be possible to simply fetch a platform sample array from the OceanOPS API in OceanJSON format:

https://www.ocean-ops.org/api/data/oceanjson/platforms?fields=ref,status

!! WARNING !! THE API DELIVERS A DEPRECATED TEST VERSION OF OceanJSON !

## Property Key Naming Standard 

Property keys will all be based on the OceanMeta names that should all be identified with their respective code and definition.

## OceanJSON Validator

There will be an online tool where you can test that you JSON is valid OceanJSON.


