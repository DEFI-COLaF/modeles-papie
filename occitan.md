# PaPie models for Occitan

## Datasets
Our PaPie models for Occitan are based on the following datasets:
- [Tolosa Treebank v2](https://zenodo.org/records/10569962) (TTB), a manually annotated corpus (POS+lemma) of 26K tokens, 
    distinguishing between four Occitan varieties (Langedocian, Gascon, Limousin, Provençal) and already split between training/development/test sets.
- [OcWikiAnnot](https://zenodo.org/records/7777340) (WIKI), a fully automatically annotated corpus (POS+lemma) of 2M tokens, 
    based on an extraction of pages from Wikipedia in Occitan

So far, we've experimented with training models from scratch or from existing models in French/Spanish/Catalan.
We've tried training with only one single dataset (TTB or WIKI), or with both concatenated (WIKI then TTB in each epoch), 
as well as fine-tuning a model firstly trained on WIKI, with TTB data.

Here we report on our best results so far.

## POS tagging

| Model info                                                                           | Finetuned from             | Training data  | Model+Training hyperparameters                                                                                                   | Accuracy (TTB testset all dialects) |
|--------------------------------------------------------------------------------------|----------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| MaChAmp by (Hopton and Aepli, 2024)                                                  | mBERT finetuned on Occitan | TTB            |                                                                                                                                  | 94.10                               |
| [PaPie_POS_WIKITTB](https://github.com/DEFI-COLaF/modeles-papie/releases/tag/v0.0.1) | scratch                    | WIKI + TTB     | - 18 epochs <br/>- 1 layer for SentRNN, CharRNN, AttentionalDecoder <br/>- embeddings + hidden size 128 <br/>- include PaPie LM during training | 93.58                               |
| MaChAmp by (Miletic, 2023)                                                           | mBERT                      | TTB            |                                                                                                                                  | 92.26                               |


## Lemmatization

| Model info                                                                                       | Finetuned from | Training data  | Model+Training hyperparameters                                                                                         | Accuracy (TTB testset all dialects) |
|--------------------------------------------------------------------------------------------------|----------------|----------------|------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| Stanza by (Miletic, 2023)                                                                        | FastText       | TTB            | - input token+POS                                                                                                      | 93.21                               |
| [PaPie_Lemma_finetune-WIKI2TTB](https://github.com/DEFI-COLaF/modeles-papie/releases/tag/v0.0.1) | WIKI           | TTB            | - vocabulary expanded with new words/chars/lemmas/labels from TTB: 592 chars / 24000 words / 798 lemmas<br>- 39 epochs | 92.89                               |
