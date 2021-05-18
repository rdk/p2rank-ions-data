
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
# random split
#
cat ZN_ppu_all.ds | grep pdb/ | awk '{print $1}' | sed 's|pdb/||' | sort -u > _ppu_all.list
shuf _ppu_all.list > _ppu_all_shufA.list
wc -l _ppu_all_shufA.list
split -a1 -d -l $(( 1752 * 66 / 100 )) - _ppu_all_splitA < _ppu_all_shufA.list
mv _ppu_all_splitA0 _ppu_all_A_train.list
mv _ppu_all_splitA1 _ppu_all_A_test.list
echo HEADER >> _ppu_all_A_train.list
echo HEADER >> _ppu_all_A_test.list

cat ZN_ppu_all.ds | grep -f _ppu_all_A_train.list > ZN_ppu_all_Atrain.ds
cat ZN_ppu_all.ds | grep -f _ppu_all_A_test.list > ZN_ppu_all_Atest.ds
cat ZN_ppu_exposed.ds | grep -f _ppu_all_A_train.list > ZN_ppu_exposed_Atrain.ds
cat ZN_ppu_exposed.ds | grep -f _ppu_all_A_test.list > ZN_ppu_exposed_Atest.ds
cat ZN_ppu_burried.ds | grep -f _ppu_all_A_train.list > ZN_ppu_burried_Atrain.ds
cat ZN_ppu_burried.ds | grep -f _ppu_all_A_test.list > ZN_ppu_burried_Atest.ds
~~~