## Adding restrictions to mets.xsd with another schema eark.xsd

This example uses `<xs:redefine>` and `<xs:restriction>` to change the definition of an attribute (make it mandatory). As a result, an ordinary METS.xml document can be validated against both schemas.

`structMapType/@TYPE` is defined optional in `mets.xsd` (line 647):
```xml
<xsd:attribute name="TYPE" type="xsd:string" use="optional">
```
The same attribute definition in `eark.xsd`:
```xml
<xs:attribute name="TYPE" type="xs:string" use="required">
```

Line 70 of METS.xml reads (i.e. no TYPE attribute):
```xml
<structMap ID="ID040789CF-82D5-4CE0-8AC4-CCF330E33EA3" LABEL="RODA structural map">
```

Validation against mets.xsd (`structMapType/@TYPE` optional):
```
$ xmllint --noout --schema mets.xsd METS.xml 
METS.xml validates
```

Validation against eark.xsd (`structMapType/@TYPE` required):
```
$ xmllint --noout --schema eark.xsd METS.xml 
METS.xml:70: element structMap: Schemas validity error : Element '{http://www.loc.gov/METS/}structMap': The attribute 'TYPE' is required but missing.
METS.xml fails to validate
```
