# PQC File Sharing System Documentation

This repository contains the published documentation for the
[`smu.smc.pqc.mtc`](https://github.com/yjm9110/smu.smc.pqc.mtc) source-code
repository.

The two repositories are independent Git repositories. This documentation
repository is normally cloned as the ignored `docs-site/` directory inside a
local checkout of the source repository. A documentation commit therefore does
not change the source repository, and the source repository does not record a
documentation commit reference.

The published site is available at:

<https://yjm9110.github.io/smu.smc.pqc.mtc.docs/>

## Generated content

Do not edit the generated HTML manually. The source repository builds it from
its README files, Java source and Javadoc comments, JavaScript source and
JSDoc comments, and JavaScript tutorials.

| Output | Source |
| --- | --- |
| `index.html` | Source repository `README.md` |
| `java/index.html` | `java/PQC-MTC/README.md` |
| `java/apidocs/` | Java source and Javadoc content |
| `js/index.html` | `js/README.md` |
| `js/api/` | JavaScript source, JSDoc content, and tutorials |

The empty `.nojekyll` file tells GitHub Pages to publish these generated files
directly without processing them with Jekyll.

## Initial local setup

Clone this repository into `docs-site/` at the root of the source repository:

```bash
git clone https://github.com/yjm9110/smu.smc.pqc.mtc.git
cd smu.smc.pqc.mtc
git clone https://github.com/yjm9110/smu.smc.pqc.mtc.docs.git docs-site
```

The source repository ignores `docs-site/`, so changes and commits made here
will not appear in the source repository's Git status.

Install the JavaScript documentation dependencies once from the source
repository root:

```bash
cd js
npm ci
cd ..
```

The Java documentation generator also requires the Java and Maven environment
used by the source project. The project's VS Code development container
provides the expected build environment.

## Update and publish the documentation

Run the following commands from the source repository root:

```bash
# Start from the latest published documentation branch.
git -C docs-site switch main
git -C docs-site pull --ff-only origin main

# Generate the homepage, Java documentation, and JavaScript documentation.
./scripts/generate-docs.sh

# Review the generated changes before publishing them.
git -C docs-site status
git -C docs-site diff --stat

# Commit and publish only in the documentation repository.
git -C docs-site add -A
git -C docs-site commit -m "Update documentation"
git -C docs-site push origin main
```

The generation command does not commit or push either repository. After the
final push, GitHub Pages publishes the latest content from this repository's
`main` branch and `/ (root)` directory. No commit is required in the source
repository.

## Repository layout

```text
.
├── .nojekyll          Disable Jekyll processing on GitHub Pages
├── README.md          Relationship and publishing instructions
├── index.html         Documentation homepage
├── java/
│   ├── index.html     Java guide
│   └── apidocs/       Generated Javadoc
└── js/
    ├── index.html     JavaScript guide
    └── api/           Generated JSDoc and tutorials
```
