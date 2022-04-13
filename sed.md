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
