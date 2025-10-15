# -----------------------------------------------------------------------------
# Stage: build
# -----------------------------------------------------------------------------
FROM golang:1.25.3-alpine3.22@sha256:aee43c3ccbf24fdffb7295693b6e33b21e01baec1b2a55acc351fde345e9ec34 AS build

ARG GITHUB_HEAD_REF="main"
ARG GITHUB_EVENT_NAME="push"

# Add github
RUN apk update && \
  apk upgrade && \
  apk add --no-cache \
  git \
  make

WORKDIR /go/src

HEALTHCHECK CMD git --version || exit 1

# Clone repo
RUN git clone https://github.com/senzing-factory/github-action-github-issue-creation.git

# Checkout to target branch and if not main, then locally test
# merging main into branch.
WORKDIR /go/src/github-action-github-issue-creation
RUN git checkout ${GITHUB_HEAD_REF}; \
  if [[ "${GITHUB_HEAD_REF}" != "main" && ${GITHUB_EVENT_NAME} == "pull_request" ]]; then \
  git merge main; \
  fi

# Building go app
RUN make build

# -----------------------------------------------------------------------------
# Stage: build
# -----------------------------------------------------------------------------
FROM alpine:3.22@sha256:4b7ce07002c69e8f3d704a9c5d6fd3053be500b7f1c69fc0d80990c2ad8dd412

LABEL name="senzing-factory/github-action-github-issue-creation" \
  maintainer="support@senzing.com" \
  version="1.0.0"

LABEL "com.github.actions.icon"="message-square"
LABEL "com.github.actions.color"="purple"
LABEL "com.github.actions.name"="GitHub Action GitHub Issue Creation"
LABEL "com.github.actions.description"="Create a GitHub Issue"

COPY --from=build /go/bin/github-action-github-issue-creation /usr/bin
COPY --from=build /go/src/github-action-github-issue-creation/LICENSE /
COPY --from=build /go/src/github-action-github-issue-creation/README.md /

USER 1001

ENTRYPOINT ["github-action-github-issue-creation"]
