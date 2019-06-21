### Shell rename

Rename part of a filename with discrete shell expansion:
```sh
mv /long/annoying/path/{file,stuff}.txt # rename to stuff
mv /long/annoying/path/{,the-}file.txt  # adds prefix
```

### Private key num bits

How to figure out how many bits your id private key.
https://security.stackexchange.com/a/42272/135955
```sh
openssl rsa -text -noout -in id_rsa
```

### Generate random string

Generate a random password.
https://unix.stackexchange.com/a/306107/162041
```sh
openssl rand -hex 12
```

### Copy ssh key to remote box

Copy an ssh key to a box, inluding adding to `authorized_keys`.
```sh
ssh-copy-id -n -f -i ~/.ssh/mykey user@host
```

### Keep all of one side git conflict

Choose all of one or another during a git conflict.
http://gitready.com/advanced/2009/02/25/keep-either-file-in-merge-conflicts.html
```sh
git checkout --ours FILE
git checkout --theirs FILE
```

### Undo git commit ammend

Undo a git commit --amend
https://stackoverflow.com/a/1459264/2601179
```sh
git reset --soft HEAD@{1} && git reset
```

### Write to file from shell

Write several lines to a file in a script. Note that the EOF is just an
arbitrary string.
```sh
cat > FILE <<<EOF
some
lines
about
stuff
EOF
```

### Elasticsearch aggregations

Get aggregations of some field in Elasticsearch.
```py
d = requests.get('http://localhost:9200/INDEX/doc/_search', json={
  'size': 0, 'aggregations': {'NAME': {'terms': {'size': 32, 'field': 'FIELD'}}},
}).json()
[(b['doc_count'], b['key']) for b in d['aggregations']['NAME']['buckets']]
```

### Inspect a command or alias

Do `command -V FOO` to display what an alias is set to or, whether it's a
function instead. To see how that custom function is defined as do `declare -f
FOO`.

### Loop over values with arg assignment

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

### List all untracked files in git

```sh
# https://stackoverflow.com/a/3801554/2601179
git ls-files --others --exclude-standard
```
