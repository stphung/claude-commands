# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Claude command templates repository containing structured markdown templates for specific Claude AI assistant interactions. The repository serves as a collection of reusable prompts to standardize and improve Claude-assisted development sessions.

## Template Files

### brainstorm.md
A template for exploring multiple implementation approaches for new features. Use this when you need to:
- Generate multiple solutions for a feature request
- Compare different architectural approaches
- Explore trade-offs between implementation strategies

### prime.md
A project initialization template that helps establish Claude's understanding of a codebase. Use this to:
- Introduce Claude to a new project's architecture
- Set up working patterns and conventions
- Establish the project context before starting development work

### refine.md
A code quality improvement template focused on:
- Identifying missing test coverage
- Suggesting refactoring opportunities
- Analyzing code structure and proposing enhancements

## Working with Templates

These templates are designed to be copied and customized for specific use cases. When using a template:
1. Copy the relevant template content
2. Replace placeholder sections with actual project information
3. Paste the customized content into a Claude conversation

## Repository Maintenance

This is a git repository for version controlling template changes. The templates themselves don't require building, testing, or linting - they are documentation files meant to be read and adapted.

## Permissions

The `.claude/settings.local.json` file configures Claude's permissions in this repository, currently allowing:
- `ls` command for directory exploration
- `find` command for file discovery