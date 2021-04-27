
~~~sh

# list all unique pdbs from datasets
cat *.ds | grep pdb/ | awk '{print $1}' | sed 's|pdb/||' | sort -u > _pdbs.list

# copy from existing dir
cat _pdbs.list | xargs -P2 -I{} cp -v ../../p2rank-ions-data-rdk/2020-10/pdb/{} pdb

# download pdbs that don't are missing in pdb subdir
cat _pdbs.list | xargs -P12 -I{} wget -nc https://files.rcsb.org/download/{} -O pdb/{}

# find duplicates
comm -12  <(ls ZN/pdb) <(ls MG/pdb)

~~~