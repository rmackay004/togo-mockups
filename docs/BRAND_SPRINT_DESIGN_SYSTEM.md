# Togo Health - Brand Sprint Design System

> **Purpose**: This document captures the complete design system, brand identity, and visual language of Togo Health for use in brand sprint exercises, design handoffs, and development implementation.

---

## Executive Summary

**Brand Name**: Togo Health
**Tagline**: "Unified Clinical Workforce Management Platform"
**Brand Promise**: Giving healthcare workers back their time, one automated task at a time
**Industry**: Healthcare Technology (B2B2C SaaS)
**Target Audience**: Hospital administrators (buyers), clinical staff (users)

---

## 1. Brand Personality & Positioning

### Brand Attributes

**Primary Traits**:
- **Intelligent**: Sophisticated AI-powered automation without the complexity
- **Trustworthy**: Clinical-grade reliability and HIPAA compliance
- **Empathetic**: Designed to reduce clinician burnout and improve wellbeing
- **Professional**: Healthcare-appropriate tone without being sterile
- **Innovative**: Cutting-edge multi-agent AI while remaining approachable

**Secondary Traits**:
- Efficient (saving time)
- Collaborative (human + AI partnership)
- Proactive (anticipates needs)
- Transparent (clear about what AI does)
- Scalable (works for 50 or 5,000 staff)

### Brand Voice

**Tone Guidelines**:
- **Do**: Use clear, jargon-free language; explain AI benefits in human terms; emphasize time savings and wellbeing
- **Don't**: Use overly technical AI jargon; make promises you can't keep; use healthcare clichés ("disruptive," "revolutionary")

**Voice Examples**:
- ✅ "Your AI companion submitted last week's timesheet with 38.5 hours"
- ❌ "The autonomous agent executed the timesheet submission workflow"
- ✅ "12.5 hours saved this month—time you can spend with patients"
- ❌ "Our platform optimizes administrative efficiency through ML algorithms"

### Two Language Modes

**Technical Mode** (for investors, technical buyers):
- Use: "agents," "autonomous," "human-in-the-loop," "orchestration"
- Audience: VCs, CTOs, technical evaluators
- Files: `clinician-dashboard-ai.html`, `admin-dashboard.html`

**Companion Mode** (for end users, demos):
- Use: "assistants," "automatic," "needs approval," "companion"
- Audience: Clinicians, nurses, end users
- Files: `clinician-dashboard-companion.html`, `admin-dashboard-companion.html`

### Brand Story

**The Problem**:
Healthcare workers spend 50%+ of their time on administrative tasks—timesheets, credential renewals, shift swaps, documentation. This leads to burnout (1 in 3 nurses report it) and costs the US healthcare system $265 billion annually.

**The Solution**:
Togo Health unifies three proven workforce platforms (Med App, Core Schedule, myhealthPD) and adds 15 specialized AI assistants that automate 70% of repetitive admin work. Clinicians get back 12.5 hours/month—time they can spend on patient care.

**The Vision**:
A future where healthcare workers focus on care, not paperwork. Where AI handles the mundane so humans can do what they do best: heal.

---

## 2. Visual Identity

### Logo & Wordmark

**Primary Logo**: "Togo Health"
- **Font**: Inter Bold (700 weight)
- **Letter Spacing**: -0.5px (navigation), -1px (hero size)
- **Sizes**:
  - Hero: 56px
  - Navigation: 32px
  - Compact: 24px
- **Color Treatments**:
  - On white background: Purple gradient (#667EEA to #764BA2)
  - On gradient background: White
  - On dark background: White

**Sub-brand Taglines**:
- Primary: "Unified Clinical Workforce Management Platform"
- Secondary: "AI-Powered Workforce" (used in technical mode)
- Secondary: "Your AI Companion" (used in companion mode)

**Logo Usage**:
```html
<!-- Standard header usage -->
<h1 style="font-size: 32px; font-weight: 700; background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent;">Togo Health</h1>
<p style="font-size: 11px; color: #6B7280; font-weight: 500;">UNIFIED WORKFORCE</p>
```

**Logo Don'ts**:
- Don't stretch or distort the wordmark
- Don't use colors outside the brand palette
- Don't add drop shadows or effects
- Don't place on busy backgrounds without sufficient contrast

---

## 3. Color System

### Primary Brand Colors

**Brand Gradient** (Primary Identity Color)
```css
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
```
- **Usage**: Primary CTAs, hero sections, logo, feature highlights
- **Hex Values**:
  - Start: `#667EEA` (Vibrant Purple)
  - End: `#764BA2` (Deep Purple)
- **RGB**:
  - Start: `rgb(102, 126, 234)`
  - End: `rgb(118, 75, 162)`

**Primary Purple**: `#667EEA`
- **Usage**: Links, active states, accent elements, tags
- **Accessibility**: AA compliant on white (4.53:1 contrast ratio)

**Deep Purple**: `#764BA2`
- **Usage**: Gradient endpoints, hover states, depth/hierarchy

### Functional Color System

**Workflow Type Colors** (Semantic Meaning)

**🟢 Autonomous/Automatic (Green)**
- **Primary**: `#10B981` (Emerald)
- **Light Background**: `#F0FDF4`
- **Border**: `#10B981`
- **Text**: `#065F46` (Dark Green)
- **Meaning**: Completed tasks, success, no action needed
- **Use Case**: Auto-submitted timesheets, completed documentation

**🟠 Human-in-the-Loop/Needs Approval (Orange)**
- **Primary**: `#F59E0B` (Amber)
- **Light Background**: `#FFFBEB`
- **Border**: `#F59E0B`
- **Text**: `#92400E` (Dark Amber)
- **Meaning**: Pending approval, requires decision
- **Use Case**: Shift swap requests, credential review

**🔵 Human-on-the-Loop/Monitored (Blue)**
- **Primary**: `#3B82F6` (Sky Blue)
- **Light Background**: `#EFF6FF`
- **Border**: `#3B82F6`
- **Text**: `#1E3A8A` (Dark Blue)
- **Meaning**: Active monitoring, FYI, can override
- **Use Case**: Auto-booked training, schedule optimization

### Semantic Colors

**Success**: `#10B981` (Green) - Confirmations, completed actions
**Warning**: `#F59E0B` (Amber) - Attention needed, expiring items
**Error**: `#EF4444` (Red) - Failures, critical alerts
**Info**: `#3B82F6` (Blue) - Informational messages, tips

### Neutral Palette

**Text Colors**:
- **Primary Text**: `#1A1A1A` (Near Black) - Body text, headings
- **Secondary Text**: `#6B7280` (Medium Gray) - Helper text, metadata
- **Tertiary Text**: `#9CA3AF` (Light Gray) - Timestamps, captions

**UI Colors**:
- **Border**: `#E5E7EB` (Light Gray)
- **Background**: `#F9FAFB` (Off-White)
- **Card Background**: `#FFFFFF` (White)
- **Page Background**: `#F8F9FA` (Subtle Gray)

### Color Usage Matrix

| Element | Color | Hex Code | Usage Context |
|---------|-------|----------|---------------|
| Primary CTA | Gradient | #667EEA → #764BA2 | Main action buttons |
| Secondary CTA | White + Purple Border | #667EEA border | Less prominent actions |
| Links | Purple | #667EEA | Text links, nav items |
| Success State | Green | #10B981 | Completions, valid items |
| Warning State | Amber | #F59E0B | Expirations, pending |
| Error State | Red | #EF4444 | Failures, critical issues |
| Disabled State | Light Gray | #9CA3AF | Inactive elements |

### Accessibility Standards

**Contrast Ratios** (WCAG 2.1 AA):
- Normal text (14px+): 4.5:1 minimum ✅
- Large text (18px+): 3:1 minimum ✅
- Interactive elements: Clear focus states with 3:1 contrast ✅

**Color Blindness Considerations**:
- Don't rely solely on color to convey information
- Use icons + color combinations (✓ + green, ⚠ + amber)
- Ensure shape/position also communicates meaning

---

## 4. Typography

### Font Family

**Primary Font**: Inter (Google Fonts)
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

**Fallback Stack**:
```css
font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
```

**Why Inter?**
- Designed specifically for digital interfaces
- Excellent legibility at all sizes
- Professional yet approachable
- Wide range of weights (300-700)
- Open-source and widely supported

### Type Scale

| Style | Size | Weight | Line Height | Letter Spacing | Usage |
|-------|------|--------|-------------|----------------|-------|
| **Display** | 56px | 700 | 1.1 | -1px | Landing page logo |
| **H1** | 32px | 700 | 1.2 | 0 | Page titles |
| **H2** | 28px | 700 | 1.2 | 0 | Section headers |
| **H3** | 24px | 700 | 1.3 | 0 | Card titles |
| **H4** | 20px | 700 | 1.3 | 0 | Component headers |
| **H5** | 18px | 700 | 1.4 | 0 | Subsection titles |
| **H6** | 16px | 600 | 1.4 | 0 | Small headers |
| **Body Large** | 16px | 400 | 1.6 | 0 | Primary body text |
| **Body** | 14px | 400 | 1.6 | 0 | Standard text |
| **Body Small** | 13px | 400 | 1.5 | 0 | Secondary info |
| **Caption** | 12px | 400-600 | 1.4 | 0 | Labels, timestamps |
| **Micro** | 11px | 600 | 1.3 | 0.5px | Tags, badges |
| **Tiny** | 10px | 700 | 1.3 | 0.5px | AI badges, compact UI |

### Typography Best Practices

**Hierarchy**:
- Use size, weight, and color to establish clear hierarchy
- Limit to 3 levels of hierarchy on any given screen
- Maintain consistent spacing between heading levels

**Readability**:
- Body text: 14-16px, line-height 1.6 for optimal reading
- Maximum line length: 75 characters for body text
- Use sufficient contrast (4.5:1 for normal text)

**Emphasis**:
- **Bold (600-700)**: For emphasis, labels, headers
- *Italic*: Avoid in UI; use for quotes only
- Color: Use purple (#667EEA) for interactive elements
- ALL CAPS: Use sparingly for badges/tags (10-12px max)

---

## 5. Spacing & Layout

### 8-Point Grid System

All spacing values are multiples of 8px for consistency:

```css
--space-1: 4px;   /* Tight */
--space-2: 8px;   /* Compact */
--space-3: 12px;  /* Standard */
--space-4: 16px;  /* Medium */
--space-5: 24px;  /* Large */
--space-6: 32px;  /* Extra Large */
--space-7: 40px;  /* Section */
--space-8: 48px;  /* Hero */
```

**Usage Guidelines**:
- **4px**: Icon padding, tight gaps between related items
- **8px**: Form field gaps, icon-to-text spacing
- **12px**: Tag padding, list item gaps
- **16px**: Card internal padding, standard gaps
- **24px**: Card-to-card spacing, section separation
- **32px**: Major section padding
- **40px**: Content margin from edges
- **48px**: Hero section margins

### Layout Grid

**Desktop** (1200px+):
- 12-column grid
- Column gap: 24px
- Side margins: 40px

**Tablet** (768px - 1199px):
- 8-column grid
- Column gap: 16px
- Side margins: 32px

**Mobile** (320px - 767px):
- 4-column grid
- Column gap: 16px
- Side margins: 20px

### Container Max-Widths

- **Landing Page**: 900px
- **Dashboard Content**: 1400px (with 260px sidebar)
- **Card Content**: Fluid within grid
- **Reading Content**: 720px (optimal for text)

---

## 6. Components & Patterns

### Buttons

**Primary Button**
```css
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
color: white;
padding: 12px 24px;
border-radius: 10px;
font-weight: 600;
font-size: 14px;
transition: transform 0.2s;
```
Hover: `transform: translateY(-2px)`

**Secondary Button**
```css
background: white;
color: #667EEA;
border: 2px solid #667EEA;
padding: 12px 24px;
border-radius: 10px;
font-weight: 600;
font-size: 14px;
```

**Ghost Button**
```css
background: transparent;
color: #6B7280;
border: 1px solid #E5E7EB;
padding: 8px 16px;
border-radius: 8px;
font-weight: 500;
font-size: 14px;
```

**Button States**:
- **Hover**: Lift (-2px) + subtle shadow
- **Active/Pressed**: No lift, slight scale (0.98)
- **Disabled**: 50% opacity, no pointer events
- **Focus**: 2px solid purple outline, 2px offset

### Cards

**Standard Card**
```css
background: white;
border-radius: 16px;
border: 1px solid #E5E7EB;
padding: 24px;
box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
```

**Card Hover Effect**
```css
transform: translateY(-8px);
box-shadow: 0 20px 60px rgba(0, 0, 0, 0.25);
transition: all 0.3s;
```

**Featured Card** (AI-powered elements)
```css
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
border-radius: 20px;
padding: 28px;
color: white;
border: 2px solid #667EEA; /* For non-gradient variants */
```

### Badges & Tags

**Status Badge**
```css
padding: 4px 10px;
border-radius: 6px;
font-size: 12px;
font-weight: 600;
```

Color variants:
- Success: `background: #D1FAE5; color: #065F46;`
- Warning: `background: #FEF3C7; color: #92400E;`
- Info: `background: #EEF2FF; color: #667EEA;`

**AI Badge**
```css
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
color: white;
padding: 4px 10px;
border-radius: 6px;
font-size: 10px;
font-weight: 700;
```
Text: "✨ AI POWERED"

### Form Elements

**Input Field**
```css
padding: 12px 16px;
border: 1px solid #E5E7EB;
border-radius: 8px;
font-size: 14px;
transition: all 0.2s;
```

**Focus State**
```css
border-color: #667EEA;
box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
outline: none;
```

### Icons

**Icon Sizes**:
- Small: 16px (inline with text)
- Medium: 20px (navigation)
- Large: 24px (featured)
- Hero: 48px (main focal points)

**Icon Style**: Emoji-based for mockups
- Provides instant visual recognition
- Language-agnostic
- Friendly and approachable
- Production: Replace with custom icon set or Lucide/Heroicons

**Icon Color**:
- Navigation: Match text color
- Feature icons: Purple (#667EEA) or gradient
- Status icons: Semantic colors (green, amber, blue)

---

## 7. Motion & Animation

### Animation Principles

**Purpose-Driven**: Every animation should have a reason (feedback, guidance, delight)
**Performance-First**: Use transform and opacity; avoid animating width/height
**Subtle**: Healthcare professionals need efficiency, not distraction

### Standard Transitions

**Fast** (UI feedback): `transition: all 0.2s ease;`
- Button hovers, input focus, link underlines

**Medium** (Content): `transition: all 0.3s ease;`
- Card hovers, dropdown menus, modals

**Slow** (Major changes): `transition: all 0.5s ease-in-out;`
- Page transitions, layout shifts

### Micro-Interactions

**Button Hover**:
```css
transform: translateY(-2px);
box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
transition: all 0.2s;
```

**Card Hover**:
```css
transform: translateY(-8px);
box-shadow: 0 20px 60px rgba(0, 0, 0, 0.25);
transition: all 0.3s;
```

**Icon Scale**:
```css
transform: scale(1.1);
transition: transform 0.2s;
```

### Loading States

**Pulse Animation** (for AI indicators):
```css
@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 0.5; }
  50% { transform: scale(1.1); opacity: 0.3; }
}
animation: pulse 3s ease-in-out infinite;
```

**Accessibility**: Respect `prefers-reduced-motion`
```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 8. Special Design Elements

### Glassmorphism (Overlay Effect)

Used for modal overlays and floating AI panels:
```css
background: rgba(255, 255, 255, 0.15);
backdrop-filter: blur(10px);
border: 1px solid rgba(255, 255, 255, 0.2);
border-radius: 12px;
```

**Usage**:
- Multi-agent orchestration cards
- Notification overlays
- Feature callouts on gradient backgrounds

### Gradient Overlays

**Primary Gradient** (Brand):
```css
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
```

**Success Gradient**:
```css
background: linear-gradient(135deg, #F0FDF4 0%, #DCFCE7 100%);
border: 1px solid #86EFAC;
```

**Warning Gradient**:
```css
background: linear-gradient(135deg, #FFFBEB 0%, #FEF3C7 100%);
border: 1px solid #FCD34D;
```

**Info Gradient**:
```css
background: linear-gradient(135deg, #EFF6FF 0%, #DBEAFE 100%);
border: 1px solid #93C5FD;
```

### Shadow System

**Elevation Levels**:
```css
--shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.1);
--shadow-md: 0 4px 12px rgba(0, 0, 0, 0.15);
--shadow-lg: 0 20px 60px rgba(0, 0, 0, 0.25);
--shadow-purple: 0 8px 20px rgba(102, 126, 234, 0.3); /* For purple CTAs */
```

**Usage**:
- Cards: `--shadow-sm`
- Modals/Dialogs: `--shadow-md`
- Hover states: `--shadow-lg`
- Primary buttons (hover): `--shadow-purple`

### Border Radius System

```css
--radius-sm: 8px;   /* Form inputs, small badges */
--radius-md: 12px;  /* Buttons, standard cards */
--radius-lg: 16px;  /* Large cards */
--radius-xl: 20px;  /* Feature cards, hero sections */
--radius-full: 9999px; /* Pills, notification dots */
```

---

## 9. Iconography & Visual Language

### Icon System

**Primary Icon Set**: Emoji (mockup phase)
- ✅ Pro: Universal, no licensing, instant recognition
- ⚠️ Con: Limited customization, platform-dependent rendering
- 🎯 Production: Migrate to Lucide Icons or Heroicons

**Icon Categories & Examples**:

**Navigation & System**:
- 🏠 Home/Dashboard
- 📊 Analytics/Reports
- ⚙️ Settings
- 👤 Profile
- 🔔 Notifications

**Clinical & Medical**:
- 👨‍⚕️ Clinician
- 🏥 Hospital/Facility
- 📋 Medical records
- 🩺 Clinical work
- 💊 Medication

**Workflow Types**:
- ✓ Autonomous (green checkmark)
- ⏸ Human-in-loop (orange pause)
- ⚡ Human-on-loop (blue lightning)
- 🤖 AI/Agent
- 👁️ Monitoring

**Status Indicators**:
- ✅ Complete/Success
- ⚠️ Warning/Attention
- ❌ Error/Failed
- 📤 Upload/Submit
- 📥 Download/Receive

### Visual Metaphors

**AI as Companion**: Use friendly, collaborative imagery
- 🤝 Partnership (not replacement)
- ✨ Magic/enhancement (subtle, not flashy)
- 🎯 Precision (accuracy, reliability)

**Time Savings**: Visual representation
- ⏰ Clock icons for time-related features
- 📊 Charts showing before/after
- 💚 Heart for wellbeing impact

**Workflow Clarity**: Color-coded by type
- 🟢 Green = Automatic (no action needed)
- 🟠 Orange = Approval required (decision point)
- 🔵 Blue = Monitored (informational)

---

## 10. Responsive Design Breakpoints

### Breakpoints

```css
/* Mobile First Approach */
--mobile: 320px;    /* Minimum support */
--tablet: 768px;    /* iPad portrait */
--desktop: 1200px;  /* Standard desktop */
--wide: 1600px;     /* Large desktop */
```

### Layout Behavior

**Mobile (320px - 767px)**:
- Single column layout
- Stack all cards vertically
- Sidebar becomes bottom navigation
- Touch targets: minimum 44px × 44px
- Font sizes: Slightly smaller (90% scale)

**Tablet (768px - 1199px)**:
- Two-column grid for cards
- Sidebar remains visible (can collapse)
- Maintain desktop component sizing
- Touch-friendly tap targets

**Desktop (1200px+)**:
- Full multi-column layouts
- Sidebar always visible (260px)
- Hover states active
- Mouse-optimized interactions

### Grid Adaptation

```css
.grid {
  display: grid;
  gap: 24px;
}

/* Desktop: 2 columns */
@media (min-width: 1200px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}

/* Tablet: 2 columns */
@media (min-width: 768px) and (max-width: 1199px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}

/* Mobile: 1 column */
@media (max-width: 767px) {
  .grid { grid-template-columns: 1fr; }
}
```

---

## 11. Accessibility Guidelines

### WCAG 2.1 AA Compliance

**Color Contrast**:
- Normal text: 4.5:1 minimum ✅
- Large text (18px+): 3:1 minimum ✅
- Interactive elements: Clear focus indicators ✅

**Keyboard Navigation**:
- All interactive elements must be keyboard accessible
- Tab order follows logical flow
- Focus indicators: 2px solid purple outline, 2px offset
- Skip links for main content

**Screen Reader Support**:
- Semantic HTML (nav, main, section, article)
- ARIA labels for icon-only buttons
- Alt text for all images (when used)
- Heading hierarchy (h1 → h2 → h3)

**Focus States**:
```css
:focus {
  outline: 2px solid #667EEA;
  outline-offset: 2px;
}

:focus:not(:focus-visible) {
  outline: none; /* For mouse users */
}

:focus-visible {
  outline: 2px solid #667EEA;
  outline-offset: 2px;
}
```

### Inclusive Design Considerations

**Color Blindness**:
- Don't rely solely on color (use icons + text)
- Red/Green: Add shapes/icons (✓ vs ⚠)
- Blue/Yellow: Ensure sufficient contrast

**Cognitive Accessibility**:
- Clear, simple language
- Progressive disclosure (don't overwhelm)
- Consistent patterns across UI
- Error messages with clear next steps

**Motor Impairments**:
- Large touch targets (44px minimum)
- Generous padding around clickable areas
- Avoid time-based interactions
- Support keyboard shortcuts

---

## 12. Content Guidelines

### Writing Style

**Voice**: Professional yet warm, confident yet humble
**Tone**: Clear, direct, empathetic
**Reading Level**: 8th grade (healthcare context is complex enough)

**Good Examples**:
- ✅ "Your timesheet was submitted automatically"
- ✅ "3 shifts this week"
- ✅ "Credential expires in 14 days"
- ✅ "12.5 hours saved this month"

**Bad Examples**:
- ❌ "Timesheet submission workflow executed successfully"
- ❌ "Rostering schedule for current week period"
- ❌ "Your credential will reach expiration in 14 calendar days"
- ❌ "Optimized 12.5 hours of administrative burden"

### Microcopy

**Button Labels**:
- Action-oriented: "Submit Timesheet" not "Timesheet Submission"
- Short: "Save" not "Save Changes"
- Clear outcomes: "Approve Shift Swap" not just "Approve"

**Status Messages**:
- Success: "✓ Completed • No action needed"
- Pending: "⏸ Pending your approval"
- Monitoring: "ℹ️ FYI • Assistant monitoring progress"

**Empty States**:
- Helpful: "No shifts scheduled yet. Check back tomorrow."
- Actionable: "Start by adding your availability preferences."
- Encouraging: "All caught up! No pending approvals."

### Number Formatting

**Time Savings**: "12.5 hours" (not "12.5h" or "12 hours 30 minutes")
**Percentages**: "28% reduction" (with context: "28% burnout reduction")
**Currency**: "$12.4k/month" (abbreviated for readability)
**Large Numbers**: "247 staff" (not "247 staff members")

---

## 13. Technical Implementation

### CSS Custom Properties

Implement design system with CSS variables:

```css
:root {
  /* Colors */
  --primary-purple: #667EEA;
  --primary-dark: #764BA2;
  --autonomous-green: #10B981;
  --hitl-orange: #F59E0B;
  --hotl-blue: #3B82F6;

  /* Text */
  --text-primary: #1A1A1A;
  --text-secondary: #6B7280;
  --text-tertiary: #9CA3AF;

  /* Borders */
  --border-color: #E5E7EB;

  /* Spacing */
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;

  /* Radius */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 20px;

  /* Shadows */
  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.15);
  --shadow-lg: 0 20px 60px rgba(0, 0, 0, 0.25);
}
```

### Component Naming Convention

Use BEM-inspired naming:

```css
.card { } /* Block */
.card__header { } /* Element */
.card--featured { } /* Modifier */

.button { }
.button--primary { }
.button--secondary { }
.button--ghost { }
```

### Utility Classes

Consider utility-first for spacing/layout:

```css
.mt-4 { margin-top: 16px; }
.p-6 { padding: 24px; }
.rounded-lg { border-radius: 16px; }
.text-primary { color: var(--text-primary); }
```

---

## 14. Brand Applications

### Marketing Materials

**Primary Brand Color**: Purple gradient (#667EEA → #764BA2)
**Photography Style**: Real healthcare workers (diverse, authentic)
**Illustration Style**: Modern, minimal, 2D flat (if used)

### Email Templates

**Header**: Togo Health logo (purple gradient on white)
**Body**: White background, purple accents
**CTA Buttons**: Purple gradient, white text
**Footer**: Light gray background (#F9FAFB)

### Presentation Slides

**Title Slide**: Purple gradient background, white text
**Content Slides**: White background, purple headers
**Data Slides**: Use semantic colors (green/amber/blue)
**Closing Slide**: Purple gradient with CTA

### Social Media

**Profile Image**: "TH" monogram in purple gradient circle
**Cover Images**: Purple gradient with tagline
**Post Graphics**:
- Background: White or purple gradient
- Text: Inter Bold
- Accent: Workflow colors (green/amber/blue)

---

## 15. Brand Do's and Don'ts

### Visual Do's ✅

- Use the purple gradient for primary brand moments
- Maintain consistent border radius (16px for cards)
- Use workflow colors consistently (green/amber/blue)
- Provide clear visual hierarchy with size and weight
- Use whitespace generously—don't cram
- Implement smooth, subtle animations
- Ensure all text meets contrast requirements

### Visual Don'ts ❌

- Don't use colors outside the brand palette
- Don't stretch or distort the logo
- Don't use more than 3 font weights in one view
- Don't create busy backgrounds that reduce readability
- Don't use drop shadows on the logo
- Don't animate without purpose
- Don't sacrifice accessibility for aesthetics

### Content Do's ✅

- Use plain language (avoid jargon)
- Lead with benefits, not features
- Show real numbers (12.5 hours, 28% reduction)
- Explain AI clearly ("automatic assistant" not "ML model")
- Focus on time savings and wellbeing
- Use active voice ("Your assistant submitted...")
- Be specific ("14 days" not "soon")

### Content Don'ts ❌

- Don't use healthcare clichés ("revolutionary," "disruptive")
- Don't make promises you can't keep
- Don't use technical AI jargon with end users
- Don't say "AI" without explaining what it does
- Don't forget the human element
- Don't use passive voice ("was submitted by...")
- Don't be vague ("your credential status has changed")

---

## 16. Future Considerations

### Dark Mode

**Status**: Not yet implemented
**Priority**: High (healthcare workers on night shifts)

**Proposed Colors**:
- Background: `#1A1A1A`
- Card: `#2D2D2D`
- Text: `#F9FAFB`
- Purple: Slightly lighter (#7C8EF5) for better contrast

### Theme Customization

**Per-Hospital Branding**:
- Allow custom accent colors (replaces purple)
- Logo replacement in header
- Maintain workflow colors (green/amber/blue) for consistency

### Localization

**Language Support**: English (primary)
**Future**: Spanish, French, German
**Considerations**:
- Text expansion (German ~30% longer)
- RTL support (Arabic, Hebrew)
- Date/time formats by locale

### Component Library

**Recommendation**: Build Storybook or similar
**Include**:
- All buttons, cards, badges
- Form elements
- Layout components
- Interactive states
- Responsive variants

---

## 17. Quick Reference

### Most Common Patterns

**Primary CTA**:
```css
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
color: white; padding: 12px 24px; border-radius: 10px; font-weight: 600;
```

**Card**:
```css
background: white; border-radius: 16px; padding: 24px; border: 1px solid #E5E7EB;
```

**Success Badge**:
```css
background: #D1FAE5; color: #065F46; padding: 4px 10px; border-radius: 6px; font-weight: 600;
```

**Heading**:
```css
font-size: 24px; font-weight: 700; color: #1A1A1A; margin-bottom: 16px;
```

### Color Quick Copy

```
Brand Purple: #667EEA
Deep Purple: #764BA2
Success Green: #10B981
Warning Amber: #F59E0B
Info Blue: #3B82F6
Text Primary: #1A1A1A
Text Secondary: #6B7280
Border: #E5E7EB
```

### Spacing Quick Copy

```
4px  | 8px  | 12px | 16px | 24px | 32px | 40px | 48px
```

---

## 18. Brand Evolution & Governance

### Design System Ownership

**Maintainer**: Product Design Lead
**Contributors**: Engineering, Product, Marketing
**Review Cadence**: Quarterly
**Version**: 1.0 (Current mockup phase)

### Change Process

1. **Propose**: Submit design change with rationale
2. **Review**: Design team evaluates impact
3. **Prototype**: Create examples in context
4. **Approve**: Stakeholder sign-off
5. **Document**: Update this guide
6. **Implement**: Roll out to codebase
7. **Communicate**: Notify all teams

### Version History

**v1.0** (Current) - Initial design system for investor mockups
- Purple gradient brand identity
- Three workflow type color system
- Inter typography
- Companion vs. Technical language modes

**Future v2.0** - Production-ready system
- Dark mode support
- Component library (Storybook)
- Custom icon set (replace emojis)
- Theme customization framework

---

## Appendix: Files Reference

**Mockup Files**:
- `index.html` - Landing page
- `clinician-dashboard-ai.html` - Technical version
- `clinician-dashboard-companion.html` - User-friendly version
- `admin-dashboard.html` - Technical admin view
- `admin-dashboard-companion.html` - User-friendly admin view
- `mobile-view.html` - Mobile mockup
- `clinician-dashboard.html` - Baseline dashboard
- `clinician-dashboard-alt.html` - Alternative layout

**Documentation**:
- `README.md` - Project overview
- `docs/MULTI_AGENT_WORKFLOWS.md` - Workflow patterns
- `docs/VISUAL_DESIGN_SYSTEM.md` - Design specs
- `docs/PLATFORM_INTEGRATION.md` - Technical integration
- `docs/INVESTOR_PRESENTATION_GUIDE.md` - Presentation guide
- `docs/BRAND_SPRINT_DESIGN_SYSTEM.md` - This document

---

**Last Updated**: October 2025
**Prepared For**: Brand sprint exercises, design handoffs, development implementation
**Contact**: [Design team placeholder]

---

**End of Brand Sprint Design System**
