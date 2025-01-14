# Data Mining for Methods and Datasets in Biomedical Articles

This repo contains code to extract mentions of **experimental methods** and **datasets** as accession numbers IDs from biomedical articles.
This is a NER model built on BioBERT[1] and trained on 279876 sentences coming from 36k biomedical research articles containing 5250 dataset (as accession number IDs) and 78318 method mentions. <br>
You can use the prediction code on your own files!

### Examples of outputs
Example 1:
```,sentence,sent_idx,start_word_idx,end_word_idx,mention,tag
0,Single-cell transcriptomic data are available at the N CBI Gene Expression Omnibus (GEO) under accession GSE115746.,0,17,17,GSE115746,DAT
1,The virus infection microarray data are available in GEO under accession GSE55278.,1,11,11,GSE55278,DAT
2,Serum samples were obtained at sacrifice (day 49) and analyzed by ELISA.,2,13,13,ELISA,MET
```
Example 2:
```
,sentence,sent_idx,start_word_idx,end_word_idx,mention,tag
0,(E) PCA of the gene expression of in vitro differentiation systems and human cortical development.,44,3,3,PCA,MET
1,"To determine the stages of in vivo cortical development that best matched these various in vitro models, we compared transcriptome data to the BRAINSPAN human brain developmental transcriptome RNA-seq dataset (Kang et al., 2011, Figure 1C and D).",50,29,29,RNA-seq,MET
2,"Therefore the differential transcriptomic dynamics of in vitro cultures captured by PC2 in the PCA analysis could be at least partially explained by the distinct expression patterns of ECM genes, which were unusually high in CORTECON and telencephalic aggregates compared with CO samples and fetal brain.",73,14,14,PCA,MET
3,"To test whether mCH was enriched in super-enhancers in COs and fetal cortex, we identified putative super-enhancers with ChIP-seq data of H3K4me1 that were available for both fetal brain and adult cortex (Whyte et al., 2013; Roadmap Epigenomics Consortium et al., 2015).",116,19,19,ChIP-seq,MET
4,"However, the phenomenon of hypo-DMR block was specific for in vitro neural cultures since COs and neurospheres had normal global mCG levels (~0.8) whereas GM12878 and HepG2 genomes were aberrantly lowly methylated (Figure S4C bottom panel).",181,27,27,GM12878,DAT
5,"Heatmaps show mCG, DNase-seq and ChIP-seq signals for regions +/- 3kb from the center of DMRs.",209,6,6,ChIP-seq,MET
6,"To further determine the degree that CO differentiation mimics the epigenomic remodeling of brain development, chromatin accessibility and histone modifications were examined for the DMR regions with DNase-seq and ChIP-seq data generated from fetal brain (Figure 5A and B).",214,30,30,ChIP-seq,MET
7,"For RNA-seq analysis, the following samples were collected from each of two independent batches: H9 hES day 0 (remaining cells from EB generation), 5 pooled EBs day 18, 3 pooled COs day 40, 3 pooled COs day 60.",307,1,1,RNA-seq,MET
8,"Methyl-Seq and RNA-seq library preparation
A detailed protocol for MethylC-seq libraries preparation can be found in Urich et al., 2015.",309,2,2,RNA-seq,MET
9,"Stranded RNA-seq libraries were constructed with Truseq Stranded mRNA LT kit (Illumina, RS-122-2101 and RS-122-2102) and were sequenced on Illumina HiSeq 2500 with 100 bases single-ended reads.",311,1,1,RNA-seq,MET
10,prepared MethylC-seq and RNA-seq libraries.,328,3,3,RNA-seq,MET
```
Example 3:
```,sentence,sent_idx,start_word_idx,end_word_idx,mention,tag
0,"below mean for age and sex, Figure 6a ) and reduced stature (−6.7 s.d., Supplemental Text , Extended Data Figure 6a ), who, as determined through exome sequencing and confirmed by capillary sequencing ( Figure 6b ), had compound heterozygous truncating mutations in CDK5RAP2 .",116,31,32,exome sequencing,MET
1,"The CDK5RAP2 expression construct was generated using the Gateway system (Invitrogen) by PCR amplification of CDK5RAP2 from MGC human CDK5RAP2 cDNA (clone ID: 9052276) using the primers with AttB sites: Forward: GGGGACAAGTTTGTACAAAAAAGCAGGCTTCATGATGGACTTGGTGTTGGAAGA, Reverse: GGGGACCACTTTGTACAAGAAAGCTGGGTCAGCTTTATTGGCTGAAAGTTCTTCTC.",158,14,14,PCR,MET
2,Cell culture and western blot HEK293T cells were grown in 10% FBS/DMEM and split at 40% into a 6-well dish (BD Falcon) followed by transfection the next day using TurboFect (Thermo Scientific) with 5ug plasmid DNA.,200,28,28,transfection,MET
3,Dermal fibroblasts were obtained by skin punch biopsy and were cultured in amnioMAX C-100 complete medium (Invitrogen) and maintained in a 37°C incubator with 5% CO2 and 3% O2.,202,7,7,biopsy,MET
4,Mutations were confirmed by bi-directional sequencing of PCR products using dye terminator chemistry on an ABI 3730 capillary sequencer (Applied Biosystems).,215,7,7,PCR,MET
5,The DNA mix was added to the DMEM/Fugene6 mix while vortexing to generate the final transfection mix.,219,15,15,transfection,MET
6,"After a 15min incubation at RT, the transfection mix was added onto 80% confluent 293 cells, cultured in 13ml 293 culture medium.",220,8,8,transfection,MET
7,"Virus-containing medium was harvested and replaced with fresh medium 48h, 60h and 72h after transfection.",221,15,15,transfection,MET
```
## Updates
February 2022: <br>
- Making training data, as well as train/val/test splits available under `data` <br>
- Making training script available - `train.py` <br>


## Data
Training, validation and test data splits are under the `data` directory. <br>
We are making the data available under a [CC-O license](https://creativecommons.org/publicdomain/zero/1.0/). <br>

Training, Validation and Test Split Characteristics:
| | Train Split | Val Split | Test Split | Total | 
|-|-|-|-|-|
| Number of sentences | 52206 | 6526 | 6526 | 65258 |
| Number of dataset mentions | 862 | 141 | 116 | 1119 | 
| Number of method mentions | 53249 | 6642 | 6634 | 66525 | 

### Dataset Creation
The dataset was created by retrieving [Europe PMC](http://europepmc.org/) annotations through the [Europe PMC AnnotationsAPI](https://europepmc.org/AnnotationsApi), mapping them to corresponding full-text papers and sentences in our own full-text corpus and engaging an expert team of biomedical experts for further curation. <br> 
- Our full-text corpus consists of full-text content from the [PubMed Central Open Access (PMC-OA) Subset](https://www.ncbi.nlm.nih.gov/pmc/tools/openftlis), an open-access collection of articles from [PubmedCentral (PMC)](https://www.ncbi.nlm.nih.gov/pmc/). <br>
- From this set, we chose 8 journals containing 35410 articles.<br>
- We called the Europe PMC API to retrieve annotations of experimental methods and data accession number IDs corresponding to these journal articles' PMIDs or PMCIDs. <br>
- For accession number IDs, we only focused on a set of databases which we decided are a good representation of biomedical datasets, such as GEO, BioProject or ArrayExpress. <br>
- For experimental methods, we filtered out terms retrieved from Europe PMC that did not fit our own definitions.

## Prediction
The model checkpts can be downloaded from [here](https://drive.google.com/drive/folders/12hj0nFiQH3wdOfaVzmoTAErbs-c7s9zT?usp=sharing)

### Getting started
You can follow these steps to use the code for prediction on your own biomedical papers
#### 1. Code Setup

After cloning the repo locally, run the following commands: <br>
1. Download the trained *model.pt* file from [here](https://drive.google.com/file/d/1MiA60qli7mwo5hMa4fl401bpctfR9VeJ/view?usp=sharing) and add the file in the *model_artifacts* folder. <br> 
This contains the trained model needed for prediction.
2. Install all the packages required for the prediction code: ```pip install -r requirements.txt``` 
3. Add the files corresponding to the articles you want to predict under the ```papers``` folder 
- There are some examples already in this folder: example.txt, PMC3817409, PMC4900885, PMC5495578 <br>
4. Run the prediction script on your text by running ```python predict.py -i article_path```
- For instance, if you want to get predictions on the PMC3817409 paper, you would run: <br>
```python predict.py -i papers/PMC3817409```
5. The results will be printed in the terminal. If you want to save the results to a file, you can do so by adding the '-o' flag. <br>
- For instance, if you want to get predictions on the PMC3817409 paper **and** save them to *predictions/PMC3817409*, you would run: <br>
```python predict.py -i papers/PMC3817409 -o predictions/PMC3817409```
- The predictions will be saved as a csv file under *predictions/PMC3817409*
- The output format for the predictions is:
```sentence,sent_idx,start_word_idx,end_word_idx,mention,tag``` where
**sentence** = sentence where the mention was found <br>
**sent_idx** = index of the sentence where the mention was found, in the text <br>
**start_word_idx** = start index of the found mention in the sentence <br>
**end_word_id** = end index of the found mention in the sentence <br>
**mention** = actual mention found <br>
**tag** = the type of mention found; this is either a *DAT* for a data mention or *MET* for a method mention <br>

#### 2. Trained Model Artifacts
The prediction code uses a BioBERT-based trained machine learning model. <br>
All the artifacts needed for training are under *model_artifacts*. <br>
This folder should contain:
1. ```model.pt``` - trained BERT-based pytorch model
2. ```idx2tag.json``` - artifact used both in the training and prediction code
3. ```biobert_vocab.txt``` - BioBERT vocab needed both for training and prediction.

## Metrics of Trained Model
```Train: B-DAT Precision: 0.88 B-DAT Recall: 0.974 F1: 0.925``` <br>
```Train: B-MET Precision: 0.984 B-MET Recall: 0.987 F1: 0.985``` <br>
```Train: I-MET Precision: 0.989 I-MET Recall: 0.973 F1: 0.981``` <br>
```Val: B-DAT Precision: 0.857 B-DAT Recall: 0.96 F1: 0.906``` <br>
```Val: B-MET Precision: 0.983 B-MET Recall: 0.986 F1: 0.984``` <br>
```Val: I-MET Precision: 0.992 I-MET Recall: 0.973 F1: 0.982``` <br>

## Limitations
- For **datasets**, current model has only been trained on Accession Number IDs. There are many more types of dataset identifiers, such as through DOIs or external URLs. The model does not currently address these
- For **methods**, there is some variety in the community as to the definition of an experimental method. Current model has only been trained on experimental biomedical methods. We are working on finalizing our own definition for experimental methods.


## Next steps
- We will be working on releasing the training data, as well as the training code to the community. <br> We have released the prediction code hoping it will be helpful for researchers who wish to extract mentions of datasets and methods from their own texts or journal articles, without having to train a model themselves. 

## References
1. Lee, Jinhyuk, et al. “BioBERT: a pre-trained biomedical language representation model for biomedical text mining.” Bioinformatics 36.4 (2020): 1234–1240. <br>
2. Devlin, Jacob, et al. “Bert: Pre-training of deep bidirectional transformers for language understanding.” arXiv preprint arXiv:1810.04805 (2018).

## License
We are making the data available under a [CC-O license](https://creativecommons.org/publicdomain/zero/1.0/). <br>

## Reporting Security Issues
To report a security issue, please follow the steps outlined in [SECURITY.md](SECURITY.md) <br> <br>
This project adheres to the Contributor Covenant code of conduct. By participating, you are expected to uphold this code. Please report unacceptable behavior to opensource@chanzuckerberg.com.
