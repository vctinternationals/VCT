# VCT Internationals - HVAC Services Website

A modern, responsive static website built with Hugo for VCT Technical Services, offering professional HVAC solutions in Dubai and Hyderabad.

## 🏗️ Project Overview

This is a Hugo-based static website featuring:
- **Multi-location business** (India/Hyderabad & Dubai offices)
- **Service-focused content** (HVAC, Air Duct Cleaning, Kitchen Exhaust Cleaning, etc.)
- **Contact form with reCAPTCHA** protection
- **Location-based form routing** (different StaticForms API keys)
- **Responsive design** with Bootstrap 5
- **Firebase Hosting** deployment

## 📋 Prerequisites

### Required Software
- **Hugo Extended** v0.151.2+ (required for SCSS compilation)
- **Node.js** v22.20.0+ (for npm packages)
- **npm** v10.9.3+ (package management)
- **Firebase CLI** v14.20.0+ (deployment)
- **Git** v2.51.1+ (version control)

### Installation Commands
```bash
# Install Hugo Extended (Windows)
choco install hugo-extended

# Install Node.js and npm
# Download from https://nodejs.org/

# Install Firebase CLI
npm install -g firebase-tools

# Install Git
# Download from https://git-scm.com/
```

## 🚀 Quick Start

### 1. Clone Repository
```bash
git clone <repository-url>
cd VCT
```

### 2. Install Dependencies
```bash
# No npm dependencies required - Hugo handles everything
# All libraries are included in static/lib/
```

### 3. Development Server
```bash
# Start Hugo development server
hugo server -D

# Site will be available at http://localhost:1313
```

### 4. Build for Production
```bash
# Generate static site
hugo --minify

# Output will be in public/ directory
```

## 📁 Project Structure

```
VCT/
├── archetypes/           # Hugo content templates
├── assets/              # Source assets (SCSS, etc.)
│   └── scss/
│       ├── _variables.scss
│       ├── main.scss
│       ├── styles.scss
│       ├── theme-dark.scss
│       └── theme-light.scss
├── content/             # Site content (Markdown/HTML)
│   ├── _index.html      # Homepage
│   ├── about-us.html
│   ├── contact-us.html
│   ├── products.html
│   ├── engineering-services.html
│   ├── services/        # Service pages
│   └── thank-you.html  # Form success page
├── data/               # Site data (JSON)
│   └── common.json     # Company details, contact info
├── layouts/            # Hugo templates
│   ├── _default/       # Base templates
│   ├── partials/       # Reusable components
│   └── shortcodes/     # Custom shortcodes
├── static/             # Static assets
│   ├── css/            # Compiled CSS
│   ├── images/         # Images and media
│   ├── js/             # JavaScript files
│   └── lib/            # Third-party libraries
├── public/             # Generated site (after hugo build)
├── hugo.json           # Site configuration
├── firebase.json       # Firebase hosting config
└── README.md
```

## ⚙️ Configuration

### Site Configuration (`hugo.json`)

The main configuration file contains all site settings, parameters, and integrations:

#### Basic Site Settings
```json
{
  "baseURL": "https://yourdomain.com/",
  "languageCode": "en-us",
  "title": "Your Site Title"
}
```
- **`baseURL`**: **Critical** - Must match your actual domain for proper asset loading and SEO
- **`languageCode`**: **Important for SEO** - Helps search engines understand content language
- **`title`**: **Essential for branding** - Used in browser tabs and search results

#### Markup Configuration
```json
"markup": {
  "goldmark": {
    "renderer": {
      "unsafe": true
    }
  }
}
```
- **`unsafe: true`**: Allows raw HTML in Markdown content for complex layouts

#### Site Parameters (`params`)
```json
"params": {
  "theme": "light",
  "siteTitle": "Your Company - Professional Services",
  "siteDescription": "Your company description for SEO",
  "companyName": "Your Company Name",
  "keywords": "your, relevant, keywords, for, SEO"
}
```
- **`theme`**: **Important for UX** - Controls light/dark mode (affects user experience)
- **`siteTitle`**: **Critical for SEO** - Appears in search results and browser tabs
- **`siteDescription`**: **Essential for SEO** - Meta description for search engines
- **`companyName`**: **Important for branding** - Used throughout templates for consistency
- **`keywords`**: **Valuable for SEO** - Helps search engines categorize your content

#### Analytics & Tracking
```json
"gtmId": "YOUR_GTM_CONTAINER_ID",
"gaMeasurementId": "YOUR_GA4_MEASUREMENT_ID",
"googleAdsConversionId": "YOUR_GOOGLE_ADS_ID",
"facebookPixelId": "YOUR_FACEBOOK_PIXEL_ID",
"linkedinPartnerId": "YOUR_LINKEDIN_PARTNER_ID",
"twitterPixelId": "YOUR_TWITTER_PIXEL_ID",
"clarityProjectId": "YOUR_CLARITY_PROJECT_ID"
```
- **`gtmId`**: **Primary analytics container** - Centralizes all tracking codes
- **`gaMeasurementId`**: Direct Google Analytics 4 integration - **Important for detailed analytics**
- **`googleAdsConversionId`**: **Critical for conversion tracking** and ROI measurement
- **`facebookPixelId`**: **Essential for Facebook/Meta advertising** and retargeting
- **`linkedinPartnerId`**: **Important for B2B marketing** and LinkedIn advertising
- **`twitterPixelId`**: **Valuable for Twitter advertising** and audience insights
- **`clarityProjectId`**: **Useful for user behavior analysis** and UX optimization

#### Contact Form Configuration
```json
"recaptchaEnabled": true,
"recaptchaSiteKey": "YOUR_RECAPTCHA_SITE_KEY",
"staticFormsApiKeyIndia": "YOUR_INDIA_API_KEY",
"staticFormsApiKeyDubai": "YOUR_DUBAI_API_KEY"
```
- **`recaptchaEnabled`**: Boolean flag to enable/disable reCAPTCHA protection globally
- **`recaptchaSiteKey`**: Google reCAPTCHA v2 site key - **Critical for spam protection**
- **`staticFormsApiKeyIndia`**: **Essential** for routing India/Hyderabad submissions to correct office
- **`staticFormsApiKeyDubai`**: **Essential** for routing Dubai submissions to correct office

#### Configuration Usage in Templates
```go
// Access site parameters in templates
{{ .Site.Params.companyName }}
{{ .Site.Params.recaptchaSiteKey }}
{{ .Site.Params.staticFormsApiKeyIndia }}

// Conditional reCAPTCHA loading
{{ if and .Site.Params.recaptchaEnabled (eq .RelPermalink "/contact-us/") }}
  <script src="https://www.google.com/recaptcha/api.js" async defer></script>
{{ end }}
```

### Company Data (`data/common.json`)

Contains structured data for both office locations and social media. This file is **critical** for maintaining consistent contact information across the site.

#### Structure Overview
```json
{
  "workingHours": "Business hours display",
  "indiaCompanyDetails": {
    "contactNumber": "India office phone",
    "whatsappNumberDetails": {
      "number": "WhatsApp number for links",
      "display": "Formatted display number"
    },
    "email": "India office email",
    "supportEmail": "India support email",
    "address": "Complete India office address"
  },
  "dubaiCompanyDetails": {
    "contactNumber": "Dubai office phone",
    "whatsappNumberDetails": {
      "number": "WhatsApp number for links",
      "display": "Formatted display number"
    },
    "email": "Dubai office email",
    "supportEmail": "Dubai support email",
    "address": "Complete Dubai office address"
  },
  "socialMediaHandlers": {
    "facebook": "Facebook page URL",
    "youtube": "YouTube channel URL",
    "linkedin": "LinkedIn profile URL",
    "instagram": "Instagram profile URL"
  }
}
```

#### Importance of Each Section
- **`workingHours`**: **Important for customer expectations** - Shows when customers can reach you
- **Office Details**: **Critical for lead generation** - Contact info must be accurate and up-to-date
- **WhatsApp Integration**: **Essential for international business** - Enables direct messaging
- **Email Addresses**: **Critical for business communication** - Separate support emails for better organization
- **Addresses**: **Important for local SEO** - Helps with Google My Business and local search
- **Social Media**: **Valuable for brand building** - Centralizes all social platform links

#### Usage in Templates
```go
// Access company data
{{$common := site.Data.common}}

// India office details
{{$common.indiaCompanyDetails.contactNumber}}
{{$common.indiaCompanyDetails.email}}
{{$common.indiaCompanyDetails.address}}

// Dubai office details
{{$common.dubaiCompanyDetails.contactNumber}}
{{$common.dubaiCompanyDetails.email}}
{{$common.dubaiCompanyDetails.address}}

// Social media links
{{$common.socialMediaHandlers.facebook}}
{{$common.socialMediaHandlers.youtube}}
{{$common.socialMediaHandlers.linkedin}}
{{$common.socialMediaHandlers.instagram}}

// WhatsApp links
{{$common.indiaCompanyDetails.whatsappNumberDetails.number}}
{{$common.dubaiCompanyDetails.whatsappNumberDetails.number}}
```

## 🎨 Styling & Assets

### SCSS Structure
- **`_variables.scss`**: Color schemes, fonts, breakpoints
- **`main.scss`**: Core styles and imports
- **`styles.scss`**: Component-specific styles
- **`theme-dark.scss`** & **`theme-light.scss`**: Theme variations

### Third-Party Libraries (in `static/lib/`)
- **Bootstrap 5.3.0**: CSS framework
- **Font Awesome 6.5.1**: Icons
- **Animate.css**: CSS animations
- **Owl Carousel**: Image carousels
- **WOW.js**: Scroll animations
- **CounterUp**: Number animations
- **Parallax.js**: Parallax effects
- **Waypoints**: Scroll triggers

### Images Structure
```
static/images/
├── about-*.jpeg        # About section images
├── carousel-*.jpg/png  # Homepage carousel
├── service-*.jpg       # Service images
├── team-*.jpg          # Team photos
├── testimonial-*.jpg   # Customer testimonials
├── bg/                 # Background images
├── blog/               # Blog images
├── client/             # Client logos
├── icon/               # Favicons and icons
├── process/             # Process images
└── services/           # Service-specific images
```

## 📝 Content Management

### Pages Structure
- **Homepage** (`content/_index.html`): Uses `home-page` shortcode
- **About Us** (`content/about-us.html`): Uses `aboutUs-page` shortcode
- **Contact** (`content/contact-us.html`): Uses `contact-us-page` shortcode
- **Services** (`content/services/`): Individual service pages
- **Thank You** (`content/thank-you.html`): Form success page

### Shortcodes
- **`home-page.html`**: Homepage layout with carousel, services, testimonials
- **`aboutUs-page.html`**: About page with company info and team
- **`contact-us-page.html`**: Contact form with reCAPTCHA and location-based routing

## 🔧 Features

### Contact Form

The contact form (`layouts/shortcodes/contact-us-page.html`) is a sophisticated multi-location form with the following features:

#### Form Fields
- **Name** (required): Customer's full name
- **Email** (required): Valid email address with HTML5 validation
- **Phone** (required): Contact number with tel input type
- **Service Location** (required): Dropdown with options:
  - India (Hyderabad)
  - Dubai
- **Message** (required): Textarea with 1000 character limit and live counter

#### Security Features
- **reCAPTCHA v2 Checkbox**: "I'm not a robot" verification
- **Client-side validation**: Prevents submission without completing reCAPTCHA
- **Server-side protection**: StaticForms handles spam filtering

#### Location-Based Routing
The form dynamically selects API keys based on service location:
- **India/Hyderabad** → Uses `staticFormsApiKeyIndia`
- **Dubai** → Uses `staticFormsApiKeyDubai`
- **Dynamic switching**: API key is set only on form submission

#### Form Submission Flow
1. User fills form and selects service location
2. Client-side validation checks all required fields
3. reCAPTCHA verification is validated
4. API key is set based on location selection
5. Form submits to StaticForms with appropriate API key
6. User is redirected to thank-you page
7. StaticForms sends email notification to appropriate office

### Responsive Design
- **Mobile-first** approach
- **Bootstrap 5** grid system
- **Custom breakpoints** for optimal viewing
- **Touch-friendly** navigation

### SEO Optimization
- **Meta tags** (title, description, keywords)
- **Open Graph** tags for social sharing
- **Twitter Card** support
- **Canonical URLs**
- **Structured data** ready

## 🚀 Deployment

### Firebase Hosting Setup
1. **Initialize Firebase**:
   ```bash
   firebase login
   firebase init hosting
   ```

2. **Configure Firebase** (`firebase.json`):
   ```json
   {
     "hosting": {
       "public": "public",
       "ignore": [
         "firebase.json",
         "**/.*",
         "**/node_modules/**"
       ]
     }
   }
   ```

### Deployment Process
```bash
# 1. Build the site
hugo --minify

# 2. Deploy to Firebase
firebase deploy

# 3. Verify deployment
firebase open hosting:site
```

### Environment Variables
Set these in your deployment environment:
- `HUGO_ENV=production` (for production builds)
- Firebase project configuration

## 🔐 Security & Privacy

### reCAPTCHA Configuration
1. **Register site** at [Google reCAPTCHA Admin](https://www.google.com/recaptcha/admin)
2. **Add domains**: `vctinternationals.com`, `localhost` (for testing)
3. **Update `recaptchaSiteKey`** in `hugo.json`

### StaticForms Setup
1. **Create accounts** for India and Dubai
2. **Get API keys** from StaticForms dashboard
3. **Update keys** in `hugo.json`:
   - `staticFormsApiKeyIndia`
   - `staticFormsApiKeyDubai`

## 🧪 Development

### Local Development
```bash
# Start development server with drafts
hugo server -D

# Start with live reload
hugo server -D --disableFastRender

# Build with verbose output
hugo --verbose
```

### Testing
- **Form functionality**: Test contact form with both locations
- **reCAPTCHA**: Verify protection works
- **Responsive design**: Test on various screen sizes
- **Performance**: Use Lighthouse for optimization

### Git Workflow
```bash
# Create feature branch
git checkout -b feature/new-feature

# Make changes and commit
git add .
git commit -m "Add new feature"

# Push and create PR
git push origin feature/new-feature
```

## 📊 Performance

### Optimization Features
- **Minified CSS/JS** in production
- **Compressed images** (WebP support ready)
- **Lazy loading** for images
- **Critical CSS** inlining
- **CDN-ready** static assets

### Monitoring
- **Google Analytics** (GTM-P2B6VDB9)
- **Firebase Performance** monitoring
- **Lighthouse** audits

## 🛠️ Troubleshooting

### Common Issues

#### Hugo Build Errors
```bash
# Clear Hugo cache
hugo --gc

# Check Hugo version compatibility
hugo version
```

#### SCSS Compilation Issues
- Ensure **Hugo Extended** is installed
- Check `layouts/partials/libsass.html` configuration
- Verify SCSS syntax in `assets/scss/`

#### Firebase Deployment Issues
```bash
# Re-authenticate
firebase logout
firebase login

# Check project configuration
firebase projects:list
firebase use <project-id>
```

#### reCAPTCHA Issues
- Verify site key in `hugo.json`
- Check domain whitelist in Google reCAPTCHA console
- Ensure script loads only on contact page

### Debug Mode
```bash
# Enable debug logging
hugo server -D --logLevel debug

# Check build output
hugo --verbose --logLevel debug
```

## 📞 Support

### Contact Information
- **India Office**: +91 8688912223
- **Dubai Office**: +971 58 694 4831
- **Email**: info@vctinternationals.com

### Technical Support
- **Documentation**: This README
- **Issues**: GitHub Issues
- **Updates**: Check Hugo and Firebase documentation

## 📄 License

This project is proprietary to VCT Technical Services. All rights reserved.

---

**Built with ❤️ using Hugo, Bootstrap, and Firebase**