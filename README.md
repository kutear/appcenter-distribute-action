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
      - main

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@master
        
      - name: Check file existence
        id: check_files
        uses: andstor/file-existence-action@v1
        with:
          files: "*.apk"

      - name: File exists
        if: steps.check_files.outputs.files_exists == 'true'
        # Only runs if all of the files exists
        run: echo All files exists!

      - name: Install Dependencies
        run: npm install npm@latest -g

      - name: Distribute to AppCenter
        uses: grndvl1/appcenter-distribute-action@master
        with:
          args: stores publish --file /path/to/file.apk-or-aab --store Production --app yourName/sample-app
        env:
          APPCENTER_ACCESS_TOKEN: ${{ secrets.APP_CENTER_TOKEN }}
```

## License

The Dockerfile and associated scripts and documentation in this project are released under the [MIT License](LICENSE).


### Credits
Thanks to [Jeremy Shore](https://github.com/w9jds) for the firebase-action repo.
