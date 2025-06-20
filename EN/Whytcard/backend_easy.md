# WhytCard Backend – Simple Overview

This document explains the **backend** of WhytCard in simple terms, with visuals, for non-technical readers.

## What is the Backend?

- Think of the backend as the **brain and engine room** of our app.
- It **takes requests** from the front (like fetching data), **processes** them, and **returns** results.

## High-Level Diagram

```
    [User / App]          
         |  
         v  
    +------------+        
    |  Frontend  |  <-- You interact here (web or mobile)
    +------------+        
         |  
         v  
+-------------------+     
|     Backend       |     
|  (API & Logic)    |     
+-------------------+     
         |  
         v  
 +-----------------+      
 |  Data Storage   |      
 +-----------------+      
```

The **Backend** has different **departments** (modules):

```
+---------------------------------------------+
|                 Backend                     |
|                                             |
|  [Config]  [Data]  [Scraping]  [RAG]  [Train]|
|                                             |
+---------------------------------------------+
```

## Departments Explained

1. **Config (Settings)**
   - Stores app settings (folder names, default values).
   - Automatically creates needed folders for data and logs.

2. **Data (📊 Dataset Module)**
   - Manages **collections of data** called *datasets*.
   - You can **create**, **view**, **update**, and **delete** datasets.
   - Also **import** records from files (CSV, JSON) and **clean/process** them.

3. **Scraping (🌐 Web Fetching Module)**
   - **Gathers information** from websites on demand.
   - You submit a **scraping job**, wait for it to finish, then **view results**.
   - Future: will handle HTML, PDFs, and follow robots.txt rules.

4. **RAG (🔍 Smart Search Module)**
   - **Indexes** data in a special vector store (like a smart library).
   - **Queries** let you ask questions and get **enhanced answers** using AI.
   - Currently a stub, to be implemented.

5. **Training (🤖 ML Model Module)**
   - **Runs model training** workflows to build or fine-tune AI models.
   - You can start a training job and **monitor** its progress.
   - Future tasks will handle data preparation and evaluation.

6. **Utils (🛠️ Helpers)**
   - Contains **shared tools**:
     - Error handling (uniform messages)
     - Logging setup (records what happens)
     - Common functions used by all modules.

## How It Works Together

1. **Frontend** (Web or Mobile) sends a request to the backend.
2. **Backend** routes the request to the right department:
   - Data → for any dataset work
   - Scraping → to fetch web data
   - RAG → to ask smart questions
   - Training → to train models
3. The department's **Service** does the work:
   - Reads/writes files
   - Calls AI or parsing tools
   - Applies data cleaning or model training
4. **Backend** sends the result back to the **Frontend**.

## Why This Matters

- **Separation of Concerns**: each module focuses on one job.
- **Clarity**: easy to add new features in their own area.
- **Maintenance**: bugs are easier to find and fix in small modules.

---

*End of simple backend overview.* 