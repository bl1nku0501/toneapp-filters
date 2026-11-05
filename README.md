# ToneApp Filters

Kho filter tải thêm cho ứng dụng ToneApp. App đọc `index.json`, hiện danh sách bộ filter
và chỉ tải một bộ (`packs/<id>.zip`) khi người dùng bấm "Tải về".

## Cấu trúc

```
index.json              danh sách bộ filter (tên, mô tả, số tone, dung lượng, sha256, giấy phép)
packs/<id>.zip          manifest.json + các LUT PNG 512x512 (8x8 ô, 64 mức)
packs/<id>/cover.png    ảnh bìa
sources/<id>/           bản gốc của từng bộ: pack.json + LUT
LICENSE-<id>.txt        giấy phép riêng của bộ (nếu có)
```

## Thêm / sửa một bộ filter

1. Tạo `sources/<id>/` gồm các LUT PNG 512x512 và `pack.json`
   (xem `sources/toneapp-goc/pack.json`). Tăng `version` khi sửa bộ cũ để app báo "Cập nhật".
2. Dựng lại (script nằm trong dự án ToneApp):
   ```
   python tools/build_filter_repo.py <thư mục repo này> sources/toneapp-goc sources/<id> ...
   ```
3. Commit và push. App thấy bộ mới ở lần mở Kho filter tiếp theo.

Chỉ đưa lên filter được phép phân phối lại, ghi rõ tác giả và giấy phép trong `pack.json`.
