# Purpose and usage

This XSLT is a proof of concept for the HTML+RDFa representation of metadata based on [DCAT-AP](https://joinup.ec.europa.eu/node/63567/), and related extensions (as [GeoDCAT-AP](https://joinup.ec.europa.eu/node/139283/)), available on Joinup, the collaboration platform of the [EU ISA Programme](http://ec.europa.eu/isa).
  
As such, this XSLT must be considered as unstable, and can be updated any time based on the revisions to the DCAT-AP specifications and related extensions.

Comments and inquiries should be sent to the GeoDCAT-AP WG mailing list: 

    dcat_application_profile-geo@joinup.ec.europa.eu

# Content

* [`dcat-ap-rdf2rdfa.xsl`](./dcat-ap-rdf2rdfa.xsl): The XSLT transforming a set of DCAT-AP records from RDF/XML to HTML+RDFa.
* [`LICENCE.md`](./LICENCE.md): The XSLT's licence.
* [`README.md`](./README.md): This document. 

# How it works

The XSLT requires as input DCAT / DCAT-AP compliant metadata records in RDF/XML format. 

The following sections provide examples of code from popular programming languages that can be used to run the XSLT.

## PHP

````php
<?php

// The URL of the RDF/XML document to be transformed.
  $xmlURL = "http://some.site/dataset.rdf";

// The URL pointing to the latest version of the XSLT.
  $xslURL = "https://webgate.ec.europa.eu/CITnet/stash/projects/ODCKAN/repos/iso-19139-to-dcat-ap/browse/iso-19139-to-dcat-ap.xsl?raw";

  $xml = new DOMDocument;
  $xml->load($xmlURL) or die();

  $xsl = new DOMDocument;
  $xsl->load($xslURL) or die();

  $proc = new XSLTProcessor();
  $proc->importStyleSheet($xsl);

  echo $proc->transformToXML($xml);

?>
````

## Python

````python
import lxml.etree as ET

# The URL of the RDF/XML document to be transformed.
xmlURL = "http://some.site/dataset.rdf"

# The URL pointing to the latest version of the XSLT.
xslURL = "https://webgate.ec.europa.eu/CITnet/stash/projects/ODCKAN/repos/iso-19139-to-dcat-ap/browse/iso-19139-to-dcat-ap.xsl?raw"

xml = ET.parse(xmlURL)
xsl = ET.parse(xslURL)

transform = ET.XSLT(xsl)

print(ET.tostring(transform(xml), pretty_print=True))
````

## Java

TBD
  
#  Credits
  
This work is supported by the [EU Interoperability Solutions for European Public Administrations Programme (ISA)](http://ec.europa.eu/isa) through [Action 1.17: Re-usable INSPIRE Reference Platform (ARe3NA)](http://ec.europa.eu/isa/actions/01-trusted-information-exchange/1-17action_en.htm).
