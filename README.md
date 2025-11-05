# AI Summarisation Tool

Turn long articles, research papers, or documents into concise summaries instantly. Then evaluate how good your summaries are with objective metrics.

## What This Does

1. **Summarize** any text (articles, research papers, news, docs, etc.)
2. **Evaluate** how good the summary is with objective metrics
3. **Improve** by understanding what makes a great summary
4. Works locally - you control your data and API keys

## How We Evaluate Summaries

After you generate a summary, we use three specialized metrics to evaluate how good it is:

### 1. **Summarization Score** (0.0 - 1.0)
Purpose-built metric specifically for evaluating summaries.

**What it checks:**
- Does the summary preserve key information from the source? (QA-based evaluation)
- Is the summary appropriately concise? (Length penalty)
- Are important facts and details captured?

**How it works:**
- Extracts keyphrases from the source text
- Generates questions based on those keyphrases
- Checks if the summary answers those questions
- Penalizes overly long summaries

**How to interpret:**
- **0.8-1.0**: ✅ Excellent - Summary captures all key information with good conciseness
- **0.6-0.8**: ✅ Good - Summary covers main points well
- **0.4-0.6**: ⚠️ Fair - Summary could better capture key information
- **<0.4**: ❌ Poor - Summary is missing important content

**Example:**
- Article has 500 words discussing Apple, investment, AI, researchers, locations
- Bad summary: "Apple made announcement" → Missing key details (low score)
- Good summary: "Apple investing $1B in AI research with 500 new hires" → Captures essentials (high score)

---

### 2. **Faithfulness** (0.0 - 1.0)
Measures if the summary stays grounded in the source material without hallucinating.

**What it checks:**
- Are claims in the summary supported by the source?
- Does it avoid making up information?
- Are facts accurately represented?

**How to interpret:**
- **0.9-1.0**: ✅ Excellent - Summary is faithful to source
- **0.7-0.9**: ✅ Good - Mostly accurate with minor issues
- **0.5-0.7**: ⚠️ Fair - Some claims not fully grounded
- **<0.5**: ❌ Poor - Summary contains hallucinations

**Example:**
- Source: "Revenue was $10 billion in 2023"
- Faithful summary: "The company reported $10 billion revenue" ✅
- Hallucinated summary: "The company doubled revenue to $20 billion" ❌

---

### 3. **Overall Quality** (Categorical: poor/fair/good/excellent)
Expert assessment of the summary quality across multiple dimensions.

**What it checks:**
- Is the summary well-written and clear?
- Does it accurately convey the source material?
- Is it useful and informative?
- Overall expert judgment on summary quality

**How to interpret:**
- **Excellent**: Outstanding summary - accurate, complete, well-written
- **Good**: High-quality summary - meets all key requirements
- **Fair**: Acceptable summary - has strengths but some areas for improvement
- **Poor**: Low-quality summary - needs significant revision

---

## 🚀 Quick Start

### 1. Install Dependencies

```bash
pip install ragas langchain-openai python-dotenv pypdf python-docx
```

Or for minimal setup:
```bash
pip install ragas langchain-openai python-dotenv
```

**What you're installing:**
- `ragas` - Evaluation metrics
- `langchain-openai` - OpenAI integration
- `python-dotenv` - Load environment variables from .env
- `pypdf` - Optional: Read PDF files
- `python-docx` - Optional: Read Word documents

### 2. Set Up LLM Credentials

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

### 3. Run the Notebook

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

## 💡 What The Scores Mean

**All three metrics combined tell you if your summary is good or needs work:**

| Summarization | Faithfulness | Overall Quality | Interpretation |
|---|---|---|---|
| 0.8+ | 0.9+ | Excellent/Good | ✅ Excellent summary - accurate, complete, professional |
| 0.6-0.8 | 0.7-0.9 | Good/Fair | ✅ Good summary - trustworthy and captures key info |
| 0.4-0.6 | 0.5-0.7 | Fair | ⚠️ Acceptable - could be improved |
| <0.4 | <0.5 | Poor | ❌ Poor summary - needs significant revision |

---

## How It Works

```
Your Text (article, research paper, etc.)
    ↓
[LLM generates summary]
    ↓
Generated Summary
    ↓
[Ragas evaluates with 3 metrics]
    │
    ├─ Summarization Score (QA-based + conciseness)
    ├─ Faithfulness (checks for hallucinations)
    └─ Overall Quality (expert assessment)
    ↓
Scores + Interpretation + Recommendations
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

## ⚠️ Important Notes

- **All metrics require an LLM** (uses your API key - OpenAI, Claude, etc.)
- **Summarization Score** uses keyphrases and QA to evaluate comprehensiveness
- **Faithfulness** checks if summary stays grounded in source
- **Overall Quality** combines multiple evaluation perspectives
- Costs depend on LLM provider (typically $0.01-0.05 per evaluation)
- For best results, use recent models (GPT-4o, Claude 3.5 Sonnet)

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
