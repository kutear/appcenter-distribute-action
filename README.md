# GitHub Actions for Firebase

This Action for [appcenter distribute](https://github.com/microsoft/appcenter-cli) enables arbitrary actions with the `appcenter` command-line client.

## Inputs

* `args` - **Required**. This is the arguments you want to use for the `appcenter` cli


## Environment variables

* `APPCENTER_ACCESS_TOKEN` - **Required**. The token to use for authentication. This token can be aquired through the `appcenter dashboard`.

## Example

To authenticate with AppCenter, and deploy to AppCenter:

```yaml
name: Build and Deploy
on:
  push:
    branches:
      - master

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@master
      - name: Install Dependencies
        run: npm install
      - name: Distribute to AppCenter
        uses: akinncar/appcenter-distribute-action@master
        with:
          args: stores publish  --file /path/to/file.aab --store Production --app yourName/sample-app --release-notes "Some note."
        env:
          APPCENTER_ACCESS_TOKEN: ${{ secrets.APPCENTER_ACCESS_TOKEN }}
```


## License

The Dockerfile and associated scripts and documentation in this project are released under the [MIT License](LICENSE).


### Credits
Thanks to [Jeremy Shore](https://github.com/w9jds) for the firebase-action repo.
