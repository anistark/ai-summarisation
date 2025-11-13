# AI Summarisation Tool

Turn long articles, research papers, or documents into concise summaries instantly. Then evaluate how good your summaries are with objective metrics.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/anistark/ai-summarisation/blob/main/summarisation_demo.ipynb)

## What This Does

1. **Summarize** any text (articles, research papers, news, docs, etc.)
2. **Evaluate** how good the summary is with objective metrics
3. **Improve** by understanding what makes a great summary
4. Works locally - you control your data and API keys

## Evaluation Metrics

The tool uses RAGAS 0.3.9 metrics to evaluate summaries:

### 1. **Summary Score** (0.0 - 1.0)
QA-based metric evaluating information preservation and conciseness.

- **How**: Extracts keyphrases → generates questions → verifies answers in summary
- **0.8-1.0**: ✅ Excellent - Captures key information
- **0.6-0.8**: ✅ Good - Covers main points
- **0.4-0.6**: ⚠️ Fair - Missing important details
- **<0.4**: ❌ Poor - Significant information loss

### 2. **Faithfulness** (0.0 - 1.0)
Verifies claims are grounded in source without hallucination.

- **How**: Checks if summary statements are supported by source text
- **0.9-1.0**: ✅ Excellent - Fully grounded
- **0.7-0.9**: ✅ Good - Mostly accurate
- **0.5-0.7**: ⚠️ Fair - Some ungrounded claims
- **<0.5**: ❌ Poor - Contains hallucinations

---

## 🚀 Quick Start

### Option A: Run in Google Colab (Easiest)

Click the button at the top to open in Google Colab. Then:

1. Run the first cell to install dependencies
2. When prompted, add your OpenAI API key to Colab Secrets:
   - Click the 🔑 icon in the left sidebar
   - Create new secret: `OPENAI_API_KEY`
   - Paste your API key
3. Run the remaining cells

No setup needed - everything runs in the browser! ☁️

---

### Option B: Run Locally

#### 1. Install Dependencies

```bash
pip install ragas==0.3.9 langchain-openai langchain-core python-dotenv pypdf python-docx
```

**Required packages:**
- `ragas==0.3.9` - Evaluation metrics (SummaryScore, Faithfulness)
- `langchain-openai` - OpenAI integration
- `langchain-core` - LangChain base components
- `python-dotenv` - Environment variable management
- `pypdf` - PDF support
- `python-docx` - Word document support

#### 2. Set Up LLM Credentials

Copy the example env file and add your API key:

```bash
# Copy the example file
cp .env.example .env

# Edit .env and add your API key
# OPENAI_API_KEY=sk-...
```

**Supported LLM providers:**
- **OpenAI** (GPT-4o, GPT-4o-mini) - Recommended
- **Anthropic** (Claude 3.5 Sonnet, Claude 3 Opus)
- **Cohere** (Command R+)

The notebook will automatically load your API key from `.env`

⚠️ **Important:** Never commit `.env` to version control. It's already in `.gitignore`

#### 3. Run the Notebook

```bash
jupyter notebook summarisation_demo.ipynb
```

Then follow the cells to:
- Load example articles or your own files
- Generate summaries
- Run Ragas evaluations
- Interpret the scores

---

## File Support

The notebook supports:
- **Plain text** (.txt)
- **Markdown** (.md)
- **PDF** (.pdf) - requires `pypdf`
- **Word** (.docx) - requires `python-docx`

Just update the file path in the notebook cell.

---

## Score Interpretation

| Summary Score | Faithfulness | Result |
|---|---|---|
| 0.8+ | 0.9+ | ✅ High quality - publish with confidence |
| 0.6-0.8 | 0.7-0.9 | ✅ Good quality - minor review recommended |
| 0.4-0.6 | 0.5-0.7 | ⚠️ Acceptable - needs improvement |
| <0.4 | <0.5 | ❌ Poor - significant revision needed | |

---

## Workflow

```
Input Text
    ↓
LLM Summarization (gpt-3.5-turbo or custom)
    ↓
Generated Summary
    ↓
RAGAS Evaluation
    ├─ Summary Score (information preservation)
    └─ Faithfulness (factual accuracy)
    ↓
Scores + Recommendations
    ↓
Optional: Test Optimization Strategies
    ├─ Longer summary (5-7 sentences)
    ├─ Structured prompt (WHAT/WHY/WHERE)
    └─ Bullet points (key facts)
```

---

## Use Cases

- **News outlets**: Generate summaries and verify they're accurate before publishing
- **Research teams**: Automatically summarize papers and check if key findings are captured
- **Content creators**: Quickly summarize long articles and evaluate the quality
- **Learning**: Understand what makes a summary good using objective feedback
- **Model comparison**: Test different LLMs and see which generates better summaries

---

## 🤝 Examples in Notebook

The notebook includes pre-loaded examples:
1. Apple AI investment announcement
2. Electric vehicle environmental impact study
3. FDA medical treatment approval

Try running the evaluation on these first, then use your own content.

---

## Technical Notes

- **RAGAS 0.3.9**: Uses AsyncOpenAI client (not text-only mode)
- **LLM Required**: AsyncOpenAI for evaluations, OpenAI for summarization
- **API Costs**: ~$0.01-0.05 per summary + evaluation
- **Best Models**: GPT-4o, gpt-4o-mini (recommended for cost/quality)
- **Optimization**: Test multiple prompts to improve Summary Score
- **Faithfulness**: Automatically detects hallucinations and ungrounded claims

---

## 📚 Learn More

- [Ragas Documentation](https://docs.ragas.io/)
- [Faithfulness Metric](https://docs.ragas.io/en/latest/concepts/metrics/faithfulness.html)
- [Answer Relevance](https://docs.ragas.io/en/latest/concepts/metrics/answer_relevance.html)

---

## 📝 Next Steps

1. Fork/Clone this project
2. Install dependencies
3. Open `summarisation_demo.ipynb`
4. Run the example cells
5. Try with your own articles!
