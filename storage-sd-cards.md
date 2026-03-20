# Storage: SD / Micro SD cards

- https://www.sdcard.org/developers/sd-standard-overview/
- https://www.kingston.com/en/blog/personal-storage/memory-card-speed-classes

## Summary
- Typical look for
    - SDXC / SDHC (slightly older) / SHUC
    - Classes or speeds:
        - U# (speed: 10#MB/s)
        - V# (speed: #MB/s)
    - UHS-I mode / UHS-II & III mode
- High end special use cases:
    - SD Express mode: with E# (#MB/s) speeds
- Special notes based on usage
    - Video recording
        - Look for minimum speeds based on resolution
        - 8K: minimum U3/V30
        - 4K: minimum C6/V6
        - 1080p: minumum C4
    - Storing Applications:
        - A1/A2 ratings for consistent random read and writes
    - Endurance rating
        - For lots of continuous writes (e.g. dashcam / security cam)
        - No official ratings


## Dimensions
- SD: 32 x 24 x 2.1 mm
- microSD: 11 x 15 x 1.0 mm

## Capacity Standards (SD, SDHC, SDXC, SDUC)

- SD: Up to 2GB. FAT 12 and 16 file systems
- SDHC: 2GB - 32GB. FAT32 file system
- SDXC: 32GB - 2TB. exFAT file system
- SDUC: 2TB - 128TB. exFAT file system

## Speed Classes

- Rating based on minimum sequential write speeds
- Number typicall indicates speed in MB/s e.g. C10 => 10MB/s
- A single card can have multiple speed classses

### Classes (Speed: C / UHS Speed: U / Video: V / SD Express: E)
- Speed Class (C2, C4, C6, C10)
- UHS Speed Class (U1, U3): Number indicates speed in MB/s after 10 multiple, U1 => 10MB/s, U3 => 30MB/s
- Video Speed Class (V6, V10, V30, V60, V90):
- SD Express Speed Class (E150, E300, E450, E600)

### Modes (Normal / High / UHS-I / UHS-II & UHS-III / SD Express)
- Normal Speed: C2, C4, C6
- High Speed: C2, C4, C6, C10, V6, V10
- UHS-I: C2, C4, C6, C10U1, U3V6, V10, V30 (Only on SDHC / SDXC / SDUC. Not available on SD)
- UHS-II & III: C4, C6, C10U1, U3V6, V10, V30, V60, V90 (Only on SDHC / SDXC / SDUC. Not available on SD)
- SD Express: E150, E300, E450, E600 (Only on SDXC / SDUC. Not available on SD / SDHC)

## Application Performance Class

For devices that run apps directly from the card (like smartphones or handheld consoles).

- A1: Minimum random read of 1500 IOPS; random write of 500 IOPS. Minimum sequential write 10MB/s
- A2: Minimum random read of 4000 IOPS; random write of 2000 IOPS. Minimum sequential write 10MB/s

## Endurance

- No official ratings
- Typically for long write life over speeds: best for dash cams, security cameras, and surveillance
