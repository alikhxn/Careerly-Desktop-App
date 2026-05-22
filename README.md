# 🚀 Careerly — AI-Powered Career Assistant & Personalization Suite

**Careerly** is a premium, feature-rich Windows desktop application designed to modernize the job search, resume architecting, and interview preparation pipeline. Featuring a sleek dark-theme user interface built with high-fidelity GDI+ graphics, Careerly integrates a local **SQLite database**, advanced profile-compatibility search algorithms, and the state-of-the-art **Groq Cloud AI API (LLaMA 3.3)**.

---

## 🌟 Key Application Pillars

| Module | Core Responsibility | Core Technologies |
| :--- | :--- | :--- |
| **🔐 Secure Access Control** | Session-persistent login, secure account registrations. | SQLite, Regex validation |
| **👤 Live Portfolio Hub** | Centralized profiles mapping out user narratives, skills, and experiences. | relational SQLite schemas |
| **🔍 "For You" Job Matching** | Customized matchmaking scanning resume profiles against active job boards. | Stopword tokenization, Weighted relevance |
| **🤖 AI Resume Architect** | Generates highly optimized, ATS-friendly professional resumes. | LLaMA 3.3 70B, `PdfSharp`, Print services |
| **📝 MCQ Interview Prep** | Tailored technical questionnaires dynamically retrieved from the cloud or local fallbacks. | Groq Prompt-to-JSON, local MCQs |
| **🗺️ Career Roadmap Visualizer** | 4-stage milestone progressions calculating tiers based on user qualifications. | Dynamic GDI+ drawing, heuristic tier scoring |
| **🔔 Fuzzy Real-Time Job Alerts** | Dynamic alerts grading opportunities as *Top Match*, *Skill Match*, or *New*. | Match-percentage formulas, double buffering |

---

## 🎨 Premium Visual Interface & Design Aesthetics
Careerly prioritizes user experience with a tailored visual layout:
* **Rich Glassmorphism UI**: Backgrounds render dynamic **Radial and Path Gradient Brushes** with deep dark blues (`#102646` to `#000B29`) and electric cyan/blue borders (`#38B6FF`).
* **High-Performance Rendering**: Double-buffering is dynamically enabled on panels via reflection to eliminate flickering during rendering, ensuring ultra-smooth list scrolling.
* **GDI+ Visual Layouts**: UI controls utilize custom rounded corners rendered via specialized graphics path clipping.

---

## 📂 Deep Dive: Features & Core Functionality

### 1. Unified SQLite Backend & Persistent Sessions (`DatabaseHelper.cs`)
Careerly has moved away from scattered JSON file structures to a centralized, transaction-safe SQLite database (`careerly.db`). It automatically sets high-performance flags like **Write-Ahead Logging (PRAGMA journal_mode = WAL)**.
* **`Users` Table**: Secure accounts store logins.
* **`Sessions` Table**: Tracks active user sessions, allowing users to remain logged in automatically when the application is reopened.
* **`Portfolios` Table**: Relational database linking details like chosen fields, work experience lists, and skill keywords.

### 2. Advanced "For You" Matching Algorithm (`portfolioSearch.cs`)
Matches job seeking candidates with ideal roles by parsing the SQLite portfolio.
* **Fuzzy Parsing**: Automatically filters out standard English stopwords (e.g., *the*, *with*, *and*, *about*) to extract core contextual keywords.
* **Real-time Scoring**: Analyzes job titles, skills, descriptions, and experience requirements against the extracted profile tokens.
* **Seamless Fallback**: If no direct matches are found, it lists all jobs to prevent displaying an empty interface.

### 3. AI-Powered ATS-Optimized Resume Architect (`resume_generator.cs`)
Generates high-quality professional resumes on the fly.
* **LLaMA 3.3 Integration**: Sends structured candidate data (summary, skills, roles) to the **Groq API** (`llama-3.3-70b-versatile`) with target rules demanding structured, ATS-friendly plain-text formatting.
* **Offline Backup Template**: If the network is down or API limits are hit, a robust local string-builder formats a beautiful clean resume template automatically.
* **Multi-Format Exporting**:
  * **PDF Export**: Renders beautiful structured A4 documents utilizing `PdfSharp` and a custom Windows font resolver to avoid font-mapping errors.
  * **Plain Text**: Outputs `.txt` files for rapid copy-pasting.
  * **System Print**: Connects directly to local print systems via `PrintDocument`.

### 4. Interactive MCQ Interview Prep Engine (`interview_prep.cs`)
A fully-interactive suite enabling users to prepare for technical interviews.
* **Dynamic AI Quizzes**: Connects to the Groq API to dynamically generate exactly 10 advanced multiple-choice questions for any custom topic, returning them in a strict JSON schema.
* **Offline Fallbacks**: Includes extensive localized MCQ databases (`dsa_mcq_questions.json`, `mysql_mcq_questions.json`, etc.) with randomizers.
* **Micro-Interactive Feedback**: Color codes user options instantly (Green for correct, Red for incorrect) and displays an ending performance report card detailing score percentages and grades.

### 5. Multi-Stage Career Roadmaps (`career_roadmap.cs`)
Creates structured, step-by-step development plans customized to the candidate's chosen industry (Software Engineering, Data Science, Marketing, Finance, or Healthcare).
* ** Milestones**: Guides the user through 4 major milestones: **Foundation**, **Intermediate**, **Advanced**, and **Expert**.
* **Smart Placement**: Evaluates the user's current skills and experiences to mathematically estimate where they fit on the roadmap.
* **Requirements & Roles**: Recommends key industry certifications (e.g., AWS Solutions Architect, HubSpot certifications) and outlines specific target roles for each milestone.

### 6. Personalized Job Alerts Suite (`job_alerts.cs`)
Monitors and displays active job opportunities, calculating match percentages and categorizing alerts:
* **Top Match** ($\ge 75\%$): Roles highly aligned with candidate skills.
* **Skill Match**: Highlights roles matching specific technical keywords.
* **New Opportunity**: Displays newly posted positions within their field.
* **Fuzzy Filters**: Users can run live text searches across titles, companies, and skills.

---


## 💻 Tech Stack & Dependencies
* **Core Runtime**: `.NET 8.0` SDK / Windows Desktop Runtime
* **Language**: C# 12
* **Desktop Framework**: Windows Forms (WinForms) with custom paint overrides
* **Database**: SQLite via NuGet `Microsoft.Data.Sqlite`
* **JSON Processing**: `Newtonsoft.Json`
* **PDF Engine**: `PdfSharp` (Version 6+)
* **AI Integration**: Groq Cloud REST APIs (LLaMA 3.3 70B model)

---

## 🚀 How to Set Up & Run the Project

Follow these steps carefully to run Careerly on your local Windows machine:

### 1. Unblock the ZIP Folder (Crucial for Windows Security)
* Locate your downloaded `Careerly.zip` file.
* Right-click the file and select **Properties**.
* In the **General** tab, check the **Unblock** box (found at the bottom of the window). Click **Apply** and **OK**.

### 2. Extract the Files
* Extract the contents of the ZIP folder.
* *Note: To avoid Windows path length limitations, extract the project to a short path close to the root drive (e.g., `C:\Projects\Careerly`).*

### 3. Launch in Visual Studio
* Open **Visual Studio 2022** (or latest).
* Choose **Open a project or solution**.
* Navigate to your extracted directory and select the `idkabhikeliyetry.sln` solution file.

### 4. Restore NuGet Packages & Run
* Wait for Visual Studio to restore the necessary NuGet packages (`Microsoft.Data.Sqlite`, `Newtonsoft.Json`, and `PdfSharp`).
* Verify that you have an active internet connection (required for the AI Resume Builder and AI Interview Quiz features).
* Press **F5** or click the **Start/Run** button to launch the application.

---

## 🔍 Inspecting the Database (Optional)
If you want to view, audit, or verify the saved profiles, credentials, or sessions directly, a helper Python script is included in the project:

1. Open your terminal inside the project directory.
2. Run the script:
   ```bash
   python view_database.py
   ```
*(Note: Ensure the app has been run at least once so the `careerly.db` file is successfully generated in the build output directory).*
