# openapi-go ![test](https://github.com/toollery/openapi-go/workflows/test/badge.svg?event=push)

An OpenAPI Generator template for Go API clients. This set of templates are
intended to replace those that are built into the OpenAPI Generator tool,
implementing configurable request flow and failure methods.

## Prerequisites

You will need the following things properly installed on your computer.

* [Go](https://golang.org/): any one of the **three latest major**
  [releases](https://golang.org/doc/devel/release.html)
* [OpenAPI Generator](https://openapi-generator.tech/)

## Installation

Clone this repository to a path accessible by the [OpenAPI
Generator](https://openapi-generator.tech/) tool.

```bash
$ git clone <repository-url>
```

## Usage

A Go API client may be generated using this template by instructing the OpenAPI
Generator tool to use this repository as the template directory instead of
using the built-in templates that ship with the tool.

```bash
$ openapi generate -c openapi-config.yaml -t <path-to-these-templates> -o out
```

This command assumes a configuration file with the following values. Some of
these can be change but everything under files must remain as defined.

```yaml
# openapi-config.yaml
inputSpec: openapi.yaml
generatorName: go
gitUserId: toollery      # Change as appropriate
gitRepoId: myapi-go      # Change as appropriate
httpUserAgent: myapi/go/ # Change as appropriate
additionalProperties:
  enumClassPrefix: true
  generateInterfaces: true
  packageName: "myapi"   # Change as appropriate
files:
  # APIError is a type defined in the specification but it has special meaning
  # and needs to implement the error interface. Therefore the type is redefined
  # and included as a separate template.
  #
  # NOTE: remember to explicitly ignore model_api_error.go
  error.mustache:
    destinationFilename: error.go
  error_test.mustache:
    destinationFilename: error_test.go
  options.mustache:
    destinationFilename: options.go
  backoff/backoff.mustache:
    folder: backoff
    destinationFilename: backoff.go
  backoff/backoff_test.mustache:
    folder: backoff
    destinationFilename: backoff_test.go
  backoff/constant.mustache:
    folder: backoff
    destinationFilename: constant.go
  backoff/exponential.mustache:
    folder: backoff
    destinationFilename: exponential.go
  backoff/linear.mustache:
    folder: backoff
    destinationFilename: linear.go
  credentials/basic.mustache:
    folder: credentials
    destinationFilename: basic.go
  credentials/bearer.mustache:
    folder: credentials
    destinationFilename: bearer.go
  credentials/credentials_test.mustache:
    folder: credentials
    destinationFilename: credentials_test.go
  throttle/group.mustache:
    folder: throttle
    destinationFilename: group.go
  throttle/throttle_test.mustache:
    folder: throttle
    destinationFilename: throttle_test.go
  throttle/transport.mustache:
    folder: throttle
    destinationFilename: transport.go
```

# Future Work

Instead of defining only a set of templates to be used with a pre-existing
generator it would be more ideal to create an entirely new generator bespoke to
these template files.

Due to how these templates integrate with a pre-existing generator there are
a few features missing from templates that were regarded non-essential and
perhaps could better abstracted in the future.

## License

This project is licensed under the [MIT License](LICENSE.md).
