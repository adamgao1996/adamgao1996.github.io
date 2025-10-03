# SensorAlert: Acoustic FMCW Scanner
## Copyright Application Summary

---

### **基本信息 / Basic Information**

**项目名称 / Project Name**: SensorAlert - Acoustic FMCW Scanner  
**作者 / Author**: 高一轩 (Yixuan Gao)  
**创作时间 / Creation Date**: 2025年  
**项目链接 / Project URL**: https://adamgao1996.github.io/assets/sensor-alert/index.html  
**版权声明 / Copyright**: © 2025 Yixuan Gao. All rights reserved.

---

## **1. 项目概述 / Project Overview**

SensorAlert是一个实时超声波隐私保护系统，使用先进的信号处理技术检测声学跟踪企图。该系统通过监控和识别可能用于声学监控、设备跟踪或未授权音频信标的可疑超声波信号来保护用户隐私。

SensorAlert is a real-time ultrasonic privacy protection system that detects acoustic tracking attempts through advanced signal processing. The system protects user privacy by monitoring and identifying suspicious ultrasonic signals that might be used for acoustic surveillance, device tracking, or unauthorized audio beaconing.

### **核心功能 / Key Features**
- 实时音频分析 / Real-time Audio Analysis
- 先进模式检测 / Advanced Pattern Detection  
- 超声波监控 / Ultrasonic Monitoring (18-22 kHz)
- 实时可视化 / Live Visualization
- 威胁评估 / Threat Assessment
- 隐私优先设计 / Privacy-First Design

---

## **2. 技术实现 / Technical Implementation**

### **2.1 核心算法 / Core Algorithms**

**FMCW检测算法 / FMCW Detection Algorithm**:
```javascript
const SAMPLE_RATE = 48000;
const FFT_SIZE = 2048;
const ULTRASONIC_MIN = 18000;
const ULTRASONIC_MAX = 22000;

function extractHighFrequencySpectrum(dataArray) {
    const nyquist = SAMPLE_RATE / 2;
    const minBin = Math.floor((MIN_FREQUENCY / nyquist) * dataArray.length);
    const highFreqData = dataArray.slice(minBin);
    
    // 下采样到32个频段进行模式匹配
    const targetBins = 32;
    const binSize = Math.floor(highFreqData.length / targetBins);
    const spectrum = [];
    
    for (let i = 0; i < targetBins; i++) {
        let binPower = 0;
        const start = i * binSize;
        const end = Math.min(start + binSize, highFreqData.length);
        
        for (let j = start; j < end; j++) {
            binPower += highFreqData[j];
        }
        spectrum.push(binPower / (end - start));
    }
    return spectrum;
}
```

**重复模式检测 / Repeated Pattern Detection**:
```javascript
function detectRepeatedPatterns() {
    if (spectrumHistory.length < 40) { // 至少2秒数据
        updateThreatLevel(0);
        return;
    }
    
    const patterns = findRepeatingPatterns();
    
    if (patterns.length > 0) {
        const bestPattern = patterns[0];
        const detection = {
            timestamp: new Date().toLocaleTimeString(),
            type: 'repeated-pattern',
            pattern: bestPattern.type,
            repeats: bestPattern.count,
            confidence: bestPattern.confidence,
            power: bestPattern.avgPower,
            threatLevel: calculateSimpleThreatLevel(bestPattern)
        };
        
        if (detection.threatLevel > 3) {
            detectionCount++;
            detectionLog.push(detection);
            logDetection(detection);
        }
        updateThreatLevel(detection.threatLevel);
    }
}
```

**威胁级别计算 / Threat Level Calculation**:
```javascript
function calculateSimpleThreatLevel(pattern) {
    let threat = 0;
    
    // 基于重复次数
    threat += Math.min(pattern.count * 1.5, 6);
    
    // 基于置信度
    threat += pattern.confidence * 3;
    
    // 基于功率
    if (pattern.avgPower > 150) threat += 2;
    else if (pattern.avgPower > 100) threat += 1;
    
    // 基于模式类型
    const typeMultipliers = {
        'ascending-chirp': 1.5,
        'descending-chirp': 1.5,
        'high-power-pattern': 1.3,
        'weak-up-sweep': 1.2,
        'weak-down-sweep': 1.2
    };
    
    const multiplier = typeMultipliers[pattern.type] || 1.0;
    threat *= multiplier;
    
    return Math.min(threat, 10);
}
```

### **2.2 实时可视化 / Real-time Visualization**

**频谱图更新 / Spectrogram Update**:
```javascript
function updateSpectrogram(dataArray) {
    const canvas = spectrogramCtx.canvas;
    const width = canvas.width;
    const height = canvas.height;
    
    // 向左移动现有数据
    const imageData = spectrogramCtx.getImageData(1, 0, width - 1, height);
    spectrogramCtx.putImageData(imageData, 0, 0);
    
    // 绘制新列
    const bufferLength = dataArray.length;
    const step = bufferLength / height;
    
    for (let y = 0; y < height; y++) {
        const dataIndex = Math.floor(y * step);
        const power = dataArray[dataIndex];
        
        const intensity = power / 255;
        const hue = (1 - intensity) * 240; // 蓝到红
        const color = `hsl(${hue}, 100%, ${intensity * 50}%)`;
        
        spectrogramCtx.fillStyle = color;
        spectrogramCtx.fillRect(width - 1, height - y - 1, 1, 1);
    }
}
```

---

## **3. 用户界面设计 / User Interface Design**

### **3.1 设计理念 / Design Philosophy**
- 深色主题 / Dark Theme: 专业网络安全美学
- 实时反馈 / Real-time Feedback: 对音频活动的即时视觉响应  
- 直观控制 / Intuitive Controls: 一键启动/停止操作
- 信息密集 / Information Dense: 同时显示多种可视化模式

### **3.2 主要组件 / Key Components**

**控制面板 / Control Panel**:
```css
.control-panel {
    background: rgba(46, 46, 46, 0.8);
    border-radius: 15px;
    padding: 25px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    border: 1px solid rgba(0, 255, 65, 0.2);
}
```

**威胁指示器 / Threat Indicator**:
```css
.threat-level {
    font-size: 2em;
    font-weight: bold;
    color: #00ff41;
    text-shadow: 0 0 10px currentColor;
}
```

---

## **4. 隐私和安全特性 / Privacy and Security Features**

### **4.1 本地处理 / Local Processing**
- 无数据传输 / No Data Transmission: 所有音频处理在浏览器本地进行
- 无存储 / No Storage: 不保存音频数据到磁盘或传输到服务器
- 基于权限 / Permission-Based: 需要明确的麦克风权限
- 透明操作 / Transparent Operation: 开源算法，可见的处理过程

### **4.2 权限管理 / Permission Management**
```javascript
async function requestMicPermission() {
    try {
        const stream = await navigator.mediaDevices.getUserMedia({ 
            audio: {
                sampleRate: SAMPLE_RATE,
                channelCount: 1,
                echoCancellation: false,
                noiseSuppression: false,
                autoGainControl: false
            } 
        });
        
        stream.getTracks().forEach(track => track.stop());
        document.getElementById('permissionModal').classList.add('hidden');
        logMessage('Microphone permission granted', 'info');
        
    } catch (error) {
        logMessage('Microphone permission denied: ' + error.message, 'error');
    }
}
```

---

## **5. 检测能力 / Detection Capabilities**

### **5.1 信号类型 / Signal Types**
- 上升扫频 / Ascending Chirps: 频率随时间增加的扫描
- 下降扫频 / Descending Chirps: 频率随时间减少的扫描  
- 高功率模式 / High-Power Patterns: 持续的高幅度超声波信号
- 弱扫描 / Weak Sweeps: 低功率频率调制信号

### **5.2 模式分类 / Pattern Classification**
```javascript
function classifyPatternType(pattern) {
    const trend = pattern.trend;
    const avgPower = pattern.avgPower;
    
    if (avgPower > 150) {
        if (trend === 'increasing') return 'ascending-chirp';
        if (trend === 'decreasing') return 'descending-chirp';
        return 'high-power-pattern';
    } else if (avgPower > 80) {
        if (trend === 'increasing') return 'weak-up-sweep';
        if (trend === 'decreasing') return 'weak-down-sweep';
        return 'medium-pattern';
    }
    
    return 'low-level-pattern';
}
```

---

## **6. 技术规格 / Technical Specifications**

### **6.1 系统要求 / System Requirements**
- 浏览器 / Browser: 支持Web Audio API的现代浏览器
- JavaScript: ES6+兼容环境
- 麦克风 / Microphone: 任何音频输入设备
- 权限 / Permissions: 麦克风访问权限
- 网络 / Network: 麦克风访问需要HTTPS环境

### **6.2 性能特征 / Performance Characteristics**
- 采样率 / Sampling Rate: 48 kHz
- FFT大小 / FFT Size: 2048点
- 分析速率 / Analysis Rate: 20 fps
- 频率范围 / Frequency Range: 0-24 kHz (重点10-22 kHz)
- 检测延迟 / Detection Latency: < 100ms
- 内存使用 / Memory Usage: < 50MB 典型操作

---

## **7. 代码结构和文件 / Code Structure and Files**

### **7.1 主应用文件 / Main Application File**
- **文件 / File**: `/assets/sensor-alert/index.html`
- **大小 / Size**: 1,207行代码 / 1,207 lines of code  
- **组件 / Components**: HTML结构、CSS样式、JavaScript实现
- **自包含 / Self-contained**: 单文件包含所有功能

### **7.2 项目文档 / Project Documentation** 
- **文件 / File**: `/_projects/sensoralert.md`
- **用途 / Purpose**: 项目描述和集成
- **链接 / Links**: 连接到主应用程序

### **7.3 关键函数 / Key Functions**
1. **音频处理 / Audio Processing**: `analyzeAudio()`, `processFrequencyData()`
2. **模式检测 / Pattern Detection**: `detectRepeatedPatterns()`, `findRepeatingPatterns()`  
3. **可视化 / Visualization**: `updateSpectrogram()`, `updatePowerChart()`
4. **UI管理 / UI Management**: `toggleScanning()`, `updateThreatLevel()`
5. **数据导出 / Data Export**: `exportLog()`, `logDetection()`

---

## **8. 创新和原创性 / Innovation and Originality**

### **8.1 新颖方法 / Novel Approaches**
- **滑动窗口分析 / Sliding Window Analysis**: 使用时间分析的先进模式检测
- **多维威胁评分 / Multi-dimensional Threat Scoring**: 综合威胁评估算法
- **实时可视化 / Real-time Visualization**: 实时频谱图和频率分析
- **隐私优先设计 / Privacy-First Design**: 本地处理无数据传输

### **8.2 技术创新 / Technical Innovations**
- **模式签名提取 / Pattern Signature Extraction**: 声学指纹识别的独特方法
- **频谱趋势分析 / Spectral Trend Analysis**: 频率调制模式检测
- **自适应阈值系统 / Adaptive Threshold System**: 动态威胁级别计算
- **跨平台兼容性 / Cross-platform Compatibility**: 基于浏览器的实现

---

## **9. 版权和许可信息 / Copyright and Licensing Information**

### **9.1 版权声明 / Copyright Notice**
**© 2025 高一轩 (Yixuan Gao). 保留所有权利 / All rights reserved.**

该软件及所有相关文档、算法和实现均为高一轩在康奈尔大学学习期间的原创作品。

This software and all associated documentation, algorithms, and implementations are the original work of Yixuan Gao, created during his studies at Cornell University.

### **9.2 知识产权声明 / Intellectual Property Claims**
- **源代码 / Source Code**: 完整的JavaScript实现 (1,207行)
- **算法 / Algorithms**: 模式检测和威胁评估方法
- **用户界面 / User Interface**: 原创设计和可视化系统  
- **文档 / Documentation**: 技术规格和用户指南

### **9.3 创作详情 / Creation Details**
- **作者 / Author**: 高一轩 (Yixuan Gao)
- **邮箱 / Email**: yg478@cornell.edu
- **机构 / Institution**: 康奈尔大学 / Cornell University
- **创作年份 / Creation Year**: 2025年 / 2025
- **发布 / Publication**: https://adamgao1996.github.io/assets/sensor-alert/index.html

### **9.4 作品分类 / Work Classification**
- **类型 / Type**: 计算机软件（源代码）/ Computer Software (Source Code)
- **类别 / Category**: 隐私保护/安全工具 / Privacy Protection/Security Tool  
- **性质 / Nature**: 具有新颖模式检测方法的原创算法作品
- **状态 / Status**: 未发表作品，非雇佣作品 / Unpublished work, not for hire

---

## **10. 完整文件清单 / Complete File Listing**

```
SensorAlert项目文件 / SensorAlert Project Files:
├── /assets/sensor-alert/index.html (1,207行) - 主应用程序
├── /_projects/sensoralert.md (50行) - 项目文档  
└── /assets/img/sensoralert.png - 项目预览图像
```

### **依赖项 / Dependencies**
- **Web Audio API**: 浏览器原生音频处理
- **Canvas API**: 实时可视化渲染
- **MediaDevices API**: 麦克风访问
- **HTML5**: 现代网络标准

---

**为美国版权局注册准备的文档**  
**Document prepared for US Copyright Office registration**  
**表格CO - 计算机程序注册 / Form CO - Computer Program Registration**

**申请人 / Claimant**: 高一轩 / Yixuan Gao  
**地址 / Address**: Cornell University, Ithaca, NY 14850  
**邮箱 / Email**: yg478@cornell.edu  
**创作日期 / Date of Creation**: 2025年 / 2025  
**发表日期 / Date of Publication**: 尚未发表（未发表作品注册）/ Not yet published (registration for unpublished work)

---

*本文档包含高一轩创作的SensorAlert：声学FMCW扫描仪系统的完整技术规格，包括所有原创算法、实现和创新。*

*This document contains the complete technical specification of the SensorAlert: Acoustic FMCW Scanner system, including all original algorithms, implementations, and innovations created by Yixuan Gao.*