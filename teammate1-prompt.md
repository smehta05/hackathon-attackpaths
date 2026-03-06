# PathSight Dashboard - Teammate 1: Core Infrastructure & Layout

## Your Role: Foundation Architect
You are responsible for creating the core HTML structure, dark mode styling foundation, responsive layout, and data management system that your teammates will build upon.

## Product Overview

**Product Name:** PathSight
**Tagline:** "From Risk to Reality — See when an attack path becomes a real attack."

**Concept:** A modern SaaS cloud security dashboard that visualizes when theoretical attack paths become active attacks. Think enterprise security operations center with a polished, professional interface.

**Design Style:**
- Dark mode security operations dashboard
- Modern SaaS layout with card-based panels
- Clean typography (use system fonts or Google Fonts)
- Subtle shadows and glow effects for risk indicators
- Responsive layout that works on desktop and tablets
- Professional UI similar to leading cloud security platforms

## Your Specific Tasks

### 1. HTML Structure & Foundation
Create a single HTML file with:
- Semantic HTML5 structure
- CSS Grid or Flexbox layout system
- Dark mode color scheme as default
- Typography system with clear hierarchy
- Component placeholders for teammates to fill in

### 2. Dashboard Header
Build the top navigation:
```
PathSight – Attack Path Realization Engine
"From Risk to Reality — See when an attack path becomes a real attack."
```
- Professional logo area (use text-based logo)
- Clean header styling with subtle bottom border

### 3. Layout Grid System
Create responsive grid areas for:
- Header (full width)
- Summary metrics (4 cards in a row, responsive to 2x2 on mobile)
- Main content area (2-column: attack path viz + timeline)
- Bottom panels (2-column: prevention opportunities + counterfactual analysis)

### 4. Mock Data Structure
Create a JavaScript data model that teammates can use:

```javascript
const attackPathData = {
  metrics: {
    pathAge: 92,
    runtimeSignals: 3,
    compromisedResources: 1,
    realizationScore: 92
  },

  attackPath: [
    {id: 'internet', name: 'Internet', status: 'exposed'},
    {id: 'ec2', name: 'EC2 Instance', status: 'compromised'},
    {id: 'imds', name: 'Instance Metadata Service', status: 'exploited'},
    {id: 'iam', name: 'IAM Role', status: 'accessed'},
    {id: 's3', name: 'Sensitive S3 Bucket', status: 'targeted'}
  ],

  timeline: [
    {date: '2024-01-10', event: 'Attack path discovered', type: 'discovery'},
    {date: '2024-01-18', event: 'IAM privilege escalation risk detected', type: 'risk'},
    {date: '2024-02-02', event: 'Sensitive S3 bucket reachable', type: 'risk'},
    {date: '2024-04-14T10:02', event: 'SSRF attempt against IMDSv1', type: 'attack'},
    {date: '2024-04-14T10:05', event: 'Malware detected on EC2 instance', type: 'attack'},
    {date: '2024-04-14T10:07', event: 'S3 access attempt using instance role', type: 'attack'}
  ],

  preventionOpportunities: [
    'Disable IMDSv1',
    'Restrict IAM role permissions',
    'Patch exposed EC2 instance',
    'Remove public EC2 exposure'
  ],

  counterfactualControls: [
    {name: 'Disable IMDSv1', impact: 'Stops credential theft', reduction: '92% → 12%'},
    {name: 'Network Segmentation', impact: 'Blocks initial access', reduction: '92% → 8%'}
  ]
};
```

### 5. CSS Variables System
Define a consistent design system:

```css
:root {
  /* Colors */
  --bg-primary: #0a0a0a;
  --bg-secondary: #1a1a1a;
  --bg-card: #222222;
  --text-primary: #ffffff;
  --text-secondary: #b3b3b3;
  --accent-blue: #3b82f6;
  --danger-red: #ef4444;
  --warning-orange: #f59e0b;
  --success-green: #10b981;

  /* Spacing */
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
  --spacing-xl: 2rem;

  /* Typography */
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.25rem;
  --font-size-xl: 1.5rem;
  --font-size-2xl: 2rem;

  /* Shadows & Effects */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.3);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.3);
  --glow-danger: 0 0 20px rgba(239,68,68,0.3);
}
```

### 6. Responsive Layout
Ensure the layout works on:
- Desktop: 1200px+ (full 2-column layout)
- Tablet: 768px-1199px (adapted layout)
- Mobile: <768px (stacked single column)

### 7. Integration Points for Teammates

Create placeholder divs with specific IDs for teammates:

```html
<!-- For Teammate 2 (Visualizations) -->
<div id="attack-path-container"></div>
<div id="timeline-container"></div>
<div id="progress-meter-container"></div>

<!-- For Teammate 3 (Business Logic) -->
<div id="metrics-cards-container"></div>
<div id="simulation-controls"></div>
<div id="prevention-panel"></div>
<div id="counterfactual-panel"></div>
```

## Coordination with Teammates

**Shared with Teammate 2:**
- Provide CSS variables for colors/spacing
- Ensure containers have proper dimensions for visualizations
- Coordinate on animation timing and easing functions

**Shared with Teammate 3:**
- Provide the mock data structure
- Ensure card containers have proper styling hooks
- Coordinate on JavaScript event handling patterns

## Deliverable
A single HTML file with:
- Complete responsive layout and styling foundation
- Header and basic structure implemented
- Mock data structure defined
- Clear placeholder areas for teammate components
- Professional dark mode design aesthetic
- Works when opened directly in a browser

## Technical Requirements
- Single HTML file (no external dependencies except fonts)
- Vanilla CSS (no frameworks)
- Vanilla JavaScript for data structure
- Modern browser support (Chrome, Firefox, Safari, Edge)
- Mobile responsive design
- Clean, semantic HTML structure

Focus on creating a solid, professional foundation that makes it easy for your teammates to integrate their components!