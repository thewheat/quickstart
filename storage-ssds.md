# Storage: SSDs

- https://en.wikipedia.org/wiki/Solid-state_drive
- https://en.wikipedia.org/wiki/M.2
- https://www.kingston.com/en/blog/pc-performance/two-types-m2-vs-ssd
- https://www.kingston.com/en/ssd/what-is-nvme-ssd-technology

## Summary

Typically will want
- NVMe drive (PCIe Gen 5 and above)
- With a M.2 form factor (aka Next Generation Form Factor / NGFF) of size 2280 with M-key notch (notch on right when connector facing up)
- 4 lane (x4) SSD connected to x4 slot

## Protocols
- NVMe (Non-Volatile Memory Express)
    - Uses PCIe (Peripheral Component Interconnect Express) lanes
    - 2 lanes (x2) / 4 lanes (x4): determines speed (typically drives expect x4)
        - x4 drive can works x2 slot but x2 speed
        - Backward compatible: New drives work in old slots
        - Forward compatible: Old drives work in new slots
    - Generations and speeds
        - PCIe Gen 3: ~3,500 MB/s
        - PCIe Gen 4: ~7,500 MB/s
        - PCIe Gen 5: ~14,000+ MB/s
- ACHI (Advanced Host Controller Interface) (sometimes referred to as SATA SSD)
    - Uses SATA (Serial AT Attachment) controller for communications
    - SATA SSDs: ~600 MB/s

## Forms Factors

Typical consumer form factors detailed below

### M.2 (The "Gum Stick")
- Most typical form factor. Formerly known as the Next Generation Form Factor (NGFF)
- Small, rectangular strip that plugs directly into the motherboard.
- Comes in different lengths: 2230, 2242, 2280, 22110 (e.g. 2280 is 22mm wide, 80mm long and is the typical dimensions)
- Can be NVMe / SATA
- Drives and slots have notches to prevent incompatible connections
- Typical notches location (drive connector facing up)
    - M key
        - one notch on right
        - can be SATA / NVMe PCIe x4 but typical NVMe
    - B+M key
        - two notches one on right, one notch on left
        - SATA / NVMe PCIe x2 but typically SATA
    - B key
        - one notch on left (uncommon to only have B key - typicall B+M key)
        - SATA / NVMe PCIe x2 but typically SATA

### 2.5-inch SATA
- The traditional "laptop drive" shape.
- Uses a SATA cable and power connector.
- Slowest modern option (capped at ~600MB/s).

### mSATA (Mini-SATA)
- Older, smaller version of the 2.5-inch drive.
- Used in older thin laptops before M.2 became the standard.
- Limited to SATA speeds.




