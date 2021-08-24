## **Add IDS validation with BCF output to IfcOpenShell**

### Abstract

BuildingSMART organisation is currently working and about to publish new
IDS (Information Delivery Specifications) which in simple terms is a
machine-readable standard for building information modelling (BIM)
requirements. Thanks to IDS, it is possible to automatically verify
exchange requirements of BIM models delivered in IFC format.

In my project, I will first focus on the validation process using
IfcOpenShell to make sure it fully supports the new XSD (XML schema
definition) of IDS and create sample IDS files to test it against.
Furthermore, I aim to enhance this feature with BIM Collaboration Format
(BCF) output of such verification, which will be integrated into the
BIMTester tool.

The last step would be to allow for easier creation of IDS files by
non-coding users.