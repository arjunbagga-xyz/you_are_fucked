# 🔍 DIGITAL SURVEILLANCE SIMULATION

*A live demonstration of how minimal browser interactions can reveal startling amounts of personal data*

## 🌐 Overview
A self-contained browser simulation showcasing modern web tracking capabilities. This **client-side only** experience reveals:

- How 30 seconds of typing/mouse movements can estimate your:
  - Age range (±5 years)
  - Stress levels
  - Technical proficiency
- What device/network fingerprints you're leaking right now
- How attackers could weaponize these insights

**Warning:** While this is a safe simulation, these techniques are used daily by adtech and malicious actors.

## 🚀 Key Features

### Behavioral Tracking
- ⌨️ Keystroke dynamics (speed, rhythm, backspacing)
- 🖱️ Mouse/touch kinematics (velocity, precision, idle time)
- 📜 Scroll depth analysis (attention mapping)
- ⏱️ Micro-interaction timing (cognitive load estimation)

### Device Fingerprinting
- 💻 Hardware profiling (CPU cores, GPU, RAM)
- 🌐 Network characteristics (connection type, latency)
- 🖥️ Software environment (OS, browser, fonts)
- 🕵️ Cross-browser tracking techniques

### Threat Simulation
- 🔮 Psychological profiling
- ⚠️ Vulnerability assessment
- 🎯 Attack vector suggestions

## 💻 Technology Deep Dive

### Core Tracking Mechanisms
```javascript
// Multi-modal behavior capture
const telemetry = {
  keystrokes: [], // [{"key":"a","timestamp":1712345678,"elapsed":120}]
  movements: [],  // {"x":154,"y":892,"velocity":480,"type":"mousemove"}
  scrollPath: []  // [{"y":0,"time":0},{"y":400,"time":1200}]
};

// Real-time inference engine
function assessRiskProfile() {
  const motorControl = calculateMovementVariance();
  const typingPattern = analyzeKeyIntervals();
  return {
    age: motorControl > 300 ? "15-25" : "25-40",
    stress: typingPattern.jitter > 200 ? "High" : "Normal"
  };
}
```
### Keylogging
```
const keyMetadata = {
  timings: [], // Stores [keyCode, timestamp, elapsedSinceLastKey]
  pressure: 0, // Estimated via keydown-keyup delta (touch devices)
  commonPatterns: {
    backspaceSequences: 0,
    copyPasteMarkers: 0
  }
};

document.addEventListener('keydown', (e) => {
  const now = performance.now(); // High-precision timing
  const lastKeyInterval = now - (keyMetadata.timings.slice(-1)[0]?.timestamp || now);
  
  // Detect copy-paste patterns (CTRL+V interval <15ms)
  if (e.ctrlKey && e.key === 'v') {
    keyMetadata.commonPatterns.copyPasteMarkers++;
  }
  
  keyMetadata.timings.push({
    key: e.key,
    code: e.code,
    timestamp: now,
    interval: lastKeyInterval
  });
  
  // Stress calculation (jitter detection)
  const intervals = keyMetadata.timings.map(k => k.interval);
  const stressScore = Math.stddev(intervals) * 10; // Higher deviation = more stress
});
```
### pointer Fingerprinting
```
const pointerProfile = {
  pathSegments: [],
  currentTrajectory: null,
  deviceClass: null // 'mouse'|'touch'|'stylus'
};

document.addEventListener('mousemove', (e) => {
  const { movementX, movementY } = e;
  const velocity = Math.hypot(movementX, movementY) / 
    (performance.now() - pointerProfile.lastSampleTime);
  
  pointerProfile.pathSegments.push({
    x: e.clientX,
    y: e.clientY,
    t: e.timeStamp,
    v: velocity,
    // Detect motor control patterns
    isMicrocorrection: velocity > 500 && Math.hypot(movementX, movementY) < 3
  });
  
  // Classify input device type
  if (!pointerProfile.deviceClass) {
    pointerProfile.deviceClass = detectInputType(e);
  }
});

function detectInputType(e) {
  // Touch devices fire mouse events with width=height=1
  if (e.width === 1 && e.height === 1) return 'touch';
  // Graphics tablets report pressure
  if (typeof e.pressure === 'number' && e.pressure !== 0.5) return 'stylus';
  return 'mouse';
}
```
### Advanced Fingerprinting Techniques
Canvas Fingerprinting (Silent Device ID)
```

function generateCanvasFingerprint() {
  const canvas = document.createElement('canvas');
  canvas.width = 200;
  canvas.height = 50;
  const ctx = canvas.getContext('2d');
  
  // GPU-rendered text with subtle variations
  ctx.textBaseline = 'alphabetic';
  ctx.fillStyle = '#f60';
  ctx.fillRect(0, 0, 200, 50);
  ctx.fillStyle = '#069';
  ctx.font = '18pt Arial';
  ctx.fillText('CanvasFingerprint@1.0', 2, 40);
  
  // Add subtle noise
  for (let i = 0; i < 20; i++) {
    ctx.strokeStyle = `rgba(100,100,100,${Math.random()*0.2})`;
    ctx.beginPath();
    ctx.moveTo(Math.random()*200, Math.random()*50);
    ctx.lineTo(Math.random()*200, Math.random()*50);
    ctx.stroke();
  }
  
  // Extract rendering artifacts
  return canvas.toDataURL().hashCode();
}
```
AudioContext Fingerprinting
```
async function getAudioFingerprint() {
  const audioContext = new (window.AudioContext || window.webkitAudioContext)();
  const oscillator = audioContext.createOscillator();
  const analyser = audioContext.createAnalyser();
  
  oscillator.connect(analyser);
  analyser.connect(audioContext.destination);
  oscillator.start();
  
  // Capture DSP processing nuances
  const frequencyData = new Uint8Array(analyser.frequencyBinCount);
  analyser.getByteFrequencyData(frequencyData);
  
  oscillator.stop();
  await audioContext.close();
  
  // Hash the frequency response pattern
  return hashArray(frequencyData);
}
```
Behavioral Inference Algorithms
```
function estimateAge(behaviorData) {
  // Feature extraction
  const features = {
    typingSpeedVariability: calculateTypingJitter(),
    pointerPrecision: calculateMovementSmoothness(),
    scrollDepth: getScrollEngagement(),
    inputSwitchFrequency: countInputMethodChanges()
  };
  
  // Simple decision tree (real systems use ML models)
  if (features.pointerPrecision < 0.2 && 
      features.typingSpeedVariability > 300) {
    return { ageRange: "18-25", confidence: 0.72 };
  } 
  else if (features.scrollDepth > 0.8 && 
           features.inputSwitchFrequency < 2) {
    return { ageRange: "25-40", confidence: 0.68 };
  }
  return { ageRange: "40+", confidence: 0.65 };
}

function calculateCognitiveLoad() {
  const metrics = {
    keyPressDuration: median(keyTimings.map(k => k.duration)),
    mouseClickLatency: getClickResponseTimes(),
    errorRate: keyMetadata.commonPatterns.backspaceSequences / 
               keyMetadata.timings.length
  };
  
  // Weighted stress score
  return (
    0.4 * normalize(metrics.keyPressDuration, [50, 200]) +
    0.3 * normalize(metrics.mouseClickLatency, [100, 500]) +
    0.3 * normalize(metrics.errorRate, [0.05, 0.2])
  ).toFixed(2);
}
```


Privacy Safeguards
🔒 Zero network calls (verify via DevTools)

🗑️ Data self-destructs after analysis

📜 Open-source code for auditability

⏹️ Hardcoded limits on data collection


⚠️ Ethical Considerations
What This Demonstrates
How basic web APIs can become surveillance tools

Why fingerprinting resistance matters in browsers

The psychological signals leaked through UI interactions

What This Doesn't Do
❌ No actual data collection

❌ No persistent tracking

❌ No external communications


� Educational Value
Perfect for teaching:

Privacy advocates: Shows tangible tracking risks

Developers: Exposes powerful (and scary) browser APIs

Security teams: Demonstrates attack surface areas

Psychologists: Reveals behavioral biometrics

Includes real-world parallels:

How adtech segments users

How phishing attacks are personalized

Why VPNs alone don't prevent fingerprinting

📜 License
MIT License - Free for educational use. Commercial use prohibited.

Remember: This simulation shows just 10% of what's technically possible.
Always audit your browser permissions and extensions.

