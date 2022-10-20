# KSA E-invoice

## Indices

- [Auth](#auth)

  - [Login](#1-login)
  - [Register](#2-register)

- [Invoices](#invoices)

  - [Clear](#1-clear)
  - [Get Status](#2-get-status)
  - [Process](#3-process)
  - [Report](#4-report)

---

## Auth

### 1. Login

**_Endpoint:_**

```bash
Method: POST
Type: RAW
URL: {{baseUrl}}/api/auth/login
```

**_Body:_**

```js
{
    "username": "{{username}}",
    "password": "{{password}}",
    "companyId": {{companyId}}
}
```

**_More example Requests/Responses:_**

##### I. Example Request: Invalid Login

**_Body:_**

```js
{
    "username": "{{username}}1",
    "password": "{{password}}",
    "companyId": {{companyId}}
}
```

##### I. Example Response: Invalid Login

```js
{
    "type": "https://tools.ietf.org/html/rfc7235#section-3.1",
    "title": "Unauthorized",
    "status": 401,
    "traceId": "00-7b17b9e83f052a59f60a1f02daa89a15-67f88750b22ac290-00"
}
```

**_Status Code:_** 401

<br>

##### II. Example Request: Successful Login

**_Body:_**

```js
{
    "username": "{{username}}",
    "password": "{{password}}",
    "companyId": {{companyId}}
}
```

##### II. Example Response: Successful Login

```js
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiQkkiLCJqdGkiOiI3MDk1MjEwNC0xNzhjLTRmMzEtYmY3Mi0zMTI5NDI0ZjAwMTkiLCJleHAiOjE2NjYyMDEwNTZ9.2__JiLVZyBzz1RU3oEk2IiDLOPbqBczcoIBcXyWFyKA",
    "expiration": "2022-10-19T17:37:36Z"
}
```

**_Status Code:_** 200

<br>

### 2. Register

**_Endpoint:_**

```bash
Method: POST
Type: RAW
URL: {{baseUrl}}/api/auth/register
```

**_Body:_**

```js
{
    "username": "{{username}}",
    "password": "{{password}}",
    "companyId": {{companyId}}
}
```

**_More example Requests/Responses:_**

##### I. Example Request: User Exists

**_Body:_**

```js
{
    "username": "{{username}}",
    "password": "{{password}}",
    "companyId": {{companyId}}
}
```

##### I. Example Response: User Exists

```js
{
    "status": "Error",
    "message": "User already exists!"
}
```

**_Status Code:_** 400

<br>

##### II. Example Request: User Creates Successfuly

**_Body:_**

```js
{
    "username": "{{username}}1",
    "password": "{{password}}",
    "companyId": {{companyId}}
}
```

##### II. Example Response: User Creates Successfuly

```js
{
    "status": "Success",
    "message": "User created successfully!"
}
```

**_Status Code:_** 200

<br>

## Invoices

### 1. Clear

**_Endpoint:_**

```bash
Method: POST
Type: RAW
URL: {{baseUrl}}/api/taxprocessor/clear
```

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST20",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "02110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

**_More example Requests/Responses:_**

##### I. Example Request: Valid Submission

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST1",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "0111010",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### I. Example Response: Valid Submission

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLHlNSmhRcG5rUlNwODVuVjFMT2RFd1JHaFdCSW14dmdBSHBwSVJhRVhBSW89B2BNRVVDSUd1STdKMnFYL0QzTk12ZTIxSG05b2dHQ3dFYjFYeG56WERvUmFNRVEzR3hBaUVBbWRNS1VORFFOM2lrWTdtMy92SjhuNk9iOHZFZ0NtRE0xQnZiZm5ZMm96VT0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABEdifjdJ03b3+M0dTPofZCRfBK+8Gdbsnhw4TNmEqacHGTtrSNaba3UVrzamOy7hWZL2gUFQ92NuYweGxhoiuY4="
    },
    "success": true,
    "message": "CLEARED"
}
```

**_Status Code:_** 200

<br>

##### II. Example Request: Duplicate Invoice Number

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST1",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "0111010",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### II. Example Response: Duplicate Invoice Number

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLHlNSmhRcG5rUlNwODVuVjFMT2RFd1JHaFdCSW14dmdBSHBwSVJhRVhBSW89B2BNRVVDSUd1STdKMnFYL0QzTk12ZTIxSG05b2dHQ3dFYjFYeG56WERvUmFNRVEzR3hBaUVBbWRNS1VORFFOM2lrWTdtMy92SjhuNk9iOHZFZ0NtRE0xQnZiZm5ZMm96VT0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABEdifjdJ03b3+M0dTPofZCRfBK+8Gdbsnhw4TNmEqacHGTtrSNaba3UVrzamOy7hWZL2gUFQ92NuYweGxhoiuY4="
    },
    "success": false,
    "message": "Invoice is submitted before with created/valid/valid with warnings status"
}
```

**_Status Code:_** 400

<br>

##### III. Example Request: Invalid/Expired EGS

**_Body:_**

```js
{
    "EgsId": {{egsId}}1,
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST1",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "0111010",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### III. Example Response: Invalid/Expired EGS

```js
{
    "success": false,
    "message": "Invalid/Expired Company or EGS"
}
```

**_Status Code:_** 400

<br>

##### IV. Example Request: Invalid Submission

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST4",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "01110101",
            "Value": "388343432"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### IV. Example Response: Invalid Submission

```js
{
    "data": {
        "validationResults": {
            "infoMessages": [
                {
                    "type": "INFO",
                    "code": "XSD_ZATCA_VALID",
                    "category": "XSD validation",
                    "message": "Complied with UBL 2.1 standards in line with ZATCA specifications",
                    "status": "PASS"
                }
            ],
            "warningMessages": [],
            "errorMessages": [
                {
                    "type": "ERROR",
                    "code": "BR-CL-01",
                    "category": "EN_16931",
                    "message": "The document type code MUST be coded by the invoice and credit note related code lists of UNTDID 1001.",
                    "status": "ERROR"
                },
                {
                    "type": "ERROR",
                    "code": "BR-KSA-05",
                    "category": "KSA",
                    "message": "The invoice type code (BT-3) must be equal to one of value from the subset of UN/CEFACT code list 1001, D.16B agreed for KSA electronic invoices.",
                    "status": "ERROR"
                }
            ],
            "status": "ERROR"
        },
        "clearanceStatus": "NOT_CLEARED"
    },
    "success": false,
    "message": "NOT_CLEARED"
}
```

**_Status Code:_** 400

<br>

##### V. Example Request: Clearance Disabled (Valid Signing)

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST5",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "01110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### V. Example Response: Clearance Disabled (Valid Signing)

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLGtxSStQSWtLWTFRS0FRZThEU0ZEZE5pMGNtWmo0dUljTW41RWs4dlhEaW89B2BNRVFDSUNPdHBjaWRKQjdGR1BXSzFmRllLZXlaR0YzdjlLK2ZnRDdiSjNlUEQ3ZWVBaUFDaEIyTFlURnYzdDV2YndjeU1QVmtkd0F5Yk1TRHR5YjcxbFAyU2xVbk1nPT0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABGGDDKDmhWAITDv7LXqLX2cmr6+qddUkpcLCvWs5rC2O29W/hS4ajAK4Qdnahym6MaijX75Cg3j4aao7ouYXJ9E="
    },
    "success": true,
    "message": "Clearance is disabled"
}
```

**_Status Code:_** 200

<br>

##### VI. Example Request: Invoice Not Standard Tax Invoice

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST7",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "02110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### VI. Example Response: Invoice Not Standard Tax Invoice

```js
{
    "success": false,
    "message": "Invoice is not a standard invoice, it can't be cleared"
}
```

**_Status Code:_** 400

<br>

### 2. Get Status

**_Endpoint:_**

```bash
Method: GET
Type: RAW
URL: {{baseUrl}}/api/taxprocessor/getstatus
```

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "InvoiceNo": "TEST1"
}
```

**_More example Requests/Responses:_**

##### I. Example Request: Invoice Doesn't Exist

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "InvoiceNo": "INV3"
}
```

##### I. Example Response: Invoice Doesn't Exist

```js
{
    "success": false,
    "message": "Invoice doesn't exist"
}
```

**_Status Code:_** 400

<br>

##### II. Example Request: Successful Response

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "InvoiceNo": "TEST1"
}
```

##### II. Example Response: Successful Response

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLHlNSmhRcG5rUlNwODVuVjFMT2RFd1JHaFdCSW14dmdBSHBwSVJhRVhBSW89B2BNRVVDSUd1STdKMnFYL0QzTk12ZTIxSG05b2dHQ3dFYjFYeG56WERvUmFNRVEzR3hBaUVBbWRNS1VORFFOM2lrWTdtMy92SjhuNk9iOHZFZ0NtRE0xQnZiZm5ZMm96VT0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABEdifjdJ03b3+M0dTPofZCRfBK+8Gdbsnhw4TNmEqacHGTtrSNaba3UVrzamOy7hWZL2gUFQ92NuYweGxhoiuY4=",
        "status": "Valid"
    },
    "success": true,
    "message": ""
}
```

**_Status Code:_** 200

<br>

### 3. Process

**_Endpoint:_**

```bash
Method: POST
Type: RAW
URL: {{baseUrl}}/api/taxprocessor/process
```

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST17",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "01110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

**_More example Requests/Responses:_**

##### I. Example Request: Clearance Disabled (Valid Signing)

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST8",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "01110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### I. Example Response: Clearance Disabled (Valid Signing)

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLENFc2FURW5lQXpOalBPN01sRWw4N09UcmcvcnNiWlFTTnZLemp5MWs2Y289B2BNRVVDSVFEUzJSaitrY1JJc3RCZjFFWXI1L0JoVERIbm1LS0dKTUxaMEg1Z3p3a2gxUUlnSnJCeUxVU2VWMjBZZm9QMmlYYjBWRzZkK1NUeG12NWNPNklPd2dVS3kvZz0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABGGDDKDmhWAITDv7LXqLX2cmr6+qddUkpcLCvWs5rC2O29W/hS4ajAK4Qdnahym6MaijX75Cg3j4aao7ouYXJ9E="
    },
    "success": true,
    "message": "Clearance is disabled"
}
```

**_Status Code:_** 200

<br>

##### II. Example Request: Duplicate Invoice Number

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST8",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "02110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### II. Example Response: Duplicate Invoice Number

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLENFc2FURW5lQXpOalBPN01sRWw4N09UcmcvcnNiWlFTTnZLemp5MWs2Y289B2BNRVVDSVFEUzJSaitrY1JJc3RCZjFFWXI1L0JoVERIbm1LS0dKTUxaMEg1Z3p3a2gxUUlnSnJCeUxVU2VWMjBZZm9QMmlYYjBWRzZkK1NUeG12NWNPNklPd2dVS3kvZz0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABGGDDKDmhWAITDv7LXqLX2cmr6+qddUkpcLCvWs5rC2O29W/hS4ajAK4Qdnahym6MaijX75Cg3j4aao7ouYXJ9E="
    },
    "success": false,
    "message": "Invoice is submitted before with created/valid/valid with warnings status"
}
```

**_Status Code:_** 400

<br>

##### III. Example Request: Simplified Invoice (Reporting)

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST9",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "02110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### III. Example Response: Simplified Invoice (Reporting)

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLEJET2pkL0w0WFNmSUo2Z0xEWFBYMDR6Tk4rTEdjWjRqbU5jUjFiTmtURTg9B2BNRVVDSUh6WmsyeGV3SEFmTFQ4VTE3THJ2RmRwRlB5bHIvelhsNDVFNnJwQVY5aGNBaUVBdXU3QWxiaHVUZEllVm9sS2FTN21meVgyT0s3U0hKVmlXRHBNRkp5aVppYz0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABGGDDKDmhWAITDv7LXqLX2cmr6+qddUkpcLCvWs5rC2O29W/hS4ajAK4Qdnahym6MaijX75Cg3j4aao7ouYXJ9EJRjBEAiA6CM08lbTXuWwiKOZVBWQ/sbMU7YpAp30Ydq6QuAhYWwIgUkX27AqFMzEONZs37VrCycUjtEsFHED/qFn4XXC1qpQ="
    },
    "success": true,
    "message": ""
}
```

**_Status Code:_** 200

<br>

##### IV. Example Request: Valid Submission

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST11",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "01110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### IV. Example Response: Valid Submission

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLGJPMVRoYzVESURGRUFUL1FOeTRWWTE3YnNIS1FZcnlobXI3S2Nucm9KeFk9B2BNRVVDSVFEemF1Y3NoZEowVWhhb2xFSzNmY3duM1NCMjRSMktUeEw4MW0xQlA1NngyZ0lnYkdiMDBXNXI0aUJsSzlFYi8rUlpFbDcvS25sa1BZTWQ5U2RQenI1L1JLND0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABEdifjdJ03b3+M0dTPofZCRfBK+8Gdbsnhw4TNmEqacHGTtrSNaba3UVrzamOy7hWZL2gUFQ92NuYweGxhoiuY4="
    },
    "success": true,
    "message": "CLEARED"
}
```

**_Status Code:_** 200

<br>

##### V. Example Request: Invalid Submission

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST12",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "01110101",
            "Value": "388888"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### V. Example Response: Invalid Submission

```js
{
    "data": {
        "validationResults": {
            "infoMessages": [
                {
                    "type": "INFO",
                    "code": "XSD_ZATCA_VALID",
                    "category": "XSD validation",
                    "message": "Complied with UBL 2.1 standards in line with ZATCA specifications",
                    "status": "PASS"
                }
            ],
            "warningMessages": [],
            "errorMessages": [
                {
                    "type": "ERROR",
                    "code": "BR-CL-01",
                    "category": "EN_16931",
                    "message": "The document type code MUST be coded by the invoice and credit note related code lists of UNTDID 1001.",
                    "status": "ERROR"
                },
                {
                    "type": "ERROR",
                    "code": "BR-KSA-05",
                    "category": "KSA",
                    "message": "The invoice type code (BT-3) must be equal to one of value from the subset of UN/CEFACT code list 1001, D.16B agreed for KSA electronic invoices.",
                    "status": "ERROR"
                }
            ],
            "status": "ERROR"
        },
        "clearanceStatus": "NOT_CLEARED"
    },
    "success": false,
    "message": "NOT_CLEARED"
}
```

**_Status Code:_** 400

<br>

### 4. Report

**_Endpoint:_**

```bash
Method: POST
Type: RAW
URL: {{baseUrl}}/api/taxprocessor/report
```

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST15",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "02110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

**_More example Requests/Responses:_**

##### I. Example Request: Successful Response (Standard)

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST14",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "01110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### I. Example Response: Successful Response (Standard)

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLHBib3M0c0pXWms5T0duMmlCeEJ5Y3RIRVlOcU9Ka3BrenZsNVRBbG9WRjA9B2BNRVFDSUZMUG9lbWMyLzV5cXBxWmVwY00rQUtEMDAxdWVGOEw3aVIzRWpBNk5vVytBaUFNV2k3bG8xZXFza1ZqOENLYWRybEdPNkhtbGtQbjVOYUFLSGFaMzZMT0RBPT0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABGGDDKDmhWAITDv7LXqLX2cmr6+qddUkpcLCvWs5rC2O29W/hS4ajAK4Qdnahym6MaijX75Cg3j4aao7ouYXJ9E="
    },
    "success": true,
    "message": ""
}
```

**_Status Code:_** 200

<br>

##### II. Example Request: Duplicate Invoice Number

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST14",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "01110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### II. Example Response: Duplicate Invoice Number

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLHBib3M0c0pXWms5T0duMmlCeEJ5Y3RIRVlOcU9Ka3BrenZsNVRBbG9WRjA9B2BNRVFDSUZMUG9lbWMyLzV5cXBxWmVwY00rQUtEMDAxdWVGOEw3aVIzRWpBNk5vVytBaUFNV2k3bG8xZXFza1ZqOENLYWRybEdPNkhtbGtQbjVOYUFLSGFaMzZMT0RBPT0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABGGDDKDmhWAITDv7LXqLX2cmr6+qddUkpcLCvWs5rC2O29W/hS4ajAK4Qdnahym6MaijX75Cg3j4aao7ouYXJ9E="
    },
    "success": false,
    "message": "Invoice is submitted before with created/valid/valid with warnings status"
}
```

**_Status Code:_** 400

<br>

##### III. Example Request: Successful Response (Simplified)

**_Body:_**

```js
{
    "EgsId": {{egsId}},
    "CompanyId": {{companyId}},
    "customerNo": "{{customerNo}}",
    "Invoice": {
        "ID": "TEST15",
        "IssueDate": "2022-03-13",
        "IssueTime": "14:40:40",
        "InvoiceTypeCode": {
            "name": "02110101",
            "Value": "388"
        },
        "DocumentCurrencyCode": "SAR",
        "TaxCurrencyCode": "SAR",
        "AccountingSupplierParty": {
            "PartyIdentification": {
                "SchemeID": "CRN",
                "Value": "454634645645654"
            },
            "PostalAddress": {
                "StreetName": "test",
                "BuildingNumber": "3454",
                "PlotIdentification": "1234",
                "CitySubdivisionName": "test",
                "CityName": "Riyadh",
                "PostalZone": "12345",
                "CountrySubentity": "test",
                "Country": "SA"
            },
            "PartyTaxScheme": "300075588700003",
            "RegistrationName": "Ahmed Mohamed AL Ahmady"
        },
        "AccountingCustomerParty": {
            "PartyIdentification": {
                "SchemeID": "NAT",
                "Value": "2345"
            },
            "PostalAddress": {
                "StreetName": "baaoun",
                "AdditionalStreetName": "sdsd",
                "BuildingNumber": "3353",
                "PlotIdentification": "3434",
                "CitySubdivisionName": "fgff",
                "CityName": "Dhurma",
                "PostalZone": "34534",
                "CountrySubentity": "ulhk",
                "Country": "SA"
            },
            "RegistrationName": "sdsa"
        },
        "ActualDeliveryDate": "2022-03-13",
        "LatestDeliveryDate": "2022-03-15",
        "PaymentMeansCode": "10",
        "AllowanceCharge": [
            {
                "ID": "1",
                "AllowanceChargeReason": "discount",
                "Amount": "2",
                "TaxCategory": {
                    "ID": "S",
                    "Percent": "15"
                }
            }
        ],
        "TaxTotal": {
            "TaxAmount": "144.9",
            "TaxSubtotal": [
                {
                    "TaxableAmount": "966.00",
                    "TaxAmount": "144.90",
                    "TaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                }
            ]
        },
        "taxTotalAccountingCurrency": {
            "TaxAmount": {
                "CurrencyID": "SAR",
                "Value": "144.9"
            }
        },
        "LegalMonetaryTotal": {
            "LineExtensionAmount": "966.00",
            "TaxExclusiveAmount": "964.00",
            "TaxInclusiveAmount": "1108.90",
            "AllowanceTotalAmount": "2.00",
            "PrepaidAmount": "0.00",
            "PayableAmount": "1108.90"
        },
        "InvoiceLine": [
            {
                "ID": "1",
                "unitCode": "PCE",
                "quantity": "44.000000",
                "LineExtensionAmount": "966.00",
                "TaxAmount": "144.90",
                "RoundingAmount": "1110.90",
                "Item": {
                    "Name": "dsd",
                    "ClassifiedTaxCategory": {
                        "ID": "S",
                        "Percent": "15.00"
                    }
                },
                "Price": {
                    "PriceAmount": "22.00",
                    "AllowanceCharge": {
                        "AllowanceChargeReason": "discount",
                        "Amount": "2.00"
                    }
                }
            }
        ]
    }
}
```

##### III. Example Response: Successful Response (Simplified)

```js
{
    "data": {
        "qr": "ARdBaG1lZCBNb2hhbWVkIEFMIEFobWFkeQIPMzAwMDc1NTg4NzAwMDAzAxQyMDIyLTAzLTEzVDE0OjQwOjQwWgQHMTEwOC45MAUFMTQ0LjkGLDhacmFNaUJpNm9NZGNPV21acVg0alBjWU5ITlNjVHlvb0xHRm84VjVLb2s9B2BNRVVDSVFEQnpPaVpycHBWNUw3NENKbGRjcEl0UlFTODFhQlNDT1g3QkU0V2gzQWpSZ0lnRHM3NTZobGs3bE00UEFDTlpRM0VWTGlaeWZYUGxJUWRxTmFQTG81NnBVVT0IWDBWMBAGByqGSM49AgEGBSuBBAAKA0IABGGDDKDmhWAITDv7LXqLX2cmr6+qddUkpcLCvWs5rC2O29W/hS4ajAK4Qdnahym6MaijX75Cg3j4aao7ouYXJ9EJRjBEAiA6CM08lbTXuWwiKOZVBWQ/sbMU7YpAp30Ydq6QuAhYWwIgUkX27AqFMzEONZs37VrCycUjtEsFHED/qFn4XXC1qpQ="
    },
    "success": true,
    "message": ""
}
```

**_Status Code:_** 200

<br>

---

[Back to top](#ksa-e-invoice)

> Generated at: 2022-10-19 16:57:58 by [docgen](https://github.com/thedevsaddam/docgen)
