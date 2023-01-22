# Model transformation rules

## Introduction

The intent of this document is to describe multiple model 
transformation rules. These model transformation rules reduce 
complexity in encoded INSPIRE data, e.g. by reducing levels of 
aggregation, indirect referencing, using simple geometries and 
flattening structures such as arrays. As with alternative encodings, 
they have different objectives and scopes. A rule may be used with any 
number of encodings, including the default encoding, if applicable.

An alternative encoding may refer to any number of such model 
transformation rules in its requirements classes. For this purpose, each
 model transformation rule receives a unique identifier. For an 
alternative encoding to be the sole encoding, there may not be any 
information loss for the particular data set in question. Where there is
 information loss, such encoding may only be used as an additional 
encoding.

## Description of model transformation rules

Each model transformation rule is described by these properties:

- Name
- Unique identifier
- Category
- Description
- Original model
- Transformed model
- Original instance in default encoding
- Transformed instance in default encoding
- Model transformation rule
- Instance transformation rule
- Solved usability issues
- Known usability issues
- INSPIRE compliance conditions and reversibility
- Notes

## Catalogue of model transformations rules

This catalogue contains general model simplification rules identified so
 far. 

The catalogue also contains several substitution rules, where existing 
types are replaced with less complex types.

| Identifier | Name | Category |
|---|---|---|
| MT001 | [Flatten Nested Structures](./FlattenNestedStructures.md) |simplification rule |
| MT002 | [Extract Primitive Arrays](./ExtractPrimitiveArray.md) |simplification rule |
| MT003 | [Flatten Associated Components using Typenames](./AssociatedComponentsHardType.md) |simplification rule |
| MT004 | [Flatten Associated Components using Codelist Values](./AssociatedComponentsSoftType.md) |simplification rule |
| MT005 | [Simple Geographic Name](./SimplifiedGeographicName.md) | substitution rule |
| MT006 | [Refer to Property Values by Reference](./PropertyByReferenceOnly.md) |simplification rule |
| MT007 | [Simple Citation](./SimplifiedCitation.md) | substitution rule |
| MT008 | [Simple Codelist Reference](./SimplifiedCodelistReference.md) | substitution rule |
| MT009 | [Simple Period](./SimplifiedPeriod.md) | substitution rule |
| MT010 | [European Legislation Identifier](./EuropeanLegislationIdentifier.md) | substitution rule |

