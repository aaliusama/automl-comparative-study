# GitHub Setup Instructions

## Step 1: Create a New Repository on GitHub

1. Go to [github.com](https://github.com) and sign in to your account
2. Click the **"+"** icon in the top-right corner
3. Select **"New repository"**
4. Fill in the repository details:
   - **Repository name**: `automl-comparative-study` (or your preferred name)
   - **Description**: "Comprehensive benchmarking study comparing Simulated Annealing vs FLAML vs TPOT AutoML frameworks"
   - **Visibility**: Select **"Public"**
   - **Initialize repository**: Leave unchecked (we already have files locally)
5. Click **"Create repository"**

## Step 2: Push Local Repository to GitHub

After creating the repository, GitHub will show you commands. Follow these steps:

### Option A: Using HTTPS (Recommended for most users)

```bash
# Navigate to the submission folder
cd "/sessions/gracious-practical-brahmagupta/mnt/Project 1/submission"

# Add the remote repository (replace USERNAME and REPO_NAME)
git remote add origin https://github.com/USERNAME/automl-comparative-study.git

# Rename branch to main (optional but recommended)
git branch -m master main

# Push to GitHub
git push -u origin main
```

### Option B: Using SSH (If you have SSH keys configured)

```bash
# Navigate to the submission folder
cd "/sessions/gracious-practical-brahmagupta/mnt/Project 1/submission"

# Add the remote repository
git remote add origin git@github.com:USERNAME/automl-comparative-study.git

# Rename branch to main
git branch -m master main

# Push to GitHub
git push -u origin main
```

## Step 3: Verify Public Visibility

1. Go to your repository on GitHub
2. Click on **"Settings"** (top-right menu)
3. Scroll to **"Danger Zone"** section
4. Verify that **"This repository is public"** is displayed
5. If it's private, click **"Make public"** button

## Step 4: Add Repository Link to LinkedIn Post

1. Copy your repository URL from GitHub (e.g., `https://github.com/USERNAME/automl-comparative-study`)
2. Replace `[Insert GitHub URL]` in the `LINKEDIN_POST.txt` file with your actual repository URL
3. Copy the updated post and paste it on LinkedIn

## Step 5: Create .gitattributes (Optional)

To handle large binary files better, create a `.gitattributes` file:

```bash
# Add to your repository
*.pptx binary
*.ipynb binary
```

## Helpful Commands

```bash
# Check your git configuration
git config --list

# View remote repository
git remote -v

# Check repository status
git status

# View commit history
git log --oneline

# Make an additional commit with changes
git add .
git commit -m "Your commit message"
git push origin main
```

## Troubleshooting

### Authentication Issues
- For HTTPS: Use Personal Access Token (generate at Settings → Developer settings → Personal access tokens)
- For SSH: Ensure SSH keys are added to GitHub (Settings → SSH and GPG keys)

### Large File Warnings
- The `.gitignore` excludes `.csv` files by default
- If you want to include data files, use Git LFS (Large File Storage)

### Push Rejected
- If you get "rejected" error, pull first: `git pull origin main`
- Resolve any conflicts and push again: `git push origin main`

---

**Your repository is now ready for the world to see! 🚀**
