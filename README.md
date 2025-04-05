# 🔍 DIGITAL SURVEILLANCE SIMULATION

![Cyberpunk Interface Screenshot](demo-screenshot.png)

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
Advanced Techniques
Method	Detection Capability	Real-world Use
Canvas Fingerprinting	94% device recognition rate	Ad tracking
WebGL Rendering	GPU model identification	Bot detection
AudioContext Analysis	Hardware-level fingerprint	Fraud prevention
Font Enumeration	Installed software profiling	Target marketing
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

