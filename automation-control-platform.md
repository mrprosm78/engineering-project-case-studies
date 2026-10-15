# Automation Control Platform

## The problem

Automation across several projects needs clear task ownership, scoped permissions and a review trail. A task must not gain access to an unrelated project simply because it uses the same platform.

## The solution

A Laravel control application manages project records, task scheduling, access grants, approvals and worker communication. The source separates task control from the worker runtime.

## Engineering detail

- Project-scoped permission checks and task rule gates
- Scheduled task dispatch and worker claim/report APIs
- Approval and review records for controlled actions
- A separately paired worker design with bounded execution and result artifacts

## Technologies

Laravel, PHP, SQL, APIs and Python worker tooling.

## Status

The project handover records a live application. An always-on worker and completed autonomous production tasks are not claimed.

