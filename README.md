![GraphKit logo](https://raw.github.com/sourcegraph/graphkit/master/media/logo.png)

Follow [@GraphKitProj](https://twitter.com/GraphKitProj) &nbsp; &bull; &nbsp; Visit [graphkit.org](http://graphkit.org) &nbsp; &bull; &nbsp; Supports [JavaScript](https://sourcegraph.com/github.com/sourcegraph/jsg)  &nbsp; &bull; &nbsp; Coming soon: Python, Ruby, Go

<a href="https://sourcegraph.com/github.com/joyent/node"><img align=right alt="GraphKit-provided Node.js core API function list on Sourcegraph" src="https://raw.github.com/sourcegraph/graphkit/master/media/symbols-list.png"></a> <a href="https://sourcegraph.com/github.com/joyent/node/symbols/javascript/commonjs/lib/assert.js/-/equal"><img align=right alt="GraphKit-provided cross-references on Sourcegraph" src="https://raw.github.com/sourcegraph/graphkit/master/media/examples.png"></a> GraphKit is a collection of source code analyzers for several popular
programming languages, which output a standard data format listing a project's
code definitions and cross-references. The long-term vision of GraphKit is to
make dev tools (such as editors, build tools, package managers, linters, code
search, etc.) more powerful and easier to create, by providing a standard way
for them to determine information about a project's source code.

**The problem:** Dev tools (such as editors, build tools, package managers,
linters, and code search) must partially reimplement a language's compiler or
interpreter to get the information about a project's source code that's
necessary to do their job (such as autocompletion, jump-to-definition,
documentation lookup, or dependency tracking). That means it's hard to write dev
tools and they are often brittle and limited, especially for dynamic languages.

**The solution:** GraphKit's goal is to provide a high-quality, standardized
source analyzer for every popular language. Dev tools can get the information
they need about a project's code from a GraphKit source analyzer for the
language, instead of implementing their own ad-hoc analysis. This will make dev
tools more powerful and easier to create.

[See a simple example of running GraphKit on a JavaScript file.](https://github.com/sourcegraph/jsg#graph-a-single-javascript-file)

## Components

GraphKit has 2 parts: a common data format (called the **source graph**) that
contains information about a project's code, and a set of source analyzers
(called **graphers**) that output this data.

**The source graph:** A project's source graph describes every definition (of a
type, variable, class, etc.) and maps every reference to a definition in its
source code files to its target.

**Graphers:** For each supported language, GraphKit provides a source analyzer
program called a **grapher**. A grapher takes a set of files or directories
containing source code as input, performs various kinds of source analysis on
the code (such as type checking, type inference, etc.), and outputs a data dump
describing the code. The data format is described tentatively at [jsg](https://github.com/sourcegraph/jsg#schema).

## Language support status

The version of GraphKit used internally at
[Sourcegraph](https://sourcegraph.com) currently supports 4 languages, but only
JavaScript support has been released publicly so far. Significant underlying
components for supporting other languages have been released, and the graphers
should be released by mid-February 2014.

* **Project:** the project that contains the grapher for the language.
* **Underlying:** the existing type-checking or type-inference library that the grapher relies on, if any.
* **Types?:** does the grapher perform type checking (for statically typed languages) or type inference (for dynamic languages)?
* **Defs?:** does the grapher find all definitions in the code and output them?
* **Refs?:** does the grapher find and resolve source code references to definitions?
* **Docs?:** does the grapher find documentation attached to each definition?
* **Output?:** does the grapher output all of the source graph data?

| Language  | Project | Underlying | Types? | Defs? | Refs? | Docs? | Output? |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| JavaScript  | [sourcegraph/jsg](https://sourcegraph.com/github.com/sourcegraph/jsg) | [marijnh/tern](https://github.com/marijnh/tern) | YES | YES | YES | YES | YES |
| Go  | sourcegraph/gog (coming soon) | [go/types](https://code.google.com/p/go.tools) | YES | YES | YES | YES | NO |
| Python  | coming soon | [PySonar2](https://github.com/yinwang0/pysonar2) | YES | YES | YES | YES | NO |
| Ruby  | coming soon | [RubySonar](https://github.com/yinwang0/rubysonar) & [YARD](http://yardoc.org) | YES | YES | YES | YES | NO |

## Background

The sponsor of this project, [Sourcegraph](https://sourcegraph.com), analyzes
and indexes hundreds of thousands of open source projects to provide developers
with global, semantic search for code, docs, and examples. Doing this well
requires high-quality, comprehensive information about a code's definitions,
cross-references, dependencies, authorship, etc.

Sourcegraphers (including [@yinwang0](https://sourcegraph.com/yinwang0),
[@beyang](https://sourcegraph.com/beyang), and
[@sqs](https://sourcegraph.com/sqs)) have already made significant contributions
to the underlying open source projects that power Sourcegraph's analysis, such
as [yinwang0/pysonar2](https://github.com/yinwang0/pysonar2),
[yinwang0/rubysonar](https://github.com/yinwang0/rubysonar), and
[marijnh/tern](https://github.com/marijnh/tern). GraphKit sits on top of these
libraries, adding some more features and serializing the data into the source
graph output format.

## Contributors

We welcome contributions, both to this GraphKit project (which defines the
source graph format) and to the per-language graphers and analyzers.

* [Quinn Slack (@sqs)](https://sourcegraph.com/sqs)
* [Yin Wang (@yinwang0)](https://sourcegraph.com/yinwang0)
* [Beyang Liu (@beyang)](https://sourcegraph.com/beyang)
