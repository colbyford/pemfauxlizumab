# EvoDiff-Based Diffusion of novel, PD1-targeting Fab Structures


## Run EvoDiff in Docker Locally
```bash
docker run -v C:\\Users\\Colby\\Documents\\GitHub\\pemfauxlizumab\\diffusion:/workspace/evodiff/pemfaux --gpus all --ipc=host --ulimit memlock=-1 --ulimit stack=67108864 --name evodiff --rm -it evodiff /bin/bash

## cd pemfaux
```

## Evolutionary Guided equence Generation

```python
from evodiff.pretrained import MSA_OA_DM_MAXSUB
from evodiff.generate_msa import generate_query_oadm_msa_simple
import re
import torch
torch.set_default_device('cuda:0')

checkpoint = MSA_OA_DM_MAXSUB()
model, collater, tokenizer, scheme = checkpoint
```

### H Chain
```python
path_to_msa = './PD1_Hchains_aligned.a3m'
n_sequences=33 # number of sequences in MSA to subsample
seq_length=200 # maximum sequence length to subsample
selection_type='random' # or 'MaxHamming'; MSA subsampling scheme


tokenized_sample, generated_sequence  = generate_query_oadm_msa_simple(path_to_msa, model, tokenizer, n_sequences, seq_length, device=0, selection_type=selection_type)

print("New H chain sequence (no gaps, pad tokens)", re.sub('[!-]', '', generated_sequence[0][0],))
```

### L Chain
```python
path_to_msa = './PD1_Lchains_aligned.a3m'
n_sequences=33 # number of sequences in MSA to subsample
seq_length=200 # maximum sequence length to subsample
selection_type='random' # or 'MaxHamming'; MSA subsampling scheme


tokenized_sample, generated_sequence  = generate_query_oadm_msa_simple(path_to_msa, model, tokenizer, n_sequences, seq_length, device=0, selection_type=selection_type)

print("New L chain sequence (no gaps, pad tokens)", re.sub('[!-]', '', generated_sequence[0][0],))
```

## Diffused Sequences

- H Chain: `EVQLVKSGAEFKKPNDSLKITCKASGYTFTNTGTNVHWVRQAPLKQLEWMGIIYTSTKDINYAYEYQGRVEISKETSPSTAYLKLSSLKAENTAVYYCATEGQESVWHHNYLAMDQWGEGTRVTVSS`
- L Chain: `ELVPTQAIRSLSLFLSEGLKISCSSSRDIDNSSNINTELGSFHTRPERTKQDLINNKNNRASGVTELFSGRPSGKNFTLRISPIEADDAAITDILQRKVEPPSNKIVSVGTQYVIQ`