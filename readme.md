This FAQ is built in DIF's Spec-Up micro-CMS, which turns a simple markdown file
into full JS+HTML website to display as a technical specification. It is running
in "single-file" mode, i.e., the entire spec can be found in `docs/spec.md`

Feel free to open issues if you would like to see content or links added. 

To PR in new content, first clone the repo, then run spec-up locally by running: 
```
$ npm install spec-up
$ npm run edit
``` 
Meanwhile, open your local copy of /docs/index.html in a browser for a live
preview.  Each time you save the underlying markdown files, you can refresh
index.html in your browser to see the page re-rendered by gulp based on the new
input. 

When you are done, simply open a PR to merge your `docs/spec.md` and your new,
re-rendered `/index.html` file to `main` and the live FAQ will be updated
shortly after the PR is accepted. If it sits for more than a week, ping an
editor on DIF Slack!

For more information on spec-up, see its [repo at DIF](/decentralized-identity/spec-up/).
