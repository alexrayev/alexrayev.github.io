# Alexander Rayev: Portfolio

Principal Software Engineer · Cloud, Kubernetes and AI platform architect

Hands-on full-stack software architect specialising in developer-first cloud platforms and large-scale distributed systems: the APIs, CI/CD pipelines, observability and infrastructure that let engineering teams ship and scale. Details are generalised; diagrams are simplified and illustrative. All information provided here is public.

**Site:** https://alexrayev.github.io/ · **Resume:** [PDF](docs/Alexander-Rayev-Resume.pdf) · **Email:** arayev@yahoo.com

## Selected projects

| Project | Summary |
| --- | --- |
| [Adaptive ML Kube: Universal Deployment Platform](projects/adaptive-ml-kube.html) | Cloud-agnostic Kubernetes platform for ML workloads, delivered to AWS EKS and to air-gapped customer clusters with a Go installer. Live product: [Infineon/amk, latest release 0.1.2](https://github.com/Infineon/amk/tree/main/0.1.2). |
| [Adaptive ML Cloud Platform](projects/adaptive-ml-cloud.html) | Elastic, API-first ML platform on AWS: 1 to 20 workers, 45 ms audio processing, sub-100 ms APIs, 60–85% lower cost. |
| [DEEPCRAFT Voice Assistant: Production AWS Architecture](projects/deepcraft-voice-assistant.html) | Multi-AZ AWS stack deployed as code with the AWS CDK (TypeScript). Live product: [deepcraft-voice-assistant.infineon.com](https://deepcraft-voice-assistant.infineon.com/welcome). |
| [Rational AI: Agents for the Software Lifecycle](projects/rational-ai.html) | Generative-AI platform where specialised agents own each lifecycle phase. |
| [Digital-Controller Configuration GUI Refactor](projects/controller-configuration-gui.html) | Angular monolith refactored into reusable libraries with a better UX. |
| [CAPSENSE Studio: Qt Edition](projects/capsense-studio-qt.html) | Capacitive-sensing tuning tool: Qt 6 QML over a C++ core, live tuning on real hardware over UART and EzI2C. |
| [CAPSENSE Studio: WPF Edition](projects/capsense-studio-wpf.html) | Zero-dependency .NET 10 WPF/MVVM tuning GUI with a built-in telemetry simulator. |
| [Low-Power Wake-Word ML Pipeline: Optimization](projects/wake-word-ml-pipeline.html) | Fixed an inherited wake-word training pipeline: 130 to 34 GB peak data-prep memory, 50% faster GPU model training, same model quality. |
| [KAK Process and Keisan Quality Metrics](projects/keisan-quality-process.html) | Development process blending Kaizen, Agile and RUP, plus an automated daily quality pipeline feeding team dashboards. |
| [Medical-Device Software: Laser Lithotripsy and Remote Consultation](projects/medical-device-software.html) | Cross-platform laser lithotripsy system (C++ Qt, QML, ZeroMQ, MongoDB) that shortened procedures from sixty to forty minutes, and an Angular client for remote doctor consultations. |

Project descriptions are generalised and the diagrams are simplified and illustrative. No internal screenshots, hostnames or identifiers are shown.

## Repository layout

```
index.html              Landing page
projects/               One case study per project
assets/                 Styles and AWS architecture icons
docs/                   Resume (PDF)
```

The site is plain static HTML and CSS, so there is no build step.

## Credits

AWS Architecture Icons are © Amazon Web Services and are used only to illustrate architecture diagrams.
