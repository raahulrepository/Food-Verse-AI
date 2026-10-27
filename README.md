# Food Verse AI

## VS Code mein run karne ke steps

### Requirements

- Node.js 24
- pnpm
- Apni Gemini API key

### 1. Dependencies install karein

ZIP extract karke project ka root folder VS Code mein open karein. Root folder ke terminal mein:

```bash
pnpm install
```

### 2. API key set karein

`artifacts/api-server/.env.example` ki copy banakar uska naam `.env` rakhein. Is file mein apni Gemini key `GEMINI_API_KEY=` ke baad add karein:

```env
GEMINI_API_KEY=your_gemini_api_key
```

Key ZIP mein shamil nahi hai. Ise code files mein paste ya GitHub par upload na karein. Gemini usage par aapke provider account ke charges lag sakte hain.

### 3. API server start karein

VS Code mein pehla terminal kholkar project root se run karein:

**Windows PowerShell**

```powershell
$env:PORT = "5000"
pnpm --filter @workspace/api-server run dev
```

**macOS / Linux**

```bash
PORT=5000 pnpm --filter @workspace/api-server run dev
```

Terminal chalta rehne dein.

### 4. Web app start karein

`artifacts/food-verse/.env.example` ki copy usi folder mein `.env` naam se rakhein. Ismein `VITE_API_BASE_URL=http://localhost:5000` rehne dein.

VS Code mein doosra terminal kholkar root folder se run karein:

**Windows PowerShell**

```powershell
$env:PORT = "5173"
$env:BASE_PATH = "/"
pnpm --filter @workspace/food-verse run dev
```

**macOS / Linux**

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/food-verse run dev
```

Browser mein **http://localhost:5173** kholein.

## Notes

- Dono servers ko alag terminals mein chalu rakhein.
- Current version ko database ki zaroorat nahi hai.
- Photo aur video frames save nahi hote. Recent text summaries usi browser mein rehti hain.
- Food safety, hygiene, aur nutrition results AI ke estimates hain—yeh medical advice, official inspection, ya food ke safe hone ka proof nahi hain.
