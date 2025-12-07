# CTF WriteUps Website

A modern, responsive website for sharing Capture The Flag (CTF) challenge writeups with beautiful dark/light mode support.

## Features

✨ **Responsive Design** - Works seamlessly on desktop, tablet, and mobile devices  
🌓 **Dark/Light Mode** - Toggle between themes with persistent storage  
📱 **Mobile Optimized** - Touch-friendly buttons and layouts  
♿ **Accessible** - Semantic HTML5 and ARIA labels  
⚡ **Fast Loading** - Lightweight CSS and optimized assets  
🎨 **Modern UI** - Smooth animations and professional styling  

## Project Structure

```
write-up/
├── main.html                 # Homepage with CTF challenges list
├── Content/
│   ├── main.css             # Main website styles
│   ├── universalmd.css      # Markdown content styles
│   └── Wannagames/
│       ├── wannagames.html  # Challenge writeup page
│       ├── wannagames.md    # Challenge content (markdown)
│       └── wannagames.png   # Challenge image
├── Asset/                   # Images and assets
└── README.md               # This file
```

## How to Use

### On PC
1. Open `main.html` in your web browser
2. Browse CTF challenges in the card grid
3. Click "Read WriteUp" to view challenge details
4. Use the theme toggle (top-right) to switch between light and dark modes
5. Use the back arrow to return to main page

### On Mobile
1. Open `main.html` on your mobile device
2. Cards automatically stack vertically for better readability
3. Tap challenge cards to view details
4. Theme toggle works smoothly on touch devices
5. All buttons are large and easy to tap

## Responsive Breakpoints

- **Desktop** (>768px) - Full grid layout with 3 columns
- **Tablet** (481-768px) - 2-column grid layout
- **Mobile** (<480px) - Single column layout, optimized font sizes

## Color Scheme

**Light Mode:**
- Background: #F4F4F4
- Text: #222831
- Accents: #e8e8e8

**Dark Mode:**
- Background: #222831
- Text: #f0f0f0
- Accents: #2d3139

## Browser Support

- Chrome/Edge 88+
- Firefox 85+
- Safari 14+
- Mobile browsers (iOS Safari, Chrome Mobile, Firefox Mobile)

## Features Breakdown

### Dark/Light Mode
- Automatically detects system preference
- Manual toggle saves preference to localStorage
- Smooth transitions between themes

### Responsive Components
- Flexible grid layout using CSS Grid
- Mobile-first approach
- Touch-friendly interface

### Accessibility
- Semantic HTML5 elements
- ARIA labels for interactive elements
- Keyboard navigation support
- High contrast colors for readability

## Mobile Optimization Tips

- Viewport meta tag included for proper scaling
- Font sizes scale appropriately for mobile
- Touch targets are 50px minimum (guideline)
- Minimal horizontal scrolling
- Optimized images for faster loading

## Adding New Writeups

1. Create a new folder in `Content/` (e.g., `Content/ChallengeeName/`)
2. Create two files:
   - `challengename.html` - Copy structure from `wannagames.html`
   - `challengename.md` - Write your markdown content
3. Add a new card to `main.html`:
   ```html
   <article class="writeup-card">
       <div class="card-image">
           <img src="/Asset/path/to/image.png" alt="Challenge Name">
       </div>
       <div class="card-content">
           <h2>Challenge Name</h2>
           <p>Brief description</p>
           <a href="Content/ChallengeName/challengename.html" class="btn-read-more">Read WriteUp</a>
       </div>
   </article>
   ```

## Development

All styling uses CSS custom properties (variables) for easy theme customization. Modify the color values in the `html[data-theme]` blocks to change the entire color scheme.

## Author Notes

This website is built with modern web standards and focuses on:
- User experience across all devices
- Accessibility and inclusivity
- Performance and fast loading
- Clean, maintainable code

---

**Last Updated:** December 8, 2025  
Happy Hacking! 🚀
