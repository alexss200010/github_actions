# Snyk Ruby Action

A [GitHub Action](https://github.com/features/actions) for using [Snyk](https://snyk.io) to check for
vulnerabilities in your Ruby projects.

You can use the Action as follows:

```yaml
name: Example workflow for Ruby usng Snyk 
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: Run Snyk to check for vulnerabilities
      uses: garethr/snyk-actions/ruby@master
      env:
        SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

The Snyk Ruby Action has properties which are passed to the underlying image. These are
passed to the action using `with`.

| Property | Default | Description |
| --- | --- | --- |
| args |   | Override the default arguments to the Snyk image |
| version | latest | Which version of the image to use. See [snyk-images](https://github.com/garethr/snyk-images) for details |

For example, you can choose to only report on high severity vulnerabilities.

```yaml
name: Example workflow for Ruby usng Snyk 
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: Run Snyk to check for vulnerabilities
      uses: garethr/snyk-actions/ruby@master
      env:
        SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      with:
        args: snyk test --severity-threshold=high
```