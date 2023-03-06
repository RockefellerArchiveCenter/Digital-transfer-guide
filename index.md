---
layout: docs
title:  "Guide to Digital Transfer"
---
# Requirements for the Transfer of Digital Records 
## Overview 
### Transfers should
- Contain the information required to support archival management and preservation. 
- Have a consistent structure so that they can be validated automatically.
- Only contain one record type. 

### Structure
- Transfers should be structured so that they adhere to the Rockefeller Archive Center BagIt Specification. The RAC (Rockefeller Archive Center) BagIt Specification conforms with the [BagIt specification](https://datatracker.ietf.org/doc/html/draft-kunze-bagit-14), a hierarchical file packaging format for the storage and transfer of arbitrary digital content suitable for disk-based or network-based storage and transfer, developed by the Library of Congress. A [BagIt Profile](https://github.com/bagit-profiles/bagit-profiles-specification) is needed and used to validate all transfers. 

For more information, see the [Digital Transfer Structure section below](#digital-transfer-structure).

### Metadata
- A set of structured data elements that can help identify and describe the transfer. 
- Each transfer includes a set of minimum elements to support archival management of records in any format, as specified by [Describing Archives: A Content Standard](https://files.archivists.org/pubs/DACS_2019.0.3_Version.pdf). The RAC will index this metadata as structured data. These elements are key-value pairs in bag-info-txt. 
- The donor organization may include additional data elements, serialized as a single JSON or JSON-LD file named `metadata.json` using UTF-8-character encoding and included in the data/directory of the bag. The RAC will preserve this file as a bitstream (sequence of data in binary form) alongside the records that it pertains to, but it may not be indexed as structured data.   

For more information, please see the Metadata Field Specification section below. 

### Protocol
- Transfer packages are pushed to RAC temporary storage via the Amazon Web Services S3 protocol.  

### Size
- A single bag should not be more than 2GB (gigabytes) in size. If a bag exceeds this size limit and contains multiple files, then the approach would be to divide it into multiple bags which do not exceed the size limit. You should link these bags together by using Bag-Group-Identifier and Bag-Count fields. These smaller bags can then be transferred with the regular processes.  
- Bags which exceed the size limit and cannot be subdivided are considered edge cases. Please contact and consult with the RAC before any attempt is made to deliver these bags so that the appropriate method of transfer can be determined.  

### Perferred Tool
- [Dart](https://aptrust.github.io/dart-docs/) is the tool preferred by the Rockefeller Archive Center to package digital and deliver digital transfers. DART can be configured by importing settings files provided by the RAC.

## Digital Transfer Structure 
This section describes the structure of digital transfers, which allow those packages to be validated and verified. 
Donor organizations are responsible for creating structured bags which comply with this specification and transferring them via agreed-upon protocols and schedules. 


### Specifications 
- Rockefeller Archive Center bags must conform to the [BagIt packaging specification](https://datatracker.ietf.org/doc/html/draft-kunze-bagit-14). 
- Rockefeller Archive Center bags must be serialized (single .zip, .tar or tar.gz file) 
- All bags must be valid according to the organization’s BagIt Profile. 

### Structure Overview 
This section includes a simple example of a Rockefeller Archive Center BagIt Specification-compliant bag.  


 
RAC-BAG-ID/ <br>
&emsp;&emsp;    | bagit.txt <br>
&emsp;&emsp;    | manifest-sha256.txt <br>
&emsp;&emsp;    | bag-info.txt <br>
&emsp;&emsp;    \--- data/ <br>
&emsp;&emsp;&emsp;&emsp;          | [payload files] <br>
&emsp;&emsp;&emsp;&emsp;          | metadata.json <br>

### Structure Componets
#### RAC-BAG-ID 
The name of the root directory of the bag. This directory name may include Unicode characters and characters in the extended character set (128–255), except for the following reserved characters: 

- < (less than) 
- (>) (greater than) 
- : (colon) 
- " (double quote) 
- / (forward slash) 
- \ (backslash) 
- | (vertical bar or pipe) 
- ? (question mark) 
- (*) (asterisk) 

#### bagit.txt: 

This file is required in the BagIt spec and includes BagIt version and tag file character encoding. 

#### manifest-sha256.txt: 

This file is required in the BagIt spec and contains a checksum for every item included in the bag’s payload. In this example we have chosen sha256, but using sha512 is also acceptable. md5 is not accepted as a checksum algorithm. 

#### bag-info.txt: 

This file contains metadata elements, which will be indexed as structured data. For more details on the metadata fields, their content, requirements, and usage, please see the Metadata Field Specification section below. Please use standardized names and avoid the use of all acronyms as separate stakeholders may use the same acronyms for different concepts. 

#### data: 

Required directory for payload items.  

#### metadata.json: 

Valid JSON or JSON-LD file that includes metadata elements included in `bag-info.txt` as well as any additional elements donors wish to provide to the RAC. This file is optional. 

 

## Metadata Field Specifications 

 

### Required:  

Bagging-Date 
- **Definition**: Date that the content was prepared for delivery. 
- **Data type**: Values must meet ISO 8601: Standard for Representation of Dates and Times. 
- **Repeatability**: No 
- **Examples**: <br> 
“2016-04-24”  



BagIt-Profile-Identifier 
- **Definition**: An HTTP URI that identifies the BagIt Profile. The Rockefeller Archive Center will provide this identifier to the donor organization. 
- **Data type**: Locally controlled, temporary URL: https://gist.githubusercontent.com/HaSistrunk/65d59e558c436b9d934d98fd8fb0f575/raw/097f2c96c27b1e67a173c6c390458a981ffdbd83/organizational-bag-profile.json <br> 
- **Repeatability**: No <br> 
- **Examples**: <br>
"https://standards.rockarch.org/bagit/organizational-bag-profile.json" <br>
"https://rockarch.org/bagitprofiles/bag-profile.json" 

Date-Start 
- **Definition**: The earliest date on which records in the bag were created. 
- **Data type**: Values must meet ISO 8601: Standard for Representation of Dates and Times. 
- **Repeatability**: No 
- **Examples**: <br>
“1995-01-01” <br>
“2002” 

Date-End 
- **Definition**: The latest date on which records of the transfer were created. Use only if this value differs from Date-Start. 
- **Data type**: Values must meet ISO 8601: Standard for Representation of Dates and Times. 
- **Repeatability**: No 
- **Examples**: <br> 
“1997-12-31”  

External-Identifier 
- **Definition**: A unique identifier applied to each group of records composed of characters, numbers or letters, or a combination thereof, that uniquely identify the record within a given domain. 
- **Data type**: String 
- **Repeatability**: No 
- **Examples**: <br> 
“OyGpXmSFVkCpds7i4gRv” <br>
“Grant2561” 

Internal-Sender-Description 
- **Definition**: A prose description of the nature and contents of the group of records. 
- **Data type**: String 
- **Repeatability**: No 
- **Examples**: <br>
“Annual reports discussing the accomplishments and major strategic initiatives of the Ford Foundation.” <br>
“Board reports from all Russell Sage Foundation board meetings.” 

Language 
- **Definition**: The natural language(s) in which the materials are written. 
- **Data type**: Values must meet [ISO 639-2/B: Codes for the Representation of Names of Languages](https://www.loc.gov/standards/iso639-2/php/code_list.php). If materials have no language, please use “nil” 
- **Repeatability**: Yes 
- **Examples**: <br>
“eng” <br> 
“spa” 

Payload-Oxum 
- **Definition**: The “octetstream sum” of the payload, namely, a two-part number of the form OctetCount.StreamCount, where OctetCount is the total number of octets (8-bit bytes) across all payload file content and StreamCount is the total number of payload files. Payload-Oxum should be included in bag-info.txt. 
- **Data type**: OctetCount.StreamCount 
- **Repeatability**: No 
- **Examples**: <br> 
“279164409832.1198” 

Record-Type 
- **Definition**: The broad category into which the records fall. 
- **Data type**: Locally controlled. 
- **Repeatability**: No 
- **Examples**: <br>
“annual reports” <br> 
“grant records” 

Source-Organization 
- **Definition**: The organization responsible for sending the content. 
- **Data type**: Locally controlled string 
- **Repeatability**: No 
- **Examples**: <br>
“Asian Cultural Council” <br>
“Ford Foundation” <br> 
“Social Science Research Council” 

Title 
- **Definition**: The title of a group of records. Do not include dates or identifiers in the title element. This should not be a description of the material type but instead a declarative title for all the records in the bag. 
- **Data type**: String 
- **Repeatability**: No 
- **Examples**: <br>
“Annual Reports” <br> 
“Grant Records” 

 

### Optional: 

Bag-Count 
- **Definition**: Two numbers separated by ‘of,’ in particular, ‘N of T,’ where T is the total number of bags in a group of bags and N is the ordinal number within the group; if T is not known, specify it as ‘?’ (question mark). 
- **Data type**: String 
- **Repeatability**: No 
- **Examples**: <br>
“1 of 2” <br> 
“4 of 4” <br>
“3 of ?” 

Bag-Group-Identifier 
- **Definition**: A unique identifier for the entire set of bags to which this bag belongs. 
- **Data type**: String 
- **Repeatability**: No 
- **Examples**: <br> 
“xOmy5” <br>
“AnnualReports” <br>
“Group1” 

Record-Creators 
- **Definition**: Identifies the individuals, organizations or departments that created the group of records. 
- **Data type**: String 
- **Repeatability**: Yes 
- **Examples**: <br> 
“Rockefeller Brothers Fund Communications Office” <br>
“Shah, Rajiv” 

 



