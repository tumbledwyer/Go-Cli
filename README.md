# goinstant
Testing
This is a Go CLI app and is provided as a native binary for the AMD64 architecture on Windows, macOS, and Linux.

> Warning: This app is not meant to be used for container and cluster management in production or with sensitive data. It is meant for demos, training sessions, and by developers. In production and with sensitive data, administrators should use the purpose-built tools like the Docker and Kubernetes CLIs to manage resources directly and according to best practices which are outside the scope of this app.

## Usage

Download Golang version 1.17.x or higher.

On Unix-like operating systems, you must add execute permissions, ie. `chmod +x goinstant-linux`.

Without arguments, the CLI defaults to interactive mode. The CLI can also be used non-interactively as so:
```txt
Commands: 
	help 		this menu
	docker		manage package in docker, usage: docker <package> <state> e.g. docker core init
	kubernetes	manage package in kubernetes, usage: k8s/kubernetes <package> <state>, e.g. k8s core init
	install		install fhir npm package on fhir server, usage: install <ig_url> <fhir_server>, e.g. install https://intrahealth.github.io/simple-hiv-ig/ http://hapi.fhir.org/baseR4
```

## Security

This desktop app is meant as a prototype and may change. This app resides in userspace but it invokes the command line for containers and clusters. The apps it invokes, Docker and Kubernetes CLI, launch and manage containers and may have admin/root privileges.

Therefore, this app is not meant to be used for container and cluster management in production or with sensitive data. It is meant for demos, training sessions, and by developers. In production and with sensitive data, administrators should use the purpose-built tools like the Docker and Kubernetes CLIs to manage resources directly and according to best practices which are outside the scope of this app.

## Developers

### Dev prerequisites

* Install go, [see here](https://golang.org/doc/install). For Ubuntu you might want to use the go snap package, [see here](https://snapcraft.io/install/go/ubuntu).
* Add go binaries to you system $PATH, on ubuntu: Add `export PATH=$PATH:$HOME/go/bin` to the end of your ~/.bashrc file. To use this change immediately source it: `source ~/.bashrc`
* Install dependencies, run this from the goinstant folder: `go mod tidy`

### Running

For development, run the app using `go run .`.

### Testing

To run the unit tests, ensure you're in the goinstant directory, then do

```
go test . -v
```

### Building

```sh
bash ./buildreleases.sh
```

### Deploying

If any changes have been made to the Go CLI, update the version in `./version`

To build releases, create an instant tag and a release, the GitHub actions will build the code after creation of the release and add the binaries to the assets of the release if the GO CLI build succeeds.

Check [here](https://github.com/openhie/instant/actions/new) to review the output of the build and status of the binary deploy.

### Testing

The [godog library](https://github.com/cucumber/godog), which provides us with the [Cucumber Framework](https://cucumber.io/) is used for functional tests of the Go CLI. To run the tests, you'll need to [install godog](https://github.com/cucumber/godog#install).

```bash
go install github.com/cucumber/godog/cmd/godog@v0.12.0
```

Then, navigate to the `goinstant` root folder and run the command below.

```bash
godog
```

> These functional tests can only be run when the `instant` docker volume does not exist on the machine being used for running the tests. These tests make use of the mock image of the instant project `jembi/go-cli-test-image`.
