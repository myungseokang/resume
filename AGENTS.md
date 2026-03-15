# AGENTS.md - Resume Website Development Guide

This document provides guidelines for AI coding agents working on this static resume website.

---

## Project Overview

**Type**: Static HTML/CSS personal resume website  
**Tech Stack**: HTML5, CSS3, JavaScript (jQuery), Bootstrap 4  
**Language**: Korean content with English technical terms  
**Deployment**: Static hosting (GitHub Pages compatible)

This is a simple, single-page resume website with no build system, no tests, and no package managers. All dependencies are loaded via CDN.

---

## File Structure

```
resume/
├── index.html          # Main resume page (single-page application)
├── main.css            # Custom styles
├── favicon.ico         # Site favicon
├── CNAME              # Custom domain configuration
├── README.md          # Repository description
├── assets/
│   └── images/        # Profile image and other assets
└── .git/              # Git repository
```

---

## Development Commands

### Preview the Site

**No build system required.** Choose one of these methods:

```bash
# Option 1: Simple HTTP server with Python
python -m http.server 8000
# Then visit: http://localhost:8000

# Option 2: Simple HTTP server with Python 3
python3 -m http.server 8000

# Option 3: Use any static file server (Node.js, etc.)
npx serve .

# Option 4: Open directly in browser (some features may not work)
open index.html
```

### Version Control

```bash
# View changes
git status
git diff

# Commit changes
git add .
git commit -m "Update resume content"

# Deploy (if using GitHub Pages)
git push origin master
```

**No linting, testing, or build commands** - this is pure static HTML/CSS.

---

## Code Style Guidelines

### HTML Conventions

1. **Structure**
   - Use semantic HTML5 elements where appropriate
   - Follow Bootstrap 4 grid system: `.container > .row > .col-*`
   - Keep consistent indentation (2 spaces)

2. **Bootstrap Classes**
   - Use responsive classes: `col-12 col-md-9` (mobile-first)
   - Spacing utilities: `pt-5`, `pb-3`, `mt-5`, etc.
   - Text utilities: `text-center`, `text-md-right`, etc.
   - Color utilities: use custom `.blue` and `.gray` classes

3. **Sections Pattern**
   ```html
   <!-- Section Start -->
   <div class="row pt-5">
     <div class="col">
       <div class="row pb-3">
         <div class="col">
           <h2 class="blue">SECTION TITLE</h2>
         </div>
       </div>
       <!-- Section content -->
     </div>
   </div>
   <!-- Section End -->
   ```

4. **Responsive Layout Pattern**
   ```html
   <div class="row">
     <div class="col-md-3 col-12 text-md-right">
       <!-- Left column (dates, labels) -->
     </div>
     <div class="col-md-9 col-12">
       <!-- Right column (main content) -->
     </div>
   </div>
   ```

5. **Icons**
   - Use Font Awesome 4.7.0 classes: `<i class="fa fa-envelope" aria-hidden="true"></i>`
   - Always include `aria-hidden="true"` for decorative icons

6. **Links**
   - External links: use `target="_blank"` attribute
   - Email links: use `mailto:` protocol

### CSS Conventions

1. **File Organization** (`main.css`)
   - Global styles first (`.resume` base styles)
   - Utility classes next (`.blue`, `.gray`)
   - Component-specific styles last

2. **Naming**
   - Use semantic class names: `.profile-img`, `.footer-cover`
   - Use hyphen-case for multi-word classes
   - Prefer single classes over complex selectors

3. **Typography**
   - Font family: 'Noto Sans KR' (loaded from Google Fonts)
   - Base font-weight: 300
   - Line height: 1.8 for readability
   - Word breaking: `word-break: keep-all` for Korean text

4. **Colors**
   - Primary blue: `#3c78d8` (`.blue` class)
   - Secondary gray: `gray` (`.gray` class)
   - Footer background: `#f5f5f5`

5. **Responsive Considerations**
   - Rely on Bootstrap's responsive utilities
   - Keep custom CSS minimal and mobile-friendly

### JavaScript Conventions

1. **jQuery Usage**
   - jQuery 3.2.1 is loaded via CDN
   - Use `$(function() { ... })` or `$(document).ready()` for DOM-ready code
   - Selector pattern: `$('#id')` for IDs, `$('.class')` for classes

2. **Code Organization**
   - Bootstrap initialization in `<head>`: tooltip activation
   - Main logic in `<script>` before `</body>` closing tag
   - Keep JavaScript minimal - this is primarily a static site

3. **Dynamic Content**
   - Career duration calculation: automatically updates based on start date
   - Use `new Date('YYYY-MM-DD')` format for date calculations
   - Update DOM with `.text()` method

4. **Console Easter Egg**
   - ASCII art banner in console - preserve this feature
   - Use template literals or multi-line strings

5. **Variable Naming**
   - Use camelCase: `careerStartDate`, `careerGap`
   - Descriptive names: prefer `careerText` over `ct`

### Content Conventions

1. **Language**
   - Primary language: Korean (한국어)
   - Section headers: English uppercase (INTRODUCE, EXPERIENCE, etc.)
   - Technical terms: English (Product Owner, Software Engineer, etc.)

2. **Date Format**
   - Display format: `YYYY. MM ~ YYYY. MM` (e.g., "2022. 05 ~ NOW")
   - ISO format in code: `YYYY-MM-DD`

3. **Sections Order** (maintain this order)
   1. Profile (name, photo, contact info)
   2. INTRODUCE
   3. EXPERIENCE
   4. EDUCATION
   5. COMMUNITY
   6. ETC
   7. Contact buttons
   8. Footer

---

## External Dependencies (CDN)

All dependencies are loaded via CDN - **do not add npm/package.json**:

```html
<!-- jQuery 3.2.1 -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>

<!-- Bootstrap 4.0.0-beta.2 -->
<link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css" rel="stylesheet">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/js/bootstrap.bundle.min.js"></script>

<!-- Font Awesome 4.7.0 -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">

<!-- Noto Sans KR (Google Fonts) -->
<link rel="stylesheet" href="https://fonts.googleapis.com/earlyaccess/notosanskr.css">
```

---

## Editing Guidelines

### Adding a New Experience Entry

1. Copy an existing experience `<div class="row">` block
2. Update the date column with new dates
3. Update the content column with new company/role info
4. Maintain the nested `<ul>` structure for details
5. Keep the `<b>` tag for sub-sections

### Updating Career Duration

The career duration badge updates automatically. To change the start date:
```javascript
var careerStartDate = new Date('2022-05-01'), // Change this date
```

### Adding New Sections

Follow the section pattern:
```html
<!-- NewSection Start -->
<div class="row pt-5">
  <div class="col">
    <div class="row pb-3">
      <div class="col">
        <h2 class="blue">NEW SECTION</h2>
      </div>
    </div>
    <!-- Content here -->
  </div>
</div>
<!-- NewSection End -->
```

### Modifying Styles

1. Check if Bootstrap utility classes can solve your need first
2. If custom CSS needed, add to `main.css`
3. Keep selectors simple and specific
4. Test responsive behavior on mobile (use browser DevTools)

---

## Testing Checklist

Since there are no automated tests, manually verify:

- [ ] **Responsive Design**: Test on mobile (320px), tablet (768px), desktop (1200px+)
- [ ] **Links**: All `mailto:` and external links work
- [ ] **Images**: Profile image loads correctly
- [ ] **JavaScript**: Career duration calculates correctly
- [ ] **Console**: ASCII art displays in browser console
- [ ] **Bootstrap Components**: Tooltips activate on hover (if used)
- [ ] **Typography**: Korean text breaks correctly (`word-break: keep-all`)
- [ ] **Cross-browser**: Test in Chrome, Firefox, Safari

---

## Common Tasks

### Update Profile Information
Edit the profile section in `index.html` (lines 42-97)

### Update Experience
Edit the experience section (lines 115-212)

### Change Color Scheme
Modify color variables in `main.css`:
```css
.blue { color: #3c78d8; }  /* Primary color */
.gray { color: gray; }     /* Secondary color */
```

### Add Social Links
Follow the pattern in profile section:
```html
<div class="row pb-2">
  <div class="col-1 text-right">
    <i class="fa fa-icon-name" aria-hidden="true"></i>
  </div>
  <div class="col-auto">
    <b><a href="URL" target="_blank">Link Text</a></b>
  </div>
</div>
```

---

## Important Notes

1. **No Build Process**: This is intentional. Keep it simple.
2. **No Package Manager**: All dependencies are CDN-based.
3. **No Testing Framework**: Manual testing is sufficient for this static site.
4. **Single Page**: All content is in `index.html` - do not split into multiple HTML files.
5. **Korean Language**: Maintain consistent Korean language for content, English for technical terms.
6. **Commented Sections**: Some sections are commented out (e.g., PROJECTS) - they can be uncommented if needed.

---

## Deployment

This site is designed for GitHub Pages:

1. Push changes to `master` branch
2. GitHub Pages automatically serves `index.html`
3. Custom domain configured via `CNAME` file

No build or deployment scripts needed.

---

## Additional Resources

- [Bootstrap 4 Documentation](https://getbootstrap.com/docs/4.0/getting-started/introduction/)
- [Font Awesome 4.7 Icons](https://fontawesome.com/v4.7.0/icons/)
- [jQuery API Documentation](https://api.jquery.com/)
