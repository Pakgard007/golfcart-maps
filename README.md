# golfcart-maps — แผนที่ point cloud ของรถกอล์ฟ

แผนที่ 3 มิติ (`.pcd`) ที่ทำด้วย **[Mapping](https://github.com/Pakgard007/Mapping)** (LIO-SAM + Ouster OS-1-128) และใช้ใน
**[Localize_get_path](https://github.com/Pakgard007/Localize_get_path)** สำหรับ NDT localization

ไฟล์แผนที่ใหญ่เกินที่ git รับ (100MB) จึงอยู่ในหน้า **[Releases](../../releases)** ของ repo นี้
บีบอัดด้วย `zstd`

## ไฟล์

| ไฟล์ | จุด | ขนาด (.pcd) | สถานะ |
|---|---|---|---|
| `FullGlobalMap.pcd.zst` | 36,278,984 | 554 MB | **ใช้อยู่** — เกือบทั้งมหาวิทยาลัย (ตั้งแต่ 2026-11-10) |
| `GlobalMapLoop1.pcd.zst` | 5,841,778 | 90 MB | เลิกใช้ |
| `GlobalMapLoop2.pcd.zst` | 14,552,700 | 223 MB | เลิกใช้ |

ทุกไฟล์: `FIELDS x y z intensity`, `DATA binary`

## วิธีใช้

```bash
# โหลด FullGlobalMap.pcd.zst จากหน้า Releases แล้ว
sudo apt install -y zstd
zstd -d FullGlobalMap.pcd.zst -o ~/2Localize_get_path/src/FullGlobalMap.pcd

# แผนที่เก่า (ถ้าต้องใช้) วางที่ src/old_maps/ — ดู src/old_maps/README.md ใน 2Localize_get_path
```

จากนั้นตรวจว่า `map_path` ใน `src/lidar_localization_ros2-main/param/localization.yaml`
ชี้ไปที่ไฟล์นี้

## ตรวจไฟล์ (SHA-256 ของ .pcd หลังแตกไฟล์)

```text
5d3635d808791e549001de5ddff36187ab066f947e983ecf3edd007d8389236a  FullGlobalMap.pcd
c08a1fb12423e630d2ade56be710630358d7bf5f961dd8577de57a038a896d65  GlobalMapLoop1.pcd
bd616b698ca3eb24c0ac3ae094f6277eb3b27d3b5eab26cdf8e8adb0fac31699  GlobalMapLoop2.pcd
```

```bash
sha256sum FullGlobalMap.pcd
```
