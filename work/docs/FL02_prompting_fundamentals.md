# FL-02: Prompting Fundamentals on Real Tasks v2

**Target Task:** Generating boilerplate `pytest` unit tests for Python utility functions (From my FL-01 Workflow Audit).

---

## The Prompt Iteration Log

### 0. The Baseline (Naive Prompt)
**Prompt:** "Write unit tests for this python function: `[def calculate_decay_score(clicks, impressions): return impressions / (clicks + 1)]`"

**Output Excerpt:**
```python
import unittest
def test_calculate_decay_score():
    assert calculate_decay_score(10, 100) == 9.090909090909092
```

**Notes:**
- **What changed in the prompt:** N/A (Baseline).
- **What actually improved in the output:** N/A (Baseline).
- **Failure points:** It used the built-in `unittest` module instead of `pytest`, hardcoded a massive floating-point decimal instead of using `pytest.approx`, and didn't test any edge cases.

---

### 1. Version 1 (+ Role Assignment)
**Prompt:** "**Act as a Senior Python QA Engineer.** Write unit tests for this python function: `[def calculate_decay_score(clicks, impressions): return impressions / (clicks + 1)]`"

**Output Excerpt:**
```python
import pytest
def test_calculate_decay_score_standard():
    # Validates standard expected behavior
    assert calculate_decay_score(9, 100) == 10.0
```

**Notes:**
- **What changed in the prompt:** Added role assignment ("Senior Python QA Engineer").
- **What actually improved in the output:** The AI instantly switched to using `pytest` (the industry standard) and added a professional docstring/comment explaining the test's purpose.
- **Failure points:** Still missing edge case testing (like negative numbers or zero).

---

### 2. Version 2 (+ Context and Motivation)
**Prompt:** "Act as a Senior Python QA Engineer. Write unit tests for this python function: `[code]`. **These tests are part of a critical data pipeline where silent failures cause corrupted analytics. We need to be absolutely certain it handles bizarre data gracefully.**"

**Output Excerpt:**
```python
import pytest
def test_calculate_decay_score_zero_clicks():
    assert calculate_decay_score(0, 100) == 100.0

def test_calculate_decay_score_negative_values():
    with pytest.raises(ValueError):
        calculate_decay_score(-5, 100)
```

**Notes:**
- **What changed in the prompt:** Added business context and motivation.
- **What actually improved in the output:** The AI automatically started anticipating bad data, writing tests for zero clicks and negative values without me having to specifically ask for them.
- **Failure points:** The AI assumes the function raises a `ValueError` for negative numbers, but the actual function I provided doesn't do that. It hallucinated behavior.

---

### 3. Version 3 (+ Step Decomposition)
**Prompt:** "Act as a Senior Python QA Engineer. Write unit tests for this python function: `[code]`. These tests are part of a critical data pipeline. **Step 1: Analyze the provided code and list all edge cases it currently handles or fails to handle. Step 2: Write the `pytest` functions only for the behavior currently implemented in the function.**"

**Output Excerpt:**
> *Step 1 Analysis:* The function handles 0 clicks well (avoids division by zero due to +1). It does NOT handle negative numbers or non-numeric types, but since it doesn't explicitly raise an error, the math will just evaluate normally or throw a native TypeError.
```python
# Step 2 Tests
def test_calculate_decay_score_zero_clicks():
    assert calculate_decay_score(0, 100) == 100.0
```

**Notes:**
- **What changed in the prompt:** Separated the task into two distinct steps (Analyze, then Write).
- **What actually improved in the output:** By forcing it to analyze the code *first*, it realized the function doesn't actually raise a `ValueError`, and it stopped writing hallucinated tests that would fail.
- **Failure points:** The output is a bit messy to read because it's mixing conversational analysis with code blocks.

---

### 4. Version 4 (+ Output Structure)
**Prompt:** "Act as a Senior Python QA Engineer. Write unit tests for this python function: `[code]`. These tests are part of a critical data pipeline. Step 1: Analyze edge cases. Step 2: Write the tests. **Format your output exactly like this:**
**### Analysis**
**[Your bullet points here]**
**### Code**
**[Your single markdown python block here]**"

**Output Excerpt:**
> ### Analysis
> * Handles zero clicks safely.
> * Fails on string inputs.
> ### Code
> ```python
> import pytest
> # ... [tests]
> ```

**Notes:**
- **What changed in the prompt:** Added explicit formatting constraints using markdown headers.
- **What actually improved in the output:** The response is perfectly organized, easy to skim, and all the code is contained in a single block, making it easy to copy-paste.
- **Failure points:** The actual python test names are a bit generic (e.g., `test_1`, `test_2`). I want them to follow a strict naming convention.

---

### 5. Version 5 (+ Few-Shot Examples)
**Prompt:** "Act as a Senior Python QA Engineer. Write unit tests for this python function: `[code]`. These tests are part of a critical data pipeline. Step 1: Analyze edge cases. Step 2: Write the tests. Format your output into '### Analysis' and '### Code'.
**Example of a good test name and structure:**
**```python**
**def test_calculate_decay_score__happy_path__returns_float():**
**    expected = 10.0**
**    actual = calculate_decay_score(clicks=9, impressions=100)**
**    assert actual == pytest.approx(expected, rel=1e-3)**
**```**"

**Output Excerpt:**
> ### Code
> ```python
> def test_calculate_decay_score__edge_case_zero_clicks__returns_max():
>     expected = 100.0
>     actual = calculate_decay_score(clicks=0, impressions=100)
>     assert actual == pytest.approx(expected, rel=1e-3)
> ```

**Notes:**
- **What changed in the prompt:** Added a specific few-shot example showing exact naming conventions, variable layout (`expected`, `actual`), and the use of `pytest.approx`.
- **What actually improved in the output:** The AI perfectly mimicked my preferred test architecture. Every generated test now uses the exact naming convention and layout I demonstrated. The output is flawless and ready to commit.

---

## Cross-Model Comparison: Claude vs. ChatGPT

I ran the final Version 5 prompt through both Claude (3.5 Sonnet) and ChatGPT (GPT-4o).

- **Tone:** ChatGPT was slightly conversational and added a polite intro/outro ("Sure thing! Here are your tests..."). Claude stayed strictly in the assigned "Senior Python QA Engineer" persona, providing the requested headers and nothing else.
- **Accuracy:** Both correctly analyzed the code and wrote functional `pytest` code using my `pytest.approx` structure. However, Claude accurately noted that floating point precision limits applied to the native python float division, whereas ChatGPT missed that nuance in the analysis step.
- **Structure:** Both perfectly followed the requested output structure (`### Analysis` and `### Code`).
- **Failure Points:** ChatGPT occasionally tried to include type hinting (`-> float`) on the test functions, which wasn't in my example and isn't strictly necessary for `pytest`. Claude's output required zero edits.

---

## The Final Reusable Template

```text
Act as a Senior Python QA Engineer. Write unit tests for the following Python function: 
`[INSERT_CODE_HERE]`

Motivation: These tests are part of a critical data pipeline where silent failures cause corrupted analytics. We need to be absolutely certain the function handles unexpected data gracefully based ONLY on the logic currently implemented.

Step 1: Analyze the provided code and list all edge cases it currently handles or fails to handle.
Step 2: Write the `pytest` functions covering the implemented behavior.

Format your output exactly like this:
### Analysis
[Your bullet points here]
### Code
[Your single markdown python block here]

Example of the required test structure and naming convention:
```python
def test_function_name__scenario__expected_outcome():
    expected = [EXPECTED_VALUE]
    actual = function_name(args)
    assert actual == pytest.approx(expected, rel=1e-3) # Use approx for floats
```
```
