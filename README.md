# Introduction

This repository contains development datasets for P2Rank ion binding site prediction.


# Contents

* `_incoming`  original received files before tast/train splits
* `_processing` ... contains notes related to prosessing of datasets
* `ZN`, `MG`, ... datasets for individual ions


# ZN datasets

Dataset files are based on 2 main datasets: `ZN_ppu` and `ZN_benchmark`:

Description
* *ppu*: _TODO_
* *benchmark*: _TODO_

Each of them contain `_exposed` and `_buried` version.

Description
* *buried*: _TODO_
* *exposed*: _TODO_

There is also `_all` varsion for `ZN_ppu` (but not yet for `ZN_benchmark`).
Note: `ZN_ppu_all.ds` is not just union of lines from `ZN_ppu_buried.ds` and `ZN_ppu_exposed.ds` because a single protein can contain both burried and exposed ions.
Consequently, dataset file lines for such protein differ in burried and exposed `.ds` files.

Main datasets (exposed/buried split)
* `ZN_benchmark_exposed.ds`
* `ZN_benchmark_buried.ds`
* `ZN_ppu_exposed.ds`
* `ZN_ppu_buried.ds`
* `ZN_ppu_all.ds`


# train/test split of `ZN_ppu` (split A)

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


# MG datasets

Similarly as in ZN datasets:
* There are 2 main datasets: `ZN_ppu` and `ZN_benchmark`.
* Each of them contain `_exposed` and `_buried` version.

There is also `_all` varsion for `MG_ppu` (but not yet for `MG_benchmark`).
Note: `MG_ppu_all.ds` is not just union of lines from `MG_ppu_buried.ds` and `MG_ppu_exposed.ds` because a single protein can contain both burried and exposed ions.
Consequently, dataset file lines for such protein differ in burried and exposed `.ds` files.

Main datasets (exposed/buried split)
* `MG_benchmark_exposed.ds`
* `MG_benchmark_buried.ds`
* `MG_ppu_exposed.ds`
* `MG_ppu_buried.ds`
* `MG_ppu_all.ds`

Train/test split of `MG-ppu` datasets hasn't bee done yet.
