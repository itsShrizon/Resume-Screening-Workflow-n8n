# 📄 Resume Screening Workflow 

This workflow automates fetching resumes from **Google Drive**, analyzing them with **Google Gemini** and **ChatGPT 4o**, and recording the results in **Google Sheets**. It is specifically designed for screening **AI Engineer** candidates based on a strict HR scoring rubric.

<br>

## 🎥 Watch the Demo Video

**👆 Click to see the workflow in action!**

[![🎬 CLICK TO WATCH: Resume Screening Workflow Demo](https://drive.google.com/uc?export=view&id=1HhEIx13JS3q4pi79Jc3XwqSc51qS7Do4)](https://www.youtube.com/watch?v=1QE4AMowVls)

**▶️ [🎥 WATCH FULL DEMO ON YOUTUBE](https://www.youtube.com/watch?v=1QE4AMowVls)** *(3 minutes)*

*Click the image above to watch the complete workflow demonstration*

## 📊 Results: Filtered Candidates Output

**See how deserving candidates get automatically filtered based on their scores!**

![Candidate Screening Results](https://drive.google.com/uc?export=view&id=1lrt4ortJM7xM-N9VQbIduQeO943rt0-K)

*The Google Sheet automatically populates with candidate data, scores, and detailed reasoning - making it easy to identify top talent at a glance.*

-----

## ⚙️ Workflow Overview

The workflow executes the following automated steps:

1. **🚀 Trigger**:
   - Starts manually when you click **Execute Workflow** in n8n.

2. **📂 Fetch Files from Google Drive**:
   - Searches a specified Google Drive folder for resumes and retrieves the latest file.

3. **📥 Download File**:
   - Downloads the candidate's resume for processing.

4. **🧠 Analyze Resume with Google Gemini**:
   - **Extracts Key Information**:
     - Candidate Name
     - Email Address
     - University
     - Years of Experience
   - **Scores based on a 100-point rubric**:
     - **Experience** (20 pts)
     - **Projects** (30 pts)
     - **Technical Skills** (30 pts)
     - **Relevancy** (20 pts)
   - **Applies Deductions For**:
     - Grammar, design, or authenticity issues.
     - Illogical or invalid claims.
     - Incomplete educational qualifications.

5. **✅ Validate JSON Output**:
   - Uses a `Switch` + `Code` node to ensure Gemini's output is **valid JSON** and cleans the response if necessary.

6. **📊 Append Results to Google Sheets**:
   - Writes the structured data into a Google Sheet with the following columns: `Name`, `Email`, `University Name`, `University Completed`, `Years of Experience`, `Score`, `Reason`, and `File Name`.

7. **🔄 Loop & Retry Mechanisms**:
   - Includes **Wait** and **Split In Batches** nodes to handle multiple resumes and prevent API errors through intelligent retries.

-----

## 🔑 Credentials Needed

- **Google Drive OAuth2** → To access resumes stored in your Drive.
- **Google Sheets OAuth2** → To write candidate results into your Sheet.
- **Google Gemini (PaLM API)** → To use the AI model for parsing and scoring.

-----

## 🛠️ Nodes Used

- **Manual Trigger**
- **Google Drive**
- **Split in Batches**
- **Google Gemini**
- **Switch**
- **Code Node**
- **Google Sheets**
- **Wait Nodes**

-----

## 🚀 Usage Instructions

1. **Set Up Credentials**:
   - Connect your **Google Drive**, **Google Sheets**, and **Gemini API** accounts in n8n.

2. **Update Configuration**:
   - In the `Search files and folders` node, replace the placeholder URL with your **Google Drive Folder URL**.
   - In the `Append row in sheet1` node, replace the placeholder ID with your **Google Sheets document ID**.

3. **Run the Workflow**:
   - Upload resumes (PDF/DOCX) into your configured Google Drive folder.
   - Click **Execute Workflow** in n8n and watch the candidate scores appear in your Google Sheet.

-----

## ⚖️ Scoring Philosophy

This workflow is designed to be **strict and stingy with points**. Candidates are likely to lose points if:

- Their projects are not directly related to AI/ML.
- They lack practical deployment or MLOps knowledge.
- Their project experienced outside the **preferred list**.
- Their resume suffers from poor grammar or unprofessional design.

-----

## 📌 Notes

- Resumes indicating a graduation date **later than July 2025** will automatically lose **10 points**.
- JSON parsing is strictly enforced to ensure **clean, structured output** every time.

-----

## 🗂️ Example Workflow Applications

- **University HR teams** screening AI Engineer applicants.
- **Recruitment agencies** managing large candidate pools.
- **Startups** automating their early-stage technical hiring process.
