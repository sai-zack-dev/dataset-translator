# Burmese Dataset Translator

A simple command-line tool for translating English text datasets into Burmese using the Gemini API.

This tool is designed for AI/ML dataset preparation and supports batch translation, automatic error handling, and safe interruption when API limits are reached.

---

## Features

* Batch translation to reduce API requests
* Token-aware batching for stable processing
* Automatic retry for temporary API errors
* Stops safely when API quota is exceeded
* Saves translated and untranslated data separately
* Professional CLI output with clear status messages
* Works with CSV datasets

---

## Requirements

* Node.js 18 or later
* Gemini API key

This tool uses the Google Gemini model:

* Gemini 2.5 Flash

---

## Installation

Clone the repository:

```bash
git clone https://github.com/sai-zack-dev/dataset-translator.git
cd dataset-translator
```

Install dependencies:

```bash
npm install
```

---

## Dependencies

This project uses the following packages:

* prompts
* ora
* csv-parser
* csv-writer
* chalk
* @google/generative-ai

---

## Dataset Format

The CSV dataset must contain the following columns:

| Column | Description                   |
| ------ | ----------------------------- |
| text   | English sentence to translate |
| label  | Classification label          |

Example dataset:

```csv
text,label
I love programming.,2
This is very sad.,0
The movie was amazing.,1
```

---

## Usage

Run the program:

```bash
node index.js
```

The CLI will prompt for:

1. CSV dataset path
2. Gemini API key

Example:

```
Burmese Dataset Translator

Enter CSV dataset path: example_dataset.csv
Enter Gemini API Key: ********************
```

---

## Output

The program generates translated CSV files in batches.

Example:

```
burmese_dataset_0-457.csv
burmese_dataset_457-855.csv
untranslated_dataset_855-953.csv
```

* `burmese_dataset_*` contains translated rows
* `untranslated_dataset_*` contains rows that could not be translated due to API limits

---

## Error Handling

The tool includes automatic error handling for:

### Temporary API Errors

If a temporary error occurs, the program will retry the request.

### API Rate Limits

If the Gemini API quota is exceeded:

* Translation stops immediately
* Remaining rows are saved as `untranslated_dataset`
* No data is lost

---

## Token Batching

To prevent API failures, the program:

* Estimates token usage
* Groups rows into safe batches
* Sends translation requests within token limits

This ensures reliable processing even for large datasets.

---

## Example Workflow

1. Prepare dataset CSV
2. Run translator
3. Wait for batch processing
4. Use translated dataset for machine learning training

---

## Limitations

Gemini free-tier limits apply.

Typical limits include:

* Request quota per day
* Request rate per minute
* Token limits per request

Large datasets may require multiple runs.

---

## Use Cases

This tool is useful for:

* Sentiment analysis datasets
* NLP dataset localization
* Multilingual AI training data
* Dataset augmentation

---

## License

MIT License
