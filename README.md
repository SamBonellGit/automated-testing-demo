# GitHub Actions – Automated Testing Demo (TypeScript)

## What this repo is
This repository is a **minimal, practical demo of GitHub Actions CI** using **Node.js + TypeScript**.

It demonstrates:
- Automated linting and testing on every **push** and **pull request**
- A **protected `main` branch** that cannot be merged unless CI passes
- How failing tests **block merges**, and fixing them **unblocks merges**

This mirrors how real teams gate production code with CI.

---

## What the CI does (TL;DR)
On every push or PR to `main`, GitHub Actions will:
1. Install dependencies
2. Run ESLint
3. Run tests (Vitest)
4. Generate coverage
5. Fail the PR if anything breaks

---

## How to perform the demo (TL;DR steps)

### 1) Create a branch
```bash
git checkout -b demo/fail-ci
````
2) Break a test on purpose

Edit:
````
test/sum.test.ts
````

Change:
````
expect(sum(2, 3)).toBe(5)
````

To:
````
expect(sum(2, 3)).toBe(6)
````

Commit and push:
````
git add .
git commit -m "Break test to demonstrate CI gate"
git push -u origin demo/fail-ci
````

3) Open a Pull Request

Base branch: main

Compare branch: demo/fail-ci

Result:

GitHub Actions runs automatically

❌ Required check fails

🚫 Merge is blocked

4) Fix the test

Change it back:
````
expect(sum(2, 3)).toBe(5)
````

Commit and push again:
````
git add .
git commit -m "Fix test"
git push
````

Result:

CI reruns automatically

✅ Required check passes

✅ Merge button becomes available