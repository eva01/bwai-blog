## Codebase Analysis: BWAI Blog (Eleventy + Page-CMS + Cloudflare Pages)

### Architecture Overview

This is a modern static site generator setup using **Eleventy (11ty)** as the core framework, with **Page-CMS** for content management and **Cloudflare Pages** for deployment. The architecture follows Eleventy's standard structure with some customizations for the BWAI community blog.

### Key Architectural Components

#### 1. **Content Management Structure**
- **Input Directory**: `content/` - Contains all source content
- **Includes Directory**: `_includes/` - Reusable templates and partials
- **Data Directory**: `_data/` - Global site data (metadata.js)
- **Public Directory**: `public/` - Static assets (CSS, images)

#### 2. **Page-CMS Integration**
The `.pages.yml` configuration defines three main content types:
- **Posts Collection**: Blog posts in `content/blog/`
- **About Page**: Single file at `content/about/index.md`
- **Metadata**: Site configuration in `_data/metadata.js`

#### 3. **Template System**
- **Base Layout** (`layouts/base.njk`): HTML5 structure with navigation, feeds, and CSS bundling
- **Home Layout** (`layouts/home.njk`): Extends base with a message box component
- **Post Layout** (`layouts/post.njk`): Blog post template with syntax highlighting

#### 4. **Content Organization**
- **Blog Posts**: Markdown files in `content/blog/` with frontmatter
- **Pages**: Static pages like About, Tags, Archive
- **Feeds**: Atom XML and JSON feeds for syndication
- **Sitemap**: XML sitemap for SEO

### Technical Stack

#### Core Dependencies
- **Eleventy 2.0.1**: Static site generator
- **Luxon**: Date/time handling
- **Markdown-it-anchor**: Header anchors in markdown
- **Prism.js**: Syntax highlighting

#### Plugins
- **RSS Plugin**: Feed generation
- **Syntax Highlight**: Code highlighting
- **Navigation**: Menu generation
- **Bundle**: CSS/JS bundling
- **Image**: Responsive image optimization

### Deployment & Build Configuration

#### Cloudflare Pages Setup
- **Build Command**: `npm run build` (Eleventy build)
- **Output Directory**: `_site`
- **Node Version**: >=14 (from package.json engines)

#### Netlify Configuration (Legacy)
The `netlify.toml` suggests previous Netlify deployment with Lighthouse performance monitoring, but the project is now on Cloudflare Pages.

### Key Features & Patterns

#### 1. **Draft System**
- Posts can be marked as `draft: true`
- Drafts only build in serve/watch mode
- Controlled via `BUILD_DRAFTS` environment variable

#### 2. **Tag System**
- Posts support multiple tags
- Automatic tag pages generation
- Filtered tag lists (excludes system tags)

#### 3. **Image Optimization**
- Responsive images with multiple formats (AVIF, WebP, JPEG)
- Lazy loading by default
- Configurable widths and sizes

#### 4. **CSS Bundling**
- Uses Eleventy's bundle plugin
- Inlined CSS for performance
- Separate file option available for CSP compliance

#### 5. **Navigation**
- Automatic navigation from frontmatter
- Eleventy-navigation plugin integration
- Accessible menu structure

### Strengths

1. **Modern Stack**: Latest Eleventy version with performance optimizations
2. **CMS Integration**: Page-CMS provides user-friendly content editing
3. **SEO Ready**: Sitemaps, feeds, meta tags, structured data
4. **Performance**: Image optimization, CSS inlining, lazy loading
5. **Accessibility**: Semantic HTML, skip links, ARIA attributes
6. **Developer Experience**: Hot reload, draft mode, comprehensive tooling

### Areas for Consideration

1. **Deployment Migration**: Netlify config still present - could be removed
2. **Build Optimization**: Could implement incremental builds for larger sites
3. **Content Modeling**: Page-CMS config could be expanded for more content types
4. **Internationalization**: Currently single-language, could add i18n support
5. **Analytics**: No analytics setup visible - could integrate with Cloudflare Web Analytics

### Recommendations

1. **Clean up legacy configs**: Remove netlify.toml since using Cloudflare Pages
2. **Enhance Page-CMS**: Add more content types or custom fields as needed
3. **Performance monitoring**: Set up Cloudflare Pages analytics
4. **Content strategy**: Consider adding author profiles, categories, or series
5. **Security**: Implement CSP headers in Cloudflare Pages

The codebase is well-structured, follows Eleventy best practices, and is ready for content management via Page-CMS with reliable deployment on Cloudflare Pages.