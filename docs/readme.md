Commits to main, upon being merged, should re-render and re-deploy via GH Pages; see [actions tab](https://github.com/decentralized-identity/faq/actions/new) for results/updates.

To render locally, run 
```
$ npm install spec-up
$ npm run edit
``` 
And open /docs/index.html.  The each time you save the underlying markdown files, you can refresh index.html in your browser to see the page re-rendered by gulp based on the new input. 

For more information on spec-up, see its [repo at DIF](/decentralized-identity/spec-up/).
