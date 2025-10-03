# Yixuan Gao - Academic Website

<div align="center">

**Personal academic website built with [Jekyll](https://jekyllrb.com/) using the [al-folio](https://github.com/alshedivat/al-folio) theme.**

🌐 **Live Site**: [https://adamgao1996.github.io](https://adamgao1996.github.io)

---

[![Build Status](https://github.com/adamgao1996/adamgao1996.github.io/actions/workflows/pages.yml/badge.svg)](https://github.com/adamgao1996/adamgao1996.github.io/actions/workflows/pages.yml)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://adamgao1996.github.io)
[![Jekyll](https://img.shields.io/badge/Jekyll-4.3.0-red)](https://jekyllrb.com/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

</div>

## About

This repository contains the source code for Yixuan Gao's personal academic website. The site showcases research work, publications, news updates, and professional activities in the field of computer science and wireless networking.

## Features

- 📄 **Publications**: Comprehensive list of research papers with BibTeX integration
- 📰 **News**: Latest updates on research activities, paper acceptances, and presentations  
- 🎯 **Projects**: Showcase of research projects and technical work
- 📚 **Blog**: Technical posts and insights (coming soon)
- 📊 **CV**: Detailed academic and professional experience
- 🔗 **Links**: Connections to professional profiles and collaborations

## Technical Stack

This website is built using modern web technologies and academic publishing tools:

**Core Technologies:**
- **Jekyll 4.3.0**: Static site generator with advanced templating
- **GitHub Actions**: Automated building and deployment pipeline  
- **GitHub Pages**: Hosting and continuous deployment
- **Ruby 3.1**: Backend runtime environment

**Academic Features:**
- **BibTeX Integration**: Automatic bibliography generation with jekyll-scholar
- **Jupyter Notebooks**: Support for interactive code demonstrations
- **Responsive Images**: Optimized WebP image generation with ImageMagick  
- **Math Rendering**: LaTeX math expressions with MathJax
- **Citation Management**: Automatic paper metadata and links

**Plugins & Extensions:**
- `jekyll-scholar`: Academic bibliography management
- `jekyll-jupyter-notebook`: Jupyter notebook integration
- `jekyll-imagemagick`: Responsive image optimization
- `jekyll-feed`: RSS/Atom feed generation
- `jekyll-sitemap`: SEO-friendly sitemap generation
- `jekyll-archives-v2`: Organized post archives
- `jekyll-minifier`: Asset compression and optimization

## Local Development

To run this website locally:

```bash
# Clone the repository
git clone https://github.com/adamgao1996/adamgao1996.github.io.git
cd adamgao1996.github.io

# Install dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll serve --livereload
```

The site will be available at `http://localhost:4000`

## Deployment

The website uses GitHub Actions for automated deployment:

1. **Automatic Building**: Every push to `master` triggers the build workflow
2. **Dependency Management**: ImageMagick, Python, Jupyter, and Ruby are automatically installed
3. **GitHub Pages**: Built site is deployed to GitHub Pages automatically
4. **Custom Domain Ready**: Easy configuration for custom domains

## Research Focus

Current research interests include:
- **Wireless Communication Systems**
- **Acoustic Sensing and Signal Processing** 
- **IoT and Sensor Networks**
- **Machine Learning for Communications**

## Recent Updates

- ✅ **Oct 2025**: Website deployed with GitHub Actions
- ✅ **Sep 2025**: SoilSound paper published to arXiv
- ✅ **Aug 2025**: SCF paper accepted for publication
- ✅ **Dec 2024**: EWSN Best Paper Award received

---

## Original Theme

This website is built using the [al-folio](https://github.com/alshedivat/al-folio) theme by [Maruan Al-Shedivat](https://github.com/alshedivat). The theme has been customized for academic use with enhanced publication management and news system.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.