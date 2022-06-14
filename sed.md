# sed

Create a new file, keeping original file intact

```sh
export TOTALJOBS_PASS=ExamplePass1
sed "s/__password__/$TOTALJOBS_PASS/g" puppeteer-totaljobs.js > puppeteer-totaljobs-sub.js
```

Modify a file inline

```sh
sed -i "s/__password__/$TOTALJOBS_PASS/g" puppeteer-totaljobs-sub.js
```

Modify some piped text

```sh
echo hello-world | sed 's/\-//g'
.
helloworld
```

Modify some piped text - substitute multiple times

```sh
echo hello-world | sed 's/\-//g' | sed 's/world/earth/g'
.
helloearth
```

Modify some piped text - substitute with a variable

```sh
echo "env=__environ__" | sed "s/__environ__/$ENV_NAME/g"
```
