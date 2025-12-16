# Guardrailed AI Agent with Security Validators

A comprehensive implementation of a production-ready AI agent with built-in safety guardrails using Google ADK (Agent Development Kit), Gemini, and Guardrails AI.

## 🎯 Overview

This notebook implements a self-contained AI agent protected by security validators that inspect and validate both user inputs and model outputs before they reach your application. It demonstrates how to build trustworthy AI systems with automated safety checks.

## ✨ Features

### Security Guardrails
- **Profanity Detection** - Blocks inappropriate language using Guardrails Hub validators
- **URL Blocking** - Custom validator prevents sharing of potentially malicious links
- **Input Validation** - Validates user requests before LLM processing
- **Output Validation** - Validates model responses before delivery to users

### Technical Stack
- **Google ADK** - Agent framework with lifecycle hooks and session management
- **Gemini 2.5 Flash** - High-performance LLM for general knowledge tasks
- **Guardrails AI** - Production-grade validation framework
- **Jupyter Notebook** - Interactive development and testing environment

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- Jupyter Notebook
- Google API Key ([Get one here](https://makersuite.google.com/app/apikey))

### Installation

1. **Clone or download the notebook**
```bash
   # Download guardrailed_agent.ipynb to your local machine
```

2. **Open in Jupyter**
```bash
   jupyter notebook guardrailed_agent.ipynb
```

3. **Run Cell 0 - Dependencies Installation**
   
   This installs all required packages:
   - `google-adk` - Agent framework
   - `google-genai` - Gemini SDK
   - `guardrails-ai` - Validation framework
   - `guardrails/profanity_free` - Hub validator
   
   **⚠️ IMPORTANT**: After Cell 0 completes, restart the kernel:
   - **Kernel → Restart Kernel → Run All**

4. **Run Cell 1 - API Key Configuration**
   
   Paste your Google API key when prompted

5. **Run remaining cells in order** (Cells 2-8)

## 📖 Notebook Structure

### Cell 0: Dependencies Installation
Automated setup that installs all required packages and guardrails hub validators.

### Cell 1: API Key Configuration
Configure your Google API key for Gemini access.

### Cell 2: Core Imports
Imports all necessary libraries with warning suppression for clean output.

### Cell 3: Security Validators
Defines custom validators:
- `URLDetector` - Regex-based URL detection and blocking
- `ProfanityFree` - Guardrails Hub profanity validator
- `INPUT_GUARD` - Combined input validation
- `OUTPUT_GUARD` - Combined output validation

### Cell 4: Guardrail Callbacks
Lifecycle hooks that intercept agent execution:
- `input_guardrail_callback` - Validates before LLM call
- `output_guardrail_callback` - Validates after LLM response

### Cell 5: Root Agent
Creates the main agent with attached guardrails:
```python
root_agent = LlmAgent(
    name="root_agent",
    model="gemini-2.5-flash",
    before_model_callback=input_guardrail_callback,
    after_model_callback=output_guardrail_callback,
)
```

### Cell 6: Validator Unit Tests
Comprehensive test suite validating:
- ✅ Safe input acceptance
- 🚫 HTTPS/HTTP URL blocking
- 🚫 Complex URL patterns
- 🚫 Multiple URLs
- ✅ Safe output acceptance
- 🚫 Output URL blocking

### Cell 7: Integration Tests
Real-world test scenarios using ADK Runtime:
1. Safe knowledge questions
2. URL injection attempts
3. Profanity in input
4. Normal agent interactions

## 🛡️ How Guardrails Work

### Input Validation Flow
```
User Input → INPUT_GUARD → LLM (if safe) → Response
                 ↓
          (if unsafe) → Rejection Message
```

### Output Validation Flow
```
LLM Response → OUTPUT_GUARD → User (if safe)
                    ↓
             (if unsafe) → Sanitized Message
```

### Validation Rules

**URL Detection**
- Blocks `https://` and `http://` URLs
- Detects URLs with paths and query parameters
- Prevents link sharing in both input and output

**Profanity Filter**
- Uses Guardrails Hub `profanity_free` validator
- Blocks inappropriate language
- Applies to both user input and model output

## 📊 Test Results

The notebook includes two test suites:

### Validator Unit Tests (Cell 6)
```
✅ Safe Input
✅ HTTPS URL Blocking
✅ HTTP URL Blocking
✅ Safe Output
✅ Output URL Blocking
✅ Complex URL Blocking
✅ Multiple URL Blocking

📊 Results: 7/7 tests passed (100%)
```

### Integration Tests (Cell 7)
- Safe questions pass through
- URLs trigger input blocking
- Profanity triggers blocking
- Agent executes with ADK Runtime

## 🔧 Customization

### Adding New Validators

1. **Create validator class**
```python
class CustomValidator:
    @staticmethod
    def validate(text: str):
        if condition_violated(text):
            raise ValidationError("Custom rule violated")
```

2. **Add to guard**
```python
def validate_input(text: str):
    validate_url(text)
    validate_profanity(text)
    CustomValidator.validate(text)  # Add here
```

### Modifying URL Patterns

Edit the regex in `URLDetector`:
```python
URL_PATTERN = re.compile(
    r'your_custom_pattern_here',
    re.IGNORECASE
)
```

### Using Different Models

Change the model in Cell 5:
```python
root_agent = LlmAgent(
    model="gemini-2.5-pro",  # or "gemini-1.5-flash"
    # ... rest of config
)
```

## ⚠️ Important Notes

1. **Kernel Restart Required**: After installing dependencies (Cell 0), you MUST restart the kernel before proceeding

2. **Event Loop Warnings**: The notebook automatically suppresses Guardrails event loop warnings - this is expected behavior in Jupyter

3. **Synchronous Validation**: Validation uses synchronous mode in Jupyter for compatibility

4. **Session Management**: Each test run uses ADK's session service for proper conversation handling

## 🐛 Troubleshooting

### "Module not found" errors
- Ensure Cell 0 ran successfully
- Restart kernel after installation
- Check Python version (3.8+ required)

### API key errors
- Verify your Google API key is valid
- Check key has Gemini API access enabled
- Ensure key is properly pasted in Cell 1

### Guardrails validation not working
- Confirm `profanity_free` hub validator installed
- Check validation functions are properly defined
- Verify callbacks are attached to agent

## 📝 Example Usage
```python
# Safe input - passes validation
"What is the capital of France?"
→ Response: "The capital of France is Paris."

# URL in input - blocked
"Check https://example.com"
→ Response: "🚫 GUARDRAIL BLOCKED INPUT 🚫
Your request violates safety policies..."

# Profanity - blocked
"Inappropriate content here"
→ Response: "🚫 GUARDRAIL BLOCKED INPUT 🚫
Your request violates safety policies..."
```

## 🤝 Contributing

To extend this notebook:

1. Add new validators in Cell 3
2. Attach them in Cell 4 callbacks
3. Add test cases in Cells 6-7
4. Document changes in your fork

## 📄 License

This notebook is provided as-is for educational and development purposes.

## 🔗 Resources

- [Google ADK Documentation](https://developers.google.com/adk)
- [Guardrails AI Documentation](https://docs.guardrailsai.com/)
- [Guardrails Hub](https://hub.guardrailsai.com/)
- [Gemini API Documentation](https://ai.google.dev/docs)

## ✅ Validation Status

- ✅ All dependencies auto-install
- ✅ URL blocking validated
- ✅ Profanity detection validated
- ✅ Input guardrails operational
- ✅ Output guardrails operational
- ✅ ADK Runtime integration confirmed
- ✅ 100% test coverage

---

**Ready to build safe AI agents?** Start with Cell 0 and follow the notebook flow! 🚀