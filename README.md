# Shravani_Hiwase_Prediction-AI

## Prediction AI – Startup & Project Risk Analyzer

Prediction AI is an AI-assisted decision-support system built to evaluate startup ideas, business proposals, and project concepts. By analyzing project parameters, market conditions, and operational variables, it quantifies risk, assesses feasibility, and produces structured, actionable strategic guidance to help founders and teams make better decisions early.

## 📌 Output Capabilities

Starting from project information, market/competitor context, and calculated risk data, the system generates:

- Risk Assessment & Status Scoring
- Automated SWOT Analysis
- Feasibility Score
- AI-Generated Strategic Recommendations
- Risk Mitigation Strategies
- Interactive Assessment Dashboard

## 🎯 Project Objectives

- **Data Collection:** Capture and structure key project information (industry, budget, target market, business model).
- **Market Intelligence:** Analyze target market size (TAM/SAM/SOM) and competitor landscape.
- **Risk Evaluation:** Identify and quantify risk across market, team, resource, innovation, and research dimensions.
- **Risk Classification:** Classify each project by calculated risk level.
- **Success Estimation:** Estimate project success probability from the risk score.
- **Strategic Assessment:** Generate automated SWOT and feasibility analyses.
- **AI-Powered Recommendations:** Use an LLM to convert risk and SWOT data into concrete, project-specific strategic guidance, with a reliable rule-based fallback.

## 🔄 System Workflow
Project Information
↓
Market & Competitor Analysis
↓
Risk Assessment
↓
Risk Score & Risk Status
↓
Success Probability
↓
SWOT Analysis
↓
Feasibility Analysis
↓
LLM-Powered Strategic Recommendations
↓
Risk Mitigation
↓
Final Assessment Dashboard


## Milestones

### Milestone 1 – Information Collection & Market Intelligence

Establishes the project's foundation: a submission form capturing startup name, industry, business model, target market, budget, and description, feeding a market analysis module (TAM/SAM/SOM estimation) and a competitor landscape module, all persisted in PostgreSQL. This output becomes the input for risk assessment in Milestone 2.

### Milestone 2 – Risk Assessment & Feasibility

Evaluates the project across five dimensions — Market Competition, Team Expertise, Resource Availability, Innovation Level, and Market Research — to produce an Overall Risk Score, Risk Status, Success Probability, a full SWOT breakdown, and a Feasibility Score.

Risk classification:
70 or above → High Risk
40–69 → Medium Risk
Below 40 → Low Risk


Success probability:
Success Probability = max(0, 100 - Risk Score)


### Milestone 3 – Recommendations & Strategic Reasoning

Converts the outputs of Milestones 1 and 2 into concrete strategy using **direct Google Gemini integration**. The project's risk factors, SWOT data, and feasibility score are sent to Gemini, which returns tailored recommendations — each with a category, priority, problem statement, concrete action, and risk-reduction rationale — instead of fixed templated text. If the API call fails for any reason, the system automatically falls back to a rule-based recommendation engine so the dashboard never breaks.

Alongside this, a **Risk Mitigation** module provides, for each identified risk: Risk, Category, Impact, Priority, Mitigation Strategy, Preventive Action, and Contingency Action.

## Technology Stack

**Python** — primary language for all backend logic and engines.

**Streamlit** — powers the interactive four-tab dashboard (Project Input, Risk Assessment, Recommendations, Dashboard).

**Google Gemini** — the LLM reasoning layer for Milestone 3, called directly via the `google-genai` library, with the API key read securely from an environment variable rather than hardcoded.

**PostgreSQL** — structured storage for submitted projects and their generated assessments.

**HTML / CSS** — used within Streamlit for custom dashboard card styling.

## Key Project Components

- **market_analysis.py** – Generates market sizing (TAM/SAM/SOM) and competitor landscape data from project inputs.
- **risk_engine.py** – Calculates the overall risk score, risk status, and success probability.
- **swot_analysis.py** – Builds the Strengths/Weaknesses/Opportunities/Threats breakdown from risk inputs.
- **feasibility.py** – Computes the overall feasibility score.
- **recommendation_engine.py** – Rule-based recommendation logic, used as a fallback if the LLM call fails.
- **mitigation_engine.py** – Generates mitigation, preventive, and contingency strategies per identified risk.
- **llm_service.py** – Builds the prompt from project, risk, and SWOT data and calls Google Gemini to generate live, tailored strategic recommendations.
- **database.py / database.sql** – PostgreSQL connection handling and schema definitions.
- **app_streamlit.py** – The main Streamlit application tying every module together across all four tabs.

## My Contribution

- Set up and debugged the PostgreSQL + Python environment for Milestone 1 end-to-end.
- Designed and implemented the Milestone 3 Gemini LLM integration: prompt engineering in `llm_service.py`, structured JSON parsing, and wiring it into `app_streamlit.py` with an automatic rule-based fallback.
- Debugged and fixed HTML rendering and Python indentation issues across the Recommendations, Risk Mitigation, and LangGraph-panel sections of the dashboard.

## How to Run

1. `pip install -r requirements.txt`
2. Create a `.env` file in the project root: `GEMINI_API_KEY=your_key_here`
3. Set up PostgreSQL and update credentials in `database.py`
4. Run the schema in `database.sql`
5. `python -m streamlit run app_streamlit.py`

## Project Outcome

The system takes a project from raw submission through market analysis, risk scoring, and SWOT/feasibility evaluation, to a final dashboard of live, AI-reasoned strategic recommendations — helping teams understand:

What could go wrong → Why it matters → What can be done → How the project can be improved