# spdxcyclone

Prototype utility that converts SBOM documents from [CycloneDX](https://cyclonedx.org/) to [SPDX](https://spdx.dev/).

## Status
This code is still under development and may not be considered stable.

## Usage
`java -jar spdxcyclone.jar cyclonedx.json spdx.json`

where `cyclonedx.json` is an existing CycloneDX JSON file and `spdx.json` is a file path to the resulting SPDX file generated from the CycloneDX file.

Although not tested, XML formats should work for CycloneDX and all supported SPDX files formats should work for the output file (e.g. tag/value, XLSX, XML, RDF/XML, YAML).

## Design and Implementation Notes

The mappings from CycloneDX to SPDX can be found in the [SPDX-CycloneDX-Mapping Google Sheet](https://docs.google.com/spreadsheets/d/1PIiSYLJHlt8djG5OoOYniy_I-J31UMhBKQ62UUBHKVA/edit?usp=sharing).

SPDX properties highlighted in yellow do not map directly.  SPDX properties higlighted in light orange map, but has some possible exceptions listed in the notes.

Any CycloneDX properties which do not map to an existing SPDX property is added as an Annotation with `AnnotationType=OTHER` and the comment using the following format:

`MISSING_CDX_PROPERTY:<propertyname>=<propertyJSONvalue>`

where `<propertyname>` is the CycloneDX property name and `<propertyJSONvalue>` is a JSON string representation of the property value.

CycloneDX Components are mapped to SPDX Packages in most cases. For the CycloneDX type file, if there are any properties which require a package (e.g. supplier, originator), the component is converted to an SPDX package with the packageFileName having the value of the component name.  If a CycloneDX type file has no package properties, it is converted to an SPDX File.  This is basically a Duck Typing approach since Cyclone DX does not distinguish different classes for files and packages.

## Contributing
Contributions are welcome.  See the [CONTRIBUTING.md](CONTRIBUTING.md) file for more information.

