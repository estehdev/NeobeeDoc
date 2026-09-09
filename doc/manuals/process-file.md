# Process file - SHA-512
A SHA-512 hash is created on every file upload that concerns the *es_process_file* table.

### Columns
| name | type |
| :--- | :--- |
| [hash](#hash) | BINARY(64) |

## Hash
There are several ways of storing a record in the *es_process_file* table: through the UI, through post functions, or as a consequence of *OnlyOffice* saving a file version.
The hashing itself is performed during the file confirmation operation (switching the status to *Active*), after the upload has completed successfully.

At that moment, the operation is performed as follows: the file is downloaded to the server after the upload, hashing is performed, and the value of the hash operation is written in binary form into the ***hash*** column in the *es_process_file* table.

## Displaying the hash
The file hash can be seen in the user interface (UI) and through VTL evaluation.

### UI
In the user interface, the hash is displayed in the attachments table on the ticket details, within the component for displaying developer data, together with the id, the file code and the like.
In addition to this, the hash can also be seen in a component of the *AdvancedTable* type, in the variant where it is configured to work with files and the user checks the *hash* column in the component settings.

### VTL evaluation
As for VTL evaluation, the *hash* value of the file will be visible in the evaluation for components that are of the "file" type (data_type=data_def, data_subtype=es_process_file).


## VTL Examples

### Printing the field value in the json space on the ticket

```json
{
  "hashfilem": [
    {
      "key": "ATT12",
      "data": {
        "id": "5127",
        "hash": "sha512-58f8a5b000297dbb74741792b12b5eae5e05c16a5102d68b60c6c1c8dc866350466ac829bbd38fe69a52bf5195cea481ea4de758babab5b0cb97648d5768467a",
        "name": "file-sample_100kB.docx",
        "ext_code": "ATT12"
      },
      "data_type": "data_def",
      "data_subtype": "es_process_file"
    }
  ]
}
```

### Printing the field value in VTL evaluation (1)
Input:
```vtl
${form.hashfilem.value}
```

Output:
```
[
  {
    data={
      ext_code=ATT12, 
      name=file-sample_100kB.docx, 
      id=5127, 
      hash=sha512-58f8a5b000297dbb74741792b12b5eae5e05c16a5102d68b60c6c1c8dc866350466ac829bbd38fe69a52bf5195cea481ea4de758babab5b0cb97648d5768467a
    }, 
    data_subtype=es_process_file, 
    data_type=data_def, 
    key=ATT12
  }
]
```

> The hash value is located in the *data* section.

### Printing the field value in VTL evaluation (2)
Input:
```vtl
${form.hashfilem.value[1].data.hash}
```

Output:
```
sha512-58f8a5b000297dbb74741792b12b5eae5e05c16a5102d68b60c6c1c8dc866350466ac829bbd38fe69a52bf5195cea481ea4de758babab5b0cb97648d5768467a
```

## Manual validation
If it is necessary to perform manual validation of the hash, it is possible to use various tools that generate the SHA-512 hash of a given file.
The generated value should then be compared with the one stored in the *es_process_file* table. Below are examples for MacOS, Windows and Linux.

### MacOS
Open the "Terminal" application and on the command line run the "*shasum -a 512*" command, which will produce the SHA-512 hash value of the file.

Input:
```bash
shasum -a 512 /path/to/file
```

Output:
```bash
58f8a5b000297dbb74741792b12b5eae5e05c16a5102d68b60c6c1c8dc866350466ac829bbd38fe69a52bf5195cea481ea4de758babab5b0cb97648d5768467a  file-sample_100kB.docx
```

Compare the obtained hash value with the one read from the file itself, just without the "*sha512-*" prefix.

### MS Windows
Open the "PowerShell" application and on the command line run the "*Get-FileHash -Algorithm SHA512 /path/to/file | Format-List*" command, which will produce the SHA-512 hash value of the file.
Note that the "*-Algorithm SHA512*" parameter is mandatory, because *Get-FileHash* uses SHA256 by default.

Input:
```powershell
Get-FileHash -Algorithm SHA512 C:\path\to\file-sample_100kB.docx | Format-List
```

Output:
```powershell
Algorithm : SHA512
Hash      : 58F8A5B000297DBB74741792B12B5EAE5E05C16A5102D68B60C6C1C8DC866350466AC829BBD38FE69A52BF5195CEA481EA4DE758BABAB5B0CB97648D5768467A
Path      : C:\path\to\file-sample_100kB.docx
```

Take the value returned by the "*Get-FileHash*" function under the key "*Hash*" and compare it with the one read from the file itself, just without the "*sha512-*" prefix.
*Get-FileHash* returns the hash in uppercase letters, so the comparison should be case-insensitive.

### Linux
Open the "Terminal" application and on the command line run the "*sha512sum /path/to/file*" command, which will produce the SHA-512 hash value of the file.

```bash
sha512sum /path/to/file
```

Compare the obtained hash value with the one read from the file itself, just without the "*sha512-*" prefix.
