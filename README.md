# CLIPedia (Mathematica Code)

This repository contains the complete Mathematica code for reproducing CLIPedia inference results using a sample from  pre-processed corpus and a pre-trained model. 
It also includes a notebook manual and specialized functions to support building a CLIPedia from Wikipedia dumps. This repository is released alongside the following paper:
> **Nickl, Agostino. “Navigating CLIPedia: Architectonic Instruments for Querying and Questing a Latent Encyclopedia.” Frontiers of Architectural Research, forthcoming.**

---

# Data Availability

This code relies on a pre-encoded CLIP corpus (~500 GB). Due to size restrictions, **the full dataset is not included in this repository**. Without this dataset, the notebook will not fully run and will raise file access errors.  
A **small subset** is included to allow performing a couple of queries, and to demonstrate the necessary file structure through dummy files, should you want to build your own CLIPedia.

To reproduce the full setup:
- You may build and train a new CLIPedia from a Wikipedia dump using `clipedia_build.nb` – this requires several months of computation and a workstation with GPU acceleration in Mathematica. CLIPedia was built on a Windows workstation with 64 GB RAM and a GTX 3080 Ti.
- Alternatively, you may request access to the `data/` and `soms/` folders (~500 GB total) to complement the pre-trained model with a corpus, contacting the author via email: **anickl@ethz.ch** (temporary file-share link available on request).

---

## Folder and File Descriptions

- **notebooks/**
  - `clipedia_inference.nb`: Main inference notebook and CLIPedia's interface
  - `clipedia_inference_with_outputs.nb`: Inference notebook with precomputed outputs
  - `clipedia_build.nb`: A step by step notebook manual with key functions helping build a CLIPedia from Wikipedia dumps.
  - `exports/`: Exported Questbooks showing different Journeys with Archidromes, Thelodromes, Diadromes. Note: Outputs may have been cropped to not surpass 100 MB.

- **code/**
  - `clipedia_functions.nb`: Main repository notebook containing all functions for inference
  - `models/`: OpenCLIP models from the Wolfram Neural Net Repository (`.wxf` format)
  - `functions/`: Specific classifiers (e.g., wiki flag classifier)
  - `dictionaries/`: Specific dictionaries for term weighting¨

- **models/**
    Folder for OpenCLIP models from the Wolfram Neural Net Repository (not included).  
    CLIPedia depends on OpenCLIP models: Copyright (2012-2021) by Gabriel Ilharco, Mitchell Wortsman, Nicholas Carlini, Rohan Taori, Achal Dave, Vaishaal Shankar, John Miller, Hongseok Namkoong, Hannaneh Hajishirzi, Ali Farhadi, Ludwig Schmidt. https://github.com/mlfoundations/open_clip/blob/main/LICENSE.
    You can use a provided helper function to download them directly from the Wolfram Neural Net Repository. 
    By running it, you accept OpenCLIP’s license and terms. The OpenCLIP model used here was published with a paper by M. Cherti, R. Beaumont, R. Wightman, M. Wortsman, G. Ilharco, C. Gordon, C. Schuhmann, L. Schmidt, J. Jitsev, "Reproducible Scaling Laws for Contrastive Language\Image Learning," arXiv:2212.07143 (2022).

- **data/** (only sample data included)
  - `indices/`: Contains Associations of page IDs to titles, and image URLs to image IDs, split to stay within GitHubs file limits.
  - `pages/`: Wikipedia page content (`.json` files, organized by ID prefixes)
  - `text/`: Paragraphs with IDs (`.json`, organized by ID prefixes)
  - `img/`: Wikipedia images (`.jpg`, organized by ID prefixes)
  - `imgBios/`: Image metadata (`.json`), including page mentions and captions
  - `imgVecs/`: CLIP-encoded image embeddings, including ID-to-embedding associations

- **soms/** (only sample SOMs included)
  - `globalSom.wxf`: Pretrained CLIPedia SOM (Global Level)
  - `localSoms_0-512.wxf`: Pretrained CLIPedia SOM (Local Level Package 1)
  - `localSoms_513-1024.wxf`: Pretrained CLIPedia SOM (Local Level Package 2)
  - `hdf5/`: Compressed allocated embeddings, sorted by mode and subsom (image/text, stored as `.h5`)

## Repository Structure

```

clipedia_repo/
├── notebooks/
│   ├── clipedia_inference.nb
│   ├── clipedia_inference_with_outputs.nb
│   ├── clipedia_build.nb
│   └── exports/
│       ├── Flying_with_Vitruvius.nb
│       ├── Walking_with_Vitruvius.nb
│       ├── Wandering_with_Vitruvius.nb
│       └── Wandering_with_Nobody.nb
├── code/
│   ├── clipedia_functions.nb
│   ├── models/
│   │   ├── OpenCLIP_fe_imgViT-B32.wxf (To be added by users, see above)
│   │   └── OpenCLIP_fe_textViT-B32.wxf (To be added by users, see above)
│   ├── functions/
│   │   ├── 240317_wikiFlagClassifier.wxf
│   │   └── ...
│   └── dictionaries/
│       ├── 231026_dictWeights.wxf
│       └── ...
├── data/
│   ├── idTitleIndex.wxf
│   ├── idHashIndex.wxf
│   ├── pages/
│   │   ├── 12/
│   │   │   ├── 12.json
│   │   │   └── ...
│   │   └── ...
│   ├── text/
│   │   ├── 12/
│   │   │   ├── 12.json
│   │   │   └── ...
│   │   └── ...
│   ├── img/
│   │   ├── 100/
│   │   │   ├── 1001004726172902.jpg
│   │   │   └── ...
│   │   └── ...
│   ├── imgBios/
│   │   └── json/
│   │       ├── 100/
│   │       │   ├── 1001004726172902.json
│   │       │   └── ...
│   │       └── ...
│   └── imgVecs/
│       ├── imgVecIndex.wxf
│       ├── 100/ 
│       │   ├── 1001004726172902.json
│       │   └── ...
│       └── ...
├── soms/
│   └── 240805/
│       ├── globalSom.wxf/
│       ├── localSoms_0-512.wxf/
│       ├── localSoms_513-1024.wxf/
│       └── hdf5/
│           ├── img/
│           │   ├── 1/
│           │   │   ├── 1.h5
│           │   │   └── ...
│           │   └── ...
│           └── txt
│               ├── 4/
│               │   ├── 3.h5
│               │   └── ...
│               └── ...
├── README.md
├── LICENSE 
└── DATA_LICENSE 

```

---

## Requirements

- Mathematica 13.2 (tested on macOS) or 14.2 (tested on Windows PC) for inference of a pre-trained CLIPedia. At least 32 GB RAM and a GPU addressable by Mathematica for building a CLIPedia from scratch.
- ca. 2.5 GB free local storage space to host the repository and run `clipedia_inference.nb` for a demo dataset.
- ca. 30 GB free local storage to run `clipedia_build.nb` on a small fraction of the Wikipedia dump, which includes hosting the latter (ca. 25 GB).
- ca. 600-800 GB free local storage to run `clipedia_build.nb` on the full Wikipedia dump.

---

## Usage

1. Download the full repository.
2. Open `notebooks/clipedia_inference.nb` in Mathematica.
3. Load dependencies by evaluating the first cells, then follow the notebook structure to explore preview queries and quests.
4. For full functionality, you need the full corpus (ca. 500 GB), which you can request from the author (see above).
5. To build your own CLIPedia, follow the steps in `notebooks/clipedia_build.nb`.

---

## Notes on Training Code

The full data crawling and training for CLIPedia relied on periodic cleaning and interactive workflows.
We provide `notebooks/clipedia_build.nb` containing the necessary steps and functions to process Wikipedia Dumps **for reference, as demonstrated on a small subset**, noting that the full process is non-linear and may take months on a single workstation with no further optimization.

---

## License

The code in this repository is published under the MIT License.
The repository also includes Wikipedia-derived data (such as corpus subsets and examples) from the official Wikimedia dump (April 20, 2024). This data is provided under the terms of the Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0), as required by Wikimedia’s licensing.
More information can be found here: https://dumps.wikimedia.org/legal.html.
Users should ensure that any reuse, redistribution, or derivative works comply with the terms of both licenses, including appropriate attribution and share-alike provisions for the data.
This repository does not redistribute the OpenCLIP models; users must obtain them separately under their respective licenses.

---

## Citation

If you use this code, please cite:

> Nickl, Agostino. “Navigating CLIPedia: Architectonic Instruments for Querying and Questing a Latent Encyclopedia.” Frontiers of Architectural Research, forthcoming.

---

## Acknowledgements

This project was made possible thanks to the prior research into coding with Self-Organizing Maps (SOMs) at the Chair of Digital Architectonics (formerly CAAD), ETH Zurich, led by Prof. Ludger Hovestadt, and the coding courses taught by its researchers, particularly Dr. Karla Saldaña Ochoa and Dr. Guo Zifeng’s course Map & Models — Self Organizing Maps (2020). 
A special thanks goes to all fellow and past researchers at the chair who pushed the envelope of SOMs and coding practice for architects, including Dr. Mohamed Zaghloul, Dr. Miro Roman, Dr. Jorge Orozco, Dr. Nikola Marinčić, Dr. Vahid Moosavi, Dr. Diana Alvarez-Marin, Dr. Cai Chenyi, Julian Besems, Adil Bokhari – and Prof. Ludger Hovestadt himself.