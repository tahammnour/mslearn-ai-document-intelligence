# 📄 Document Analysis with Azure AI Document Intelligence

Welcome to the Document Analysis Python project! This application demonstrates how to use Azure AI Document Intelligence (formerly Form Recognizer) to extract information from invoices automatically. 🚀

## 🎯 What Does This Code Do?

The `document-analysis.py` script analyzes invoices using Azure's prebuilt invoice model to extract key information like vendor names, customer names, and totals with confidence scores.

## 📋 Prerequisites

- 🐍 Python 3.7 or higher
- 🔑 Azure AI Document Intelligence resource
- 📦 Required packages (see requirements.txt)

## 🛠️ Setup

1. **Install Dependencies** 📥
   ```bash
   pip install -r requirements.txt
   ```

2. **Configure Azure Credentials** ⚙️
   - Update the `endpoint` and `key` variables in the script with your Azure AI Document Intelligence resource details

## 🔍 Code Breakdown

### 📚 Libraries Used
```python
from azure.core.credentials import AzureKeyCredential
from azure.ai.formrecognizer import DocumentAnalysisClient
```
- 🔐 **AzureKeyCredential**: Handles authentication with Azure services
- 📝 **DocumentAnalysisClient**: Main client for document analysis operations

### 🔧 Configuration
```python
endpoint = "https://doc-read-ai.cognitiveservices.azure.com/"
key = "your-api-key-here"
fileUri = "sample-invoice-url"
fileLocale = "en-US"
fileModelId = "prebuilt-invoice"
```
- 🌐 **endpoint**: Your Azure AI Document Intelligence service URL
- 🗝️ **key**: Authentication key for the service
- 📎 **fileUri**: URL of the invoice to analyze
- 🌍 **fileLocale**: Language/region setting
- 🏷️ **fileModelId**: Specifies using the prebuilt invoice model

### 🔄 Analysis Process

1. **Client Creation** 🏗️
   ```python
   document_analysis_client = DocumentAnalysisClient(
       endpoint=endpoint, credential=AzureKeyCredential(key)
   )
   ```
   Creates an authenticated client to communicate with Azure AI Document Intelligence.

2. **Document Analysis** 🔍
   ```python
   poller = document_analysis_client.begin_analyze_document_from_url(
       fileModelId, fileUri, locale=fileLocale
   )
   ```
   Starts the analysis process using the prebuilt invoice model.

3. **Results Processing** 📊
   ```python
   receipts = poller.result()
   ```
   Retrieves the analysis results when processing is complete.

### 📤 Extracted Information

The script extracts and displays:

- 🏪 **Vendor Name**: The company that issued the invoice
- 👤 **Customer Name**: The recipient of the invoice  
- 💰 **Invoice Total**: The total amount due (with currency symbol)

Each field includes a **confidence score** 📈 indicating how certain the AI is about the extracted value.

## 🚀 How to Run

1. Make sure you have your Azure credentials configured ✅
2. Run the script:
   ```bash
   python document-analysis.py
   ```

## 📈 Sample Output

```
Connecting to Forms Recognizer at: https://doc-read-ai.cognitiveservices.azure.com/
Analyzing invoice at: [invoice-url]

Vendor Name: Contoso Ltd., with confidence 0.95.
Customer Name: Microsoft Corp, with confidence 0.89.
Invoice Total: '$1,123.45, with confidence 0.92.

Analysis complete.
```

## 🎓 Learning Objectives

This sample demonstrates:
- 🔌 How to connect to Azure AI Document Intelligence
- 📄 Using prebuilt models for common document types
- 🎯 Extracting specific fields from structured documents
- 📊 Working with confidence scores for extracted data

## 🔗 Resources

- 📖 [Azure AI Document Intelligence Documentation](https://docs.microsoft.com/azure/applied-ai-services/form-recognizer/)
- 🐍 [Python SDK Reference](https://docs.microsoft.com/python/api/azure-ai-formrecognizer/)
- 🏷️ [Prebuilt Models Overview](https://docs.microsoft.com/azure/applied-ai-services/form-recognizer/concept-model-overview)

## ⚠️ Important Notes

- 🔐 **Security**: Never commit your actual API keys to version control
- 💰 **Costs**: Document analysis operations consume Azure credits
- 🌐 **Network**: Requires internet connection to access Azure services

Happy document analyzing! 🎉📄✨
