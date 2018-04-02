# Validate

Before each deployment your file will be verified by the Application but you can at anytime check if your file is well formatted and valid using the following command :

```bash
mesg-cli workflow validate ./PATH_TO_WORKFLOW_FILE
```

This command will validate your file and let you know if there is any errors. All the different validations can be found in the [file](./file.md) section or by in the [JSON schema]({{ book.endpoints.validationSchema }}).
