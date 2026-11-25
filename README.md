# srs-ag13-architecture-design

**AG-13** · Agent Node · phiên bản **1.0.0** · giấy phép MIT

> Vietnamese-language Claude skill — one independent, reusable service of the SRS-SOP agent pipeline. Machine-readable contract: [`skill.json`](skill.json).

Agent Node AG-13 (pha Thiết kế SOP): thiết kế kiến trúc phần mềm (SAD, TL-06) từ mô hình nghiệp vụ AG-06 + NFR AG-11 — thành phần, phân tầng, tích hợp, deployment, quyết định kiến trúc (ADR), truy vết UC/NFR.

## Hợp đồng giao tiếp

Skill là một dịch vụ độc lập, ghép lỏng: nhận đầu vào và trả đầu ra dưới dạng tài liệu/JSON mô tả trong [`SKILL.md`](SKILL.md), không gọi trực tiếp skill khác và không gắn với dự án cụ thể. Dùng riêng lẻ, hoặc ghép qua bộ điều phối [`srs-sop-pipeline`](https://github.com/HaNguyen1409/srs-sop-pipeline).

| Bước SOP | Việc | Loại | Nhận từ | Chuyển tới |
|---|---|---|---|---|
| 26 | Thiết kế kiến trúc (SAD, TL-06) — chốt phong cách API + cơ chế auth | Agent | B18, B19, B9 | B27, B28, B29 |

**Skill phía trước (cấp đầu vào):** [`srs-ag10-functional-spec`](https://github.com/HaNguyen1409/srs-ag10-functional-spec) `^1.0.0` · [`srs-ag14-data-design`](https://github.com/HaNguyen1409/srs-ag14-data-design) `^1.0.0` · [`srs-ag11-nfr-spec`](https://github.com/HaNguyen1409/srs-ag11-nfr-spec) `^1.0.0` · [`srs-ag06-business-model`](https://github.com/HaNguyen1409/srs-ag06-business-model) `^1.4.2`

**Skill phía sau (dùng đầu ra):** [`srs-ag14-data-design`](https://github.com/HaNguyen1409/srs-ag14-data-design) `^1.0.0` · [`srs-ag15-api-interface-design`](https://github.com/HaNguyen1409/srs-ag15-api-interface-design) `^1.0.0` · [`srs-ag16-security-design`](https://github.com/HaNguyen1409/srs-ag16-security-design) `^1.0.0`

## Cài đặt

**Claude Code** — clone đúng phiên bản vào thư mục skill:

```bash
git clone --branch v1.0.0 https://github.com/HaNguyen1409/srs-ag13-architecture-design.git ~/.claude/skills/srs-ag13-architecture-design
```

Nâng cấp: `git -C ~/.claude/skills/srs-ag13-architecture-design fetch --tags && git -C ~/.claude/skills/srs-ag13-architecture-design checkout v<phiên-bản-mới>`.

**claude.ai / Claude Desktop** — tải `srs-ag13-architecture-design-v1.0.0.zip` ở trang [Releases](https://github.com/HaNguyen1409/srs-ag13-architecture-design/releases) rồi tải lên ở phần Skills trong cài đặt.

**Cả bộ** — xem [`srs-sop-skills`](https://github.com/HaNguyen1409/srs-sop-skills) (cài toàn bộ skill theo phiên bản đã khoá).

## Quản lý phiên bản

Theo [SemVer](https://semver.org/lang/vi/), áp cho hợp đồng giao tiếp của skill:

| Tăng | Khi |
|---|---|
| MAJOR | Đổi hợp đồng làm vỡ skill phía sau: đổi/bỏ trường JSON, đổi hệ mã ID, đổi bố cục tài liệu đầu ra |
| MINOR | Thêm khả năng tương thích ngược: trường tuỳ chọn, mục mới, chế độ mới |
| PATCH | Sửa câu chữ, sửa lỗi, làm rõ luật mà không đổi đầu ra |

Phát hành: sửa `SKILL.md` → tăng `version` trong frontmatter, `VERSION`, `skill.json` → thêm mục vào [`CHANGELOG.md`](CHANGELOG.md) → `python tools/check_skill.py` → commit → `git tag -a vX.Y.Z -m "vX.Y.Z"` → `git push --follow-tags`. GitHub Actions kiểm lại, chạy test và đính kèm zip vào Release.

## Giấy phép

MIT — xem [`LICENSE`](LICENSE).
