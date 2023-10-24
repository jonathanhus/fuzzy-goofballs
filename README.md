# Intrinsic and Extrinsic Bias Evaluation

## Get Data
```
mkdir data
wget -O data/cp.csv https://raw.githubusercontent.com/nyu-mll/crows-pairs/master/data/crows_pairs_anonymized.csv
wget -O data/ss.json https://raw.githubusercontent.com/moinnadeem/StereoSet/master/data/dev.json
python -u preprocess.py --input crows_pairs --output data/paralled_cp.json
python -u preprocess.py --input stereoset --output data/paralled_ss.json
```

## Environment Configuration
```
pip install torch
pip install tqdm
pip install transformers
```

TODO: create requirements.txt

## Execution

If using the original evalutate code:

`python evaluate.py --data [cp, ss] --output /Your/output/path --model [bert, roberta, albert] --method [aula, aul, cps, sss]`

If using the modified version, which doesn't require preprocessing

`TODO`

## Extrinsic Bias

### BiosBias
The biosbias dataset was generated following the instructions located here:
https://github.com/microsoft/biosbias

For convenience, the BIOS.pkl that was generated is included in this repo

To finetune the model on the BiosBias dataset:

`python train_biosbias.py --task train --model bert-base-uncased`

To evaluate the finetuned model on the BiosBias test dataset, specifying a model checkpoint from the previous finetuning step:

`python train_biosbias.py --task eval --model /scratch/jhus/test-trainer/checkpoint-12000/`

### STS-Bias
The STS-Bias dataset is not publicly available. As the authors did, we attempted to recreate the dataset following the procedure briefly described in 
"Measuring and Reducing Gendered Correlations in Pre-trained Models" by Kellie Webster, et al. https://arxiv.org/pdf/2010.06032.pdf

We downloaded the STS-B data from here: http://ixa2.si.ehu.es/stswiki/images/4/48/Stsbenchmark.tar.gz

To generate the STS-bias dataset:

`python create_stsbias_dataset.py`

### NLI-Bias
The NLI-Bias dataset was generated using scripts and files located here:
https://github.com/sunipa/On-Measuring-and-Mitigating-Biased-Inferences-of-Word-Embeddings.git

Using that repo, generate NLI-Bias
TODO: Verify this output is correct
`python generate_templates.py --noun --p occupations --h gendered_words --output nli-bias.csv`

For convenience the generated dataset is included in this repo as `insert filename`