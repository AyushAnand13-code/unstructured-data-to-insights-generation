#📄 Automated Invoice Data Extraction System  
*A no-code/low-code workflow using n8n, Google Drive, OCR, and Gemini for automated invoice processing*

---

## 🚀 Overview

This project automates the full process of reading invoice files (PDFs + Images) from a Google Drive folder, extracting key fields using AI, and storing the data into Google Sheets — without any manual work.

With one click, the system:

- Fetches all new files from your invoice folder  
- Identifies PDF vs PNG/JPG  
- Extracts text using PDF reader or OCR  
- Uses Google Gemini to extract structured fields  
- Updates two Google Sheets:
  - **Invoice Details**
  - **Invoice Items**

This eliminates manual copy-paste and ensures your sheet is always accurate and up to date.

---

## 🧠 Problem Statement

Manually reading invoices and adding details to a sheet is:

- Slow  
- Error-prone  
- Repetitive  
- Hard to maintain  

This workflow automates it end-to-end.

---

## 🧩 Features

✔ Works for both **PDF** and **image invoices**  
✔ AI-based field extraction  
✔ Processes all files in a folder automatically  
✔ Maintains clean & structured data  
✔ Extracts **item list** for multi-item invoices  
✔ Avoids duplicates using UID  
✔ Fully customizable

---

## 🛠️ Tech Stack

| Component | Purpose |
|----------|---------|
| **n8n** | Automation workflow |
| **Google Drive** | Invoice file storage |
| **Google Sheets** | Invoice database |
| **Google Gemini Model** | AI-powered information extraction |
| **OCR.Space API** | OCR for PNG/JPG |
| **PDF Extract Node** | Extracts text from PDFs |

---

---

## ⚙️ Step-by-step Workflow Explanation

### **1️⃣ Trigger the Workflow**
The workflow begins when you click **Execute** (can be changed to a scheduled CRON trigger).

---

### **2️⃣ Locate the Google Drive Invoice Folder**
- Uses the *Google Drive Node* to find the folder containing invoices.

---

### **3️⃣ Loop Through Files**
- Processes one file at a time through a loop node.

---

### **4️⃣ Switch Node — PDF vs PNG/JPG**
- Routes files based on type to appropriate extraction path.

---

### **5️⃣ PDF Processing**
- Uses `Extract from File` node to get text from PDF.

---

### **6️⃣ OCR for Images (PNG/JPG)**
- Uses **OCR.Space** API via HTTP Request node.

---

### **7️⃣ AI Information Extraction (Gemini)**
- Feeds raw text into n8n **Information Extractor** node powered by Gemini.

Sample prompt:
Extract key invoice fields from the following text and format output as JSON.

yaml
Copy code

---

### **8️⃣ Structured JSON Output Example**

```json
{
  "invoice_number": "INV-2045",
  "customer_name": "ABC Technologies",
  "date": "2023-11-12",
  "amount": 18450,
  "items": [
    {
      "item": "Laptop Sleeve",
      "qty": 2,
      "rate": 450,
      "total": 900
    },
    {
      "item": "Wireless Mouse",
      "qty": 1,
      "rate": 550,
      "total": 550
    }
  ]
}
9️
Write to Google Sheets — Invoice Details
Appends structured fields like:

Invoice Number

Customer Name

Amount

Date

File Name

Source

Extract and Store Item List
Uses:

Edit Fields node

Split Out node

Adds all line items into Invoice Items sheet.

A UID is generated to prevent duplicates.

