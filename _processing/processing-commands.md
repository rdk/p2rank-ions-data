
~~~sh

# list all unique pdbs from datasets
cat *.ds | grep pdb/ | awk '{print $1}' | sed 's|pdb/||' | sort -u > _pdbs.list

# copy from existing dir
cat _pdbs.list | xargs -P2 -I{} cp -v ../../p2rank-ions-data-rdk/2020-10/pdb/{} pdb

# download pdbs that are missing in pdb subdir
cat _pdbs.list | xargs -P12 -I{} wget -nc https://files.rcsb.org/download/{} -O pdb/{}

# find duplicates
comm -12  <(ls ZN/pdb) <(ls MG/pdb)


#
# Random split of ZN_ppu_all
#
# Name of the split: A
# First we randomely split all proreins from (ZN_ppu_all.ds) to train and test subsets.
# Then split ZN_ppu_exposed.ds and ZN_ppu_buried.ds according to split of ZN_ppu_all.ds.
#
cat ZN_ppu_all.ds | grep pdb/ | awk '{print $1}' | sed 's|pdb/||' | sort -u > _ppu_all.list
shuf _ppu_all.list > _ppu_all_shufA.list
wc -l _ppu_all_shufA.list # 1752 
split -a1 -d -l $(( 1752 * 66 / 100 )) - _ppu_all_splitA < _ppu_all_shufA.list # 66% vs 34% split
mv _ppu_all_splitA0 _ppu_all_A_train.list
mv _ppu_all_splitA1 _ppu_all_A_test.list
echo HEADER >> _ppu_all_A_train.list   # to match also HEADER line when doing 'grep -f'
echo HEADER >> _ppu_all_A_test.list

cat ZN_ppu_all.ds | grep -f _ppu_all_A_train.list > ZN_ppu_all_Atrain.ds
cat ZN_ppu_all.ds | grep -f _ppu_all_A_test.list > ZN_ppu_all_Atest.ds
cat ZN_ppu_exposed.ds | grep -f _ppu_all_A_train.list > ZN_ppu_exposed_Atrain.ds
cat ZN_ppu_exposed.ds | grep -f _ppu_all_A_test.list > ZN_ppu_exposed_Atest.ds
cat ZN_ppu_buried.ds | grep -f _ppu_all_A_train.list > ZN_ppu_buried_Atrain.ds
cat ZN_ppu_buried.ds | grep -f _ppu_all_A_test.list > ZN_ppu_buried_Atest.ds




#
# Random split of MG_ppu_all
#
# Name of the split: A
# First we randomely split all proreins from (MG_ppu_all.ds) to train and test subsets.
# Then split MG_ppu_exposed.ds and MG_ppu_buried.ds according to split of MG_ppu_all.ds.
#
cat MG_ppu_all.ds | grep pdb/ | awk '{print $1}' | sed 's|pdb/||' | sort -u > _ppu_all.list
shuf _ppu_all.list > _ppu_all_shufA.list
wc -l _ppu_all_shufA.list # 2348 
split -a1 -d -l $(( 2348 * 66 / 100 )) - _ppu_all_splitA < _ppu_all_shufA.list # 66% vs 34% split
mv _ppu_all_splitA0 _ppu_all_A_train.list
mv _ppu_all_splitA1 _ppu_all_A_test.list
echo HEADER >> _ppu_all_A_train.list   # to match also HEADER line when doing 'grep -f'
echo HEADER >> _ppu_all_A_test.list

cat MG_ppu_all.ds | grep -f _ppu_all_A_train.list > MG_ppu_all_Atrain.ds
cat MG_ppu_all.ds | grep -f _ppu_all_A_test.list > MG_ppu_all_Atest.ds
cat MG_ppu_exposed.ds | grep -f _ppu_all_A_train.list > MG_ppu_exposed_Atrain.ds
cat MG_ppu_exposed.ds | grep -f _ppu_all_A_test.list > MG_ppu_exposed_Atest.ds
cat MG_ppu_buried.ds | grep -f _ppu_all_A_train.list > MG_ppu_buried_Atrain.ds
cat MG_ppu_buried.ds | grep -f _ppu_all_A_test.list > MG_ppu_buried_Atest.ds






#
# Random split of ZN_biolip_all.tmp
#
# Name of the split: A
# First we randomely split all proreins from (ZN_biolip_all.tmp.ds) to train and test subsets.
#
cat ZN_biolip_all.tmp.ds | grep pdb/ | awk '{print $1}' | sed 's|pdb/||' | sort -u > _biolip_all.list
shuf _biolip_all.list > _biolip_all_shufA.list
wc -l _biolip_all_shufA.list # 1752 
split -a1 -d -l $(( 1752 * 66 / 100 )) - _biolip_all_splitA < _biolip_all_shufA.list # 66% vs 34% split
mv _biolip_all_splitA0 _biolip_all_A_train.list
mv _biolip_all_splitA1 _biolip_all_A_test.list
echo HEADER >> _biolip_all_A_train.list   # to match also HEADER line when doing 'grep -f'
echo HEADER >> _biolip_all_A_test.list

cat ZN_biolip_all.tmp.ds | grep -f _biolip_all_A_train.list > ZN_biolip_all_Atrain.tmp.ds
cat ZN_biolip_all.tmp.ds | grep -f _biolip_all_A_test.list > ZN_biolip_all_Atest.tmp.ds
#cat ZN_ppu_exposed.ds | grep -f _ppu_all_A_train.list > ZN_ppu_exposed_Atrain.ds
#cat ZN_ppu_exposed.ds | grep -f _ppu_all_A_test.list > ZN_ppu_exposed_Atest.ds
#cat ZN_ppu_buried.ds | grep -f _ppu_all_A_train.list > ZN_ppu_buried_Atrain.ds
#cat ZN_ppu_buried.ds | grep -f _ppu_all_A_test.list > ZN_ppu_buried_Atest.ds


#
# Random split of MG_biolip_all
#
# Name of the split: A
# First we randomely split all proreins from (MG_ppu_all.ds) to train and test subsets.
# Then split MG_ppu_exposed.ds and MG_ppu_buried.ds according to split of MG_ppu_all.ds.
#
cat MG_biolip_all.tmp.ds | grep pdb/ | awk '{print $1}' | sed 's|pdb/||' | sort -u > _biolip_all.list
shuf _biolip_all.list > _biolip_all_shufA.list
wc -l _biolip_all_shufA.list # 1804 
split -a1 -d -l $(( 2348 * 66 / 100 )) - _biolip_all_splitA < _biolip_all_shufA.list # 66% vs 34% split
mv _biolip_all_splitA0 _biolip_all_A_train.list
mv _biolip_all_splitA1 _biolip_all_A_test.list
echo HEADER >> _biolip_all_A_train.list   # to match also HEADER line when doing 'grep -f'
echo HEADER >> _biolip_all_A_test.list

cat MG_biolip_all.tmp.ds | grep -f _biolip_all_A_train.list > MG_biolip_all_Atrain.tmp.ds
cat MG_biolip_all.tmp.ds | grep -f _biolip_all_A_test.list > MG_biolip_all_Atest.tmp.ds
# cat MG_ppu_exposed.ds | grep -f _ppu_all_A_train.list > MG_ppu_exposed_Atrain.ds
# cat MG_ppu_exposed.ds | grep -f _ppu_all_A_test.list > MG_ppu_exposed_Atest.ds
# cat MG_ppu_buried.ds | grep -f _ppu_all_A_train.list > MG_ppu_buried_Atrain.ds
# cat MG_ppu_buried.ds | grep -f _ppu_all_A_test.list > MG_ppu_buried_Atest.ds



~~~


