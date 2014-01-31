# GraphKit

GraphKit is a collection of language-specific static source code analysis tools
which use a common output format that enumerates the definitions and
cross-references in code. The vision driving GraphKit is to make developer tools
(such as editors, code search, build tools, etc.) more powerful and easier to
create, by providing a standard way for them to determine information about a
project's source code.

Today, a programming language's standard toolchain usually consists of a
compiler or interpreter, and a debugger. Editors, build tools, package managers,
linters, etc., must partially reimplement a language's compiler or interpreter
to get the information about the project that's necessary to do their job (such
as autocompletion, jump-to-definition, documentation lookup, or dependency
tracking).

What if these other tools could get that information from a standard,
high-quality source analyzer for the language, instead of relying on their own
ad-hoc analyzer? We think that'd make development tools more powerful, more
reliable, and easier to create. That's why GraphKit's goal is to provide
high-quality source analyzers for every popular language. In the future, we
believe that languages will ship source analyzers with their standard toolchain.

## Components

GraphKit has 2 parts: a source analyzer (called a "grapher") for each supported
language, and a common data format that all graphers output.

**Graphers:** For each supported language, GraphKit provides a source analyzer called a
**grapher**. A grapher takes a set of files or directories containing source code as input, performs various kinds of analysis on the code (such as type checking, type inference, etc.), and outputs a data dump describing the code. The data format is described below.

**Data format:** The grapher output describes every definition (of a type,
variable, class, etc.) and maps every name in the source code files to the
definition it references.