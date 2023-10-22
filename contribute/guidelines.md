---
title: Contribution Guidelines
description: Guide to contribute to the DigiByte Wiki
published: true
date: 2023-10-22T10:59:30.447Z
tags: 
editor: markdown
dateCreated: 2023-10-22T09:24:43.645Z
---

# Contribution Guidelines

Thank you for considering contributing to the DigiByte Blockchain Community Wiki. This guide outlines the process and guidelines for contributing to our wiki, ensuring that your contributions are valuable, well-structured, and easy for the community to understand.

## Where to Contribute

We accept contributions exclusively through GitHub, using Pull Requests (PRs) made to the `Development` branch of our repository. You can find our GitHub repository here: [DigiByte Wiki GitHub Repository](https://github.com/dgbat/digibyte-wiki).

## Preferred Syntax for Contribution

We accept contributions in the following formats, listed in order of preference:

1. **Markdown (MD)**: Markdown is the preferred format for contributions. It is well-supported by the wiki platform.
2. **HTML**: Contributions in HTML are accepted but are not the preferred format. Ensure that your HTML is well-structured and compliant.
3. **Plaintext**: While plaintext contributions are accepted, they should be used sparingly, as they offer limited formatting options.

## Wiki Platform

Our wiki platform runs on Wiki.js, a modern and user-friendly platform for documentation. To ensure your contributions are compatible with our platform, please refer to our [Markdown Guide](https://wiki.digibyte.org/en/contribute/markdown-guide).

## Discussion and Comments

Users can engage in discussions and offer comments directly on the wiki platform. However, please note the following:

- To participate in discussions and comment on articles, users must be logged in.
- Users can log in to the wiki platform using their GitHub credentials, simplifying the authentication process.

## Suggestions and Proposals

If you wish to make suggestions or propose new content or changes to existing content, we encourage you to create GitHub Issues on our repository. This helps us manage and track suggestions, making it easier for the community to engage with your proposals.

## Contribution Workflow

1. Fork the [DigiByte Wiki GitHub Repository](https://github.com/dgbat/digibyte-wiki) to your GitHub account.

2. Clone your forked repository to your local development environment.

3. Create a new branch from the `Development` branch. Name it appropriately to describe your contribution.

4. Make your desired changes to the wiki content, ensuring they follow the preferred syntax (MD, HTML, or Plaintext).

5. Commit your changes to your branch.

6. Push your branch to your forked repository on GitHub.

7. Create a Pull Request (PR) from your branch to the `Development` branch of the main repository. In the PR description, please provide a brief summary of your contribution.

8. Our maintainers will review your PR, provide feedback if needed, and merge it if it meets our contribution guidelines.

Your contributions are highly appreciated, and they play a crucial role in maintaining and improving the DigiByte Blockchain Community Wiki. Thank you for being part of our community!

If you have any questions or need assistance with the contribution process, please feel free to reach out to our maintainers or community members.

# Git Contribution Guide
This guide provides a quick reference for using Git to contribute to the DigiByte Blockchain Community Wiki. It assumes you have a basic understanding of Git.

## Cloning the Repository

1. **Fork the Repository**: Click the <kbd>Fork</kbd> button on the [DigiByte Wiki GitHub Repository](https://github.com/dgbat/digibyte-wiki) to create a copy in your GitHub account.

2. **Clone Your Fork**: Clone your forked repository to your local development environment.

```bash
git clone https://github.com/YourGitHubUsername/digibyte-wiki.git
```

## Create a Branch

1. **Create a New Branch**: Name it appropriately to describe your contribution. A common convention is to prefix the branch name with "feature/" or "fix/" followed by a descriptive name.

```bash
git checkout -b feature/descriptive-branch-name
```

## Making changes

### Edit and Add files

Make your desired changes to the wiki content, and add new or modified files.

```bash
# Make your changes
# Add files for staging
git add file1.md file2.md
```

### Commit Changes

Commit your changes with a descriptive message.

```bash
git commit -m "Add new content to file1.md"
```

> If you want to make a longer commit message you can ommit the `-m` flag and the message.
> You will be prompted to create the commit message in your default editor.
> The first line will be the subject title and the third line will start your actual content message.
{.is-info}

### Push and Create a Pull Request

1. **Push Your Branch**: Push your branch to your forked repository on GitHub.

```bash
git push origin feature/descriptive-branch-name
```

2. **Create a Pull Request (PR)**: Navigate to the [DigiByte Wiki GitHub Repository](https://github.com/dgbat/digibyte-wiki), click on "New Pull Request," and choose your branch.

### Branch Naming Convention

To maintain consistency and clarity in branch names, we recommend using the following naming convention:

* Feature Branch: Prefix with "feature/" and provide a descriptive name. Example: feature/update-markdown-guide.

* Fix Branch: Prefix with "fix/" and provide a descriptive name. Example: fix/typo-in-article.

This naming convention helps quickly identify the purpose of each branch and is widely used in collaborative software development.

That's it! Your contributions to the DigiByte Blockchain Community Wiki will go through the review process, and if approved, they will be merged into the main repository. Thank you for your contributions!