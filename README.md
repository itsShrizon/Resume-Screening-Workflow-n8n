# 📄 Resume Screening Workflow (n8n)

This workflow automates the process of fetching resumes from **Google Drive**, analyzing them with **Google Gemini**, and recording the results in **Google Sheets**.
It is designed for screening AI Engineer candidates based on a **strict HR scoring rubric**.

---

## ⚙️ Workflow Overview

The workflow performs the following steps:

1. **Trigger**

   * Starts manually when you click **Execute Workflow** in n8n.

2. **Fetch Files from Google Drive**

   * Searches a specified Google Drive folder for resumes.
   * Gets the latest file.

3. **Download File**

   * Downloads the candidate’s resume.

4. **Analyze Resume with Google Gemini**

   * Extracts:

     * Candidate name
     * Email
     * University
     * Years of experience
   * Scores based on a **100-point rubric**:

     * **Experience** (20 pts)
     * **Projects** (30 pts)
     * **Technical Skills** (30 pts)
     * **Relevancy** (20 pts)
   
   * Applies deductions for:

     * Grammar, design, authenticity
     * Illogical or invalid claims
     * Incomplete education

5. **Validate JSON Output**

   * Uses a `Switch` + `Code` node to ensure Gemini output is **valid JSON**.
   * Cleans response if needed.

6. **Append Results to Google Sheets**

   * Appends candidate results into a Google Sheet with columns:

     * Name
     * Email
     * University Name
     * University Completed
     * Years of Experience
     * Score
     * Reason (Justification)
     * File Name

7. **Loop & Retry Mechanisms**

   * Several **Wait** and **Split In Batches** nodes handle multiple resumes and retries to avoid API errors.

---

## 📊 Google Sheets Output Format

| Name     | Email                                       | University Name | University Completed | Years of Experience | Score | Reason                                      | File Name           |
| -------- | ------------------------------------------- | --------------- | -------------------- | ------------------- | ----- | ------------------------------------------- | ------------------- |
| John Doe | [john@example.com](mailto:john@example.com) | Example University | Yes                  | 6                   | 78    | Lost points due to missing MLOps experience | Resume\_JohnDoe.pdf |

---

## 🔑 Credentials Needed

* **Google Drive OAuth2** → Access resumes stored in Drive.
* **Google Sheets OAuth2** → Write candidate results into Sheets.
* **Google Gemini (PaLM API)** → AI model for document parsing and scoring.

---

## 🛠️ Nodes Used

* **Manual Trigger** → Starts workflow manually.
* **Google Drive** → Search & download resumes.
* **Split in Batches** → Loop through multiple resumes.
* **Google Gemini** → Resume analysis & scoring.
* **Switch** → Check JSON validity.
* **Code Node** → Parse & clean AI output.
* **Google Sheets** → Append results to spreadsheet.
* **Wait Nodes** → Prevent API overload, handle retries.

---

## 🚀 Usage Instructions

1. **Set up credentials**:

   * Connect your **Google Drive**, **Google Sheets**, and **Gemini API** accounts in n8n.

2. **Update configuration**:

   * Replace the **Google Drive Folder URL** in `Search files and folders` node with your resume folder.
   * Replace the **Google Sheets document ID** in `Append row in sheet1` node with your results sheet.

3. **Run the workflow**:

   * Upload resumes (PDF/DOCX) into the configured Google Drive folder.
   * Click **Execute Workflow** in n8n.
   * Candidate scores will appear in Google Sheets.

---

## ⚖️ Scoring Philosophy

This workflow is **strict and stingy with points**.
Candidates typically lose points if:

* Their projects are not directly related to AI/ML.
* They lack deployment/MLOps knowledge.
* They studied outside the **preferred universities** list.
* Their resume has poor grammar or design.

---

## 📌 Notes

* The **preferred university list** includes BRAC, BUET, Dhaka University, NSU, SUST, and others.
* Resumes **not completed by July 2025** automatically lose **10 points**.
* JSON parsing is enforced, ensuring **clean structured output** every time.

---

## 🗂️ Example Workflow Applications

* **University HR teams** screening AI Engineer applicants.
* **Recruitment agencies** handling large candidate pools.
* **Startups** automating early-stage technical hiring.

