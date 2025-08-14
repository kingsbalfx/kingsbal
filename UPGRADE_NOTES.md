# Upgrade notes & deployment checklist

1. **Node version**: This project targets Node >= 18.16.0 (see package.json `engines`). Use that on your local machine and CI.
2. **Environment variables**: Copy `.env.example` to `.env.local` and set values. You can run `npm run check-env` to validate env variables locally (script added).
3. **Persistent storage**: The app currently stores subscribers and VIP users in `data/*.json`. Serverless platforms like Vercel have ephemeral filesystems — data will not persist across deployments. Migrate to a database for production:
   - Recommended: Supabase, MongoDB Atlas, PlanetScale, or any hosted SQL/NoSQL DB.
   - Replace `fs` usage in `pages/api/*.js` with DB calls (examples included below if desired).
4. **Vercel deployment**: The `vercel.json` file is included. Set environment variables in Vercel Project Settings. Vercel will run `npm run build` automatically.
5. **Security**: Never commit `.env.local` or real API keys to the repo.
6. **Next steps I can do** (pick any and I'll apply):
   - Replace file-based storage with Supabase/MongoDB integration.
   - Add GitHub Actions for CI (install + build + check-env).
   - Add server-side validation for Paystack webhook flows.