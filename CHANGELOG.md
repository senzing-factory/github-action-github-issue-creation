# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog], [markdownlint],
and this project adheres to [Semantic Versioning].

## [1.0.0] - 2020-01-11

### Added to 1.0.0

- Docker file to build the image used by Git Actions.
- Added standard documentation artifacts and license.
- Go Lang app that pushes a message to Slack.
- Git Actions CI pipeline to test the Docker build and go app build on commits.
- Git Actions CD pipeline triggered on pull request to verify the merged changes does not break main.

[Keep a Changelog]: https://keepachangelog.com/en/1.0.0/
[markdownlint]: https://dlaa.me/markdownlint/
[Semantic Versioning]: https://semver.org/spec/v2.0.0.html
