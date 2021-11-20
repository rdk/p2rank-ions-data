# Introduction

This repository contains development datasets for P2Rank ion binding site prediction.

P2Rank repo: https://github.com/rdk/p2rank

# Contents

Directories:
* `_incoming`  original received files before tast/train splits
* `_processing` ... contains notes related to prosessing of datasets
* `ZN`, `MG`, ... datasets for individual ions


## ZN datasets

Dataset files are based on 2 main datasets: `ZN_ppu` and `ZN_benchmark`:

Description
* **ppu**: It contains X-ray structures from PDB, with a resolution of 3.0 Å or better, that include at least one (ion) ligand of interest. The dataset has been treated for protein redundancy by applying a sequence identity cutt-off of 30%, and for chain redundancy with UniProt, so as to discard identical chains within a single protein. It has been filtered to exclude structures from the benchmark dataset.
* **benchmark**: This dataset has been used in the literature for evaluating previous predictors. It contains a sub-set of ion-binding proteins from the BioLip database, with a pairwise sequence identity below 30% and a length over 50 residues. The dataset collectively includes proteins that bind nine metal ligands.

Each of them contain `_exposed` and `_buried` version.

Description
* **buried**: It contains (ion) ligands that are located below the computed solvent accessible surface area of the protein structure that they bind to, and are thus considered inaccessible to the solution.
* **exposed**: It contains (ion) ligands that have a non-zero computed solvent accessible surface area, and are thus at least partially exposed to the solution.

There is also `_all` version for `ZN_ppu` (and for `ZN_benchmark`).
Note: `ZN_ppu_all.ds` is not just union of lines from `ZN_ppu_buried.ds` and `ZN_ppu_exposed.ds` because a single protein can contain both buried and exposed ions.
Consequently, dataset file lines for such protein differ in buried and exposed `.ds` files.

Main datasets (exposed/buried split)
* `ZN_benchmark_exposed.ds`
* `ZN_benchmark_buried.ds`
* `ZN_benchmark_all.ds`
* `ZN_ppu_exposed.ds`
* `ZN_ppu_buried.ds`
* `ZN_ppu_all.ds`


### train/test split of `ZN_ppu` (split A)

Additionaly there are datasets that represent train/test split of `ZN_ppu`.
First, single random split of `ZN_ppu_all.ds` was performed: split "A" (train:66%, test:34%):.
Then `ZN_ppu_exposed.ds` and `ZN_ppu_buried.ds` were split according to subsets of proteins from split A.

* `ZN_ppu_all_Atrain.ds`
* `ZN_ppu_all_Atest.ds`
* `ZN_ppu_exposed_Atrain.ds`: subset of `ZN_ppu_buried.ds` containing only proteins from `ZN_ppu_all_Atrain.ds`
* `ZN_ppu_exposed_Atest.ds`: subset of `ZN_ppu_exposed.ds` containing only proteins from `ZN_ppu_all_Atest.ds` 
* `ZN_ppu_buried_Atrain.ds`: subset of `ZN_ppu_buried.ds` containing only proteins from `ZN_ppu_all_Atrain.ds`
* `ZN_ppu_buried_Atest.ds`: subset of `ZN_ppu_buried.ds` containing only proteins from `ZN_ppu_all_Atest.ds` 

Conseuently, it is possible to train and test on different versions (`all`/`exposed`/`buried`) in a single run:
e.g. train on `ZN_ppu_all_Atrain.ds` and test on `ZN_ppu_exposed_Atest.ds` or `ZN_ppu_buried_Atest.ds`.


## MG datasets

Similarly as in ZN datasets:
* There are 2 main datasets: `MG_ppu` and `MG_benchmark`.
* Each of them contain `_exposed` and `_buried` version.

There is also `_all` version for `MG_ppu` (and for `MG_benchmark`).
Note: `MG_ppu_all.ds` is not just union of lines from `MG_ppu_buried.ds` and `MG_ppu_exposed.ds` because a single protein can contain both buried and exposed ions.
Consequently, dataset file lines for such protein differ in buried and exposed `.ds` files.

Main datasets (exposed/buried split)
* `MG_benchmark_exposed.ds`
* `MG_benchmark_buried.ds`
* `MG_benchmark_all.ds`
* `MG_ppu_exposed.ds`
* `MG_ppu_buried.ds`
* `MG_ppu_all.ds`

Train/test split of `MG-ppu` datasets hasn't been done yet.

### train/test split of `ZN_ppu` (split A)

Similarly as in ZN datasets: Additionaly there are datasets that represent train/test split of `MG_ppu`.
First, single random split of `MG_ppu_all.ds` was performed: split "A" (train:66%, test:34%):.
Then `MG_ppu_exposed.ds` and `MG_ppu_buried.ds` were split according to subsets of proteins from split A.

* `MG_ppu_all_Atrain.ds`
* `MG_ppu_all_Atest.ds`
* `MG_ppu_exposed_Atrain.ds`: subset of `MG_ppu_buried.ds` containing only proteins from `MG_ppu_all_Atrain.ds`
* `MG_ppu_exposed_Atest.ds`: subset of `MG_ppu_exposed.ds` containing only proteins from `MG_ppu_all_Atest.ds` 
* `MG_ppu_buried_Atrain.ds`: subset of `MG_ppu_buried.ds` containing only proteins from `MG_ppu_all_Atrain.ds`
* `MG_ppu_buried_Atest.ds`: subset of `MG_ppu_buried.ds` containing only proteins from `MG_ppu_all_Atest.ds` 

Conseuently, it is possible to train and test on different versions (`all`/`exposed`/`buried`) in a single run:
e.g. train on `MG_ppu_all_Atrain.ds` and test on `MG_ppu_exposed_Atest.ds` or `MG_ppu_buried_Atest.ds`.
