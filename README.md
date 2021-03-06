## azurydev/deploy-action

Please refer to [`action.yml`](https://github.com/azurystudio/deploy-action/blob/dev/action.yml) for a full list of all features.

```yml
name: 'Publish'

on:
  push:
    tags:
      - 'v*'

jobs:
  deploy:
    runs-on: ubuntu-latest
        
    steps:
      - name: Git Checkout
        uses: actions/checkout@v2
        
      - name: Setup Node.js
        uses: actions/setup-node@v1
        with:
          node-version: 18.x

      - name: Install Dependencies
        run: npm ci

      - name: Build App
        run: npm run build

      - name: Deploy App
        uses: azurystudio/deploy-action@v0
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USERNAME }}
          privateKey: ${{ secrets.SSH_KEY }}
          destination: /root/whatever
          dependencies: true # update remote package.json, package-lock.json, and dependencies
          directory: /dist # upload all files from a directory
          pm2: 0 # pm2 process name or id
```

<hr>
<div align='center'>
  <h3>Chat with us</h3>
  <a href='https://azury.dev/discord'><b>Join our Discord</b></a>
</div>
<hr>
