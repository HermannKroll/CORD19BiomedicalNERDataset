# A Semantically Enriched Dataset based on Biomedical NER for the COVID19 Open Research Dataset Challenge


This repository belongs to our [arXiv publication](https://arxiv.org/abs/2005.08823) and contains the CORD19 entity mentions as *JSON*-dumps. The files are collections of the entity mentions found by [TaggerOne](https://www.ncbi.nlm.nih.gov/research/bionlp/tools/taggerone/) and [GNormPlus](https://www.ncbi.nlm.nih.gov/research/bionlp/Tools/gnormplus/) via our Python pipeline. They are based on the [CORD-19 dataset](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge).  The code for our pipeline will be released soon.
The data is published for free reuse under the [Creative Commons Attribution 4.0 International license (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

The dumps will be updated continuously. If you use our repository, please cite the following paper:
```
@misc{kroll2020cord19entityannotations,
    title={A Semantically Enriched Dataset based on Biomedical NER for the COVID19 Open Research Dataset Challenge},
    author={Hermann Kroll and Jan Pirklbauer and Johannes Ruthmann and Wolf-Tilo Balke},
    year={2020},
    eprint={2005.08823},
    archivePrefix={arXiv},
    primaryClass={cs.DL}
}
```
 

## Files
This repository contains three dumps:

CORD19 - Version 38:
- [Entity Mentions in titles and abstracts (V38)](https://1drv.ms/u/s!ArDgbq3ak3Zuh50gCtnPRMcgnLLaiw?e=Ld0WdJ) contains entity mentions within documents' titles and abstracts only
- [Entity Mentions in full texts (V38)](https://1drv.ms/u/s!ArDgbq3ak3Zuh50fRKVNlikDQ2hJKQ?e=Otce0l) contains all entity mentions within the titles, abstracts and document body texts
- [Metadata.csv (V38)](https://1drv.ms/u/s!ArDgbq3ak3Zuh50c8APxx84f6xtL1g?e=c6u38A) contains metadata of all files. This file is included in the original CORD19 dump. The SHA column contains the SHAs of the pdf scans which we use as the identifier for the files. These SHAs are also the original file names of the JSON parses.


CORD19 - Version 30:
- [Entity Mentions in titles and abstracts (V30)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5t0gMLGB-B9RVP2Vg?e=rGkTCO) contains entity mentions within documents' titles and abstracts only
- [Entity Mentions in full texts (V30)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5t2-BBUKPwr0evppg?e=xDSJtF) contains all entity mentions within the titles, abstracts and document body texts
- [Metadata.csv (V30)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5t1HgjSwhILXHTiNA?e=fGrf6b) contains metadata of all files. This file is included in the original CORD19 dump. The SHA column contains the SHAs of the pdf scans which we use as the identifier for the files. These SHAs are also the original file names of the JSON parses.


CORD19 - Version 22:
- [Entity Mentions in titles and abstracts (V22)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5swZCUL9wNeG7G8tw?e=a4cKch) contains entity mentions within documents' titles and abstracts only
- [Entity Mentions in full texts (V22)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5syeLZamNRzORn6JA?e=LODHmi) contains all entity mentions within the titles, abstracts and document body texts
- [Metadata.csv (V22)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5sx0LqCE9lqX7rtfg?e=RjdKWN) contains metadata of all files. This file is included in the original CORD19 dump. The SHA column contains the SHAs of the pdf scans which we use as the identifier for the files. These SHAs are also the original file names of the JSON parses.

CORD19 - Version 9:
- [Entity Mentions in titles and abstracts (V9)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5oeo_b_Qo50j9QmeA?e=qclJQ4) contains entity mentions within documents' titles and abstracts only
- [Entity Mentions in full texts (V9)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5ofm6bOXIOvEcqu6w?e=BggneA) contains all entity mentions within the titles, abstracts and document body texts
- [Metadata.csv (V9)](https://1drv.ms/u/s!ArDgbq3ak3Zuh5ogtS6q2sUITSRHpA?e=fuoIIz) contains metadata of all files. This file is included in the original CORD19 dump. The SHA column contains the SHAs of the pdf scans which we use as the identifier for the files. These SHAs are also the original file names of the JSON parses.

## Dump format
Both *JSON*-Dumps follow this format: 
```
[
  <paper_id: str>: [ #For every JSON-parse of the dataset 
    {   # For every entity mention
      "location": {
        "paragraph": <int>  # 0 = title, 1 = abstract
                            # > 1 = body text
        "start": <int> # 0 = first character of paragraph
        "end": <int>
      },
      "entity_str": <str> # entity mention in source text
      "entity_type": <"Chemical"|"Disease"|"Gene"|"Species">
      "entity_id": <str> # e.g. MESH-Identifier
    },...
  ],...
]
```
 - **paper-id** is the the filename of the original *JSON*-parse. The value is a list of entity mention entries.
 - **location** contains the location of the entity mention within in the document 
	 - **paragraph** denotes which paragraph **start** and **end** refer to. The following encodings are used:
	 	- 0: Document title
	 	- 1: Document abstract
	 	- \>1: Index of the paragraphs in the document body, starting with 2, i.e. 2 is the first body text and so on. 
	 - **start** is the first character position in the text
	 - **end** is the last character position in the text
 - **entity_str** is the string of the entity mention found by the NER *excluding any non-ASCII-Characters*.
 - **entity_type** is the entity type of the mention:
 	- "Chemical" \(TaggerOne\)
 	- "Disease" \(TaggerOne\)
 	- "Gene" \(GNormPlus\)
 	- "Species" \(GNormPlus\)
 - **entity_id** contains the unique ID of an entity. 

Entity IDs stems from one of the following vocabularies. 
- [Medical Subject Heading (MeSH)](https://www.nlm.nih.gov/mesh/meshhome.html): IDs start with `MESH` (Chemicals and Diseases)
- [OMIM Database](https://www.ncbi.nlm.nih.gov/omim): IDs start with `OMIM` (Diseases)
- [NCBI Gene Information](https://www.ncbi.nlm.nih.gov/gene/) for Genes
- [NCBI Species Taxonomy](https://www.ncbi.nlm.nih.gov/taxonomy) for Species


## Example
For further clarification, here are some example entries from the full text dump:
```
{
  "c4dc1c0360d3fe9ceddc4650aea022f24d88cd99.json": [
    {
      "location": {
        "paragraph": 1,
        "start": 821,
        "end": 842
     },
     "entity_str": "surface glycoproteins",
     "entity_type": "Chemical",
     "entity_id": "MESH:D039842"
    },
    {
         "location": {
            "paragraph": 0,
            "start": 77,
            "end": 82
         },
         "entity_str": "fever",
         "entity_type": "Disease",
         "entity_id": "MESH:D005334"
    },
    {
       "location": {
          "paragraph": 2,
          "start": 20,
          "end": 36
       },
       "entity_str": "thrombocytopenia",
       "entity_type": "Disease",
       "entity_id": "MESH:D013921"
    },...
  ],...
}

```

The document named `"c4dc1c0360d3fe9ceddc4650aea022f24d88cd99.json"` contains the entity `fever` of type `Disease` with MeSH-ID [D013921](https://meshb.nlm.nih.gov/record/ui?ui=D005334) in the title. The entity mention is located at character positions 77 to 82.

Likewise, there are the entities `surface glycoproteins` at position 821 to 842 in the abstract and `thrombocytopenia` at position 20 to 36 in the first paragraph of the body text.
