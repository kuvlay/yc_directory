# YC Directory · Startup Discovery

A startup-directory application with searchable listings, detail pages, author profiles, and a pitch-submission flow backed by Sanity CMS. It is based on a JavaScript Mastery tutorial and retains the tutorial source alongside the adapted application.

**Next.js · TypeScript · Sanity · NextAuth · Tailwind CSS · Sentry**

[Existing demo](https://yc-directory-opal-beta.vercel.app/) · [Portfolio](https://github.com/kuvlay) · [Tutorial credits](yc_directory-main/README.md)

## Application features in the source

- Startup listing queries with title, category, and author search.
- Startup detail pages with Markdown pitch content.
- Author profiles and their associated startups.
- GitHub sign-in through NextAuth.
- Authenticated pitch submission through a server action.
- Sanity Studio at `/studio` and Sentry integration configuration.

## Repository layout

| Location | Responsibility |
| --- | --- |
| `app/`, `components/`, `lib/` | Main application routes, UI, and server actions |
| `sanity/` | CMS schema, queries, and read/write clients |
| `auth.ts` | GitHub authentication callbacks |
| `yc_directory-main/` | Preserved tutorial/reference source, excluded from the root TypeScript build |

Run commands from the repository root. The root manifest currently specifies Next.js 16 and React 18; the nested tutorial copy uses different historical versions.

## Local setup

Requirements: Node.js/npm compatible with the locked Next.js dependencies, a Sanity project/dataset, and your own GitHub OAuth application for sign-in.

```bash
git clone https://github.com/kuvlay/yc_directory.git
cd yc_directory
npm ci
```

Create `.env.local` with your own settings:

```dotenv
NEXT_PUBLIC_SANITY_PROJECT_ID=YOUR_PROJECT_ID
NEXT_PUBLIC_SANITY_DATASET=production
NEXT_PUBLIC_SANITY_API_VERSION=2025-04-03
SANITY_API_TOKEN=YOUR_SERVER_SIDE_TOKEN
AUTH_SECRET=YOUR_AUTH_SECRET
AUTH_GITHUB_ID=YOUR_GITHUB_CLIENT_ID
AUTH_GITHUB_SECRET=YOUR_GITHUB_CLIENT_SECRET
```

The root write client reads `SANITY_API_TOKEN`. Keep this token server-side and configure the OAuth callback for your actual deployment. Configure the included Sentry integration for your own account before enabling monitoring/source-map uploads.

```bash
npm run dev
```

Open the address printed by Next.js. `npm run typegen` extracts the Sanity schema and generates types. `npm run build` and `npm start` are the production-build/start commands.

## Status and compatibility

The existing demo returned a successful HTTP response during review. Sign-in, pitch creation, and a fresh local build were not exercised. Dependency compatibility still needs validation: the root manifest uses React 18 while the form imports `useActionState`, and the inherited lint script uses `next lint`. These are setup concerns to resolve before claiming a clean current build.

<details>
<summary>Credits and project history</summary>

The preserved reference directory explicitly credits the [JavaScript Mastery tutorial](https://www.youtube.com/@javascriptmastery/videos). Source lineage: [aarish-io/yc_directory](https://github.com/aarish-io/yc_directory). Original tutorial attribution and contributor history are retained; this project is not presented as an entirely original design or sole-origin implementation. No standalone license was present in the reviewed source.

</details>
