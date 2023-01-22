# Flattening of Nested Structures (MT001)

## Category

simplification rule

## Description

The complex structure of model elements can be reduced by applying a flattening method. The principle of the flattening is to derive a flat model structure by moving the nested child elements to its parent. The elements can be renamed to represent the former element path in the name of the resulting element and to avoid naming conflicts. The multiplicity of the derived elements should be calculated from the multiplicities of the former element path. When applied recursively, this method flattens the structure of multiple levels.

When applied recursively, this method flattens the structure of multiple levels and will result in properties such as these:

- `inspireId_namespace`
- `name_spelling_text`

This model transformation rule does not handle multiplicities greater than 1; it thus does not introduce any numeric elements into the new property name to account for multiple occurrences. It also does not make use of the element names as they would be encoded in XML to keep the resulting property names shorter. In most cases outside the use of substitution groups, this does not lead to issues. These should be resolved using any of the three Transformation Rules that can deal with that ([Primitive Array](./ExtractPrimitiveArray.md), [Associations to Soft Typed properties](./AssociatedComponentsSoftType.md), [Associations to Hard Typed properties](./AssociatedComponentsHardType.md)).

## Original model

```mermaid
classDiagram
    class ManagementRestrictionOrRegulationZone {
        …
    }
    <<featureType>> ManagementRestrictionOrRegulationZone
    class DocumentCitation {
        name: CharacterString
        shortName: CharacterString [0..1]
        date: CI_Date
        link: URL [1..*]
        specificReference: CharacterString [0..*]
    }
    class CI_Date {
        date: Date
        dateType: CI_DateTypeCode
    }
    <<dataType>> CI_Date
    class LegislationCitation {
        …
    }
    DocumentCitation <|-- LegislationCitation
    ManagementRestrictionOrRegulationZone --> "legalBasis 1..*" LegislationCitation
```

## Transformed model

```mermaid
classDiagram
    class ManagementRestrictionOrRegulationZone {
        legalBasis_name: CharacterString
        legalBasis_shortName: CharacterString [0..1]
        legalBasis_date_date: Date
        legalBasis_date_dateType: CI_DateTypeCode
        legalBasis_link: URL [1..*]
        legalBasis_specificReference: CharacterString [0..*]
        …
    }
    <<featureType>> ManagementRestrictionOrRegulationZone
```

## Original instance in default GML encoding

```xml
<am:ManagementRestrictionOrRegulationZone>
  <!-- ... -->
  <am:legalBasis>
    <base2:LegislationCitation>
      <base2:name>Bekendtgørelse af lov om skove</base2:name>
      <base2:shortName>LBK nr 122 af 26/01/2017</base2:shortName>
      <base2:date>
        <gmd:CI_Date>
          <gmd:date>
            <gco:Date>2017-01-26</gco:Date>
          </gmd:date>
          <gmd:dateType>
            <gmd:CI_DateTypeCode
              codeListValue="creation"
              codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_DateTypeCode" />
          </gmd:dateType>
        </gmd:CI_Date>
      </base2:date>
      <base2:link>http://www.retsinformation.dk/eli/lta/2017/122</base2:link>
      <base2:level
	    xlink:href="http://inspire.ec.europa.eu/codelist/LegislationLevelValue/national"
		xlink:title="national" />
    </base2:LegislationCitation>
  </am:legalBasis>
  <!-- ... -->
</am:ManagementRestrictionOrRegulationZone>
```
   
## Transformed instance in default GML encoding

```xml
<ams:ManagementRestrictionOrRegulationZone>
  <!-- ... -->
  <ams:legalBasis_name>Bekendtgørelse af lov om skove</ams:legalBasis_name>
  <ams:legalBasis_shortName>LBK nr 122 af 26/01/2017</ams:legalBasis_shortName>
  <ams:legalBasis_date_date>2017-01-26</ams:legalBasis_date_date>
  <ams:legalBasis_date_dateType.codeListValue>creation</ams:legalBasis_date_dateType.codeListValue>
  <ams:legalBasis_date_dateType.codeList>http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_DateTypeCode</ams:legalBasis_date_dateType.codeList>
  <ams:legalBasis_link>http://www.retsinformation.dk/eli/lta/2017/122</ams:legalBasis_link>
  <ams:legalBasis_linklevel>national</ams:legalBasis_linklevel>
  <ams:legalBasis_linklevel.href>http://inspire.ec.europa.eu/codelist/LegislationLevelValue/national</ams:legalBasis_linklevel.href>
  <!-- ... -->
</ams:ManagementRestrictionOrRegulationZone>
``` 

## Model transformation rule

### Parameters

- `separator`: The character to use to separate the original property name from the type name of the components.

### Execution

Recursively go down through the complex structure of the property and concatenate the local name of the property, using the `separator` character in between each local name. This rule will drop inherited properties that have the same local name as a property declared on the feature type or property type itself, e.g. `gml:name` vs. `gn:name`. Note that Geometry properties are excluded from this rule!</p>

## Instance transformation rule

### Parameters

None.

### Execution

As described above, this rule does not handle property cardinalities greater than 1; if more than one instance of a property occurs, only the first instance will be kept.

## Solved usability issues

This rule deals with most nested property structures and flattens them, so that the data can be used easily in analysis and visualisation.

## Known usability issues

This rule has no fixed limit in the character length of the resulting property names. Some of these names can get very long. The rule should thus be combined with others that reduce the likelyhood of that happening, such as [SimpleGeographicName](./SimpleGeographicName.html).

## INSPIRE compliance conditions and reversibility

Data transformed using this rule is INSPIRE compliant as long as the cardinality of the affected properties in the source data was 0 or 1.

## Notes

Geometry properties are excluded from this rule.
