# YOUR_OWN_AI
## A repo for  people have gpus and want to make money using it, BY making ai models for others 


 ## Required Notice: Copyright 2026 [Aadarsh Pandey]

## How to use it

Upload the client’s files as a private Kaggle Dataset and set DATA_DIR, ORG, CLIENT and MODEL_SIZE in the first cell.
Set the accelerator to T4 x2, turn Internet on, and run the cells in order.
Download <client>_package.zip from the Output tab, then run the wipe cell.

## What the cells do

Parse: Reads PDF, Word, Excel, CSV, PowerPoint, Markdown, text and images. Scanned PDFs and images go through OCR.

Clean and chunk: Hides Aadhaar, PAN and card numbers by default. Phone and email hiding is off because the chatbot may need the business’s own contact details. Chunks keep their headings, and Excel chunks repeat the table header. Near-duplicate chunks are dropped.

Index: Uses bge-m3 (works for Hindi and English) with FAISS plus keyword search merged together.

Model: MODEL_SIZE picks Qwen2.5 at 1.5B, 3B or 7B, matching your website’s Small, Medium and Large options.

Training data: The model writes question-and-answer pairs from the chunks. Each pair is trained with its document context, plus about 10% “not in the documents” examples. This teaches the model to answer from the supplied context and cite its source, rather than memorize facts.

Test: Runs your TEST_QUESTIONS on the tuned model and on the base model, so you can see whether fine-tuning actually helped.
Chat: Starts a password-protected Gradio link that shuts itself down after SESSION_MINUTES.

Wipe: Set CONFIRM_WIPE = True and run the last cell to delete the working folder.

## Things to watch

Small datasets: With fewer than 60 training examples the notebook skips fine-tuning and uses RAG only. Set MODE = "rag_only" for a fast first demo.

Single GPU: Only one T4 is used, so the second sits idle. For two clients at once, open a second notebook.

Library versions: Unsloth, TRL and Gradio change often. The notebook has fallbacks for the common renames. Once a run works, pin the versions with pip freeze.

Saving a version: Never use “Save Version” with client data, because Kaggle stores the logs and outputs. Delete the private dataset after each job.

Answer quality: The training answers come from the same small model that is being trained, so the fine-tune mostly improves format and “I don’t know” behavior. The RAG search does most of the work on accuracy.
