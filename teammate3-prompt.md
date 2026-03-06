# PathSight Dashboard - Teammate 3: Business Logic & Interactive Panels

## Your Role: JavaScript Logic & Interactive Features
You are responsible for the summary metrics cards, attack simulation system, prevention recommendations, and counterfactual analysis controls that make the dashboard interactive and intelligent.

## Product Overview

**Product Name:** PathSight
**Tagline:** "From Risk to Reality — See when an attack path becomes a real attack."

**Concept:** A modern SaaS cloud security dashboard that visualizes when theoretical attack paths become active attacks. Your role is to build the interactive intelligence that makes this tool useful for security teams.

**Business Context:**
- Security teams discover attack paths but struggle to prioritize them
- Most attack paths are theoretical - only some become real attacks
- Your components help teams understand risk realization and prevention

## Your Specific Components

### 1. Summary Metrics Cards
Create 4 interactive cards displaying key metrics:

**Card 1: Attack Path Age**
- Value: 92 days
- Subtitle: "Time since discovery"
- Visual: Subtle orange glow (indicates growing risk with time)

**Card 2: Runtime Signals Detected**
- Value: 3
- Subtitle: "Active attack indicators"
- Visual: Red glow with pulse animation

**Card 3: Likely Compromised Resources**
- Value: 1
- Subtitle: "Resources under attack"
- Visual: Red glow

**Card 4: Attack Realization Score**
- Value: 92%
- Subtitle: "Probability of active exploitation"
- Visual: Strong red glow

**Requirements:**
- Cards should glow based on risk level
- Smooth animations when values update
- Hover effects showing additional context
- Responsive grid layout

**Container:** `#metrics-cards-container`
**Data Source:** `attackPathData.metrics` (from Teammate 1)

### 2. Attack Simulation System
Create the core playback functionality:

**"Play Attack Simulation" Button:**
- Prominent call-to-action button
- Smooth hover and click states
- Disabled state during playback

**Simulation Logic:**
1. Step through timeline events chronologically
2. Trigger visual updates in attack path (via Teammate 2)
3. Update progress meter stages
4. Highlight "Point of No Return" moment
5. Update metrics in real-time
6. Provide play/pause/reset controls

**Event Timing:**
```javascript
const simulationSequence = [
  {delay: 0, event: 'discovery', action: () => highlightTimelineEvent('discovery')},
  {delay: 1000, event: 'risk1', action: () => updateAttackPathNode('ec2', 'risk')},
  {delay: 2000, event: 'risk2', action: () => updateAttackPathNode('imds', 'risk')},
  {delay: 3000, event: 'ssrf', action: () => showPointOfNoReturn()},
  {delay: 3500, event: 'malware', action: () => updateAttackPathNode('ec2', 'compromised')},
  {delay: 4000, event: 's3access', action: () => updateAttackPathNode('s3', 'accessed')}
];
```

**Container:** `#simulation-controls`

### 3. Missed Prevention Opportunities Panel
Display actionable security recommendations:

**Panel Title:** "Missed Prevention Opportunities"

**Recommendations List:**
- ✗ Disable IMDSv1
- ✗ Restrict IAM role permissions
- ✗ Patch exposed EC2 instance
- ✗ Remove public EC2 exposure

**Requirements:**
- Clean list design with red X indicators
- Each item shows implementation difficulty and impact
- Hover effects with detailed explanations
- Professional styling matching SaaS aesthetics

**Container:** `#prevention-panel`
**Data Source:** `attackPathData.preventionOpportunities`

### 4. Counterfactual Analysis Panel
Interactive "what-if" analysis tool:

**Panel Title:** "Break the Attack Path"

**Interactive Controls:**
Each control shows:
- Control name (e.g., "Disable IMDSv1")
- Toggle switch (on/off)
- Impact description ("Stops credential theft step")
- Risk reduction ("92% → 12%")

**When toggled ON:**
- Update Attack Realization Score
- Visually break the attack path at that point
- Show updated risk metrics
- Highlight which attack steps are prevented

**Example Controls:**
```javascript
const counterfactualControls = [
  {
    id: 'disable_imdsv1',
    name: 'Disable IMDSv1',
    impact: 'Stops credential theft step',
    riskReduction: '92% → 12%',
    breaksPath: ['imds', 'iam', 's3']
  },
  {
    id: 'network_segmentation',
    name: 'Network Segmentation',
    impact: 'Blocks initial access',
    riskReduction: '92% → 8%',
    breaksPath: ['internet', 'ec2', 'imds', 'iam', 's3']
  }
];
```

**Container:** `#counterfactual-panel`

### 5. State Management System
Coordinate all interactive elements:

```javascript
class PathSightState {
  constructor() {
    this.isSimulating = false;
    this.currentStep = 0;
    this.activeControls = new Set();
    this.metrics = {...attackPathData.metrics};
  }

  startSimulation() {
    // Coordinate with Teammate 2's visualizations
    // Update metrics in real-time
    // Manage playback state
  }

  toggleControl(controlId) {
    // Update counterfactual analysis
    // Recalculate risk scores
    // Trigger visualization updates
  }

  updateMetrics(newMetrics) {
    // Smooth transitions for card values
    // Trigger glow effects based on risk levels
  }
}
```

### 6. Dynamic Risk Calculation
Implement intelligent risk scoring:

**Base Risk Factors:**
- Attack path age (older = higher risk)
- Number of runtime signals
- Ease of exploitation
- Impact of compromise

**Risk Reduction Logic:**
When counterfactual controls are enabled:
- Calculate which attack steps are prevented
- Update realization score accordingly
- Show visual feedback in metrics cards

## Technical Integration

### Events to Dispatch:
```javascript
// For Teammate 2's visualizations
const events = {
  simulationStart: new CustomEvent('startAttackSimulation'),
  simulationStep: new CustomEvent('simulationStep', {detail: {step, nodeId, status}}),
  controlToggled: new CustomEvent('controlToggled', {detail: {controlId, enabled}})
};
```

### API for Visual Integration:
```javascript
// Functions that Teammate 2 will implement
const visualAPI = {
  updateAttackPathStatus: (nodeId, status) => {},
  highlightTimelineEvent: (eventId) => {},
  animateProgressMeter: (stage) => {},
  showPointOfNoReturn: () => {}
};
```

## Interactive Features

### Glow Effects for Cards:
```css
.metric-card.high-risk {
  box-shadow: var(--glow-danger);
  animation: pulse-glow 2s infinite;
}

.metric-card.medium-risk {
  box-shadow: 0 0 15px rgba(245,158,11,0.4);
}
```

### Smooth Value Transitions:
Animate metric changes with CountUp.js-style effects:
```javascript
function animateMetricChange(element, oldValue, newValue, duration = 1000) {
  // Smooth number transitions
  // Color transitions for risk level changes
}
```

## Coordination with Teammates

**With Teammate 1:**
- Use provided mock data structure
- Follow CSS variable system for consistent styling
- Ensure proper responsive behavior

**With Teammate 2:**
- Coordinate animation timing for smooth user experience
- Provide clear events for visualization updates
- Sync simulation playback with visual effects

## Deliverable
Your JavaScript code should provide:
- Interactive metrics cards with dynamic risk indicators
- Smooth attack simulation playback system
- Intelligent counterfactual analysis with risk recalculation
- Professional user interactions and state management
- Seamless integration with visualization components

## Technical Requirements
- Vanilla JavaScript (no frameworks)
- Smooth 60fps animations for metrics updates
- Proper event handling and state management
- Mobile-friendly touch interactions
- Error handling and edge cases covered

Focus on creating intelligent, responsive interactions that make security professionals feel like they're using a cutting-edge cloud security platform!