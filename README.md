# BioMPNNs.jl

This package brings several "inverse folding" models (structure → sequence) based on message-passing neural networks to Julia using
[Lux](https://github.com/LuxDL/Lux.jl)! 

| Model | Types | Upstream | Checkpoints |
|---|---|---|---|
| `ProteinMPNN` | vanilla, soluble, Cα-only | [dauparas/ProteinMPNN](https://github.com/dauparas/ProteinMPNN) | `vanilla_48_*`, `soluble_48_*`, `ca_48_*` |
| `LigandMPNN` | ligand/ion/nucleic-acid atom context, optional side-chain context | [dauparas/LigandMPNN](https://github.com/dauparas/LigandMPNN) | `ligandmpnn_v_32_{005,010,020,030}_25` |
| `MembraneMPNN` | per-residue / global membrane label | [dauparas/LigandMPNN](https://github.com/dauparas/LigandMPNN) | `{per_residue,global}_label_membrane_mpnn_v_48_020` |

The Julia models reproduce the PyTorch reference to float tolerance on complete structures
(see *Tests*). Weights are the authors' released checkpoints, converted to safetensors and hosted at
[biofold-jl/proteinmpnn](https://huggingface.co/biofold-jl/proteinmpnn) and
[biofold-jl/ligandmpnn](https://huggingface.co/biofold-jl/ligandmpnn); each checkpoint is downloaded on
first use (see *Weights*).

## Relationship to LuxProteinMPNN.jl

BioMPNNs.jl grew out of [LuxProteinMPNN.jl](https://github.com/Janssena/LuxProteinMPNN.jl), which stays
as it is; ProteinMPNN's code was moved into the shared core and `src/models/protein_mpnn`, and its
weights were converted once and now live on Hugging Face. Known difference from upstream (inherited): residues with `mask = false` are
not visible to the sequence-conditioned message, whereas upstream feeds them through; upstream's own
pipeline passes complete residues, where the two agree.

License: MIT (code and the upstream model parameters are MIT-licensed).
