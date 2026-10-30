# Cài đặt chi tiết

B-AutoLearn điều khiển Chrome qua MCP server
[`chrome-devtools-mcp`](https://github.com/ChromeDevTools/chrome-devtools-mcp) ở chế độ
`--autoConnect` (gắn vào Chrome bạn đang mở, dùng sẵn các phiên đăng nhập).

## 1. Chép skill vào Claude

```bash
git clone https://github.com/haobv/B-AutoLearn.git
mkdir -p ~/.claude/skills
cp -r B-AutoLearn/skills/auto-learn ~/.claude/skills/
```

## 2. Thêm MCP server (phạm vi user — dùng ở mọi thư mục)

```bash
claude mcp add -s user chrome-devtools -- npx -y chrome-devtools-mcp@latest --autoConnect
```

Gỡ sau này: `claude mcp remove -s user chrome-devtools`.

Yêu cầu: **Chrome 144+** (để hỗ trợ `--autoConnect`) và Node.js (cho `npx`).

## 3. Bật remote debugging cho Chrome

`--autoConnect` gắn vào Chrome đang chạy đã bật remote debugging.

- Mở `chrome://inspect/#remote-debugging` và bật cho phép; hoặc
- Khởi động Chrome với cờ remote debugging, ví dụ:
  - **macOS:**
    ```bash
    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --remote-debugging-port=9222
    ```
  - **Windows:**
    ```bat
    "C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222
    ```
  - **Linux:**
    ```bash
    google-chrome --remote-debugging-port=9222
    ```

Khi Claude kết nối, Chrome có thể hiện hộp thoại cho phép — bấm **Allow**. Trong lúc bị
điều khiển, Chrome hiển thị thanh "đang được phần mềm tự động điều khiển" (bình thường).

## 4. (Chỉ macOS) Cấp Full Disk Access

Trên macOS, app chạy Claude (Terminal hoặc VS Code) cần quyền đọc file cấu hình của Chrome
(`DevToolsActivePort`). Nếu thiếu, bạn sẽ gặp lỗi `EPERM`.

1. **System Settings → Privacy & Security → Full Disk Access**.
2. Bật cho **Terminal** (hoặc **Visual Studio Code**). Thêm bằng nút **+** nếu chưa có.
3. Thoát hẳn app (Cmd+Q) rồi mở lại.

## 5. (Tùy chọn) Cho phép sẵn các công cụ chỉ-đọc

Để Claude khỏi hỏi quyền mỗi lần cho các thao tác chỉ-đọc, thêm allowlist trong
`settings.json` — xem [`settings.snippet.json`](settings.snippet.json). Các thao tác ghi
(click, điền form, chạy script) vẫn nên để hỏi quyền.

## 6. Mở phiên Claude Code mới

Công cụ MCP và skill chỉ nạp khi bắt đầu phiên mới. Mở phiên mới, gõ `/mcp` để kiểm tra
`chrome-devtools` đã **Connected**, rồi bắt đầu dùng skill `auto-learn`.

## Khắc phục sự cố

| Triệu chứng | Cách xử lý |
|---|---|
| `Could not connect to Chrome` | Chrome chưa mở hoặc chưa bật remote debugging — xem bước 3 |
| `EPERM` khi đọc `DevToolsActivePort` | macOS thiếu Full Disk Access — xem bước 4, cấp xong khởi động lại app |
| Không thấy tool `mcp__chrome-devtools__*` | Chạy lại bước 2, rồi mở phiên Claude Code mới |
| Chrome hiện hộp thoại cho phép kết nối | Bấm **Allow** |
