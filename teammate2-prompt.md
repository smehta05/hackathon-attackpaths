# PathSight Dashboard - Teammate 2: Visualizations & Interactive Components

## Your Role: Visual Design & Animation Specialist
You are responsible for creating the attack path visualization, timeline view, progress indicators, and all visual animations that bring the security data to life.

## Product Overview

**Product Name:** PathSight
**Tagline:** "From Risk to Reality — See when an attack path becomes a real attack."

**Concept:** A modern SaaS cloud security dashboard that visualizes when theoretical attack paths become active attacks. Your visualizations are the core of the user experience - they need to be both beautiful and informative.

**Design Style:**
- Dark mode security operations dashboard with subtle glows
- SVG-based visualizations with smooth animations
- Color-coded risk indicators (red=danger, orange=warning, blue=info)
- Smooth transitions and micro-interactions
- Professional enterprise security tool aesthetic

## Your Specific Components

### 1. Attack Path Visualization
Create a vertical flow diagram showing the attack progression:

```
Internet
   ↓
EC2 Instance
   ↓
Instance Metadata Service (IMDS)
   ↓
IAM Role
   ↓
Sensitive S3 Bucket
```

**Requirements:**
- SVG-based nodes and connections
- Nodes change color based on attack status:
  - Gray: Normal
  - Orange: At Risk
  - Red: Compromised/Exploited
- Smooth color transitions when status changes
- Clean connecting lines with arrow indicators
- Hover effects showing additional details
- Responsive sizing

**Container:** `#attack-path-container`
**Data Source:** `attackPathData.attackPath` (from Teammate 1)

### 2. Timeline Visualization
Create a horizontal timeline showing the attack lifecycle:

**Timeline Events:**
- Jan 10: Attack path discovered
- Jan 18: IAM privilege escalation risk detected
- Feb 2: Sensitive S3 bucket reachable from instance role
- Apr 14 10:02: SSRF attempt against IMDSv1
- Apr 14 10:05: Malware detected on EC2 instance
- Apr 14 10:07: S3 object access attempt using instance role

**Requirements:**
- Horizontal timeline with date markers
- Different visual styles for different event types:
  - Discovery events: Blue dots
  - Risk events: Orange triangles
  - Attack events: Red diamonds
- "Point of No Return" marker at SSRF attempt (large red indicator)
- Tooltips showing event details on hover
- Smooth scrolling/panning for long timelines
- Responsive design that works on mobile

**Container:** `#timeline-container`
**Data Source:** `attackPathData.timeline` (from Teammate 1)

### 3. Point of No Return Marker
Special visual treatment for the critical moment:

```
POINT OF NO RETURN – attacker gained cloud credentials
```

- Prominent red warning indicator
- Animated glow effect
- Clear visual connection to timeline and attack path
- Explanatory text about why this moment is critical

### 4. Attack Progress Meter
Visual progress bar showing attack stages:

```
Exposure Identified → Exploit Attempt → Credential Compromise → Data Access
```

**Requirements:**
- Horizontal progress bar with 4 distinct stages
- Fill animation as attack progresses
- Stage labels with icons
- Color progression from blue → orange → red
- Smooth transitions during playback

**Container:** `#progress-meter-container`

### 5. Animation System for Attack Playback
When "Play Attack Simulation" is triggered:

**Sequence:**
1. Highlight timeline events in chronological order
2. Update attack path nodes as they're compromised
3. Fill progress meter stages
4. Show glowing effects on compromised components
5. Display "Point of No Return" marker with emphasis

**Animation Timing:**
- 500ms between timeline events
- 300ms node color transitions
- Smooth easing functions (ease-in-out)
- Coordinated with Teammate 3's business logic

### 6. Visual Polish & Effects
- Subtle glow effects around high-risk components
- Smooth hover states and micro-interactions
- Professional shadows and depth
- Consistent visual hierarchy
- Smooth loading animations

## Technical Specifications

### Color Coding System
Use these CSS variables (provided by Teammate 1):
```css
--danger-red: #ef4444;
--warning-orange: #f59e0b;
--success-green: #10b981;
--accent-blue: #3b82f6;
--glow-danger: 0 0 20px rgba(239,68,68,0.3);
```

### Animation Guidelines
```css
/* Standard transitions */
.smooth-transition { transition: all 0.3s ease-in-out; }

/* Glow effects for compromised nodes */
.compromised {
  box-shadow: var(--glow-danger);
  animation: pulse-glow 2s infinite;
}

@keyframes pulse-glow {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.7; }
}
```

### SVG Structure Example
```html
<svg id="attack-path-svg" viewBox="0 0 400 600">
  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto">
      <polygon points="0 0, 10 3, 0 6" fill="#666"/>
    </marker>
  </defs>

  <!-- Attack path nodes -->
  <g id="attack-nodes">
    <!-- Nodes will be dynamically styled based on status -->
  </g>

  <!-- Connecting lines -->
  <g id="attack-connections">
    <!-- Lines with arrow markers -->
  </g>
</svg>
```

## JavaScript Integration Points

### Events to Listen For:
```javascript
// From Teammate 3 - simulation controls
document.addEventListener('startAttackSimulation', handleSimulationStart);
document.addEventListener('simulationStep', handleSimulationStep);
document.addEventListener('simulationComplete', handleSimulationComplete);

// From Teammate 3 - counterfactual changes
document.addEventListener('controlToggled', updateVisualization);
```

### Functions to Expose:
```javascript
// For Teammate 3 to trigger animations
window.visualizationAPI = {
  updateAttackPathStatus: (nodeId, status) => {},
  highlightTimelineEvent: (eventId) => {},
  animateProgressMeter: (stage) => {},
  showPointOfNoReturn: () => {},
  resetVisualization: () => {}
};
```

## Coordination with Teammates

**With Teammate 1:**
- Use provided CSS variables and spacing
- Ensure visualizations fit within allocated containers
- Follow established responsive breakpoints

**With Teammate 3:**
- Coordinate on animation timing and event handling
- Provide visual feedback for business logic changes
- Ensure smooth integration with simulation playback

## Deliverable
Your JavaScript and CSS code should:
- Create stunning, interactive visualizations
- Integrate seamlessly with the foundation layout
- Respond to business logic events from Teammate 3
- Work smoothly on desktop and mobile
- Look professional and polished for demo

## Technical Requirements
- Pure SVG and CSS (no external charting libraries)
- Smooth 60fps animations
- Touch-friendly on mobile devices
- Accessible with proper ARIA labels
- Performance optimized for real-time updates

Focus on creating visualizations that are both beautiful and functional - they're the star of the demo!