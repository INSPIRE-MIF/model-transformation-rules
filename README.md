# Model transformation rules repository

This repository contains a collection of generic, encoding-agnostic 
model transformation rules that can be applied to the 
[INSPIRE data models](https://inspire.ec.europa.eu/Data-Models/Data-Specifications/2892).
By applying those rules, a modified UML data model, that is more fit for 
certain use cases – such as basic data exchange and direct visualisation
in standard geographic information tools – can be created.

After applying a transformation, an encoding rule (UML-to-GML, 
UML-to-GeoPackage, etc.) is applied in order to encode INSPIRE 
datasets. The INSPIRE default encoding rule is specified in 
[Guidelines for the encoding of spatial data](https://inspire.ec.europa.eu/documents/guidelines-encoding-spatial-data). 
Other encoding rules for use in INSPIRE are defined in separate
[good practices](https://inspire.ec.europa.eu/portfolio/good-practice-library).

## Background

A first collection of model transformation rules was developed in the 
context of the 
[Action 2017.2 on alternative encodings for INSPIRE data](https://wikis.ec.europa.eu/pages/viewpage.action?pageId=33528121), 
see also the 
[associated GitHub repository](https://github.com/INSPIRE-MIF/2017.2).