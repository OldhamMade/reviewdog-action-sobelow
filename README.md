# GitHub Action: Run sobelow with reviewdog

[![Docker Image CI][docker-image-ci]][urls-action]
[![Release][images-release]][urls-releases]

This action runs [sobelow][urls-sobelow] with
[reviewdog][urls-reviewdog] on pull requests to improve code review
experience.

This action is **heavily** based on
[`review-action-credo`][url-review-action-credo] from the gang at
[red-shirts][url-red-shirts].

## Inputs

### `github_token`

**Required**. Must be in form of `github_token: ${{ secrets.github_token }}`'.

### `level`

Optional. Report level for reviewdog [info,warning,error].
It's same as `-level` flag of reviewdog.

### `reporter`

Reporter of reviewdog command [github-pr-check,github-pr-review].
Default is github-pr-check.
github-pr-review can use Markdown and add a link to rule page in reviewdog reports.

## Example usage

### [.github/workflows/reviewdog.yml](.github/workflows/reviewdog.yml)

```yml
name: reviewdog
on: [pull_request]
jobs:
  sobelow:
    name: runner / sobelow
    runs-on: ubuntu-latest
    container:
      image: elixir:1.9.1-slim
    steps:
      - uses: actions/checkout@v1
      - name: Install Dependencies
        run: |
          mix local.rebar --force
          mix local.hex --force
          mix deps.get
      - name: sobelow
        uses: OldhamMade/reviewdog-action-sobelow@v1
        with:
          github_token: ${{ secrets.github_token }}
          reporter: github-pr-review # Change reporter.
```

[docker-image-ci]: https://github.com/OldhamMade/reviewdog-action-sobelow/workflows/Docker%20Image%20CI/badge.svg
[images-release]: https://img.shields.io/github/release/OldhamMade/reviewdog-action-sobelow.svg?maxAge=43200
[urls-action]: https://github.com/OldhamMade/reviewdog-action-sobelow/actions
[urls-releases]: https://github.com/OldhamMade/reviewdog-action-sobelow/releases
[urls-sobelow]: https://github.com/rrrene/sobelow
[urls-reviewdog]: https://github.com/reviewdog/reviewdog
[urls-review-action-credo]: https://github.com/red-shirts/reviewdog-action-credo
[urls-red-shirts]: https://github.com/red-shirts
