🧠 Prompt Quality Scoring Agent
> A LangChain-powered agent that evaluates AI prompt quality across 5 criteria, returns a score out of 10, and suggests improvements — runnable in Google Colab.
📌 What It Does
Takes any prompt as input and returns:
Output	Description
Final Score	Weighted average of 5 criteria (0–10)
Per-Criterion Scores	Clarity, Specificity, Context, Output Format, Persona
Explanation	Short summary of strengths and weaknesses
Suggestions	2–3 concrete, actionable improvements
---
🏗️ Architecture
```
User Input (Prompt)
        │
        ▼
┌───────────────────┐
│  LangChain Chain  │
│  ┌─────────────┐  │
│  │ ChatPrompt  │  │
│  │  Template   │  │
│  └──────┬──────┘  │
│         │         │
│  ┌──────▼──────┐  │
│  │   LLM       │  │
│  │ (GPT-4o or  │  │
│  │  Claude 3)  │  │
│  └──────┬──────┘  │
│         │         │
│  ┌──────▼──────┐  │
│  │  Pydantic   │  │
│  │ OutputParser│  │
│  └─────────────┘  │
└───────────────────┘
        │
        ▼
Structured Evaluation Report
```
---
📊 Scoring Criteria
#	Criterion	What It Checks
1	Clarity	Is the goal easy to understand?
2	Specificity / Details	Are requirements and details provided?
3	Context	Is background, audience, or use case mentioned?
4	Output Format & Constraints	Is the expected format/tone/length specified?
5	Persona Defined	Is a role or persona assigned to the AI?
Final Score = Mean of all 5 criteria scores
---
🚀 Quick Start (Google Colab)
Step 1 — Open the Notebook
Click the Open in Colab badge above, or upload `prompt_quality_agent.ipynb` manually.
Step 2 — Install Dependencies
Run Cell 1 (Installation). This installs LangChain, OpenAI, and supporting libraries.
Step 3 — Set Your API Key
In Cell 2, enter your OpenAI API key when prompted:
```
Enter your OpenAI API key: sk-...
```
> **Note:** The key is stored in memory only and never written to disk.
Step 4 — Choose Your Model (Optional)
Default is `gpt-4o`. To use Claude 3.5 Sonnet instead, set:
```python
MODEL_PROVIDER = "anthropic"   # or "openai"
MODEL_NAME = "claude-3-5-sonnet-20241022"
```
Step 5 — Run the Agent
In the Interactive Demo cell, enter any prompt when prompted:
```
Enter a prompt to evaluate: Write me a poem
```
Step 6 — View Results
The agent prints a formatted evaluation report with scores and suggestions.
---
📦 Installation (Local)
```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/prompt-quality-agent.git
cd prompt-quality-agent

# Create a virtual environment
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set API key
export OPENAI_API_KEY="sk-..."

# Run the script version
python prompt_quality_agent.py
```
---
📋 Requirements
```
langchain>=0.2.0
langchain-openai>=0.1.0
langchain-anthropic>=0.1.0   # Optional, for Claude
openai>=1.0.0
pydantic>=2.0.0
python-dotenv>=1.0.0
rich>=13.0.0
```
---
🧪 Sample Test Results
Below are 8 test prompts with their expected scores, ranging from poor to excellent quality:
#	Prompt	Score
1	`Write me a poem`	~2.0
2	`Summarize this article`	~1.8
3	`Write a Python function to sort a list`	~3.5
4	`As a senior dev, explain REST APIs for beginners in 300 words`	~6.0
5	`Write a blog intro about AI trends for tech executives, 150 words, professional tone`	~6.8
6	`Act as a data analyst. Summarize this CSV sales data by region and month. Return a markdown table.`	~7.5
7	`You are a senior Python engineer. Write a type-annotated function that validates email addresses using regex. Include docstring and 3 unit tests. Return only code.`	~8.8
8	`You are an expert technical writer creating documentation for junior developers. Write a 500-word tutorial on async/await in Python. Use headers, bullet points, and one code example per concept. Tone: friendly but precise.`	~9.2
Full detailed results with per-criterion breakdowns are in Section 6 of the notebook.
---
📁 File Structure
```
prompt-quality-agent/
├── prompt_quality_agent.ipynb   # Main Google Colab notebook
├── prompt_quality_agent.py      # Standalone Python script
├── requirements.txt             # Python dependencies
├── README.md                    # This file
└── sample_outputs/
    └── test_results.json        # Pre-generated test results
```
---
🔧 Configuration Options
```python
# In Cell 2 of the notebook
CONFIG = {
    "model_provider": "openai",          # "openai" or "anthropic"
    "model_name": "gpt-4o",              # Model to use
    "temperature": 0.2,                  # Low = more consistent scores
    "show_raw_json": False,              # Show raw JSON output
    "export_results": False,             # Save results to JSON file
}
```
---
🤝 Contributing
Fork the repo
Create a feature branch: `git checkout -b feature/my-improvement`
Commit your changes: `git commit -m "Add my improvement"`
Push and open a Pull Request
---
📄 License
MIT License — see LICENSE for details.
---
