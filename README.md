# B-AutoLearn

Trợ lý học các khoá online bằng **Claude Code + Chrome của chính bạn**.

B-AutoLearn là một [skill](https://code.claude.com/docs/en/skills) cho Claude Code. Sau khi
cài, bạn chỉ cần kết nối Claude với Chrome rồi bảo:

> "Dùng skill auto-learn, học giúp mình khoá này: `<link khoá học>`"

Claude sẽ mở link trong Chrome của bạn (tận dụng sẵn phiên đăng nhập), đi qua từng bài,
đọc/tóm tắt nội dung, điền các hoạt động học, chụp màn hình và báo tiến độ — **dừng xin
xác nhận trước mọi thao tác không hoàn tác được** (nộp bài, gửi, xoá…).

> ⚠️ **Dùng có trách nhiệm.** Công cụ này điều khiển trình duyệt của chính bạn cho các khoá
> học bạn đã ghi danh. Bạn tự chịu trách nhiệm tuân thủ điều khoản sử dụng của từng nền tảng.

## Yêu cầu

- [Claude Code](https://code.claude.com) (CLI, hoặc extension VS Code) — đã `/login`.
- Google Chrome (hoặc trình duyệt Chromium).
- Node.js (để chạy `npx`).
- macOS / Windows / Linux (xem lưu ý theo HĐH trong [`setup/install.md`](setup/install.md)).

## Cài đặt nhanh

1. **Clone repo và chép skill vào Claude:**
   ```bash
   git clone https://github.com/haobv/B-AutoLearn.git
   mkdir -p ~/.claude/skills
   cp -r B-AutoLearn/skills/auto-learn ~/.claude/skills/
   ```
2. **Thêm MCP điều khiển Chrome:**
   ```bash
   claude mcp add -s user chrome-devtools -- npx -y chrome-devtools-mcp@latest --autoConnect
   ```
3. **Bật remote debugging trên Chrome** và (macOS) cấp Full Disk Access cho terminal/VS Code
   — chi tiết trong [`setup/install.md`](setup/install.md).
4. Mở một phiên Claude Code mới để nạp skill và công cụ.

## Cách dùng

1. Mở Chrome, đăng nhập sẵn vào nền tảng học của bạn.
2. Trong Claude Code:
   > "Dùng skill auto-learn mở và học giúp mình: `https://…/course/…`"
3. Lần đầu Chrome có thể hỏi cho phép kết nối — bấm **Allow**.
4. Gặp màn hình đăng nhập/MFA, Claude sẽ nhờ bạn tự đăng nhập rồi tiếp tục.

Xem thêm ví dụ prompt trong [`examples.md`](examples.md).

## An toàn (tóm tắt — chi tiết trong SKILL)

- Chỉ thao tác trên tab Claude tự mở; không đụng tab khác của bạn.
- Không nhập mật khẩu/OTP/thẻ; không đăng xuất; không đổi cài đặt.
- Dừng xin xác nhận trước khi Submit/Gửi/Xoá/Nộp bài.
- Bài thi một-lần/tính giờ: báo bạn trước khi vào.
- Việc cần sản phẩm thật (code, tài liệu nộp): giao lại cho bạn, không bịa.

## License

[MIT](LICENSE)
