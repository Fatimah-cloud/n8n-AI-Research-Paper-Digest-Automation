#  AI Research Paper Digest Automation

##  Overview

AI Research Paper Digest Automation is an **n8n workflow** that automatically retrieves the latest Artificial Intelligence research papers from the arXiv API every day, summarizes them using OpenAI, extracts important keywords, and stores the results in Google Sheets.

The workflow also filters papers based on abstract length, prevents duplicate entries, aggregates all processed papers into a single daily digest, and sends one email containing the summaries and links of all newly processed papers.


---

#  Features

-  Automatically runs every day at **8:00 AM**
-  Retrieves the latest AI research papers from the arXiv API
-  Converts XML responses into JSON
-  Processes each paper individually
-  Generates AI-powered summaries using OpenAI
-  Extracts five keywords for every paper
-  Saves results to Google Sheets
-  Prevents duplicate papers from being added
-  Sends Gmail notifications for skipped or failed papers
-  Includes error handling for reliable execution
-  Aggregates all processed papers into a single daily email digest

---

##  Technologies Used

- **n8n**
- **OpenAI GPT**
- **Google Sheets**
- **Gmail**
- **arXiv API**

---
<img width="752" height="199" alt="image" src="https://github.com/user-attachments/assets/e254748f-d499-41b0-bdc6-306a86cffdcf" />


##  Workflow

```
Schedule Trigger (Daily at 8:00 AM)
          │
          ▼
     HTTP Request
          │
          ▼
      XML Parser
          │
          ▼
      Split Out Papers
          │
          ▼
     Remove Duplicates
          │
          ▼
 IF (Abstract > 100 words?)
      /             \
     /               \
 True               False
  │                   │
  ▼                   ▼
OpenAI           Gmail Notification
  │
  ▼
Merge Original Data + AI Output
  │
  ▼
Google Sheets
 │
  ▼
Aggregate Papers
  │
  ▼
Gmail Daily Digest
---

#  Workflow Description

1. The workflow is triggered automatically every day at **8:00 AM**.
2. It retrieves the latest AI research papers from the **arXiv API**.
3. The XML response is converted into JSON format.
4. Each paper is processed individually.
5. Papers with abstracts longer than 100 words are summarized using OpenAI.
6. OpenAI returns:
   - A concise three-sentence summary
   - Five relevant keywords
7. The AI-generated content is merged with the original paper information.
8. The workflow checks for duplicate PaperIDs before saving.
9. New papers are appended to Google Sheets.
10. If a paper is skipped or an error occurs, Gmail sends a notification.
11. After all papers have been processed, the Aggregate node combines them into a single collection.
12. Gmail sends one daily email digest containing the summaries, keywords, publication dates, and links for all newly processed papers.

---

#  Google Sheets Output

| Column | Description |
|---------|-------------|
| PaperID | Unique arXiv paper identifier |
| Title | Research paper title |
| Authors | Paper authors |
| Summary | AI-generated summary |
| Keywords | AI-generated keywords |
| Published | Publication date |
| Link | Original arXiv URL |

---

#  Error Handling

The workflow includes error handling to improve reliability.

- Duplicate papers are skipped before processing.
- Papers with abstracts below the required threshold are excluded.
- OpenAI processes only valid papers.
- Processed papers are safely stored in Google Sheets.
- All successfully processed papers are aggregated into a single daily email.
- Individual failures do not interrupt the processing of the remaining papers.

