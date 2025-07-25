---
title: 基于ESP32-C5的无线感知系统
date: 2025-06-26 15:54:41
tags: 
  - C++
  - 嵌入式
  - ESP32-C5
top: 9
---

# 基于ESP32-C5的无线感知系统

## 简历描述

基于 ESP32-C5 的无线感知系统 - C++/嵌入式

- 构建双 ESP32-C5 架构的 Wi-Fi CSI 感知系统，实现信道状态信息的采集、传输与板载处理
- 基于 ESP-DSP 库在 MCU 上实现 FFT 与频域特征提取，完成呼吸率估计（MAE = 1.04）与运动检测（准确率达 95%）
- 自建数据集并调优采样率，实现模型量化部署，边缘推理延迟控制在 50ms 内，功耗降低约 30%
- 利用 FreeRTOS 事件循环与回调机制构建多任务处理系统，保障算法实时性与系统稳定性
- 通过 MQTT 实时上传处理结果，结合 Web 前后端实现可视化监控与交互展示

## 问题

> 构建双 ESP32-C5 架构的 Wi-Fi CSI 感知系统，实现信道状态信息的采集、传输与板载处理

1. **什么是 Wi-Fi CSI？ESP32-C5 是如何获取 CSI 数据的？是否使用了 esp_wifi_set_csi_rx_cb 回调？**
2. **双 ESP32 架构是如何设计的？主从分工是怎样的？之间如何通信（UART/SPI/Wi-Fi）？**
3. **ESP32-C5 相比 ESP32/ESP32-S3 在感知任务中有哪些优势？**
4. **CSI 采集频率和数据量有多大？是否做了同步或时序对齐？**
5. **CSI 原始数据如何处理噪声？是否有滤波、归一化、滑动平均等预处理？**
6. **板载处理是完全在 ESP32 上完成的吗？涉及多少资源占用（CPU 占比、内存）？**

> 基于 ESP-DSP 库在 MCU 上实现 FFT 与频域特征提取，完成呼吸率估计（MAE = 1.04）与运动检测（准确率达 95%）

1. **为什么选择 ESP-DSP？是否评估过 CMSIS-DSP 或自实现 FFT？**
2. **FFT 使用的是多少点？采样窗口长度是多少？是否应用了窗函数？**
3. **呼吸率估计的算法原理是什么？是通过主频率检测还是包络分析？**
4. **MAE = 1.04 是在什么基准下评估的？单位是 bpm 吗？是否在多人体环境测试过？**
5. **运动检测的特征是频域能量变化还是基于模式识别？是否引入了机器学习？**
6. **准确率 95% 是在多大样本量的数据集上得到的？有无混淆矩阵或 ROC 曲线？**

> 自建数据集并调优采样率，实现模型量化部署，边缘推理延迟控制在 50ms 内，功耗降低约 30%

1. **数据集是如何采集和标注的？包括哪些场景（静止/呼吸/走动）？**
2. **采样率是如何选取和调优的？对延迟、准确率、功耗分别有什么影响？**
3. **模型是自研还是迁移已有结构？部署使用了哪种框架（如 TFLite Micro）？**
4. **模型量化是采用哪种策略（Post-training、QAT）？精度损失有多大？**
5. **推理延迟 50ms 是如何测试的？包含数据预处理和 FFT 吗？**
6. **功耗下降 30% 是对比优化前后的吗？通过哪种方式测得（电流采样/功率分析仪）？**

> 利用 FreeRTOS 事件循环与回调机制构建多任务处理系统，保障算法实时性与系统稳定性

1. **系统中划分了哪些任务？每个任务负责哪部分功能？优先级如何设置？**
2. **事件循环机制是如何实现的？是否用了队列、信号量或 Event Group？**
3. **CSI 采集、FFT 处理和 MQTT 上传分别在哪些任务中？它们如何同步？**
4. **是否遇到任务阻塞、堆栈溢出或死锁问题？如何调试与避免？**
5. **使用了 Watchdog 吗？任务异常是否会触发系统重启？**
6. **系统稳定性测试做了多久？有没有长时间运行压力测试（如 24 小时稳定性）？**

> 通过 MQTT 实时上传处理结果，结合 Web 前后端实现可视化监控与交互展示

1. **为什么选用 MQTT 协议？相比 HTTP/CoAP 有哪些优势？**
2. **MQTT 是同步发送还是异步？是否支持断点续传？QoS 等级是多少？**
3. **发送的数据格式是 JSON 吗？包含了哪些字段（时间戳、特征值、状态标签等）？**
4. **Web 可视化用的是什么技术栈？前端是否使用 ECharts/Vue？后端是否用了 Flask/Node.js？**
5. **消息发布频率是多少？网络波动下如何保证可靠性？是否使用了重传机制？**
6. **MQTT 是否配置了 TLS 加密？是否使用用户名密码/Token 做身份认证？**
7. **Web 可视化展示哪些核心指标？是否支持实时刷新与历史查询？**
