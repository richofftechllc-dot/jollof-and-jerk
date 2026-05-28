# Jollof & Jerk — Deploy Instructions

## Option A: Vercel CLI (run from your Mac)
```bash
# 1. Copy project to your machine
# (files are in the zip below)

# 2. Install Vercel CLI if needed
npm i -g vercel

# 3. Deploy to Rich Off Tech team
cd jnj-site
vercel --team team_nt4pW0uOQZNNe7TR9CF7PLwl --name jollof-and-jerk

# 4. On first deploy, link to team account
# When prompted: select "Rich Off Tech" team
# Project name: jollof-and-jerk
```

## Option B: Vercel Dashboard (drag & drop)
1. Go to vercel.com/richofftech
2. "Add New Project"
3. Drag the entire `jnj-site/` folder
4. Name: jollof-and-jerk
5. Deploy

## Option C: GitHub → Vercel (recommended for auto-deploy)
```bash
# Push to GitHub
git remote add origin https://github.com/richofftech/jollof-and-jerk.git
git push -u origin main

# Then connect in Vercel dashboard:
# vercel.com/new → Import from GitHub → jollof-and-jerk
```

## File Structure
```
jnj-site/
├── index.html              (full site, 988 lines)
├── vercel.json             (deploy config)
├── .gitignore
└── assets/
    ├── food/               (5 cropped food photos, 800x800)
    │   ├── jerk-chicken-tray.jpg
    │   ├── jerk-jollof-plate.jpg
    │   ├── jerk-plate-full.jpg
    │   ├── oxtail-closeup.jpg
    │   └── smoke-oxtail.jpg
    └── media/              (GIFs + frame from ABC7)
        ├── leslys-food-closeup-clip-web.gif
        ├── leslys-group-shot-clip-web.gif
        ├── leslys-sport-bar-grill-frame-end.jpg
        └── leslys-sport-bar-grill-video-clip.gif
```

## Still Needed from Mamadou
- [ ] Custom domain (jollofandjerk.com or similar)
- [ ] Uber Eats store_id (to wire live ordering)
- [ ] Google Business Profile access
- [ ] Phone number for the one-text system
