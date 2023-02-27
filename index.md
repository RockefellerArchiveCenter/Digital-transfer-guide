---
layout: docs
title:  "Guide to Digital Transfer"
---
# Requirements for the Transfer of Digital Records 
## Overview 
### Transfer should
- Contain the information required to support archival management and preservation. 
- Have a consistent structure so that they can be validated automatically.
- Only contain one record type. 

### Structure
- Transfers should be structured so that they adhere to the Rockefeller Archive Center BagIt Specification. The RAC (Rockefeller Archive Center) BagIt Specification      conforms with the [BagIt specification](https://datatracker.ietf.org/doc/html/draft-kunze-bagit-14), a hierarchical file packaging format for the storage and transfer of arbitrary digital content suitable for disk-based or network-based storage and transfer, developed by the Library of Congress. A [BagIt Profile](https://github.com/bagit-profiles/bagit-profiles-specification) is needed and used to validate all transfers. 

For more information, see the Digital Transfer Structure section below. 

### Metadata
- A set of structured data elements that can help identify and describe the transfer. 
- Each transfer includes a set of minimum elements to support archival management of records in any format, as specified by [Describing Archives: A Content Standard](https://files.archivists.org/pubs/DACS_2019.0.3_Version.pdf). The RAC will index this metadata as structured data. These elements are key-value pairs in bag-info-txt. 
- The donor organization may include additional data elements, serialized as a single JSON or JSON-LD file named metadata.json using UTF-8-character encoding and         included in the data/directory of the bag. The RAC will preserve this file as a bitstream (sequence of data in binary form) alongside the records that it pertains to, but it may not be indexed as structured data.   

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
- > (greater than) 
- : (colon) 
- " (double quote) 
- / (forward slash) 
- \ (backslash) 
- | (vertical bar or pipe) 
- ? (question mark) 
- * (asterisk) 



