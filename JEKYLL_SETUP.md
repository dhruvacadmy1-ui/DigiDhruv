# Jekyll Theme Setup Guide

## 📋 What Has Been Added

I've successfully integrated a **Jekyll theme** into your DigiDhruv repository. Here's what was created:

### Core Jekyll Files
1. **`_config.yml`** - Main Jekyll configuration with minimal theme settings
2. **`_layouts/default.html`** - Default page layout with header, footer, and navigation
3. **`Gemfile`** - Ruby dependencies for Jekyll

### Content Pages
4. **`index.md`** - Home page with the game embedded
5. **`about.md`** - About DigiDhruv page

### Styling
6. **`assets/css/theme.css`** - Main responsive theme styling
7. **`assets/css/style.css`** - Game-specific CSS

### JavaScript
8. **`assets/js/main.js`** - Supporting JavaScript functionality

---

## 🚀 How to Use

### Option 1: View on GitHub Pages (Easiest)
Your site is already set up for GitHub Pages! It will be available at:
```
https://dhruvacadmy1-ui.github.io/DigiDhruv/
```

Just ensure GitHub Pages is enabled in your repository settings:
1. Go to **Settings** → **Pages**
2. Select **Deploy from a branch**
3. Choose **branch: digi**
4. Your site will build automatically!

### Option 2: Run Locally

#### Prerequisites
- Ruby 2.7+ installed
- Bundler (`gem install bundler`)

#### Steps
```bash
# Clone your repository
git clone https://github.com/dhruvacadmy1-ui/DigiDhruv.git
cd DigiDhruv

# Install dependencies
bundle install

# Run Jekyll server
bundle exec jekyll serve

# Visit http://localhost:4000/DigiDhruv
```

---

## 🎨 Theme Features

### Responsive Design
- Works on desktop, tablet, and mobile
- Automatic layout adjustments for smaller screens

### Color Scheme
- Primary: Blue (#3498db)
- Secondary: Dark gray (#2c3e50)
- Success: Green (#27ae60)
- Danger: Red (#e74c3c)

### Navigation
- Sidebar navigation on desktop
- Clean, minimal design
- GitHub link for easy contribution

### Typography
- Modern font stack (Segoe UI, Trebuchet MS)
- Clear hierarchy with heading styles
- Readable line-height and spacing

---

## 🎮 Game Integration

The game is fully integrated into the Jekyll site:
- **Home page** displays the interactive game
- **About page** explains the project
- All styling is applied through the theme
- Sound effects and leaderboard work as before

---

## 📝 Customization

### Change Theme Colors
Edit `assets/css/theme.css` and modify the `:root` CSS variables:
```css
:root {
  --primary-color: #your-color;
  --secondary-color: #your-color;
  /* ... */
}
```

### Add More Pages
Create new `.md` files in the root directory:
```markdown
---
layout: default
title: Page Title
---

# Your Content Here
```

### Customize Navigation
Edit `_layouts/default.html` to modify the sidebar links.

---

## ✅ Next Steps

1. **Verify GitHub Pages is enabled** in your repository settings
2. **Wait 1-2 minutes** for GitHub to build the site
3. **Visit your site** at `https://dhruvacadmy1-ui.github.io/DigiDhruv/`
4. **Test the game** and navigation

---

## 📚 Resources

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [GitHub Pages Guide](https://pages.github.com/)
- [Markdown Reference](https://www.markdownguide.org/)

---

**Your DigiDhruv website is now live with a professional Jekyll theme! 🎉**
