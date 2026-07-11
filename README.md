# Hanzi Mnemonics Generator

GitHub Action chạy **10 worker song song** để generate câu chuyện ghi nhớ (mnemonics) tiếng Việt cho chữ Hán trong bảng `zh_kanji_builder` (Supabase) bằng **Mistral AI**.

## Cấu trúc repo

```
zh-mnemonics-generator/
├── .github/
│   └── workflows/
│       └── generate-mnemonics.yml    # Workflow 10 workers
└── scripts/
    └── ai/
        ├── generate_mnemonics.py     # Python script (Mistral API)
        └── README.md                 # Hướng dẫn chi tiết
```

## Setup (1 lần)

### 1. Tạo GitHub repo mới

Vào https://github.com/new → đặt tên `zh-mnemonics-generator` (hoặc gì cũng được) → **Create repository**.

### 2. Add GitHub Secrets

Vào repo mới → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**:

| Secret | Value |
|--------|-------|
| `SUPABASE_URL` | `https://zpkesloqadbqpwrgjrwi.supabase.co` |
| `SUPABASE_SERVICE_KEY` | Service role key từ Supabase Dashboard → Settings → API |
| `MISTRAL_API_KEY_1` | Key 1 từ https://console.mistral.ai/api-keys/ |
| `MISTRAL_API_KEY_2` | Key 2 |
| `MISTRAL_API_KEY_3` | Key 3 |
| `MISTRAL_API_KEY_4` | Key 4 |
| `MISTRAL_API_KEY_5` | Key 5 |
| `MISTRAL_API_KEY_6` | Key 6 |
| `MISTRAL_API_KEY_7` | Key 7 |
| `MISTRAL_API_KEY_8` | Key 8 |
| `MISTRAL_API_KEY_9` | Key 9 |
| `MISTRAL_API_KEY_10` | Key 10 |

**Tổng cộng: 12 secrets.**

### 3. Push code lên repo mới

```bash
# Clone repo mới (thay URL bằng repo của bạn)
git clone https://github.com/YOUR_USERNAME/zh-mnemonics-generator.git
cd zh-mnemonics-generator

# Copy files từ folder này vào repo
# (hoặc dùng download từ máy local)

# Add + commit + push
git add .
git commit -m "Initial commit - 10-worker Mistral AI mnemonics generator"
git push
```

### 4. Chạy workflow

Vào tab **Actions** → **"AI Generate Hanzi Mnemonics (10x Parallel)"** → **Run workflow**:
- **total_limit**: tổng số chữ (chia đều 10 workers) — VD `100` → mỗi worker 10 chữ
- **model**: `mistral-small-latest` (rẻ) / `mistral-large-latest` (chất lượng hơn)
- **batch_size**: 5 (default)

## Tốc độ

| # Chars | 10 workers (song song) | 1 worker |
|---------|------------------------|----------|
| 100 | ~10 giây | ~1.7 phút |
| 1000 | ~1.7 phút | ~17 phút |
| 3000 | ~5 phút | ~50 phút |

## Logs

Mỗi worker có artifact riêng:
- `mnemonics_worker_1.log` + `failed_chars_worker_1.json`
- `mnemonics_worker_2.log` + ...
- ... (worker 3-10)

Vào Actions → run cụ thể → download artifact để xem chi tiết.

## Troubleshooting

Xem file `scripts/ai/README.md` để biết chi tiết troubleshooting, customization, test local.
