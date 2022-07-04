# Commit message style guide

Version 1.0.1
<!-- MarkdownTOC -->

- [1. Introduction](#1-introduction)
- [2. Commit message](#2-commit-message)
    - [2.1 Subject line](#21-subject-line)
        - [i. Type](#i-type)
        - [ii. Jira Issue](#ii-jira-issue)
        - [iii. Brief summary](#iii-brief-summary)
    - [2.2 Description \(optional\)](#22-description-optional)
- [3. Examples](#3-examples)
- [4. Exceptions](#4-Exceptions)
- [5. References](#5-references)

<!-- /MarkdownTOC -->

---

## 1. Introduction

This guide outlines how messages SHOULD be formatted when committing code to any version control system, such as Git or Subversion (SVN). 

Before reading this guide it is necessary to know [Atomic Commit][atomiccommit].

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
* `(Jira Issue)`
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
         <tr>
            <td><code>DB</code></td>
            <td>SQL files, migrations, ORM (schemas, models) that depend on database changes.</td>
        </tr>
    </tbody>
</table>

#### ii. Jira Issue

Every commit MUST contain a reference to the ticket in Jira.

#### iii. Brief summary

The summary portion of the subject line should very succinctly describe the change. To keep the entire subject line under 50 or 70 characters, you will need to be very brief. Use the [Description](#22-description-optional) section if you feel more detail is helpful.

Use the imperative mood, as in "Add ability to export to JSON" (not "Adding" or "Added"). An easy test for imperative mood is that your summary should complete the sentence: "Applying this patch will…" - though there is no need for perfect grammar. i.e. "Add ability…" rather than "Add the ability…" as long as it is clear.

---------------

### 2.2 Description \(optional\)

The **Description** is optional - but if you wish to include it, always separate from the Subject line by a blank line. In other words, the 2nd line in your commit message should always be blank if you are making a multi-line commit.

The **Description** is a chance to elaborate on the change you made. Focus on the motivation and extra considerations for the change rather than detailing *what* you changed. The details of what changed can be seen in the file diff. But extra considerations such as side effects or migration hints are less obvious from the code, and could be helpful to detail here.

Continue using imperative mood, as you did in the subject line.

Multiple paragraphs can be used (separated by blank lines) for clarity/organization.

---------------

## 3. Examples

```git
ESLINT (PRO-01) Add default props in login template
```
```git
FIX (PRO-02) Update login to be able to start the app
```
```git
TEST (PRO-03) Add login test
```
```git
BREAK (PRO-04) Remove getFriends API endpoint

In accordance with new privacy policy, remove the getFriends API endpoint. 
(The endpoint will continue to exist for a while and return a deprecation notice)
```
```git
FILES (PRO-05) Add mockup.json
```
```git
CI (PRO-06) Update DeployDev job
```
---------------

## 4. Exceptions

Merges or conflict resolved using the default messages.

```git
Merge pull request #63 from Project/story/PRO-07
```

```git
Merge branch 'story/PRO-08' of github.com:BlackstoneStudio/Project into subtask/PRO-09
```

---------------

## 5. References

Inspired by and based heavily on:

* [Atomic Commit][atomiccommit]
* [Bluejava Git commit message format guide][bluejavacommit]
* [How to Write a Git Commit Message][gitcommit]


[atomiccommit]: https://www.freshconsulting.com/insights/blog/atomic-commits/ "Atomic Commit"
[bluejavacommit]: https://github.com/bluejava/git-commit-guide "Bluejava Git commit message format guide"
[gitcommit]: https://cbea.ms/git-commit/ "How to Write a Git Commit Message"
