# PDF-Analysis-using-LLM

A comprehensive Python toolkit for analyzing documents using state-of-the-art Large Language Models. This project demonstrates how to extract, summarize, generate questions, and answer queries from PDF documents using transformer-based models.

## 🚀 Features

- **PDF Text Extraction**: Extract text content from PDF documents
- **Document Summarization**: Generate concise summaries using T5 models
- **Intelligent Text Splitting**: Break documents into manageable passages
- **Automatic Question Generation**: Create relevant questions from document content
- **Question Answering**: Extract answers from documents using BERT-based QA models
- **Duplicate Question Filtering**: Avoid redundant question processing

## 📋 Prerequisites

- Python 3.7+
- pip package manager

## 🛠️ Installation

1. **Clone the repository**:
```bash
git clone <repository-url>
cd document-analysis-llm
```

2. **Install required dependencies**:
```bash
pip install pdfplumber
pip install transformers
pip install torch
pip install nltk
```

3. **Download NLTK data**:
```python
import nltk
nltk.download('punkt')
```

## 🎯 Usage

### Basic Document Analysis

1. **Place your PDF document** in the project directory

2. **Update the PDF path** in the script:
```python
pdf_path = "your_document.pdf"
```

3. **Run the analysis**:
```python
python main.py
```

### Step-by-Step Process

The analysis follows these key steps:

#### 1. Text Extraction
```python
import pdfplumber

with pdfplumber.open(pdf_path) as pdf:
    extracted_text = ""
    for page in pdf.pages:
        extracted_text += page.extract_text()
```

#### 2. Document Summarization
```python
from transformers import pipeline

summarizer = pipeline("summarization", model="t5-small")
summary = summarizer(document_text[:1000], max_length=150, min_length=30)
```

#### 3. Text Segmentation
```python
from nltk.tokenize import sent_tokenize

sentences = sent_tokenize(document_text)
# Combine into 200-word passages
```

#### 4. Question Generation
```python
qg_pipeline = pipeline("text2text-generation", model="valhalla/t5-base-qg-hl")
questions = qg_pipeline(f"generate questions: {passage}")
```

#### 5. Question Answering
```python
qa_pipeline = pipeline("question-answering", model="deepset/roberta-base-squad2")
answer = qa_pipeline({'question': question, 'context': passage})
```

## 🔧 Configuration

### Model Selection

You can customize the models used for different tasks:

- **Summarization**: `t5-small`, `t5-base`, `facebook/bart-large-cnn`
- **Question Generation**: `valhalla/t5-base-qg-hl`, `valhalla/t5-small-qg-hl`
- **Question Answering**: `deepset/roberta-base-squad2`, `distilbert-base-cased-distilled-squad`

### Parameters

Adjust these parameters based on your needs:

- **Passage Length**: Default 200 words (adjustable in text splitting)
- **Summary Length**: `max_length=150`, `min_length=30`
- **Questions per Passage**: Default 3 (configurable in `min_questions`)

## 📊 Output Format

The script generates:

1. **Extracted Text**: Saved as `extracted_text.txt`
2. **Document Summary**: Printed to console
3. **Generated Questions**: Organized by passage
4. **Question-Answer Pairs**: With confidence scores

### Sample Output
```
Passage 1:
GOOGLE TERMS OF SERVICE
Effective May 22, 2024...

Generated Questions:
- What is the meaning of the Terms of Service?
- What are the terms of service that govern how Google operates?
- What do these Terms of Service help define?

Q: What is the meaning of the Terms of Service?
A: certain things we've always believed to be true
```

## 🧪 Example Use Cases

- **Legal Document Analysis**: Extract key terms and conditions
- **Research Paper Review**: Generate study questions and summaries
- **Policy Document Processing**: Create FAQs from policy texts
- **Educational Content**: Generate quiz questions from textbooks
- **Contract Analysis**: Identify important clauses and obligations

## ⚡ Performance Optimization

- **Large Documents**: Process in chunks to avoid memory issues
- **GPU Acceleration**: Use CUDA-enabled PyTorch for faster inference
- **Model Caching**: Models are cached after first load for subsequent runs
- **Batch Processing**: Process multiple passages simultaneously

## 🚨 Limitations

- **PDF Complexity**: Complex layouts may affect text extraction quality
- **Model Size**: Larger models provide better results but require more resources
- **Language Support**: Current models are optimized for English text
- **Context Length**: Long documents may need chunking for optimal results

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 🙏 Acknowledgments

- **Hugging Face Transformers**: For the pre-trained models
- **Google Research**: For T5 and BERT architectures
- **NLTK**: For natural language processing utilities
- **pdfplumber**: For reliable PDF text extraction

## 📞 Support

For questions and support:
- Open an issue on GitHub
- Check the [documentation](docs/)
- Review existing issues for solutions

## 🔄 Version History

- **v1.0.0**: Initial release with basic document analysis features
- **v1.1.0**: Added question deduplication and improved error handling
- **v1.2.0**: Enhanced summarization with multiple model support

---

Made with ❤️ for the AI and NLP community
