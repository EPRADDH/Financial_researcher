# Financial Research Project with CrewAI

## Project Overview
This project uses CrewAI to perform automated financial research on companies. The system creates a crew of AI agents that work together to gather, analyze, and compile comprehensive financial reports.

## Project Structure
```
Fin-research/
├── financ/
│   ├── src/
│   │   └── financ/
│   │       ├── __init__.py
│   │       ├── main.py          # Main execution script
│   │       ├── crew.py          # CrewAI crew definition
│   │       ├── config/
│   │       │   ├── agents.yaml  # Agent configurations
│   │       │   └── tasks.yaml   # Task definitions
│   │       └── tools/
│   │           ├── __init__.py
│   │           └── custom_tool.py
│   ├── knowledge/
│   │   └── user_preference.txt
│   ├── tests/
│   ├── pyproject.toml
│   ├── README.md
│   └── uv.lock
└── project.md (this file)
```

## Project Components

### 1. Main Execution (`main.py`)
- Entry point for the application
- Creates output directory
- Runs research on specified company (currently set to 'Apple')
- Saves report to `output/report.md`

### 2. Crew Definition (`crew.py`)
- **ResearchCrew Class**: Main crew orchestrator
- **Two Agents**:
  - **Researcher Agent**: Gathers financial data using SerperDevTool
  - **Analyst Agent**: Analyzes data and creates reports
- **Two Tasks**:
  - **Research Task**: Comprehensive company research
  - **Analysis Task**: Report generation and analysis

### 3. Agent Configuration (`agents.yaml`)
- **Researcher Agent**:
  - Role: Senior Financial Researcher
  - Goal: Research company, news, and potential
  - Uses OpenAI GPT-4o-mini
- **Analyst Agent**:
  - Role: Market Analyst and Report Writer
  - Goal: Create comprehensive, well-structured reports
  - Uses OpenAI GPT-4o-mini

### 4. Task Configuration (`tasks.yaml`)
- **Research Task**:
  - Focuses on: company status, performance, challenges, news, outlook
  - Output: Structured research document
- **Analysis Task**:
  - Creates executive summary and comprehensive report
  - Includes market outlook (non-trading advice)
  - Output: Professional report saved to `output/report.md`

## Setup Steps

### 1. Python Version Requirements
**CRITICAL**: This project requires Python 3.10-3.13 (as specified in pyproject.toml)

#### Why Python 3.10+?
- CrewAI requires Python >=3.10,<3.14
- Avoids compilation issues with C++ extensions on Windows
- Ensures compatibility with all dependencies

### 2. Create Virtual Environment
```powershell
# Navigate to project root
cd "C:\Users\pradeep.dhote\Videos\Pradeep Prectice Folder -Gen AI & MLOps\Crew-AI\Fin-research"

# Create virtual environment with Python 3.10
py -3.10 -m venv .venv

# Activate virtual environment (PowerShell)
.\.venv\Scripts\Activate.ps1

# Verify Python version
python --version  # Should show Python 3.10.x
```

### 3. Install Dependencies
```powershell
# Navigate to financ directory
cd financ

# Install project dependencies using pyproject.toml
pip install -e .

# Or install directly
pip install "crewai[tools]>=0.130.0,<1.0.0"
```

### 4. Environment Variables Setup
Create a `.env` file in the project root:
```env
# Required API Keys
OPENAI_API_KEY=your_openai_api_key_here
SERPER_API_KEY=your_serper_api_key_here

# Optional: Additional API keys for enhanced functionality
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_key_here
YAHOO_FINANCE_API_KEY=your_yahoo_finance_key_here
```

## Running the Project

### Basic Execution
```powershell
# From financ directory, with virtual environment activated
cd financ/src
python -m financ.main
```

### Using Project Scripts
```powershell
# From financ directory
financ
# OR
run_crew
```

### Custom Company Research
Modify the `inputs` dictionary in `main.py`:
```python
inputs = {
    'company': 'Microsoft',  # Change company name here
}
```

## Dependencies

### Core Dependencies (from pyproject.toml)
- **crewai[tools]>=0.130.0,<1.0.0**: Main framework with tools support
- **Python >=3.10,<3.14**: Required Python version range

### Tools Used
- **SerperDevTool**: Web search functionality for research
- **OpenAI GPT-4o-mini**: LLM for both agents

## Known Issues and Solutions

### 1. Python Version Issues
- **Problem**: CrewAI requires specific Python version range
- **Solution**: Use Python 3.10-3.13 as specified in pyproject.toml
- **Error**: If using Python 3.14+, downgrade to 3.13 or lower

### 2. Windows C++ Compilation Issues
- **Problem**: Some dependencies require C++ compilation on Windows
- **Error**: `cl.exe failed with exit code 2`
- **Solutions**:
  - Install Visual Studio Build Tools 2022
  - Use pre-compiled wheels: `pip install --prefer-binary crewai[tools]`
  - Install Microsoft C++ Build Tools

### 3. API Key Issues
- **Problem**: Missing or invalid API keys
- **Solution**: Ensure OPENAI_API_KEY and SERPER_API_KEY are set in .env file
- **Verification**: Check API key permissions and quotas

## Project Features

### 1. Automated Financial Research
- Company financial analysis
- News and event tracking
- Performance evaluation
- Future outlook assessment

### 2. Two-Agent System
- **Research Agent**: Gathers comprehensive company data using web search
- **Analysis Agent**: Processes data and creates professional reports

### 3. Structured Output
- Markdown reports saved to `output/report.md`
- Executive summary included
- Professional formatting with clear sections

## Troubleshooting

### Common Issues

1. **Import Errors**
   - Ensure you're in the correct directory (`financ/src`)
   - Check that virtual environment is activated
   - Verify Python path includes project modules

2. **API Key Errors**
   - Verify OPENAI_API_KEY and SERPER_API_KEY are set
   - Check API key permissions and quotas
   - Ensure keys are valid and active

3. **Installation Errors**
   - Use Python 3.10-3.13
   - Install Visual Studio Build Tools for Windows
   - Try: `pip install --prefer-binary crewai[tools]`

4. **Output Issues**
   - Ensure `output/` directory exists
   - Check file permissions
   - Verify report generation completed successfully

## Development Notes

### Current Configuration
- Uses OpenAI GPT-4o-mini for both agents
- Sequential process execution
- Verbose logging enabled
- SerperDev tool for web research

### Customization Options
- Modify `agents.yaml` to change agent roles and models
- Update `tasks.yaml` to customize research focus
- Add new tools in `tools/` directory
- Change company target in `main.py`

---

**Last Updated**: December 2024
**Python Version**: 3.10-3.13 (Required)
**CrewAI Version**: >=0.130.0,<1.0.0
**Project Status**: Functional with basic financial research capabilities 