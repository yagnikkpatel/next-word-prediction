# Next Word Prediction with an LSTM

An LSTM trained on Shakespeare's *Hamlet* that predicts the next word of a line, with a small Streamlit app to try it.

The model is trained to **memorise the play**: given the start of a line from *Hamlet*, it returns the word that follows. It is not a general language model and will be unreliable on text that is not in the play.

## Files

| File | Purpose |
|---|---|
| `experiemnts.ipynb` | Training notebook: run it top to bottom to train and save the model |
| `app.py` | Streamlit app |
| `hamlet.txt` | Training text (NLTK Gutenberg corpus) |
| `next_word_lstm.h5` | Trained model |
| `tokenizer.pickle` | Word-to-number mapping used by the model |
| `requirements.txt` | Python dependencies |

## Setup

Requires Python 3.9-3.11 (TensorFlow 2.15).

```
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Run the app

```
streamlit run app.py
```

Type the start of a line, for example `Hor. My Lord, I came to see your Fathers`, and click **Predict Next Word**.

## Train the model yourself

Open `experiemnts.ipynb` (`jupyter notebook`) and run all cells. Training takes roughly 10-15 minutes on a laptop CPU and overwrites `next_word_lstm.h5` and `tokenizer.pickle`.

Training stops when the model predicts the check word set in the notebook's settings cell and its accuracy is within 3% of the best accuracy possible on this text.

## Limitations

- Each line of the play is a separate training example, so the model cannot continue a phrase across a line break.
- The best possible accuracy is about 85%, because the same words are often followed by different words in different places.
- The text uses the original spelling (`funerall`, `giue`, `selfe`).
