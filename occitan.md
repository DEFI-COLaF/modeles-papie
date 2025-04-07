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

## Bibliography

PIE Framework:
```
@inproceedings{manjavacas_improving_2019,
	address = {Minneapolis, Minnesota},
	title = {Improving {Lemmatization} of {Non}-{Standard} {Languages} with {Joint} {Learning}},
	url = {http://aclweb.org/anthology/N19-1153},
	doi = {10.18653/v1/N19-1153},
	abstract = {Lemmatization of standard languages is concerned with (i) abstracting over morphological differences and (ii) resolving token-lemma ambiguities of inﬂected words in order to map them to a dictionary headword. In the present paper we aim to improve lemmatization performance on a set of non-standard historical languages in which the difﬁculty is increased by an additional aspect (iii): spelling variation due to lacking orthographic standards. We approach lemmatization as a stringtransduction task with an encoder-decoder architecture which we enrich with sentence context information using a hierarchical sentence encoder. We show signiﬁcant improvements over the state-of-the-art when training the sentence encoder jointly for lemmatization and language modeling. Crucially, our architecture does not require POS or morphological annotations, which are not always available for historical corpora. Additionally, we also test the proposed model on a set of typologically diverse standard languages showing results on par or better than a model without enhanced sentence representations and previous state-of-the-art systems. Finally, to encourage future work on processing of non-standard varieties, we release the dataset of non-standard languages underlying the present study, based on openly accessible sources.},
	language = {en},
	booktitle = {Proceedings of the 2019 {Conference} of the {North}},
	publisher = {Association for Computational Linguistics},
	author = {Manjavacas, Enrique and Kádár, Ákos and Kestemont, Mike},
	year = {2019},
	pages = {1493--1503}
}


@misc{manjavacas_papie_2023,
	title = {({Pa}){PIE}: {A} {Framework} for {Joint} {Learning} of {Sequence} {Labeling} {Tasks}},
	copyright = {MIT},
	shorttitle = {({Pa}){PIE}},
	url = {https://github.com/lascivaroma/PaPie},
	author = {Manjavacas, Enrique and Clérice, Thibault and Kestemont, Mike and Akos, Kadar},
	month = apr,
	year = {2023}
}
```

Datasets:
```
@inproceedings{miletic_four-dialect_2020,
	address = {Barcelona, Spain (Online)},
	title = {A {Four}-{Dialect} {Treebank} for {Occitan}: {Building} {Process} and {Parsing} {Experiments}},
	url = {https://aclanthology.org/2020.vardial-1.13},
	booktitle = {Proceedings of the 7th {Workshop} on {NLP} for {Similar} {Languages}, {Varieties} and {Dialects}},
	publisher = {International Committee on Computational Linguistics (ICCL)},
	author = {Miletić, Aleksandra and Bras, Myriam and Vergez-Couret, Marianne and Esher, Louise and Poujade, Clamença and Sibille, Jean},
	editor = {Zampieri, Marcos and Nakov, Preslav and Ljubešić, Nikola and Tiedemann, Jörg and Scherrer, Yves},
	month = dec,
	year = {2020},
	pages = {140--149}
}

@inproceedings{miletic_outiller_2023,
	address = {Paris, France},
	title = {Outiller l'occitan : nouvelles ressources et lemmatisation},
	url = {https://aclanthology.org/2023.jeptalnrecital-long.17},
	language = {French},
	booktitle = {Actes de {CORIA}-{TALN} 2023. {Actes} de la 30e {Conférence} sur le {Traitement} {Automatique} des {Langues} {Naturelles} ({TALN}), volume 1 : travaux de recherche originaux – articles longs},
	publisher = {ATALA},
	author = {Miletić, Aleksandra},
	editor = {Servan, Christophe and Vilnat, Anne},
	month = jun,
	year = {2023},
	pages = {217--231}
}
```

State-of-the-art comparison models:
```
@inproceedings{miletic_outiller_2023,
	address = {Paris, France},
	title = {Outiller l'occitan : nouvelles ressources et lemmatisation},
	url = {https://aclanthology.org/2023.jeptalnrecital-long.17},
	language = {French},
	booktitle = {Actes de {CORIA}-{TALN} 2023. {Actes} de la 30e {Conférence} sur le {Traitement} {Automatique} des {Langues} {Naturelles} ({TALN}), volume 1 : travaux de recherche originaux – articles longs},
	publisher = {ATALA},
	author = {Miletić, Aleksandra},
	editor = {Servan, Christophe and Vilnat, Anne},
	month = jun,
	year = {2023},
	pages = {217--231}
}

@inproceedings{hopton_modeling_2024,
	address = {Mexico City, Mexico},
	title = {Modeling {Orthographic} {Variation} in {Occitan}'s {Dialects}},
	url = {https://aclanthology.org/2024.vardial-1.6},
	doi = {10.18653/v1/2024.vardial-1.6},
	booktitle = {Proceedings of the {Eleventh} {Workshop} on {NLP} for {Similar} {Languages}, {Varieties}, and {Dialects} ({VarDial} 2024)},
	publisher = {Association for Computational Linguistics},
	author = {Hopton, Zachary and Aepli, Noëmi},
	editor = {Scherrer, Yves and Jauhiainen, Tommi and Ljubešić, Nikola and Zampieri, Marcos and Nakov, Preslav and Tiedemann, Jörg},
	month = jun,
	year = {2024},
	keywords = {Computer Science - Computation and Language},
	pages = {78--88}
}
```
