 # Roman Urdu Scam Detector

Most scam filters are built for English. This project tests whether a model trained on a public Roman Urdu phishing SMS dataset can detect scams it has never seen.

## Key finding
A model scoring **100%** on its own dataset scored only **60%** on new messages, and caught just **5 of 10 scams**. The public dataset is too templated for its own test split to be trusted.

## Data
- Public Roman Urdu phishing SMS dataset from Zenodo: https://zenodo.org/records/21810885
- 1,000 messages: 595 legit (label 0), 405 phishing (label 1). Labels verified by reading samples.
- **369 of 1,000 messages start with just 10 phrases**, so the data is heavily templated.

## Method
1. Explored the data and counted repeated templates.
2. Trained TF-IDF + Logistic Regression: 100% accuracy on a random 80/20 split.
3. Kept at most 3 messages per template (371 left): still 100%. A random split can't expose the problem.
4. Tested on 20 new messages (10 scam, 10 legit), different in style from the dataset.

## Results on new messages
| | Precision | Recall |
|---|---|---|
| Legit | 0.58 | 0.70 |
| Scam | 0.62 | 0.50 |

- Missed scams: lucky draw, parcel fee, work-from-home, SIM block, and fake job offer messages.
- False alarms included a wedding congratulation. "Mubarak ho" likely acts as a scam keyword, because many scams in the data open with it.

## Limitations
- The 20 test messages are synthetic: written by me with AI assistance, not collected from real phones.
- 20 messages is a pilot, not proof.

## Next steps
- Collect real messages (numbers and names removed) as a proper test set.
- Try models that read meaning instead of word counts.

## Files
- `01_explore_data.ipynb`: data exploration, model, and test 
