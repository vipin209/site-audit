# 🔗 Site-Audit

A **Node.js** tool for checking URLs from a sitemap, detecting broken links, and monitoring network requests.

## 🚀 Features

- **Sitemap Parsing**: Extracts all URLs from a given XML sitemap.
- **HTTP Status Checking**: Identifies URLs returning **400+ errors**.
- **Network Request Monitoring**: Detects failed network requests on loaded pages.
- **Concurrent Requests**: Uses a **semaphore** to limit concurrent connections.
- **JSON Reports**: Saves results in structured JSON files.

---

## 🛠️ Installation

### **1️⃣ Clone the Repository**

```sh
git clone https://github.com/your-username/link-checker.git
cd link-checker
```

### **2️⃣ Install Dependencies**

```sh
npm install
```

### **3️⃣ Run the Link Checker**

```sh
node index.js
```

---

## ⚙️ Configuration

You can modify the configuration in `index.js` or pass values via environment variables.

| Option           | Default Value | Description                          |
| ---------------- | ------------- | ------------------------------------ |
| `resultsFolder`  | "results"     | Folder where JSON reports are saved. |
| `batchSize`      | `20`          | Number of URLs processed at a time.  |
| `maxConnections` | `50`          | Max concurrent HTTP requests.        |

---

## 📌 Usage

### **1️⃣ Checking URLs from a Sitemap**

To check for **400+ HTTP errors**, modify `index.js` and call:

```js
const checker = new LinkChecker();
checker
  .fetchAndSplitUrls("https://example.com/sitemap.xml")
  .then((urls) => checker.checkUrlStatus(urls));
```

💾 **Output:**  
Results are saved in `results/non-200-responses.json` and `results/network-failures.json`.

`results/non-200-responses.json` would be save in the following format

```
[
  { "url": "https://example.com/about", "status": 404 },
  { "url": "https://example.com/safety", "status": 500 }
]
```

`results/network-failures.json` would be save in the following format

```
[
  {
    "url": "https://www.standuptocancer.org.uk/sites/default/files/downloadable_quiz_pack.pdf?_rsc=5wyb7",
    "status": 403,
    "resourceType": "fetch",
    "initiatingPage": "https://standuptocancer.org.uk/quiz"
  }
]
```
