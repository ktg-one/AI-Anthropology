# How to Test Chain of Density

**Actual test methodology: Chain of Density + Memory Recall + 10 Questions**

---

## 🎯 What You Actually Tested

**Your Test Method:**
1. **Chain of Density prompt** - Applied to content/conversation
2. **Memory recall prompt** - Your special KTG-MEM protocol  
3. **10 questions append** - Ask LLM to "append 10 questions for another session to answer"
4. **Cross-session validation** - Test if those questions help context across sessions

**This tests:**
- ✅ **Context extension** - Can CoD preserve context for future sessions?
- ✅ **Memory retention** - Does compressed memory survive session boundaries?
- ✅ **Cross-session continuity** - Can LLM answer questions from previous session?
- ✅ **Information preservation** - Is context actually maintained?

---

## 🚀 Your Actual Test Method

### Step 1: Apply Chain of Density + Memory Recall
Give LLM:
- Chain of Density prompt
- Your special memory recall prompt (KTG-MEM)
- Content/conversation to compress

### Step 2: Generate 10 Questions
**Ask LLM**: "Append 10 questions for another session to answer"

LLM should generate 10 questions that:
- Cover key topics from the session
- Test important information retention
- Enable context validation in next session

### Step 3: Save Memory + Questions
- Save compressed memory (CoD output)
- Save the 10 questions
- Document Session 1 state

### Step 4: Test in Next Session
**Session 2:**
- Load compressed memory
- Present the 10 questions
- **Test**: Can LLM answer them correctly?
- **Measure**: Context retention quality

### Step 5: Evaluate
- ✅ **Success**: LLM answers questions correctly → CoD + Memory works!
- ❌ **Failure**: LLM can't answer → Context lost, need improvement

---

## 📊 Evaluation Metrics

### 1. Entity Count
- Count entities per iteration
- Should increase: 1-3 → 4-6 → 7-9 → 10-12 → 13-15

### 2. Token Count
- Should stay roughly constant (CoD's key feature)
- Baseline: Variable length
- CoD: Fixed length, increasing density

### 3. Information Retention
- Test: Can model answer questions about original text?
- CoD should retain more information than baseline

### 4. Density Score
- Entities per token
- Target: ~0.15 entities/token (optimal)

---

## 🧪 Test Format

### For Testing Me (Claude):

**Prompt:**
```
[Your Chain of Density prompt here]

Article: [Your test article]
```

**What to look for:**
- ✅ 5 iterations produced
- ✅ Each iteration adds entities
- ✅ Token count stays consistent
- ✅ Information density increases
- ✅ Quality improves per iteration

### For Testing Other LLMs:

**Same prompt, different models:**
- GPT-5
- Gemini Pro
- GPT-4 (baseline comparison)
- Claude 3.5 Sonnet

**Compare:**
- Which models follow CoD instructions best?
- Which produce best density?
- Which maintain quality?

---

## 📝 Test Cases

### Test Case 1: News Article
- **Source**: News article (~500-1000 words)
- **Measure**: Entity density, information retention
- **Expected**: CoD > Baseline

### Test Case 2: Technical Content
- **Source**: Technical documentation
- **Measure**: Concept retention, clarity
- **Expected**: CoD maintains technical accuracy

### Test Case 3: Research Paper
- **Source**: Research paper excerpt
- **Measure**: Key findings retention
- **Expected**: CoD captures more findings

---

## 🔬 Using Evaluation Frameworks

### OpenAI Evals
Create test dataset:
- Input: Article + CoD prompt
- Expected: 5 iterations with increasing density
- Measure: Entity count, token consistency

### Vertex AI
- Test CoD prompts in Vertex AI Studio
- Get percentile scores
- **⚠️ Screenshot results!**

### Custom Metrics (Benchmarks.md)
Apply your metrics:
- **Effectiveness**: Does CoD improve output quality?
- **Efficiency**: Token efficiency vs baseline
- **Worth**: Overall value score

---

## ✅ Quick Test Checklist

**Before testing:**
- [ ] Test article selected
- [ ] CoD prompt ready
- [ ] Evaluation criteria defined
- [ ] Results folder ready (`evals/results/`)

**During testing:**
- [ ] Test on Claude (me) - current conversation
- [ ] Test on GPT-5
- [ ] Test on Gemini Pro
- [ ] Test baseline (standard summarization)

**After testing:**
- [ ] Screenshot all results
- [ ] Document scores/metrics
- [ ] Compare CoD vs baseline
- [ ] Save to `evals/results/`

---

## 💡 Ready to Test?

**Give me:**
1. Your Chain of Density prompt
2. A test article
3. I'll produce the 5 iterations
4. We'll evaluate together

**Or test other models:**
- Use same prompt/article
- Compare results
- Document everything

---

*Let's test Chain of Density and get those validation stamps!*

