# Dual-Channel Solenoid Valve Controller

A dual-channel solenoid valve driver board with independently adjustable pulse voltage (0–30V), pulse width (1ms step), frequency (0.01–10Hz), and channel delay (50ms step).

## Project Background

This project reconstructs a legacy dual-channel solenoid control system. The original design only reached the schematic and PCB draft stage. This repository documents the complete closed-loop reconstruction: PCB fabrication, hardware assembly, firmware, LabVIEW host software, and a low-cost oscilloscope built with an Arduino ADC for waveform verification without professional lab equipment.

## System Architecture

LabVIEW Host (PC)
│ USB Serial
▼
Arduino / ESP32 ──► DAC ──► Op-Amp ──► MOSFET ──► Solenoid / LED Load
│ │
└──────── ADC ◄── Voltage Divider ◄────┘
(custom oscilloscope)


## Key Specifications

| Parameter | Value |
|---|---|
| Channels | 2 (independent, synchronized) |
| Output Voltage | 0–30V, adjustable, 0.01V resolution (calibrated) |
| Pulse Width | Adjustable, 1ms minimum step |
| Frequency | 0.01–10Hz |
| Channel Delay | 50ms minimum step |
| Pulse Count / Duration | Configurable |

## Repository Structure

- `labview/` — LabVIEW host VI files
- `arduino/firmware/` — Main control firmware
- `arduino/oscilloscope/` — Custom ADC-based oscilloscope firmware
- `python/` — Real-time waveform plotting script
- `hardware/` — Gerber, schematic, BOM
- `simulation/` — LTspice simulation files
- `docs/` — Troubleshooting manual and design review
- `media/` — Waveform screenshots and demo video link

## Core Challenge: No Oscilloscope

The lab lacks a professional oscilloscope. To verify the 1ms pulse width and the inductive load freewheeling protection, an Arduino ADC samples the output through a resistor divider and streams data over serial to a Python/Serial Plotter display. This low-cost approach successfully captured the MOSFET drain voltage spike and confirmed the effectiveness of the freewheeling diode.

## Status

- [ ] LTspice simulation
- [ ] PCB fabrication
- [ ] Hardware assembly
- [ ] Firmware development
- [ ] LabVIEW integration
- [ ] Custom oscilloscope validation
- [ ] Demo video

## License

MIT


dual-solenoid-controller/
├── README.md
├── LICENSE
├── .gitignore
├── labview/                  # LabVIEW 上位机 .vi 文件
├── arduino/
│   ├── firmware/             # 主控固件 .ino
│   └── oscilloscope/         # 自制示波器 .ino
├── python/
│   └── plotter.py            # 实时波形绘图脚本
├── hardware/
│   ├── gerber/               # 嘉立创导出 Gerber
│   ├── schematic/            # 原理图 PDF / 图片
│   └── bom.csv               # BOM 清单
├── simulation/
│   └── ltspice/              # LTspice .asc 仿真文件
├── docs/
│   ├── troubleshooting.md    # 排障手册
│   └── design_review.md      # 设计复盘
└── media/
    ├── waveform_screenshots/ # 波形截图
    └── demo_video_link.md    # 演示视频链接