# Lab: Text Embeddings & Cosine Similarity

In this lab you will use OpenAI's API to convert sentences into numerical vectors called **embeddings**, then write your own algorithm to find which sentences are most similar to a given query.

---

## What You Will Build

1. **Embed text** — call the OpenAI API to turn sentences into vectors of numbers.
2. **Mean pool** — collapse a list of vectors into a single representative vector.
3. **Cosine similarity** — implement the math that measures how "close" two vectors are.
4. **Top-K retrieval** — use your similarity function to find the K most relevant sentences for a query.

---

## Prerequisites

- Python 3.10 or later
- An OpenAI API key (your instructor will provide one, or create one at platform.openai.com)

---

## Project Structure

```
mar24/
├── lab.py            ← Your working file. Complete every TODO here.
├── requirements.txt  ← Python packages this project depends on.
├── .env.example      ← Template showing which environment variables are needed.
├── .env              ← YOUR secrets (you create this — never commit it).
├── .gitignore        ← Tells git which files to ignore.
└── README.md         ← This file.
```

---

## Setup

### 1. Create a virtual environment

A virtual environment keeps this project's packages separate from the rest of your system. Think of it as a clean, isolated workspace.

```bash
python -m venv venv
```

Activate it:

```bash
# macOS / Linux
source venv/bin/activate

# Windows
venv\Scripts\activate
```

You should see `(venv)` appear at the start of your terminal prompt. Run this activation command every time you open a new terminal for this project.

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

This reads `requirements.txt` and installs all the listed packages into your virtual environment.

### 3. Set up your environment file

Environment variables are how you pass secret values (like API keys) to your program without hardcoding them into your source code. **Never put a real API key directly in a `.py` file.**

Copy the provided template:

```bash
cp .env.example .env
```

Open `.env` in your editor and fill in your values:

```
OPENAI_API_KEY=sk-...        ← paste your real API key here
EMBEDDING_MODEL=text-embedding-3-small
```

The `python-dotenv` package (already in `requirements.txt`) will automatically load this file when you run the lab.

### 4. Run the lab

```bash
python lab.py
```

You will see errors until you complete the TODOs — that is expected.

---

## Environment Variables Reference

| Variable | Required | Description |
|----------|----------|-------------|
| `OPENAI_API_KEY` | Yes | Your secret API key for authenticating with OpenAI. Treat this like a password. |
| `EMBEDDING_MODEL` | No | The OpenAI model used to generate embeddings. Defaults to `text-embedding-3-small` if not set. |

### What is an environment variable?

An environment variable is a key-value pair stored outside your code that your program can read at runtime. This keeps secrets out of your source files and makes it easy to change configuration without editing code.

The `.env` file is just a convenient place to store these variables locally. The `python-dotenv` library reads that file and loads the variables into your program automatically.

---

## What to Commit and What Not to Commit

When working on a software project, not everything should go into version control (git). A good rule of thumb:

**Commit these:**
- `lab.py` — your work and code changes
- `requirements.txt` — so others can recreate your environment
- `.env.example` — the template (no real secrets, safe to share)
- `README.md`

**Never commit these:**
- `.env` — contains your real API key. If this ends up on GitHub, anyone can find it and use your key, which can lead to unexpected charges or account suspension.
- `venv/` — the virtual environment folder is large and can always be recreated from `requirements.txt`.
- `__pycache__/` — auto-generated Python bytecode, not meaningful to commit.

The `.gitignore` file in this project is already configured to block `.env` and other files that should not be committed. You can open it to see the full list.

---

## Key Concepts

**Embedding**
A way of representing text as a list of numbers (a vector) that captures its meaning. Sentences with similar meanings will have vectors that point in similar directions in high-dimensional space.

**Mean pooling**
When you have multiple vectors (e.g. one per chunk of a long document), averaging them element-by-element produces a single vector that represents the whole. For a single vector, this is a no-op.

**Cosine similarity**
A measure of how similar two vectors are, regardless of their length. A score of `1.0` means identical direction (very similar meaning), `0.0` means unrelated, and `-1.0` means opposite. The formula is:

```
cosine_similarity(a, b) = (a · b) / (||a|| × ||b||)
```

Where `a · b` is the dot product and `||a||` is the magnitude (norm) of vector `a`.

**Top-K retrieval**
Given a query, compute its similarity to every item in a corpus and return the K items with the highest scores. This is the foundation of semantic search.

---

## Troubleshooting

**`AuthenticationError` or `Invalid API key`**
Your `.env` file is missing, in the wrong directory, or the key value is incorrect. Double-check that `.env` exists in the same folder as `lab.py` and that `OPENAI_API_KEY` is set correctly.

**`ModuleNotFoundError`**
You either forgot to activate your virtual environment or skipped the `pip install -r requirements.txt` step. Run both and try again.

**`NotImplementedError`**
This is intentional — it means you have not completed that TODO yet.
