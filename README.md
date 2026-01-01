# 🧠 AI News Summarizer (Python)

A simple Python-based AI project that summarizes long text into short,
meaningful sentences using basic Natural Language Processing (NLP).

## 🚀 Features
- Automatic text summarization
- No external libraries required
- Beginner-friendly AI logic
- Clean and readable Python code

## 🛠 Technologies Used
- Python
- NLP (Frequency-based summarization)
- Regex & Collections

## 📌 How to Run
```bash
python summarizer.py
AI is being used in healthcare finance and education.
Many companies are investing heavily in AI research.
Ethical concerns about AI are growing rapidly.

---
summarizer.py
import re
from collections import Counter

def clean_text(text):
    text = text.lower()
    text = re.sub(r'[^a-zA-Z. ]', '', text)
    return text

def summarize(text, max_sentences=3):
    text = clean_text(text)
    sentences = text.split(".")
    words = text.split()

    stopwords = {
        "the","is","and","to","of","in","a","that","it",
        "on","for","with","as","was","were","this","by"
    }

    word_freq = Counter(word for word in words if word not in stopwords)

    sentence_scores = {}
    for sentence in sentences:
        for word in sentence.split():
            if word in word_freq:
                sentence_scores[sentence] = sentence_scores.get(sentence, 0) + word_freq[word]

    summary_sentences = sorted(sentence_scores, key=sentence_scores.get, reverse=True)
    summary = ". ".join(summary_sentences[:max_sentences])

    return summary.strip()

if __name__ == "__main__":
    article = """
    Artificial Intelligence is transforming the world.
    AI is being used in healthcare, finance, and education.
    Many companies are investing heavily in AI research.
    Ethical concerns about AI are growing rapidly.
    """

    print("Summary:")
    print(summarize(article))

