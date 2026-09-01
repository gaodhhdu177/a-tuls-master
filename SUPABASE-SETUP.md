# A-Tuls — সব ব্রাউজারে একই ডেটা (Supabase Setup)

## ১. Supabase Dashboard-এ যান
https://supabase.com/dashboard → আপনার প্রজেক্ট (tibnmcjnuzkibkoaluwl)

## ২. SQL Editor খুলে নিচের কোড রান করুন

```sql
-- API Keys টেবিল
CREATE TABLE IF NOT EXISTS a_tuls_api_keys (
  id BIGSERIAL PRIMARY KEY,
  user_id TEXT,
  username TEXT,
  key TEXT UNIQUE NOT NULL,
  type TEXT DEFAULT 'free',
  expires TIMESTAMPTZ,
  created TIMESTAMPTZ DEFAULT NOW()
);

-- Users টেবিল
CREATE TABLE IF NOT EXISTS a_tuls_users (
  id TEXT PRIMARY KEY,
  username TEXT,
  email TEXT UNIQUE,
  password TEXT,
  gender TEXT,
  package TEXT DEFAULT 'Free',
  role TEXT DEFAULT 'user',
  api_code TEXT,
  api_type TEXT,
  whatsapp TEXT,
  telegram TEXT,
  security_question TEXT,
  security_answer TEXT,
  fb TEXT DEFAULT '',
  created TIMESTAMPTZ DEFAULT NOW()
);

-- Stories টেবিল
CREATE TABLE IF NOT EXISTS a_tuls_stories (
  id BIGSERIAL PRIMARY KEY,
  name TEXT,
  package TEXT DEFAULT 'Free',
  text TEXT,
  created TIMESTAMPTZ DEFAULT NOW()
);

-- Public read/write (anon key দিয়ে কাজ করবে)
ALTER TABLE a_tuls_api_keys ENABLE ROW LEVEL SECURITY;
ALTER TABLE a_tuls_users ENABLE ROW LEVEL SECURITY;
ALTER TABLE a_tuls_stories ENABLE ROW LEVEL SECURITY;

CREATE POLICY "allow_all_api_keys" ON a_tuls_api_keys FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "allow_all_users" ON a_tuls_users FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "allow_all_stories" ON a_tuls_stories FOR ALL USING (true) WITH CHECK (true);
```

## ৩. কোড আপলোড
`a-tuls-full-site.zip` আনজিপ করে Render-এ আপলোড/রিডিপ্লয় করুন।

## ৪. টেস্ট
1. Admin Panel → API Key Generate (যেকোনো ডিভাইস)
2. অন্য ফোন/ব্রাউজারে Signup → সেই API Code দিন
3. কাজ করবে ✅
