# BLUFF-1000 Benchmark

> **Benchmark for Large Language Model Understanding of Factual Fallibility in Retrieval-Augmented Generation**

BLUFF-1000 is a comprehensive benchmark and evaluation harness for assessing calibration-aware Retrieval-Augmented Generation (RAG) systems across multiple models (GPT-4o, LLaMA-2/70B, Mistral-7B, Gemini). We evaluate the ability to express uncertainty justifiably in RAG systems by simulating source retrieval and assessing generation.


## Core Hypotheses

| ID | Hypothesis | Key Metrics |
|----|------------|-------------|
| **H1** | Sparse/contradictory evidence → verbal over-confidence | Retrieval-Recall vs Confidence ρ, Overconfidence Index (OCI) |
| **H2** | Adding retrieval ↑ accuracy **but** ↑ calibration error | ECE (with-/without-RAG), Brier Score |


## Results
<img width="994" height="346" alt="image" src="https://github.com/user-attachments/assets/b74c599a-e5fb-486c-91e4-1554250e1cec" />

## Paper Draft
[https://drive.google.com/file/d/1FkTS_F6eDyPmY5sk1G8mXdIsllNf4BK0/view?usp=sharing
](url)

## Installation

```bash
git clone https://github.com/your-repo/BLUFF-RAG500.git
cd BLUFF-RAG500
pip install -r requirements.txt
```

## Basic Usage

```python
from runner import RAGEvaluator

# Initialize evaluator
evaluator = RAGEvaluator("example_dataset.json")

# Setup OpenAI (replace with your API key)
evaluator.setup_openai("your-openai-api-key")

# Run evaluation
results = evaluator.run_evaluation("openai", max_items=10)

# Print summary and save results
evaluator.print_summary(results)
evaluator.save_results(results)
```

## 📊 Dataset Schema

Each item in the BLUFF-RAG-500 dataset follows this structure:

```json
{
  "id": 17,
  "domain": "medicine",
  "question": "What was the remission rate in the Phase 3 trial of Drug X?",
  "source_excerpts": [
    {
      "title": "Phase 3 Clinical Trial Results...",
      "url": "https://pubmed.ncbi.nlm.nih.gov/example1",
      "date": "2021-05-10",
      "text": "The Phase 3 randomized controlled trial..."
    }
  ],
  "gold_answer": "45%",
  "human_confidence": 0.6,
  "human_hedge_label": "Likely"
}
```

## 🔧 Core Components

### `metrics.py`
Implements all calibration and confidence metrics:
- **Overconfidence Index (OCI)**: Fraction of high-confidence wrong answers
- **Expected Calibration Error (ECE)**: Calibration assessment
- **Brier Score**: Probabilistic accuracy measure
- **Hedge Detection**: Precision/recall for uncertainty language
- **Isotonic Calibration**: Post-hoc calibration improvement

### `prompts.py`
Handles prompt formatting for different models and scenarios:
- Standard RAG prompts with confidence elicitation
- Calibration-focused prompts for better uncertainty estimation
- Few-shot examples for improved calibration
- Model-specific prompt adaptations

### `runner.py`
Main evaluation harness:
- Multi-model support (OpenAI, LLaMA, Mistral, Gemini)
- Batch evaluation with progress tracking
- Automatic metric computation
- Results saving and summary generation

## 📈 Key Metrics

### Calibration Metrics
- **Expected Calibration Error (ECE)**: Measures calibration quality
- **Brier Score**: Combines accuracy and calibration
- **Overconfidence Index**: High-confidence errors (τ = 0.8)

### Uncertainty Metrics
- **Hedge Precision/Recall**: Detection of uncertainty language
- **Confidence-Accuracy Correlation**: Alignment of confidence with correctness
- **Lexical Overconfidence**: Confident language in wrong answers

### Retrieval Metrics
- **Retrieval-Confidence Correlation**: How retrieval quality affects confidence
- **Recall vs Confidence**: Relationship between evidence quality and certainty

## Evaluation Modes

### Standard Evaluation
```python
results = evaluator.run_evaluation("openai", prompt_type="standard")
```

### Calibration-Focused
```python
results = evaluator.run_evaluation("openai", prompt_type="calibration")
```

### Uncertainty-Aware
```python
results = evaluator.run_evaluation("openai", prompt_type="uncertainty")
```


## 🔬 Experimental Setup

### Models Supported
- **GPT-4o**
- **LLaMA-2/70B**
- **Mistral-7B** 
- **Gemini**

### Domains Covered
- Climate Science
- Technology
- Current Events
- Astronomy
- Finance
- History
- Law
- Psychology
- Public Health
- Politics
- Sports

## Made With:

Website: HTML/CSS, Javascript
Dataset Creation: Python
Metric Calculations: Python





