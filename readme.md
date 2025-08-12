# LSPP Assignment - Intelligent Agent: Information Extraction

This project demonstrates an intelligent agent for extracting structured company information from unstructured essays using LangChain and Google's Gemini API. The agent processes text paragraph-by-paragraph to extract:

- **Company Name**: The name of the company
- **Founding Date**: When the company was founded (normalized to YYYY-MM-DD format)
- **Founders**: List of founders (real human names only)

## Features

- 📄 Paragraph-wise extraction using LangChain Expression Language (LCEL)
- 🤖 Utilizes Gemini LLM for accurate information extraction
- 📅 Smart date normalization (handles formats like "2010", "March 2010", "March 15, 2010")
- 📊 Outputs results to CSV with proper formatting
- 🔄 Rate limiting to avoid API quota issues
- 🔍 Preview functionality to see results before saving

## Setup Requirements

- Google Colab environment
- Gemini API key (stored in Colab secrets)
- Internet connection for package installation

## Files

- `Company_Info_Extractor.ipynb`: Main Jupyter notebook for running the extraction pipeline
- `company_info_extractor.py`: Python script containing core extraction logic
- `essay.txt`: Sample essay text containing company founding stories

# 🎯 How to Use This Notebook

### Step 1: Setup
1. **Add your Gemini API key** to Google Colab secrets:
   - Click the 🔑 icon in the left sidebar
   - Add a new secret named `GEMINI_API_KEY`
   - Paste your API key as the value

### Step 2: Run the Cells
1. **Run all cells** from top to bottom (Runtime → Run all)
2. The notebook will automatically process the sample essay text
3. Results will be displayed and saved to `company_info.csv`

### Step 3: Customize (Optional)

#### Use Your Own Text
Replace the `SAMPLE_ESSAY` variable with your own text:

```python
# Replace SAMPLE_ESSAY with your text
SAMPLE_ESSAY = """Your essay text here..."""
```

#### Upload a Text File
```python
# Upload and read a text file
from google.colab import files
uploaded = files.upload()
filename = list(uploaded.keys())[0]
with open(filename, 'r', encoding='utf-8') as f:
    SAMPLE_ESSAY = f.read()
```

#### Adjust Configuration
Modify the `CONFIG` dictionary to customize behavior:

```python
CONFIG = {
    'delay_sec': 2.0,          # Increase for stricter rate limiting
    'max_paragraphs': 5,       # Limit for testing (None = all)
    'show_preview': True,      # Show results preview
    'output_csv': 'my_companies.csv'  # Custom output filename
}
```

### Output Format

The CSV file contains these columns:
- **S.N.**: Serial number
- **Company Name**: Extracted company name
- **Founded in**: Founding date (YYYY-MM-DD format)
- **Founded by**: List of founders (JSON format)

### Troubleshooting

- **API Key Error**: Make sure your `GEMINI_API_KEY` is correctly set in Colab secrets
- **Rate Limit Error**: Increase `delay_sec` in the configuration
- **No Results**: Check if your text contains clear company founding information
- **Date Format Issues**: The system handles various date formats automatically

### Download Results

```python
# Download the CSV file
from google.colab import files
files.download('company_info.csv')
```

## Example Output

| S.N. | Company Name         | Founded in  | Founded by                                 |
|------|---------------------|-------------|--------------------------------------------|
| 1    | Microsoft Corporation| 1975-04-04  | ["Bill Gates", "Paul Allen"]               |
| 2    | Apple Inc.          | 1976-04-01  | ["Steve Jobs", "Steve Wozniak", "Ronald Wayne"] |

## Troubleshooting

- **API Key Error**: Ensure your Gemini API key is set correctly
- **Rate Limit Error**: Increase the delay between API calls
- **No Results**: Check if your text contains clear company founding information
- **Date Format Issues**: The system handles various date formats automatically

