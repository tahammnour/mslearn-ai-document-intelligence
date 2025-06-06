# 🤖 Custom Document Intelligence - Python Implementation

Welcome to the Python implementation of Azure Document Intelligence custom model testing! This project demonstrates how to use Azure's Document Intelligence service to analyze custom forms and extract structured data.

## 📁 Project Overview

This Python application uses Azure Document Intelligence to analyze custom documents and extract specific fields with high confidence scores. It's designed to work with custom-trained models that can identify and extract data from various types of forms and documents.

## 🗂️ Files in this Directory

- `test-model.py` - Main Python script for document analysis
- `requirements.txt` - Python dependencies
- `README.md` - This documentation file
- `readme.txt` - Basic project description

## 🔧 Requirements

### Python Dependencies

Install the required packages using pip:

```bash
pip install -r requirements.txt
```

The `requirements.txt` file includes:
- `dotenv` 📄 - For loading environment variables from .env files
- `azure-ai-formrecognizer==3.3.3` 🔍 - Azure Document Intelligence client library

### Environment Variables

You need to set up the following environment variables in a `.env` file:

```env
DOC_INTELLIGENCE_ENDPOINT=your_azure_endpoint_here
DOC_INTELLIGENCE_KEY=your_azure_key_here
MODEL_ID=your_custom_model_id_here
```

## 🚀 How to Run

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Set up your environment variables** in a `.env` file

3. **Run the script:**
   ```bash
   python test-model.py
   ```

## 📊 Code Explanation

### Main Components

The `test-model.py` script performs the following operations:

1. **🔐 Authentication Setup**
   ```python
   document_analysis_client = DocumentAnalysisClient(
       endpoint=endpoint, credential=AzureKeyCredential(key)
   )
   ```

2. **📄 Document Analysis**
   ```python
   response = document_analysis_client.begin_analyze_document_from_url(model_id, formUrl)
   result = response.result()
   ```

3. **🔍 Field Extraction**
   ```python
   for name, field in document.fields.items():
       field_value = field.value if field.value else field.content
       print("Found field '{}' with value '{}' and with confidence {}".format(name, field_value, field.confidence))
   ```

### Key Features

- ✅ **Confidence Scoring** - Each extracted field comes with a confidence score
- 🌐 **URL-based Analysis** - Analyzes documents from web URLs
- 📋 **Multiple Field Types** - Extracts various types of data fields
- 🔄 **Batch Processing** - Can handle multiple documents in one analysis

## 📈 Sample Output

When you run the application successfully, you should see output similar to this:

```
@tahammnour ➜ .../mslearn-ai-document-intelligence/Labfiles/02-custom-document-intelligence/Python (main) $ python test-model.py
--------Analyzing document #1--------
Document has type docAI:docAI
Document has confidence 0.832
Document was analyzed by model with ID docAI
Found field 'PurchaseOrderNumber' with value '3929423' and with confidence 0.994
Found field 'PhoneNumber' with value '555-348-6512' and with confidence 0.99
Found field 'Website' with value 'www.herolimited.com' and with confidence 0.99
Found field 'CompanyAddress' with value '343 E Winter Road Seattle, WA 93849 Phone:' and with confidence 0.486
Found field 'Email' with value 'accounts@herolimited.com' and with confidence 0.949
Found field 'Subtotal' with value '$6750.00' and with confidence 0.994
Found field 'Quantity' with value '50.0' and with confidence 0.99
Found field 'Total' with value '$7350.00' and with confidence 0.994
Found field 'DatedAs' with value '04/04/2020' and with confidence 0.994
Found field 'Tax' with value '$600.00' and with confidence 0.993
Found field 'Signature' with value 'Josh Granger' and with confidence 0.452
Found field 'Merchant' with value 'Hero Limited' and with confidence 0.99
Found field 'CompanyName' with value 'Yoga for You' and with confidence 0.991
Found field 'VendorName' with value 'Seth Stanley' and with confidence 0.99
Found field 'CompanyPhoneNumber' with value '234-986-6454' and with confidence 0.995
-----------------------------------
```

## 📊 Extracted Fields

The custom model in this example can extract the following fields from documents:

| Field Name | Description | Sample Value | Confidence |
|------------|-------------|--------------|------------|
| 🆔 PurchaseOrderNumber | Order identification number | 3929423 | 0.994 |
| 📞 PhoneNumber | Contact phone number | 555-348-6512 | 0.99 |
| 🌐 Website | Company website URL | www.herolimited.com | 0.99 |
| 📍 CompanyAddress | Business address | 343 E Winter Road Seattle, WA | 0.486 |
| 📧 Email | Contact email address | accounts@herolimited.com | 0.949 |
| 💰 Subtotal | Pre-tax amount | $6750.00 | 0.994 |
| 📦 Quantity | Item quantity | 50.0 | 0.99 |
| 💵 Total | Final amount | $7350.00 | 0.994 |
| 📅 DatedAs | Document date | 04/04/2020 | 0.994 |
| 🏷️ Tax | Tax amount | $600.00 | 0.993 |
| ✍️ Signature | Signatory name | Josh Granger | 0.452 |
| 🏢 Merchant | Merchant name | Hero Limited | 0.99 |
| 🏪 CompanyName | Company name | Yoga for You | 0.991 |
| 👤 VendorName | Vendor name | Seth Stanley | 0.99 |
| ☎️ CompanyPhoneNumber | Company phone | 234-986-6454 | 0.995 |

## 🚨 Troubleshooting

### Common Issues

1. **🔑 Authentication Errors**
   - Verify your endpoint and key in the `.env` file
   - Ensure your Azure subscription is active

2. **📋 Model Not Found**
   - Check that your `MODEL_ID` is correct
   - Verify the model is deployed and accessible

3. **🌐 Network Issues**
   - Ensure you have internet connectivity
   - Check if the document URL is accessible

### 📝 Notes

- **Confidence Scores**: Values range from 0 to 1, where higher values indicate better accuracy
- **Field Detection**: Some fields may have lower confidence due to document quality or field complexity
- **Model Training**: Custom models need to be trained with sample documents before use

## 🔗 Related Resources

- [Azure Document Intelligence Documentation](https://docs.microsoft.com/azure/applied-ai-services/form-recognizer/)
- [Python SDK Documentation](https://docs.microsoft.com/python/api/azure-ai-formrecognizer/)
- [Custom Model Training Guide](https://docs.microsoft.com/azure/applied-ai-services/form-recognizer/how-to-guides/build-training-data-set)

---

*Happy Document Processing! 🎉*
