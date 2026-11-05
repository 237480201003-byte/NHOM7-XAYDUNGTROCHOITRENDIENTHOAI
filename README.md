#  Xây Dựng Trò Chơi Trên Điện Thoại

Dự án xây dựng trò chơi **Chill Chill**, một game nông trại pixel-art yên bình cho thiết bị di động, từ khâu lên ý tưởng, thiết kế, lập trình, kiểm thử cho đến đóng gói sản phẩm.

##  Giới thiệu

Game di động hiện nay phần lớn xây dựng trên áp lực: đếm ngược thời gian, bảng xếp hạng, nhiệm vụ hằng ngày. **Chill Chill** đi theo hướng ngược lại: người chơi thừa kế một mảnh đất bỏ hoang ở đáy thung lũng, dọn dẹp, cày xới, gieo hạt và chờ xem một năm làm nông sẽ mang lại điều gì. **Không có bộ đếm thời gian thúc ép và không có cách nào để thua cuộc.**

Dự án là cơ hội để nhóm sinh viên vận dụng kiến thức về lập trình, thiết kế, làm việc nhóm và quản lý dự án vào một sản phẩm thực tế. Nhóm áp dụng quy trình: **lập kế hoạch → phân công → phát triển → kiểm thử → nghiệm thu**.

##  Mục tiêu

**Mục tiêu chung:** Xây dựng thành công một trò chơi nông trại hoàn chỉnh, chạy ổn định, giao diện thân thiện và thể hiện nhất quán triết lý "chơi thư giãn" ở cả lối chơi lẫn cách tổ chức phần mềm.

**Mục tiêu cụ thể:**
- Thiết kế lối chơi yên bình, dễ tiếp cận: 4 mùa, 15 loại cây trồng, 7 loài vật nuôi, chuỗi sản xuất 3 cấp
- Xây dựng giao diện pixel-art trực quan: toàn bộ màn hình là game, không widget DOM
- Lập trình đầy đủ chức năng cốt lõi: di chuyển, canh tác, chăn nuôi, cửa hàng, qua đêm (Overnight Pass), lưu/tải game
- Tích hợp đồ họa pixel và âm thanh tổng hợp (WebAudio) tạo trải nghiệm sinh động
- Hỗ trợ khả năng tiếp cận: điều khiển bằng bàn phím, trình đọc màn hình, giảm chuyển động
- Kiểm thử bằng unit test trước khi phát hành
- Rèn luyện kỹ năng làm việc nhóm, quản lý tiến độ và sử dụng Git/GitHub

##  Gameplay (Game CHILL CHILL tóm tắt)

Mỗi ngày trong game chạy từ 6:00 sáng đến 2:00 sáng hôm sau. Người chơi đi bộ quanh trang trại, dùng công cụ trên ô đối diện, vào các tòa nhà, và đi ngủ để sang ngày mới. Một năm có 4 mùa, mỗi mùa 28 ngày; thời tiết có ý nghĩa thực sự (mưa tưới cả trang trại qua đêm, tuyết không tưới, cây khô 3 ngày liên tiếp sẽ héo).

Các màn hình chính:
- Trang trại (màn hình chính) – thế giới game, toàn bộ màn hình là game
- Bên trong tòa nhà – chuồng gà, chuồng bò, nhà chính, xưởng, silo (20 tòa nhà đều bước vào được)
- Cửa hàng (phím B) – mua hạt giống, vòi phun, phân bón, động vật; bán sản phẩm
- Túi đồ (phím I) – xem vật phẩm đang có
- Báo cáo buổi sáng (DayReport) – hiển thị kết quả qua đêm: đã cho ăn, sản xuất, máy móc hoàn thành, động vật ốm
- Trợ giúp (phím H / F1) – hướng dẫn chơi

Điều khiển chính: mũi tên/WASD để đi, Space/Enter để dùng vật phía trước, 1-7 chọn công cụ, Q/E đổi hạt giống, N đi ngủ, M tắt tiếng, Esc đóng panel.

##  Công nghệ và công cụ sử dụng

| Nhóm | Công cụ |
|---|---|
| Phát triển | TypeScript, Vite, Electron, Canvas 2D, Visual Studio Code |
| Thiết kế & đồ họa & âm  | Pixel-art vẽ từ code, font bitmap 5×7, WebAudio API (âm thanh tổng hợp từ oscillator) |
| Quản lý dự án & cộng tác | Git & GitHub, GitHub Actions, Google Drive / Docs, Messenger |
| Kiểm thử & triển khai |Vitest, electron-builder, Squirrel.Windows, Capacitor 6 + Android Studio (bản Android) |

Yêu cầu môi trường: Node.js 22 trở lên. Với bản Android: JDK 17, Android SDK 34, Android Studio Hedgehog (2023.1.1) trở lên.

##  Cấu trúc dự án

```
├── src/
│   ├── game/        # Luật chơi thuần: lịch, cây trồng, sinh thế giới, hành động, cửa hàng, save
│   ├── engine/      # Nguyên thủy pixel: palette, font 5×7, vẽ, input, UI, âm thanh tổng hợp
│   ├── art/         # Vẽ tile, cây, nông dân, phong cảnh, thời tiết
│   └── renderer/    # Scene, vòng lặp frame, cầu nối tới Electron
├── electron/        # Main process và preload script
├── tests/           # Unit test cho tầng luật chơi
├── docs/            # Hợp đồng module cho từng lớp
├── DESIGN.md        # Định hướng nghệ thuật: màu, ánh sáng, chuyển động, UI, âm thanh
├── .gitignore
└── README.md
```

##  Nhóm thực hiện & Phân chia công việc

| Thành viên | Vai trò | Công việc phụ trách |
|---|---|---|
| Nguyễn Thị Phương Diễm | Trưởng nhóm / Quản lý dự án | Lập kế hoạch, phân công, theo dõi tiến độ (Trello/Jira), tổng hợp báo cáo, |
| Đinh Xuân Quang | Lập trình Gameplay (Lead Developer) |Tầng luật chơi, canh tác, chăn nuôi, Overnight Pass, lưu trạng thái game |
| Trần Đức Giang | Lập trình UI/UX & Âm thanh | Giao diện cửa hàng, túi đồ, trợ giúp; âm thanh WebAudio |
| Hà Duy Quang | Đồ họa & Thiết kế màn chơi |Sprite, tile, cây trồng, phong cảnh, thời tiết; sinh thế giới|
| Đỗ Việt Anh | Kiểm thử phần mềm (Tester/QA) & Tài liệu | Test case, kiểm thử đa thiết bị, bug report, tài liệu hướng dẫn |

##  Kế hoạch thực hiện (Timeline)

| Thời gian | Giai đoạn | Nội dung chính |
|---|---|---|
| Tuần 1 – 2 | Khởi động dự án | Họp nhóm, chọn ý tưởng game, xây dựng tài liệu thiêt , phân công vai trò |
| Tuần 3 – 5 | Xây dựng nền tảng | Thiết lập dự án, engine pixel, khung gameplay cơ bản |
| Tuần 6 – 8 | Phát triển tính năng | Hoàn thiện canh tác, chăn nuôi, chuỗi sản xuất, cửa hàng, âm thanh, đồ họa |
| Tuần 9 – 10 | Kiểm thử & sửa lỗi | Viết/chạy unit test, kiểm thử, sửa lỗi |
| Tuần 11 | Hoàn thiện & đóng gói | Tối ưu hiệu năng, đóng gói installer, chuẩn bị demo |
| Tuần 12 | Báo cáo & nghiệm thu | Tổng hợp tài liệu, thuyết trình, báo cáo tổng kết |

##  Đầu ra mỗi thành viên cần đạt

- **Quản lý dự án:** Tài liệu hoàn chỉnh, kế hoạch dự án, báo cáo tổng kết, biên bản họp nhóm hằng tuần
- **Lập trình Gameplay:** Tầng luật chơi ổn định, source code có chú thích rõ ràng, không lỗi crash
- **UI/UX & Âm thanh:** Bộ giao diện hoàn chỉnh , âm thanh tích hợp mượt
-** **Đồ họa & Level Design:** Bộ pixel-art đúng phong cách (bảng màu hoàng hôn), thế giới sinh từ seed
- **Kiểm thử & Tài liệu:** Bảng unit test đầy đủ, bug list kèm mức độ ưu tiên, README hướng dẫn cài đặt & sử dụng

##  Kết quả mong đợi

Một bản build Chill Chill hoàn chỉnh (installer Windows, kèm bản Android qua Capacitor), chạy ổn định, cùng bộ tài liệu đầy đủ (tổng quan game, sơ đồ phân tích thiết kế hệ thống gồm DFD, ERD, Use Case, sơ đồ lớp) làm nền tảng để nhóm tiếp tục phát triển, mở rộng game.
##  Quy trình quản lý mã nguồn

- Quản lý mã nguồn bằng **Git/GitHub** theo mô hình nhánh (feature branch)
- Review code trước khi gộp (merge) vào nhánh `main`
- Theo dõi công việc bằng bảng Kanban trên Trello: **Cần làm – Đang làm – Đã xong**

##  Hướng dẫn chạy dự án 

1. Cài đặt Node.js 22 trở lên
2. Chạy npm install để cài các phụ thuộc
3. npm run dev để xem nhanh trên trình duyệt (Vite dev server), hoặc npm start để build và chạy trong Electron
4. npm test để chạy unit test (vitest)
5. npm run build để type-check và build; npm run package để đóng gói installer vào release/

##  License

Dự án phục vụ mục đích học tập.
