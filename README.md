# golfcart-maps — แผนที่ point cloud ของรถกอล์ฟ

แผนที่ 3 มิติ (`.pcd`) ที่ทำด้วย **[Mapping](https://github.com/Pakgard007/Mapping)** (LIO-SAM + Ouster OS-1-128)
และใช้ใน **[Localize_get_path](https://github.com/Pakgard007/Localize_get_path)** สำหรับ NDT localization

## 🗺️ แผนที่

| ไฟล์ | จุด | ขนาด | หมายเหตุ |
|---|---|---|---|
| `FullGlobalMap.pcd` | 36,278,984 | 554 MB | เกือบทั้ง มจธ. บางมด (ใช้ตั้งแต่ 2026-11-10) · `FIELDS x y z intensity` · `DATA binary` |

GitHub รับไฟล์ละไม่เกิน 100 MB แผนที่จึงถูกแบ่งเป็น 6 ชิ้นในโฟลเดอร์ [`FullGlobalMap/`](FullGlobalMap)
ต้องโหลดมาแล้วต่อกลับเป็นไฟล์เดียวก่อนใช้

## 📥 วิธีโหลดและต่อไฟล์

```bash
git clone https://github.com/Pakgard007/golfcart-maps.git
cd golfcart-maps
cat FullGlobalMap/FullGlobalMap.pcd.part-* > FullGlobalMap.pcd
sha256sum FullGlobalMap.pcd      # ต้องตรงกับค่าด้านล่าง
cp FullGlobalMap.pcd ~/2Localize_get_path/src/
```

<details>
<summary>Windows</summary>

```bat
copy /b FullGlobalMap\FullGlobalMap.pcd.part-00+FullGlobalMap\FullGlobalMap.pcd.part-01+FullGlobalMap\FullGlobalMap.pcd.part-02+FullGlobalMap\FullGlobalMap.pcd.part-03+FullGlobalMap\FullGlobalMap.pcd.part-04+FullGlobalMap\FullGlobalMap.pcd.part-05 FullGlobalMap.pcd
certutil -hashfile FullGlobalMap.pcd SHA256
```

</details>

จากนั้นตรวจว่า `map_path` ใน `src/lidar_localization_ros2-main/param/localization.yaml`
(ใน Localize_get_path) ชี้ไปที่ไฟล์นี้

## ✅ SHA-256

```text
5d3635d808791e549001de5ddff36187ab066f947e983ecf3edd007d8389236a  FullGlobalMap.pcd
```

## 🔁 เพิ่มแผนที่ใหม่

```bash
mkdir NewMap
split -b 95M -d -a 2 NewMap.pcd NewMap/NewMap.pcd.part-
sha256sum NewMap.pcd             # ใส่ค่าลง README
git add NewMap && git commit -m "Add NewMap" && git push
```
