Contents API
============

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [Contents API](#contents-api)
    - [Get file contents](#get-file-contents)
    - [Create a file](#create-a-file)
    - [Update a file](#update-a-file)
    - [Delete a file](#delete-a-file)

<!-- markdown-toc end -->

As opposed to the [Git Data API](./git-data.md), this part of the binding provides a _high-level_ way of reading, creating, updating and deleting files. The classes that are involved are `GHRepository` and [`GHContent`](../GitHub-Contents.package/GHContent.class/README.md). The four different use-cases are explained in the sections below.

## Get file contents

To get the contents of a file, one can send the following messages to an instance of `GHRepository`:

- **`getContentAtPath:`**: Returns an instance of `GHContent` which contains the file contents of the file at the given path.
- **`getContentAtPath:atRef:`**: Same as above, but returns the file at the given version (can be a commit name, branch name or tag name).

## Create a file

Use `GHRepository>>createContent:onPath:withMessage:`, with the parameters being the content of the file, the path of the file, and the commit message (all being instances of `String`.

## Update a file

Use `GHContent>>updateContent:withMessage:`, with similar parameters as with the method to create files. This method updates the same instance with the new content information, thus it is possible to send `updateContent:withMessage:` multiple times.

Moreover, it returns the `GHGitCommit` object representing the commit of the change. Thus from here it is possible to switch to using the [Git Data API](./git-data.md) and create commits with the returned `GHGitCommit` object as parent.

## Delete a file

Use `GHContent>>deleteContentWithMessage:`. Like `updateContent:withMessage:`, this method returns a `GHGitCommit` instance.
