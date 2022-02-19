# Commit message style guide

Version 1.0.0
<!-- MarkdownTOC -->

- [1. Introduction](#1-introduction)
- [2. Commit message](#2-commit-message)
    - [2.1 Subject line](#21-subject-line)
        - [i. Type](#i-type)
        - [iii. Brief summary](#iii-brief-summary)
    - [2.2 Description \(optional\)](#22-description-optional)
- [4. Examples](#4-examples)
- [References](#references)

<!-- /MarkdownTOC -->

---

## 1. Introduction

This guide outlines how messages SHOULD be formatted when committing code to any version control system, such as Git or Subversion (SVN). 

The future maintainer that thanks you may be yourself.

---

## 2. Commit message

<sub>Based on [BlueJava][bluejavacommit]</sub>

Each commit message SHOULD include:

* **Subject line** — with TYPE, jira issue, and a Brief summary.
* **Description** (optional) — always preceded by a blank line.

A well-formed commit message SHOULD look something like this:

```
TYPE (Jira Issue) Brief summary

Longer description with more details, such as a `code` being introduced
within the context of a `function`.

Multiple paragraphs may be added as required.

Bulleted lists:
* are
* also
* okay

```

Only the top line is required, so a minimal commit message might look like

```
TYPE (Jira Issue) Brief summary
```


### 2.1 Subject line

Generally, the subject line comprises three elements:

* `TYPE`
* `(Scope or jira issue)`
* `Brief summary`

The only **exception** is when populating a **new repository**. All that is required is a subject line of `Initial commit`.


#### i. Type

Every commit subject line MUST start with a TYPE in all CAPS and no spaces or other characters preceding it. The recognised types are:

<table>
    <thead>
        <tr>
            <th>TYPE</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>BREAK</code></td>
            <td>A breaking change such as removing a feature.</td>
        </tr>
        <tr>
            <td><code>CI</code></td>
            <td>Changes in CI or docker files.</td>
        </tr>
        <tr>
            <td><code>DEPEN</code></td>
            <td>Changes in project dependencies.</td>
        </tr>  
        <tr>
            <td><code>DOCS</code></td>
            <td>Changes to the documentation (readme, comments, swagger, etc.).</td>
        </tr>     
        <tr>
            <td><code>ESLINT</code></td>
            <td>Changes or corrections related to eslint or stylelint rules.</td>
        </tr>
        <tr>
            <td><code>FEAT</code></td>
            <td>New feature (component, module, etc).</td>
        </tr>
        <tr>
            <td><code>FILES</code></td>
            <td>Changes related to file (name, location) and folder structure.</td>
        </tr>
        <tr>
            <td><code>FIX</code></td>
            <td>Bug fix.</td>
        </tr>
        <tr>
            <td><code>FUNC</code></td>
            <td>Changes related to the functionality of a component, module, service, etc. already created.</td>
        </tr>
        <tr>
            <td><code>STYLE</code></td>
            <td>Changes related to style files.</td>
        </tr>
        <tr>
            <td><code>TEST</code></td>
            <td>Adding missing tests or editing tests.</td>
        </tr>        
    </tbody>
</table>



---

## References

Inspired by and based heavily on:

* [Bluejava Git commit message format guide][bluejavacommit]
* [How to Write a Git Commit Message][gitcommit]


[bluejavacommit]: https://github.com/bluejava/git-commit-guide "Bluejava Git commit message format guide"
[gitcommit]: https://cbea.ms/git-commit/ "How to Write a Git Commit Message"
