# Awesome Mobile On-Device AI Security

<p align="center">
  <img src="https://img.shields.io/badge/Companion%20Resource%20for-SoK%20on%20MoAI%20Security-2563EB?style=for-the-badge" height="28" align="absmiddle" />
</p>

<h2 align="center">SoK: Attack and Defense Landscape of Mobile On-device AI Systems</h3>

<p align="center">
  <b>Yujin Huang, Xin Zheng, Xingliang Yuan, Kwok-Yan Lam</b><br><br>
  <a href="https://arxiv.org/pdf/2607.00362">
    <img src="https://img.shields.io/badge/Paper-arXiv%3A2607.00362-B31B1B?style=flat" height="22" align="absmiddle" />
  </a>
</p>

Mobile on-device AI systems execute AI models locally through ML frameworks such as **LiteRT/TFLite**, **Core ML**, **ExecuTorch**, **ONNX**, and hardware-backed accelerators. This repo tracks the security research needed to understand and protect such systems, as the local storage of on-device models introduces new security risks.

## Overview of a Mobile On-Device AI system
<p align="center">
  <img src="figures/moai_system.jpg" alt="Overview of a Mobile On-Device AI system">
</p>

## Contents

- [Reading roadmap](#reading-roadmap)
- [Taxonomy at a glance](#taxonomy-at-a-glance)
- [Cross-pillar Security Analysis](#cross-pillar-security-analysis)
- [Attacks on MoAI systems](#attacks-on-moai-systems)
  - [Adversarial Attacks](#adversarial-attacks)
    - [Model Similarity Exploitation](#model-similarity-exploitation)
    - [Gradient Reconstruction](#gradient-reconstruction)
    - [Preprocessing Manipulation](#preprocessing-manipulation)
  - [Backdoor Attacks](#backdoor-attacks)
    - [Payload Injection](#payload-injection)
    - [Model Quantization](#model-quantization)
    - [Image Steganography](#image-steganography)
  - [Adversarial Weight Attacks](#adversarial-weight-attacks)
  - [Model Stealing Attacks](#model-stealing-attacks)
    - [Static Analysis](#static-analysis)
    - [Dynamic Analysis](#dynamic-analysis)
    - [Side Channel](#side-channel)
  - [Energy-latency Attacks](#energy-latency-attacks)
- [Defenses for MoAI systems](#defenses-for-moai-systems)
  - [Model Obfuscation](#model-obfuscation)
    - [Software-level Concealment](#software-level-concealment)
    - [Hardware-level Concealment](#hardware-level-concealment)
  - [Model Authorization](#model-authorization)
  - [Trusted Execution Environments](#trusted-execution-environments)
    - [Monolithic Execution](#monolithic-execution)
    - [Partitioned Execution](#partitioned-execution)
    - [Obfuscated Offloading](#obfuscated-offloading)
  - [Model Watermarking](#model-watermarking)
- [Open problems](#open-problems)
- [Emerging directions](#emerging-directions)

## Reading roadmap

New to MoAI security? Start here:

1. **Understand the ecosystem.** Read empirical studies on deep learning apps and on-device models in Android/iOS apps.
2. **Learn the core risk.** Study model extraction and model protection papers, because local model residency is the central security shift in MoAI systems.
3. **Understand the attack surfaces.** Study how MoAI attacks arise across input interfaces, model artifacts, runtime execution, and hardware-backed environments.
4. **Connect defenses to the surfaces.** Examine how MoAI defenses protect these surfaces across pre-deployment, runtime execution, and post-deployment phases.
5. **Look forward.** Explore new security challenges in on-device training, on-device GenAI, and agentic MoAI systems.



<img src="https://img.shields.io/badge/-A%20minimal%20first--week%20reading%20path%20for%20newcomers%20to%20MOAI%20security-2563EB?style=for-the-badge" height="28" align="absmiddle" alt="A minimal first-week reading path for newcomers to MOAI security." />

<img src="https://img.shields.io/badge/Ecosystem-4C78A8?style=flat" height="22" align="absmiddle" /><br>
• <img src="https://img.shields.io/badge/Android-6B7280?style=flat" height="18" align="absmiddle" />&nbsp;[A First Look at Deep Learning Apps on Smartphones](https://arxiv.org/pdf/1812.05448)  
• <img src="https://img.shields.io/badge/iOS-6B7280?style=flat" height="18" align="absmiddle" />&nbsp;[A First Look at On-device Models in iOS Apps](https://arxiv.org/pdf/2307.12328)

<img src="https://img.shields.io/badge/Core%20Risk-D97706?style=flat" height="22" align="absmiddle" /><br>
• <img src="https://img.shields.io/badge/Stealing-9A3412?style=flat" height="18" align="absmiddle" />&nbsp;[Mind Your Weight(s): A Large-scale Study on Insufficient ML Model Protection in Mobile Apps](https://www.usenix.org/conference/usenixsecurity21/presentation/sun-zhichuang)

<img src="https://img.shields.io/badge/Attack%20Surfaces-7F1D1D?style=flat" height="22" align="absmiddle" /><br>
• <img src="https://img.shields.io/badge/Adversarial-B91C1C?style=flat" height="18" align="absmiddle" />&nbsp;[Robustness of On-device Models: Adversarial Attack to Deep Learning Models on Android Apps](https://arxiv.org/pdf/2101.04401)  
• <img src="https://img.shields.io/badge/Backdoor-BE123C?style=flat" height="18" align="absmiddle" />&nbsp;[DeepPayload: Black-box Backdoor Attack on Deep Learning Models through Neural Payload Injection](https://dl.acm.org/doi/10.1109/ICSE43902.2021.00035)  
• <img src="https://img.shields.io/badge/Weight-9F1239?style=flat" height="18" align="absmiddle" />&nbsp;[Typhon Unleashed: Practical Adversarial Weight Attacks Against On-Device Deep Learning Models](https://ieeexplore.ieee.org/document/11407485)  
• <img src="https://img.shields.io/badge/Latency-92400E?style=flat" height="18" align="absmiddle" />&nbsp;[Energy-Latency Attacks to On-Device Neural Networks via Sponge Poisoning](https://arxiv.org/pdf/2305.03888)

<img src="https://img.shields.io/badge/Defenses-166534?style=flat" height="22" align="absmiddle" /><br>
• <img src="https://img.shields.io/badge/Obfuscation-047857?style=flat" height="18" align="absmiddle" />&nbsp;[ModelObfuscator: Obfuscating Model Information to Protect Deployed ML-based Systems](https://arxiv.org/pdf/2306.06112)  
• <img src="https://img.shields.io/badge/TEE-0F766E?style=flat" height="18" align="absmiddle" />&nbsp;[ShadowNet: A Secure and Efficient On-device Model Inference System](https://arxiv.org/abs/2011.05905)  
• <img src="https://img.shields.io/badge/Watermarking-0E7490?style=flat" height="18" align="absmiddle" />&nbsp;[THEMIS: Towards Practical IP Protection for Post-Deployment On-Device DL Models](https://www.usenix.org/conference/usenixsecurity25/presentation/huang-yujin)



## Taxonomy at a glance

| MoAI security pillar | What it protects | Representative attacks | Representative defenses |
|---|---|---|---|
| **User-governed input integrity** | The end-to-end integrity of user inputs, from mobile data acquisition to model-input handoff | Adversarial Attacks, Backdoor Attacks, Energy-latency Attacks | - |
| **Device-resident model security** | Deployed model artifacts and all post-deployment forms in which models are stored, loaded, transformed, or materialized on devices | Adversarial Attacks, Backdoor Attacks, Adversarial Weight Attacks, Model Stealing Attacks,  Energy-latency Attacks | Model Obfuscation, Model Authorization, TEE, Model Watermarking |
| **Device-native environment confinement** | Sensitive inference computation and runtime states across the mobile OS, AI runtime, memory subsystem, and hardware-backed execution environments | Model Stealing Attacks, Energy-latency Attacks | Model Obfuscation, TEE |

## Cross-pillar Security Analysis
<p align="center">
  <img src="figures/pillar-attack-defense.jpg" alt="Cross-pillar security analysis of attacks, defenses, and open problems in MoAI systems.">
</p>

## Attacks on MoAI systems

<a id="adversarial-attacks"></a>
<img src="https://img.shields.io/badge/Adversarial%20Attacks-B91C1C?style=flat" height="24" align="absmiddle" />

#### Model Similarity Exploitation

- [**Robustness of On-device Models: Adversarial Attack to Deep Learning Models on Android Apps**](https://dl.acm.org/doi/10.1109/ICSE-SEIP52600.2021.00019) [[Code](https://github.com/Jinxhy/AppAIsecurity)]  
  <sub>IEEE/ACM International Conference on Software Engineering: Software Engineering in Practice (ICSE-SEIP 2021)</sub>

- [**Smart App Attack: Hacking Deep Learning Models in Android Apps**](https://dl.acm.org/doi/10.1109/TIFS.2022.3172213) [[Code](https://github.com/Jinxhy/SmartAppAttack)]  
  <sub>IEEE Transactions on Information Forensics and Security (TIFS 2022)</sub>

- [**Understanding Real-world Threats to Deep Learning Models in Android Apps**](https://dl.acm.org/doi/10.1145/3548606.3559388) [[Code](https://github.com/Advdroid/advdroid-pro)]    
  <sub>ACM SIGSAC Conference on Computer and Communications Security (CCS 2022)</sub>

- [**Cheating Your Apps: Black-box Adversarial Attacks on Deep Learning Apps**](https://onlinelibrary.wiley.com/doi/10.1002/smr.2528)  
  <sub>Journal of Software: Evolution and Process (JSEP 2024)</sub>

- [**A First Look at On-device Models in iOS Apps**](https://dl.acm.org/doi/10.1145/3617177) [[Code](https://github.com/huhanGitHub/iOS-App-database)]  
  <sub>ACM Transactions on Software Engineering and Methodology (TOSEM 2024)</sub>

#### Gradient Reconstruction

- [**Investigating White-Box Attacks for On-Device Models**](https://arxiv.org/abs/2402.05493) [[Code](https://github.com/zhoumingyi/REOM)]  
  <sub>IEEE/ACM International Conference on Software Engineering (ICSE 2024)</sub>

- [**TIM: Enabling Large-Scale White-Box Testing on In-App Deep Learning Models**](https://doi.org/10.1109/TIFS.2024.3455761) [[Code](https://zenodo.org/record/7548141)]  
  <sub>IEEE Transactions on Information Forensics and Security (TIFS 2024)</sub>

#### Preprocessing Manipulation

- [**Beyond the Model: Data Pre-processing Attack to Deep Learning Models in Android Apps**](https://dl.acm.org/doi/10.1145/3591197.3591308) [[Code](https://github.com/Alexender-Ye/attack-focused-on-pre-processing)]  
  <sub>Secure and Trustworthy Deep Learning Systems Workshop (SecTL 2023)</sub>

<a id="backdoor-attacks"></a>
<img src="https://img.shields.io/badge/Backdoor%20Attacks-BE123C?style=flat" height="24" align="absmiddle" />

#### Payload Injection

- [**DeepPayload: Black-box Backdoor Attack on Deep Learning Models through Neural Payload Injection**](https://dl.acm.org/doi/10.1109/ICSE43902.2021.00035) [[Code](https://github.com/yuanchun-li/DeepPayload)]  
  <sub>IEEE/ACM International Conference on Software Engineering (ICSE 2021)</sub>

- [**MalModel: Hiding Malicious Payload in Mobile Deep Learning Models with Black-box Backdoor Attack**](https://link.springer.com/article/10.1007/s10515-025-00569-7) [[Code](https://github.com/hjygh/MalModel)]  
  <sub>Automated Software Engineering (ASEJ 2026)</sub>

#### Model Quantization

- [**Quantization Backdoors to Deep Learning Commercial Frameworks**](https://arxiv.org/abs/2108.09187) [[Code](https://github.com/quantization-backdoor/quantization-backdoor)]  
  <sub>IEEE Transactions on Dependable and Secure Computing (TDSC 2024)</sub>

#### Image Steganography

- [**Stealthy Backdoor Attack to Real-world Models in Android Apps**](https://arxiv.org/abs/2501.01263)  
  <sub>arXiv preprint (arXiv 2025)</sub>

<a id="adversarial-weight-attacks"></a>
<img src="https://img.shields.io/badge/Adversarial%20Weight%20Attacks-9F1239?style=flat" height="24" align="absmiddle" />

- [**Typhon Unleashed: Practical Adversarial Weight Attacks Against On-Device Deep Learning Models**](https://ieeexplore.ieee.org/document/11407485)  
  <sub>IEEE Transactions on Dependable and Secure Computing (TDSC 2026)</sub>

<a id="model-stealing-attacks"></a>
<img src="https://img.shields.io/badge/Model%20Stealing%20Attacks-9A3412?style=flat" height="24" align="absmiddle" />

#### Static Analysis

- [**A First Look at Deep Learning Apps on Smartphones**](https://arxiv.org/pdf/1812.05448) [[Code](https://github.com/xumengwei/MobileDL)]<br>
  <sub>The World Wide Web Conference (WWW 2019)</sub>

- [**A First Look at On-device Models in iOS Apps**](https://arxiv.org/pdf/2307.12328) [[Code](https://github.com/huhanGitHub/iOS-App-database)]<br>
  <sub>ACM Transactions on Software Engineering and Methodology (TOSEM 2023)</sub>

- [**Mind Your Weight(s): A Large-scale Study on Insufficient Machine Learning Model Protection in Mobile Apps**](https://www.usenix.org/conference/usenixsecurity21/presentation/sun-zhichuang) [[Code](https://github.com/RiS3-Lab/ModelXRay)]<br>
  <sub>USENIX Security Symposium (USENIX Security 2021)</sub>

- [**REDLC: Learning-Driven Reverse Engineering for Deep Learning Compilers**](https://doi.org/10.1109/ISSRE62328.2024.00029)<br>
  <sub>IEEE International Symposium on Software Reliability Engineering (ISSRE 2024)</sub>

#### Dynamic Analysis

- [**Mind Your Weight(s): A Large-scale Study on Insufficient Machine Learning Model Protection in Mobile Apps**](https://www.usenix.org/conference/usenixsecurity21/presentation/sun-zhichuang) [[Code](https://github.com/RiS3-Lab/ModelXRay)]<br>
  <sub>USENIX Security Symposium (USENIX Security 2021)</sub>

- [**Understanding Real-world Threats to Deep Learning Models in Android Apps**](https://dl.acm.org/doi/10.1145/3548606.3559388) [[Code](https://github.com/Advdroid/advdroid-pro)]<br>
  <sub>ACM SIGSAC Conference on Computer and Communications Security (CCS 2022)</sub>

- [**DeMistify: Identifying On-device Machine Learning Models Stealing and Reuse Vulnerabilities in Mobile Apps**](https://dl.acm.org/doi/10.1145/3597503.3623325) [[Code](https://github.com/MGYN/DeMistify)]<br>
  <sub>IEEE/ACM International Conference on Software Engineering (ICSE 2024)</sub>

- [**Game of Arrows: On the (In-)Security of Weight Obfuscation for On-Device TEE-Shielded LLM Partition Algorithms**](https://www.usenix.org/conference/usenixsecurity25/presentation/wang-pengli) [[Code](https://github.com/qsxltss/Game-of-Arrows)]<br>
  <sub>USENIX Security Symposium (USENIX Security 2025)</sub>

#### Side Channel

- [**Model Extraction Attack against On-Device Deep Learning with Power Side Channel**](https://doi.org/10.1109/ISQED60706.2024.10528716)  
  <sub>IEEE International Symposium on Quality Electronic Design (ISQED 2024)</sub>

- [**DeepCache: Revisiting Cache Side-Channel Attacks in Deep Neural Networks Executables**](https://dl.acm.org/doi/10.1145/3658644.3690239)  
  <sub>ACM SIGSAC Conference on Computer and Communications Security (CCS 2024)</sub>

<a id="energy-latency-attacks"></a>
<img src="https://img.shields.io/badge/Energy--latency%20Attacks-92400E?style=flat" height="24" align="absmiddle" />

- [**Energy-Latency Attacks to On-Device Neural Networks via Sponge Poisoning**](https://dl.acm.org/doi/10.1145/3591197.3591307)  
  <sub>Secure and Trustworthy Deep Learning Systems Workshop (SecTL 2023)</sub>

## Defenses for MoAI systems

<a id="model-obfuscation"></a>
<img src="https://img.shields.io/badge/Model%20Obfuscation-047857?style=flat" height="24" align="absmiddle" />

#### Software-level Concealment

- [**ModelObfuscator: Obfuscating Model Information to Protect Deployed ML-Based Systems**](https://dl.acm.org/doi/10.1145/3597926.3598113) [[Code](https://github.com/zhoumingyi/ModelObfuscator)]<br>
  <sub>ACM SIGSOFT International Symposium on Software Testing and Analysis (ISSTA 2023)</sub>

- [**DynaMO: Protecting Mobile DL Models through Coupling Obfuscated DL Operators**](https://dl.acm.org/doi/10.1145/3691620.3694998) [[Code](https://github.com/zhoumingyi/DynaMO)]<br>
  <sub>IEEE/ACM International Conference on Automated Software Engineering (ASE 2024)</sub>

- [**Model-less Is the Best Model: Generating Pure Code Implementations to Replace On-Device DL Models**](https://dl.acm.org/doi/10.1145/3650212.3652119) [[Code](https://github.com/zhoumingyi/CustomDLCoder)]<br>
  <sub>ACM SIGSOFT International Symposium on Software Testing and Analysis (ISSTA 2024)</sub>

#### Hardware-level Concealment

- [**NNSplitter: An Active Defense Solution for DNN Model via Automated Weight Obfuscation**](https://proceedings.mlr.press/v202/zhou23h.html) [[Code](https://github.com/Tongzhou0101/NNSplitter)]<br>
  <sub>International Conference on Machine Learning (ICML 2023)</sub>

- [**A Novel Obfuscation Method Based on Majority Logic for Preventing Unauthorized Access to Binary Deep Neural Networks**](https://www.nature.com/articles/s41598-025-09722-4)<br>
  <sub>Scientific Reports (Sci. Rep. 2025)</sub>

<a id="model-authorization"></a>
<img src="https://img.shields.io/badge/Model%20Authorization-0A7763?style=flat" height="24" align="absmiddle" />

- [**MMGuard: Automatically Protecting On-Device Deep Learning Models in Android Apps**](https://ieeexplore.ieee.org/document/9474328) [[Code](https://github.com/MMGuard123/MMGuard)]<br>
  <sub>IEEE Security and Privacy Workshops (SPW 2021)</sub>

<a id="trusted-execution-environments"></a>
<img src="https://img.shields.io/badge/Trusted%20Execution%20Environments-0F766E?style=flat" height="24" align="absmiddle" />

#### Monolithic Execution

- [**Offline Model Guard: Secure and Private ML on Mobile Devices**](https://arxiv.org/abs/2007.02351)<br>
  <sub>Design, Automation and Test in Europe Conference (DATE 2020)</sub>

- [**GuardiaNN: Fast and Secure On-Device Inference in TrustZone Using Embedded SRAM and Cryptographic Hardware**](https://dl.acm.org/doi/10.1145/3528535.3531513)<br>
  <sub>ACM/IFIP International Middleware Conference (Middleware 2022)</sub>

- [**Secure and Efficient Mobile DNN Using Trusted Execution Environments**](https://dl.acm.org/doi/10.1145/3579856.3582820)<br>
  <sub>ACM Asia Conference on Computer and Communications Security (AsiaCCS 2023)</sub>

- [**T-Slices: Confidential Execution of Deep Learning Inference at the Untrusted Edge with Arm TrustZone**](https://dl.acm.org/doi/10.1145/3577923.3583648)<br>
  <sub>ACM Conference on Data and Application Security and Privacy (CODASPY 2023)</sub>

- [**LEAP: TrustZone Based Developer-Friendly TEE for Intelligent Mobile Apps**](https://dl.acm.org/doi/10.1109/TMC.2022.3207745)<br>
  <sub>IEEE Transactions on Mobile Computing (TMC 2022)</sub>

- [**ASGARD: Protecting On-Device Deep Neural Networks with Virtualization-Based Trusted Execution Environments**](https://www.ndss-symposium.org/ndss-paper/asgard-protecting-on-device-deep-neural-networks-with-virtualization-based-trusted-execution-environments/) [[Code](https://github.com/yonsei-sslab/asgard)]<br>
  <sub>Network and Distributed System Security Symposium (NDSS 2025)</sub>

- [**TZ-LLM: Protecting On-Device Large Language Models with Arm TrustZone**](https://arxiv.org/abs/2511.13717) [[Code](https://zenodo.org/records/17054270)]<br>
  <sub>European Conference on Computer Systems (EuroSys 2026)</sub>

- [**FlexServe: A Fast and Secure LLM Serving System for Mobile Devices with Flexible Resource Isolation**](https://arxiv.org/abs/2603.09046)<br>
  <sub>arXiv preprint (arXiv 2026)</sub>

#### Partitioned Execution

- [**DarkneTZ: Towards Model Privacy at the Edge Using Trusted Execution Environments**](https://arxiv.org/abs/2004.05703) [[Code](https://github.com/mofanv/darknetz)]<br>
  <sub>Annual International Conference on Mobile Systems, Applications, and Services (MobiSys 2020)</sub>

- [**HybridTEE: Secure Mobile DNN Execution Using Hybrid Trusted Execution Environment**](https://par.nsf.gov/servlets/purl/10217344) [[Code](https://github.com/hwsel/HybridTEE)]<br>
  <sub>Asian Hardware Oriented Security and Trust Symposium (AsianHOST 2020)</sub>

- [**SecDeep: Secure and Performant On-Device Deep Learning Inference Framework for Mobile and IoT Devices**](https://dl.acm.org/doi/10.1145/3450268.3453524)<br>
  <sub>International Conference on Internet-of-Things Design and Implementation (IoTDI 2021)</sub>

- [**ShadowNet: A Secure and Efficient On-Device Model Inference System for Convolutional Neural Networks**](https://ieeexplore.ieee.org/document/10179382) [[Code](https://github.com/RiS3-Lab/ShadowNet)]<br>
  <sub>IEEE Symposium on Security and Privacy (S&P 2023)</sub>

- [**MirrorNet: A TEE-Friendly Framework for Secure On-Device DNN Inference**](https://arxiv.org/abs/2311.09489)<br>
  <sub>IEEE/ACM International Conference on Computer-Aided Design (ICCAD 2023)</sub>

- [**TSQP: Safeguarding Real-Time Inference for Quantization Neural Networks on Edge Devices**](https://ieeexplore.ieee.org/document/11023493) [[Code](https://github.com/D1aoBoomm/TSQP)]<br>
  <sub>IEEE Symposium on Security and Privacy (S&P 2025)</sub>

- [**TEESlice: Protecting Sensitive Neural Network Models in Trusted Execution Environments When Attackers Have Pre-Trained Models**](https://dl.acm.org/doi/10.1145/3707453)<br>
  <sub>ACM Transactions on Software Engineering and Methodology (TOSEM 2025)</sub>

- [**TensorShield: Safeguarding On-Device Inference by Shielding Critical DNN Tensors with TEE**](https://arxiv.org/abs/2505.22735) [[Code](https://github.com/suntong30/TensorShield)]<br>
  <sub>ACM SIGSAC Conference on Computer and Communications Security (CCS 2025)</sub>

#### Obfuscated Offloading

- [**GroupCover: A Secure, Efficient and Scalable Inference Framework for On-Device Model Protection Based on TEEs**](https://proceedings.mlr.press/v235/zhang24bn.html) [[Code](https://github.com/ZzzzMe/GroupCover)]<br>
  <sub>International Conference on Machine Learning (ICML 2024)</sub>

- [**Game of Arrows: On the (In-)Security of Weight Obfuscation for On-Device TEE-Shielded LLM Partition Algorithms**](https://www.usenix.org/conference/usenixsecurity25/presentation/wang-pengli) [[Code](https://github.com/qsxltss/Game-of-Arrows)]<br>
  <sub>USENIX Security Symposium (USENIX Security 2025)</sub>

- [**MirageNet: A Secure, Efficient, and Scalable On-Device Model Protection in Heterogeneous TEE and GPU System**](https://arxiv.org/abs/2601.13826)<br>
  <sub>arXiv preprint (arXiv 2026)</sub>


<a id="model-watermarking"></a>
<img src="https://img.shields.io/badge/Model%20Watermarking-0E7490?style=flat" height="24" align="absmiddle" />


- [**THEMIS: Towards Practical Intellectual Property Protection for Post-Deployment On-Device Deep Learning Models**](https://www.usenix.org/conference/usenixsecurity25/presentation/huang-yujin) [[Code](https://github.com/Jinxhy/THEMIS)]<br>
  <sub>USENIX Security Symposium (USENIX Security 2025)</sub>

## Open problems

The following open problems summarize the main research gaps identified in our SoK. We keep the descriptions here high-level for readers using this repository. More technical discussions can be found in the paper.

<img src="https://img.shields.io/badge/ATTACK%20OPS%20%E2%80%94%20FROM%20MODEL%20ACCESS%20TO%20DEPLOYABLE%20ATTACKS-7F1D1D?style=for-the-badge" height="28" align="absmiddle" />

1. **Attack Deployment Practicality.**  
Adversarial attacks against on-device models remain hard to realize after deployment because they often require control over model inputs, insertion of adversarial perturbations, or app repackaging to modify preprocessing code. These steps can be impractical or detectable in real end-user deployments.

2. **Stealthy Model Modification.**  
Backdoor attacks need to find post-deployment entry points beyond standard training-time poisoning because on-device models are typically read-only and inference-only. The key challenge is to introduce hidden malicious behavior without producing observable changes in model artifacts.

3. **Precise Weight Localization.**  
Adversarial weight attacks expose a parameter-level integrity risk, but practical deployment depends on locating behavior-critical weights in the large parameter search space. This is difficult because attackers often lack gradient guidance and need to preserve benign utility while modifying only selected parameters.

4. **Reliable Model Extraction.**  
Local model storage does not make model stealing straightforward. Practical extraction still depends on reliable model identification, decryption, and reconstruction in the presence of customized encryption algorithms, nonstandard AI frameworks, and runtime-specific loading behavior.

5. **Hardware Heterogeneity.**  
Energy-latency attacks depend on how poisoned activation patterns interact with device-specific execution behavior. They may amplify latency and energy consumption on sparsity-sensitive accelerators, but fail to transfer to hardware without sparsity-dependent execution.

<img src="https://img.shields.io/badge/DEFENSE%20OPS%20%E2%80%94%20FROM%20PROTECTION%20MECHANISMS%20TO%20POST--RELEASE%20GUARANTEES-166534?style=for-the-badge" height="28" align="absmiddle" />

6. **Executable Equivalence.**  
Model obfuscation still needs to preserve the original prediction function during authorized inference. This executable equivalence can expose recoverable runtime states, transformed weights, operator semantics, or structural traces that enable semantic, structural, or parameter recovery.

7. **Client-side Enforcement.**  
Model authorization binds correct inference to credentials, integrity checks, and packed-weight recovery. However, these checks need to execute inside the mobile stack, making enforcement dependent on client-side code that can be reverse engineered, repackaged, hooked, or instrumented after deployment.

8. **TEE Deployment Feasibility.**  
TEE defenses require coordinated support across model formats, AI frameworks, operator libraries, delegates, accelerators, and CPU/GPU/NPU isolation interfaces. Current mobile ecosystems still lack widely adopted, developer-transparent TEE-backed inference stacks.

9. **Watermark Robustness.**  
Model watermarking enables post-deployment ownership verification, but stolen models may be redeployed through framework conversion, encryption, or app-level input-output mediation. These transformations can preserve benign inference while disrupting trigger responses, confidence patterns, or output semantics used for verification.

## Emerging directions

Beyond the nine open problems above, our SoK highlights three emerging directions where MOAI security is likely to expand next. These directions move beyond static, inference-only on-device models toward adaptive, generative, and action-oriented MoAI systems. We summarize them here at a high level. The companion paper provides more detailed motivation, threat surfaces, and research challenges.

<img src="https://img.shields.io/badge/On--device%20Training%20Security-4F46E5?style=for-the-badge" height="28" align="absmiddle" />

Current MoAI security research mainly focuses on deployed models that are read-only and inference-only. On-device training changes this assumption by allowing models to be updated locally, which exposes gradients, parameter updates, and user data during the training process. This opens new questions around local fine-tuning, update integrity, training-data exposure, personalization poisoning, and defenses for training-time states on end-user devices.

<img src="https://img.shields.io/badge/On--device%20GenAI%20Security-4F46E5?style=for-the-badge" height="28" align="absmiddle" />

Existing MoAI security studies are still largely centered on vision-based tasks such as image classification. As LLMs and generative models move onto smartphones, MoAI security must expand to prompt-driven and content-generating systems. Important challenges include prompt injection, jailbreaks, unintended information disclosure, and local context leakage for on-device LLM.

<img src="https://img.shields.io/badge/Agentic%20MoAI%20Governance-4F46E5?style=for-the-badge" height="28" align="absmiddle" />

MoAI systems are evolving from passive local inference toward agentic workflows that connect models with sensors, private user data, app contexts, OS services, and cross-app interfaces. This shifts the security focus from protecting model artifacts alone to governing context-to-action chains. Future work should study provenance for mobile context, separation of trusted user intent from untrusted environmental content, task-scoped permissions for tool and API use, confirmation and rollback for sensitive actions, and auditing of agent plans, memory, and actions.

<!--## Citation

If this repository helps your research, please cite the companion SoK paper:

```bibtex
@misc{huang2026moaisecurity,
  title        = {SoK: Attack and Defense Landscape of Mobile On-device AI Systems},
  author       = {Huang, Yujin and Zheng, Xin and Yuan, Xingliang and Lam, Kwok-Yan},
  year         = {2026},
  note         = {Companion resources: https://github.com/Jinxhy/Awesome-MoAI-Security},
  url          = {https://github.com/Jinxhy/Awesome-MoAI-Security}
}
```-->
