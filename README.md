# GraphKit

GraphKit is a collection of language-specific static source code analysis tools
which use a common output format that enumerates the definitions and
cross-references in code. The vision driving GraphKit is to make developer tools
(such as editors, code search, build tools, etc.) more powerful and easier to
create, by providing a standard way for them to determine information about a
project's source code.

**The problem:** Dev tools, such as editors, build tools, package managers,
linters, etc., must partially reimplement a language's compiler or interpreter
to get the information about a project's source code that's necessary to do
their job (such as autocompletion, jump-to-definition, documentation lookup, or
dependency tracking). That means it's hard to write dev tools and they are often
buggy and limited, especially for dynamic languages.

**The solution:** GraphKit's goal is to provide a high-quality, standardized
source analyzer for every popular language. Dev tools can get the information
about a project's code that they need from a GraphKit-provided source analyzer
for the language, instead of implementing their own ad-hoc analysis. This will make dev tools more powerful and easier to create.

## Components

GraphKit has 2 parts: a source analyzer (called a "grapher") for each supported
language, and a common data format that all graphers output.

**Graphers:** For each supported language, GraphKit provides a source analyzer called a
**grapher**. A grapher takes a set of files or directories containing source code as input, performs various kinds of analysis on the code (such as type checking, type inference, etc.), and outputs a data dump describing the code. The data format is described below.

**Data format:** The grapher output describes every definition (of a type,
variable, class, etc.) and maps every name in the source code files to the
definition it references.