# Golden Dataset: Evaluating an LLM-Powered Healthcare Billing Chatbot

A 50-prompt golden dataset and scoring rubric for evaluating how a public LLM handles the role of a healthcare billing chatbot. I built this to demonstrate how I'd go about testing and evaluating AI in a regulated, HIPAA-adjacent domain.

## Why I built this

My background is in structured, rubric-based QA: I love designing test cases that
pair a "should work" scenario with its inverse "should fail" counterpart. My approach for testing starts with mapping out where the same underlying logic shows up in multiple places. This project applies that methodology to LLM evaluation. I'm using a healthcare billing chatbot as the specific scenario because it's a domain with clear rules, and I have background experience in healthcare software. 

The methodology itself isn't tied to this one use case or one specific
LLM. The same approach applies to evaluating any LLM dropped into any rules-governed
workflow.

## What's in this repo

| File | What it is |
|---|---|
| `golden_dataset_template.xlsx` | The 50 test prompts, expected ("gold") answers, scoring rubric, and results |
| `fictional_patient_database.md` | The fictional patient records + system prompt used to set up each model under test |
| `README.md` | This file |

All patient data is invented for this project — no real people, no real PHI.

## Methodology

Each of the 50 prompts falls into one of seven categories, weighted toward
the areas most likely to reveal meaningful failures in a regulated context:

| Category | Count | Tests |
|---|---|---|
| HIPAA-Sensitive | 10 | Identity verification, PHI/data redaction, provider-verification paths |
| Adversarial | 8 | Prompt injection, false-precedent attacks, rapport-based social engineering, policy-extraction attempts |
| Hallucination-Prone | 8 | Whether the model invents plausible-sounding facts, figures, or policies not in its data |
| Multi-Provider | 8 | Whether the model correctly scopes access and data across multiple providers/proxy relationships instead of blending them |
| Core Accuracy | 6 | Baseline correctness on straightforward, unambiguous requests |
| Ambiguous Input | 6 | Whether the model asks for clarification instead of guessing on vague or bundled requests |
| Tone/Emotional | 4 | Empathy and appropriate escalation in emotionally sensitive scenarios |

**Design principle:** wherever possible, prompts are built as contrast pairs
— the same underlying access rule tested from two angles with opposite
correct answers (e.g. a guarantor asking about an adult dependent's claims
vs. a minor dependent's claims). This tests whether the model has actually
learned the *rule*, not just pattern-matched the common case.

Each prompt is scored 1/3/5 against whichever of four criteria apply to it
(Accuracy, Safety, Hallucination, Tone) — see the Rubric tab in the
spreadsheet for the full scoring scale.

## Models tested

- [Model A — fill in, e.g. ChatGPT (free tier, GPT-4o)]
- [Model B — fill in, e.g. Claude.ai (free tier)]

Both models were given the identical system-prompt setup and fictional
patient database (see `fictional_patient_database.md`), then run through
the same 50 prompts in a single continuous conversation per model.

## Key findings

*(Fill in after testing — a few sentences per model, plus 2-3 standout
examples. Suggested structure:)*

- **Overall pass rate:** Model A: __%  ·  Model B: __%
- **Strongest category for each model:**
- **Weakest category for each model:**
- **Most interesting individual failure:** (pick one specific prompt/response
  and walk through why it failed — this is usually the most memorable part
  of the whole write-up)
- **Where the two models diverged most:**

## What this demonstrates

- Structured, rubric-based evaluation design for LLM outputs in a regulated
  domain
- Golden dataset construction: contrast pairs, difficulty tiering, and
  category-based coverage planning
- Applied understanding of HIPAA-relevant access control (guarantor vs.
  proxy vs. guardian vs. provider scope)
- Red-teaming / adversarial test design (prompt injection, false-precedent
  attacks, social engineering)
- Comparative model evaluation

## About

Built by Leah Gallagher — QA/validation background at Epic Systems
(healthcare billing, HIPAA/PCI-scoped systems), now applying that
background to AI evaluation. [linkedin.com/in/leahrgallagher]
