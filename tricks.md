Rename a file only slightly, or simply add a missing section.
```sh
mv /long/annoying/path/{file,stuff}.txt # rename to stuff
mv /long/annoying/path/{,the-}file.txt  # adds prefix
```

How to figure out how many bits your id private key.
https://security.stackexchange.com/a/42272/135955
```sh
openssl rsa -text -noout -in id_rsa
```

Copy an ssh key to a box, inluding adding to `authorized_keys`.
```sh
ssh-copy-id -n -f -i ~/.ssh/mykey user@host
```

Choose all of one or another during a git merge conflict.
http://gitready.com/advanced/2009/02/25/keep-either-file-in-merge-conflicts.html
```sh
git checkout --ours
git checkout --theirs
```

Undo a git commit --amend
https://stackoverflow.com/a/1459264/2601179
```sh
git reset --soft HEAD@{1} && git reset
```

Get aggregations of some field in Elasticsearch.
```py
d = requests.get('http://localhost:9200/INDEX/doc/_search', json={
  'size': 0, 'aggregations': {'NAME': {'terms': {'size': 32, 'field': 'FIELD'}}},
}).json()
[(b['doc_count'], b['key']) for b in d['aggregations']['NAME']['buckets']]
```

Do `command -V FOO` to display what an alias is set to or, whether it's a
function instead. To see how that custom function is defined as do `declare -f
FOO`.

One can loop and assign over multiple return values or tuples like in shell
like
```sh
# Create a toy CSV file.
cat > /tmp/foo.csv <<EOF
letter,number,fruit
a,1,apple
b,2,orange
c,3,pear
EOF

# Skip first row, and split by comma.
awk 'NR>1' < /tmp/foo.csv | while IFS=, read col1 col2 col3; do
  echo "ROW: $col1 $col2 $col3"
done | column -t
```

