# Togo Health Visual Design System

## Overview

The Togo Health platform employs a modern, professional design system that balances clinical professionalism with approachability. The visual language is designed to reduce cognitive load for busy healthcare professionals while maintaining investor appeal.

---

## Color Palette

### Primary Brand Colors

**Primary Gradient**
- Purple to Violet: `linear-gradient(135deg, #667EEA 0%, #764BA2 100%)`
- Usage: Brand headers, primary CTAs, hero sections, feature highlights
- Conveys: Innovation, trust, professionalism

**Primary Purple** (#667EEA)
- Usage: Links, active states, accent elements, tags
- Accessibility: AA compliant on white backgrounds

**Deep Purple** (#764BA2)
- Usage: Gradient endpoints, hover states, depth

### Workflow Type Colors

**Autonomous Green** (#10B981)
- Background: `#F0FDF4` (light green)
- Border: `#10B981`
- Text: `#065F46` (dark green)
- Icon background: `#10B981`
- Usage: Completed autonomous agent actions, success states

**Human-in-the-Loop Orange** (#F59E0B)
- Background: `#FFFBEB` (light amber)
- Border: `#F59E0B`
- Text: `#92400E` (dark amber)
- Icon background: `#F59E0B`
- Usage: Pending approval tasks, warning states

**Human-on-the-Loop Blue** (#3B82F6)
- Background: `#EFF6FF` (light blue)
- Border: `#3B82F6`
- Text: `#1E3A8A` (dark blue)
- Icon background: `#3B82F6`
- Usage: Active monitoring tasks, informational states

### Semantic Colors

**Success**: #10B981 (green)
**Warning**: #F59E0B (amber/orange)
**Error**: #EF4444 (red)
**Info**: #3B82F6 (blue)
**Neutral**: #6B7280 (gray)

### Neutral Palette

- **Text Primary**: `#1A1A1A` (near black)
- **Text Secondary**: `#6B7280` (medium gray)
- **Border**: `#E5E7EB` (light gray)
- **Background**: `#F9FAFB` (off-white)
- **White**: `#FFFFFF`

---

## Typography

### Font Family
**Primary**: `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`

Inter is a modern, highly legible sans-serif optimized for digital interfaces. It provides excellent readability at all sizes and weights.

### Type Scale

**Display / Hero**
- Font size: 56px
- Font weight: 700 (Bold)
- Line height: 1.1
- Letter spacing: -1px
- Usage: Landing page logo, major headers

**Heading 1**
- Font size: 32px
- Font weight: 700 (Bold)
- Line height: 1.2
- Usage: Page titles, section headers

**Heading 2**
- Font size: 24px
- Font weight: 700 (Bold)
- Line height: 1.3
- Usage: Card titles, subsection headers

**Heading 3**
- Font size: 20px
- Font weight: 600 (Semi-bold)
- Line height: 1.4
- Usage: Component titles, widget headers

**Body Large**
- Font size: 16px
- Font weight: 400 (Regular)
- Line height: 1.6
- Usage: Primary body text, descriptions

**Body**
- Font size: 14px
- Font weight: 400 (Regular)
- Line height: 1.6
- Usage: Standard body text, labels

**Body Small**
- Font size: 13px
- Font weight: 400 (Regular)
- Line height: 1.5
- Usage: Secondary information, metadata

**Caption**
- Font size: 12px
- Font weight: 400 (Regular)
- Line height: 1.4
- Usage: Timestamps, helper text, tags

**Micro**
- Font size: 11px
- Font weight: 600 (Semi-bold)
- Line height: 1.3
- Usage: Agent task items, compact information

---

## Spacing System

Togo Health uses an 8-point grid system for consistent spacing:

- **4px**: Tight spacing (icon padding, small gaps)
- **8px**: Compact spacing (form field gaps, icon-text spacing)
- **12px**: Standard spacing (tag padding, list item gaps)
- **16px**: Medium spacing (card internal padding, section gaps)
- **24px**: Large spacing (card gaps, section separation)
- **32px**: Extra large spacing (major section padding)
- **48px**: Hero spacing (landing page header margins)

---

## Layout Components

### Cards

**Standard Card**
```css
background: white;
border-radius: 16px;
padding: 24px;
box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
```

**Interactive Card** (hover state)
```css
transform: translateY(-8px);
box-shadow: 0 20px 60px rgba(0, 0, 0, 0.25);
transition: all 0.3s;
```

**AI Agent Card** (featured)
```css
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
border-radius: 20px;
padding: 28px;
color: white;
position: relative;
overflow: hidden;
```

### Glassmorphism Effect

Used for overlays and floating elements:
```css
background: rgba(255, 255, 255, 0.15);
backdrop-filter: blur(10px);
border: 1px solid rgba(255, 255, 255, 0.2);
border-radius: 12px;
```

### Sidebar Navigation

**Width**: 280px
**Background**: White
**Border**: 1px solid #E5E7EB (right edge)
**Item height**: 48px
**Active state**: Purple background (#EEF2FF) with purple text (#667EEA)

### Top Navigation

**Height**: 72px
**Background**: White
**Border**: 1px solid #E5E7EB (bottom edge)
**Logo size**: 32px font size
**Shadow**: 0 1px 3px rgba(0, 0, 0, 0.05)

---

## Iconography

### Icon Style
- **Type**: Emoji-based for mockup clarity
- **Size**:
  - Small: 16px
  - Medium: 24px
  - Large: 48px
  - Hero: 64px

### Icon Usage by Category

**Navigation & System**
- 🏠 Home/Dashboard
- 📊 Analytics/Reports
- ⚙️ Settings
- 👤 Profile
- 🔔 Notifications

**Clinical & Medical**
- 👨‍⚕️ Clinician/Healthcare worker
- 🏥 Hospital/Facility
- 📋 Medical records/Documentation
- 🩺 Clinical work/Patient care
- 💊 Medication/Treatment

**Workflow Types**
- ✓ Autonomous (completed)
- ⏸ Human-in-the-loop (pending)
- ⚡ Human-on-the-loop (active)
- 🤖 AI/Agent
- 🎯 Orchestrator

**Specialized Agents**
- ⏰ Timesheet Agent
- 📜 Credential Agent
- 📅 Rostering Agent
- 🎓 LMS Agent
- 📄 Documentation Agent
- 🔔 Notification Agent
- 🔄 Shift Swap Agent
- 📊 Analytics Agent
- ✅ Compliance Agent

**Status & Actions**
- ✓ Complete/Success
- ⚠️ Warning/Attention needed
- ❌ Error/Failed
- 📤 Upload/Submit
- 📥 Download/Receive

---

## Visual Patterns

### Status Badges

**Completed Badge**
```css
padding: 4px 8px;
background: white;
border-radius: 6px;
color: #065F46;
font-weight: 600;
font-size: 11px;
```
Text: "✓ Completed • No action needed"

**Pending Approval Badge**
```css
padding: 4px 8px;
background: white;
border-radius: 6px;
color: #92400E;
font-weight: 600;
font-size: 11px;
```
Text: "⏸ Pending your approval"

**Active Monitoring Badge**
```css
padding: 4px 8px;
background: white;
border-radius: 6px;
color: #1E3A8A;
font-weight: 600;
font-size: 11px;
```
Text: "⚡ Active • Monitor"

### Agent Activity Cards

**Autonomous Action Card**
```css
display: flex;
gap: 12px;
padding: 14px;
background: #F0FDF4;
border-left: 3px solid #10B981;
border-radius: 8px;
```

**Human-in-the-Loop Card**
```css
display: flex;
gap: 12px;
padding: 14px;
background: #FFFBEB;
border-left: 3px solid #F59E0B;
border-radius: 8px;
```

**Human-on-the-Loop Card**
```css
display: flex;
gap: 12px;
padding: 14px;
background: #EFF6FF;
border-left: 3px solid #3B82F6;
border-radius: 8px;
```

### Stat Cards

**Metric Display**
```css
font-size: 36px;
font-weight: 700;
color: #1A1A1A;
margin-bottom: 8px;
```

**Metric Label**
```css
font-size: 14px;
color: #6B7280;
```

**Trend Indicator**
```css
font-size: 12px;
color: #10B981; /* Green for positive trends */
font-weight: 600;
```

---

## Interactive Elements

### Buttons

**Primary Button**
```css
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
color: white;
padding: 12px 24px;
border-radius: 10px;
font-weight: 600;
font-size: 14px;
border: none;
cursor: pointer;
transition: transform 0.2s;
```

**Hover state**:
```css
transform: translateY(-2px);
box-shadow: 0 8px 20px rgba(102, 126, 234, 0.3);
```

**Secondary Button**
```css
background: white;
color: #667EEA;
padding: 12px 24px;
border-radius: 10px;
font-weight: 600;
font-size: 14px;
border: 2px solid #667EEA;
cursor: pointer;
```

**Ghost Button**
```css
background: transparent;
color: #6B7280;
padding: 8px 16px;
border-radius: 8px;
font-weight: 500;
font-size: 14px;
border: 1px solid #E5E7EB;
cursor: pointer;
```

### Links

**Text Link**
```css
color: #667EEA;
text-decoration: none;
font-weight: 500;
```

**Hover**:
```css
text-decoration: underline;
color: #764BA2;
```

### Form Elements

**Input Field**
```css
padding: 12px 16px;
border: 1px solid #E5E7EB;
border-radius: 8px;
font-size: 14px;
font-family: 'Inter', sans-serif;
```

**Focus State**:
```css
border-color: #667EEA;
outline: none;
box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
```

---

## Animation & Motion

### Transitions

**Standard Transition**
```css
transition: all 0.3s ease;
```

**Quick Transition** (hover feedback)
```css
transition: transform 0.2s ease;
```

**Slow Transition** (large movements)
```css
transition: all 0.5s ease-in-out;
```

### Hover Effects

**Card Lift**
```css
transform: translateY(-8px);
```

**Button Lift**
```css
transform: translateY(-2px);
```

**Scale on Hover** (icons)
```css
transform: scale(1.1);
```

---

## Responsive Breakpoints

**Desktop**: 1200px and above
**Tablet**: 768px - 1199px
**Mobile**: 320px - 767px

### Responsive Grid

**Desktop**: 2-column grid for cards
```css
grid-template-columns: repeat(2, 1fr);
gap: 24px;
```

**Mobile**: Single column
```css
@media (max-width: 768px) {
  grid-template-columns: 1fr;
}
```

---

## Accessibility

### Color Contrast

All text meets WCAG 2.1 AA standards:
- **Normal text** (14px+): 4.5:1 contrast ratio minimum
- **Large text** (18px+): 3:1 contrast ratio minimum
- **Interactive elements**: Clear focus states with 3:1 contrast

### Focus States

All interactive elements have visible focus indicators:
```css
outline: 2px solid #667EEA;
outline-offset: 2px;
```

### Semantic HTML

- Proper heading hierarchy (h1 → h2 → h3)
- ARIA labels for icon-only buttons
- Semantic tags (nav, main, section, article)

---

## Mobile-Specific Design

### iPhone Frame Mockup

**Device**: iPhone 14 Pro dimensions
**Frame background**: `#1A1A1A` (dark gray)
**Screen background**: White
**Corner radius**: 40px (outer frame)
**Notch**: Centered at top

### Mobile Navigation

**Bottom Tab Bar**
```css
height: 72px;
background: white;
border-top: 1px solid #E5E7EB;
position: fixed;
bottom: 0;
```

**Tab Item**
```css
font-size: 12px;
color: #6B7280;
```

**Active Tab**
```css
color: #667EEA;
font-weight: 600;
```

### Mobile Touch Targets

Minimum touch target size: **44px × 44px** (Apple HIG standard)

---

## Brand Elements

### Logo Lockup

**Togo Health Wordmark**
- Font: Inter Bold (700)
- Size: 56px (hero), 32px (nav), 24px (compact)
- Letter spacing: -1px (hero), -0.5px (nav)
- Color: White on gradient, Purple (#667EEA) on white

### Tagline

**"Unified Clinical Workforce Management Platform"**
- Font: Inter Regular (400)
- Size: 20px
- Opacity: 0.95
- Used on landing page and marketing materials

### AI Enhancement Badge

For AI-powered features:
```css
padding: 4px 10px;
background: linear-gradient(135deg, #667EEA 0%, #764BA2 100%);
color: white;
border-radius: 6px;
font-size: 10px;
font-weight: 700;
```
Text: "✨ AI POWERED"

---

## Design Principles

### 1. Clarity Over Cleverness
Healthcare professionals need information quickly. Every element serves a clear purpose.

### 2. Progressive Disclosure
Show essential information first, details on demand. Avoid overwhelming busy clinicians.

### 3. Consistent Patterns
Similar elements behave similarly. Workflow types have consistent color coding across all views.

### 4. Trust Through Design
Professional aesthetics, proper spacing, and attention to detail build confidence in the platform.

### 5. Mobile-First Mindset
Even desktop views consider the reality of clinicians accessing data on-the-go.

---

## Implementation Notes

### CSS Custom Properties

For consistency across mockups:
```css
:root {
  --primary-purple: #667EEA;
  --primary-dark: #764BA2;
  --autonomous-green: #10B981;
  --hitl-orange: #F59E0B;
  --hotl-blue: #3B82F6;
  --text-primary: #1A1A1A;
  --text-secondary: #6B7280;
  --border-color: #E5E7EB;
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 20px;
  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.15);
  --shadow-lg: 0 20px 60px rgba(0, 0, 0, 0.25);
}
```

### Future Considerations

When building the production app:
- Consider dark mode variant (important for night shift workers)
- Implement theme customization per hospital/organization
- Ensure all animations respect `prefers-reduced-motion`
- Support high contrast mode for accessibility
