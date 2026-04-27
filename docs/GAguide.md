# Google Analytics Setup Guide for SimplyAI.work

## Overview
This guide will help you set up Google Analytics 4 (GA4) for your SimplyAI.work website.

## Step 1: Create a Google Analytics Account

1. Go to [Google Analytics](https://analytics.google.com/)
2. Sign in with your Google account
3. Click "Start measuring"
4. Enter your Account name: `SimplyAI`
5. Configure data sharing settings as desired
6. Click "Next"

## Step 2: Create a Property

1. Property name: `SimplyAI.work`
2. Select your reporting time zone: `(GMT+08:00) Hong Kong`
3. Select your currency: `Hong Kong Dollar (HKD)`
4. Click "Next"
5. Select your business industry: `Business Services`
6. Select your business size
7. Click "Create"
8. Accept the terms of service

## Step 3: Set Up a Data Stream

1. Select "Web" as your platform
2. Enter your website URL: `https://simplyai.work`
3. Stream name: `SimplyAI.work Main Site`
4. Click "Create stream"

## Step 4: Get Your Measurement ID

After creating the data stream, you'll see your **Measurement ID** in the format:

G-XXXXXXXXXX

Copy this ID.

## Step 5: Update Your Website Code

In your HTML file, find this section near the top of the `<head>`:

```html
<!-- Google Analytics (placeholder - replace G-XXXXXXXXXX with your actual ID) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'G-XXXXXXXXXX');
</script>

Replace both instances of G-XXXXXXXXXX with your actual Measurement ID.

Step 6: Verify Installation
Go back to Google Analytics
Navigate to Admin → Data Streams → Your stream
Click "View tag instructions"
Use the "Test your installation" feature
Alternatively, install the Google Tag Assistant Chrome extension
Recommended Events to Track
Custom Events (Add to your JavaScript)

javascript
// Track CTA Button Clicks
document.querySelectorAll('.btn--primary').forEach(btn => {
    btn.addEventListener('click', () => {
        gtag('event', 'cta_click', {
            'button_text': btn.textContent.trim(),
            'button_location': btn.closest('section')?.id || 'unknown'
        });
    });
});

// Track Form Submissions
document.getElementById('contactForm').addEventListener('submit', () => {
    gtag('event', 'form_submit', {
        'form_name': 'contact_form'
    });
});

// Track Chatbot Opens
document.getElementById('chatbotTrigger').addEventListener('click', () => {
    gtag('event', 'chatbot_open');
});

// Track Chatbot Messages
function trackChatMessage(isUser) {
    gtag('event', 'chatbot_message', {
        'message_type': isUser ? 'user' : 'bot'
    });
}

// Track Language Switch
document.querySelectorAll('.lang-switch__btn').forEach(btn => {
    btn.addEventListener('click', () => {
        gtag('event', 'language_switch', {
            'language': btn.dataset.lang
        });
    });
});

// Track Scroll Depth
let scrollDepths = [25, 50, 75, 100];
let trackedDepths = [];

window.addEventListener('scroll', () => {
    const scrollPercent = Math.round(
        (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100
    );
    
    scrollDepths.forEach(depth => {
        if (scrollPercent >= depth && !trackedDepths.includes(depth)) {
            trackedDepths.push(depth);
            gtag('event', 'scroll_depth', {
                'depth_percentage': depth
            });
        }
    });
});

GA4 Configuration Recommendations
1. Enable Enhanced Measurement

In your Data Stream settings, ensure these are enabled:

Page views
Scrolls
Outbound clicks
Site search
Form interactions
Video engagement
File downloads
2. Create Custom Conversions

Go to Admin → Conversions and mark these as conversions:

form_submit
chatbot_open
cta_click
3. Set Up Audiences

Create audiences for:

Engaged Users: Users who viewed 3+ pages
Form Starters: Users who clicked on contact form
Chatbot Users: Users who opened the chatbot
4. Create Custom Reports

Useful reports to create:

CTA Performance by Location
Chatbot Engagement Funnel
Language Preference Analysis
Workflow Interest Distribution
Privacy Considerations
Cookie Consent (Recommended for GDPR/PDPO Compliance)

Add a cookie consent banner. Here's a simple implementation:

javascript
// Check for consent
function hasConsent() {
    return localStorage.getItem('ga_consent') === 'true';
}

// Initialize GA only with consent
if (hasConsent()) {
    gtag('consent', 'update', {
        'analytics_storage': 'granted'
    });
} else {
    gtag('consent', 'default', {
        'analytics_storage': 'denied'
    });
}

// Function to grant consent
function grantConsent() {
    localStorage.setItem('ga_consent', 'true');
    gtag('consent', 'update', {
        'analytics_storage': 'granted'
    });
}

Troubleshooting

Data Not Appearing

Wait 24-48 hours for data to appear
Check Realtime reports first
Verify no ad blockers are active
Confirm Measurement ID is correct
Duplicate Page Views

Ensure gtag snippet appears only once
Check for SPA routing issues
Missing Events

Use GA4 DebugView (Admin → DebugView)
Check browser console for errors
