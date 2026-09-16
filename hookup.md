# Connecting Other Repositories

The portfolio can showcase other GitHub repositories without copying their
source code into this project. Choose the option that matches how much of each
repository the site needs.

## 1. GitHub API at runtime

**Best for:** repository cards, stars, languages, descriptions, and links that
should stay current.

1. Create a GitHub personal access token only if private repositories or higher
   API limits are needed; never commit the token.
2. Call the REST API endpoint
   `https://api.github.com/users/<username>/repos` from a server or a public
   endpoint for public repositories.
3. Store the response in a `useRepositories` hook and map it to a local
   `Repository` type.
4. Add loading, error, and rate-limit states.
5. Cache responses where possible so the portfolio remains fast and resilient.

For a public-only portfolio, client-side requests can work, but a small server
or serverless function is safer when credentials are required.

## 2. GitHub GraphQL API

**Best for:** selecting exactly the fields needed for a richer portfolio.

1. Create a GraphQL query for repositories, topics, languages, and releases.
2. Send it from a server-side route or serverless function.
3. Keep the token in an environment variable such as `GITHUB_TOKEN`.
4. Return a small, stable JSON shape for the React app.

This reduces over-fetching compared with REST, but requires more setup and
careful handling of API schema changes.

## 3. npm packages

**Best for:** repositories that already expose reusable components, utilities,
or a published SDK.

1. Publish the reusable repository as a scoped package, for example
   `@your-name/project-ui`.
2. Add it to this app with `npm install @your-name/project-ui`.
3. Import its public API in `src/components` or `src/data`.
4. Pin a compatible version and update it intentionally.

This shares compiled functionality, not the repository's complete source
history. It is a good fit when the portfolio needs to demonstrate or embed a
library.

## 4. Git submodules

**Best for:** keeping a checkout of a related repository available locally
without merging its history into this repository.

```bash
git submodule add https://github.com/<username>/<repository>.git external/<repository>
git submodule update --init --recursive
```

1. Add the repository under an `external/` directory.
2. Reference its built assets or documentation from the portfolio as needed.
3. Commit the submodule pointer, not a copied working tree.
4. Update it deliberately with `git submodule update --remote`.

Submodules add clone and deployment complexity, so they are usually better for
development references than for data shown to visitors.

## 5. Git subtree

**Best for:** vendoring a snapshot while retaining a relationship to the
upstream repository.

```bash
git subtree add --prefix=external/<repository> \
  https://github.com/<username>/<repository>.git main --squash
```

Unlike a submodule, a subtree is checked into this repository and deploys
easily, but it does contain a copy of the files. Use it only when a deployment
needs the external project locally.

## Suggested starting point

Start with the GitHub REST API for project cards and links. Add a small
server-side proxy when authentication or caching becomes necessary. Use npm
packages only for code you genuinely want to reuse; use submodules or subtrees
when the build must access repository files directly.
