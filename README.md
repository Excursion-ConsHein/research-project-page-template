# Research Project Showcase Page Tutorial

This tutorial will guide you through creating a professional research project showcase page with modular design, easy to maintain and extend.

**Disclaimer: This project template is intended for research and educational purposes only and does not involve any commercial use.**

**The content referenced in this project is from the latest research presentation by Carnegie Mellon University AirLab at IROS 2025, with author and institution information virtually replaced.**

**This project does not target its research content but serves as a tutorial case for the page, not representing the position or viewpoint of any research institution.**

**If you are interested in this research project, feel free to visit the project homepage: [pipe-planner.github.io](https://pipe-planner.github.io)**

## Project Overview

This research project showcase page template is developed using pure HTML/CSS/JavaScript with the following features:
- **Modular Design**: Each functional module is developed independently for easy maintenance
- **Responsive Layout**: Supports adaptive design for desktop and mobile devices
- **Configuration-Driven**: Manages content through JSON configuration files without modifying code
- **Modern UI**: Clean and beautiful interface design

## Project Structure

```
research-project-template/
├── configs/              # Configuration files directory
│   ├── signboard.json    # Top signboard configuration
│   ├── info.json         # Project basic information configuration
│   └── main.json         # Main content configuration
├── images/               # Image resources directory
│   ├── signboard/        # Signboard images
│   ├── main/            # Main content images
│   └── video/           # Video files
├── src/                  # Source code directory
│   ├── signboard.js     # Top signboard module
│   ├── info-button.js   # Info button module
│   ├── authors.js       # Author information module
│   ├── info.js          # Project information module
│   ├── main.js          # Main content module
│   ├── mobile.js        # Mobile adaptation module
│   └── copyright.js     # Footer copyright module
└── index.html           # Main page file
```

## Quick Start

### 1. Environment Setup

You only need a modern web browser and a local web server. You can start a local server using the following methods:

```bash
# Using Python built-in server
python -m http.server 8000

# Or using Node.js http-server
npx http-server -p 8000
```

### 2. Basic Configuration

#### 2.1 Top Signboard Configuration

Edit the `configs/signboard.json` file:

```json
{
    "lab": {
        "logoSrc": "Lab logo path",
        "url": "Lab website URL"
    },
    "college": {
        "logoSrc": "College logo path",
        "url": "College website URL"
    }
}
```

#### 2.2 Project Information Configuration

Edit the `configs/info.json` file:

```json
{
    "top-title": "Your Project Title",
    "conference": "Conference Name and Year",
    "institution": {
        "1": "Institution 1",
        "2": "Institution 2",
        // You can add more institutions
    },
    "authors": {
        "Author Name": {
            "homepage": "Author homepage",
            "affiliation": "1",    // Corresponds to the key in institution above
            "equal_or_not": true   // If no equal contribution, delete this line, Equal Contributions will not be displayed in the page
        }
    },
    "info-button": {
        // Note: If any of the following information is not available, delete the corresponding line, and the corresponding button will be hidden
        "arxiv": "Paper arXiv link",
        "code": "Project code repository link",
        "video": "Project video link",
        "demo": "Project demo link",
        "related_research":{
            "Related Research 1": "Related Research 1 link",
            "Related Research 2": "Related Research 2 link",
            // You can add more related research
        }
    }
}
```

#### 2.3 Main Content Configuration

Edit the `configs/main.json` file.

This document supports stacking and splicing of multiple content modules, so you can fully unleash your creativity to combine a showcase page that meets your project needs.

Each object in the JSON corresponds to a module, and the module type is determined by the key in the object. Braces correspond to a container, and containers are displayed alternately with white/light gray colors. Each container can contain multiple modules.

This template strictly follows the order in the JSON for display, truly achieving what you see is what you get.

Each module's configuration items have their specific meanings. Here are the detailed configuration items for each supported module:

- Video module, including video file path (videoSrc, videoLink, etc.), video description (description)
- Image-text module, including image path (image), title (title), content description (content)
- BibTeX citation module, including citation content (bibtex)
- Button interaction module, triggered by button, including button name (button_name), and all other module configuration items mentioned above

Note: If there are multiple modules of the same type, you can distinguish them by {module}_{number} to prevent conflicts.
Currently supported multi-module types are: description, image, title, content, button

Here is a simple example.

```json
[
    {
        "videoSrc": "Video path/link, supports local videos and online videos, with width 1000px",
        "description": "Project brief description, width follows the videoSrc above",
        "title": "Abstract",
        "content": "Project detailed content..."
    },
    {
        "videoLink": "Video path/link, supports local videos and online videos, with width 800px",
        "description": "Project brief description, width follows the videoLink above",
    },
    {
        "title": "Module Title",
        "image": "Image path, supports local images, with width 800px",
        "content": "Module content description..."
    },
    // Different modules can be stacked in different ways, there is no requirement for who must be above or below, stack according to your arrangement
    // For example, I want to make an image-text module, first write the title, then display the image-text, then follow the title, and the next image-text module...
    {
        "title_1": "Module Title 1",
        "image_1": "Image Path 1",
        "content_1": "Module Content 1",
        "title_2": "Module Title 2",
        "image_2": "Image Path 2",
        "content_2": "Module Content 2",
    },

    // Finally is the button module, different from others, buttons can only be placed below the title (if there is no title, place it at the top), this is to prevent button stacking chaos
    {
        "title": "Results Display",
        "button_1": {
            "button_name": "Button Name",
            "image": "Image path, supports local images, with width 800px"
        },
        "button_2": {
            "button_name": "Button Name",
            "content": "Content"
        },
        "button_3": {
            "button_name": "Button Name",
            "image": "Image",
            "content": "Content"
        },
    }
    // As for whether buttons can be nested?
    // Sorry, the author hasn't figured it out, but I think this is just a showcase page, no need to be so complicated

    // Finally is the citation module, it is recommended to place the citation module at the end, because the height of the citation module is fixed and cannot adapt to content height
    {
        "bibtex": "@article{example,
            title={Example Article},
            author={Author, A. and Another, B.},
            journal={Example Journal},
            year={2023},
            volume={1},
            number={1},
            pages={1-10}
        }"
    }

]
```

### 3. Module Details

#### 3.1 Top Signboard Module (signboard.js)

- **Function**: Display lab and institution logos
- **Features**: Fixed at the top of the page, responsive design
- **Configuration**: Configure logo images and links through `signboard.json`

#### 3.2 Info Button Module (info-button.js)

- **Function**: Display paper-related link buttons
- **Supported Button Types**: arXiv, code repository, video, demo, etc.
- **Style**: Unified button style with hover effects

#### 3.3 Author Information Module (authors.js)

- **Function**: Display project author information
- **Features**: Supports author homepage links, institution identification, equal contribution marking
- **Layout**: Responsive grid layout

#### 3.4 Project Information Module (info.js)

- **Function**: Display project title, conference information, etc.
- **Features**: Large title display, supports subtitle
- **Style**: Modern font and color design

#### 3.5 Main Content Module (main.js)

- **Function**: Display the main content of the project
- **Supported Content Types**:
  - Video module
  - Image-text module
  - Button interaction module
  - BibTeX citation module
- **Layout**: Modular stacking, adaptive width

#### 3.6 Mobile Adaptation Module (mobile.js)

- **Function**: Provide responsive adaptation for mobile devices
- **Adaptation Content**:
  - Vertical stacking of signboard
  - Font size adjustment
  - Container height adaptation
  - Touch-friendly interaction

#### 3.7 Footer Copyright Module (copyright.js)

- **Function**: Display footer copyright information
- **Features**: Supports custom links and styles
- **Content**: Copyright statement and project links

### 4. Custom Styles

#### 4.1 Font Configuration

Google Fonts can be configured in `index.html`:

```html
<link href="https://fonts.googleapis.com/css2?family=Google+Sans&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;500;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Poppins" rel="stylesheet">
```

#### 4.2 Color Theme

Each module has independent CSS styles. You can customize the color theme by modifying the style strings in the corresponding JavaScript files.

#### 4.3 Responsive Breakpoints

Mobile adaptation uses the following breakpoints:
- **Below 768px**: Tablet and mobile devices
- **Below 480px**: Small screen mobile devices

### 5. Deployment Guide

#### 5.1 Static Deployment

1. Upload all files to a web server
2. Ensure image paths are correct
3. Configure correct MIME types

#### 5.2 GitHub Pages Deployment

1. Create a GitHub repository
2. Upload project files
3. Enable GitHub Pages in repository settings
4. Select the main branch as the publishing source

#### 5.3 Custom Domain

If you need to use a custom domain, you can create a `CNAME` file in the project root directory with your domain name as the content.

### 6. Best Practices

#### 6.1 Image Optimization

- Use WebP format to reduce file size
- Compress images to improve loading speed
- Provide different resolution images for different devices

#### 6.2 Performance Optimization

- Compress JavaScript and CSS files
- Use CDN to accelerate fonts and static resources
- Enable browser caching

#### 6.3 Content Organization

- Keep the structure of configuration files clear
- Use meaningful file naming
- Regularly backup important files

### 7. Troubleshooting

#### 7.1 Common Issues

**Q: Page styles are not displaying**
A: Check if CSS styles are loading correctly, ensure JavaScript file paths are correct

**Q: Images cannot be displayed**
A: Check if image paths are correct, ensure image files exist

**Q: Mobile display is abnormal**
A: Check viewport settings, ensure mobile adaptation module is loading correctly

#### 7.2 Debugging Tips

- Use browser developer tools to inspect elements
- View console error messages
- Load modules step by step for testing

### 8. Extended Features

#### 8.1 Adding New Modules

1. Create a new JavaScript file in the `src/` directory
2. Add module reference in `index.html`
3. Create corresponding configuration files as needed

#### 8.2 Multi-language Support

Multi-language support can be achieved by creating multiple sets of configuration files, loading different configurations based on user language preferences.

#### 8.3 Theme Switching

You can add theme switching functionality to allow users to switch between light and dark themes.

## Summary

This tutorial provides a complete guide for creating a research project showcase page. Through modular design and configuration-driven approach, you can easily create professional research project showcase pages. The template has good scalability and maintainability, suitable for various academic research project display needs.

If you encounter problems during use, you can refer to the project source code or consult relevant documentation. Happy using!