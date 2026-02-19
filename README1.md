# Guide: Running the website on another computer using README2.md

This guide explains how to set up and run the Thái Sport homepage on a **different computer** when you only have the **README2.md** file (which contains all the project code).

---

## What you need

- **README2.md** – the file that contains all the source code (app/page.tsx, layout.tsx, configs, etc.)
- **Carousel images** (optional but recommended) – the 6 image files used in the carousel (`carousel-1.png` through `carousel-6.png`). If you have the original project, copy the `public` folder; otherwise the site will run but the carousel will show broken images until you add your own images.

---

## Step 1: Install Node.js and npm

The website is built with **Node.js**. You need it installed on the other computer.

1. Go to **[https://nodejs.org](https://nodejs.org)**.
2. Download the **LTS** (Long Term Support) version.
3. Run the installer and follow the steps (default options are fine).
4. Open a **terminal** (Command Prompt on Windows, Terminal on Mac/Linux).
5. Check that installation worked:
   ```bash
   node -v
   npm -v
   ```
   You should see version numbers (e.g. `v20.x.x` and `10.x.x`). If you get “command not found”, restart the terminal or add Node to your system PATH.

---

## Step 2: Create the project folder

1. Choose a location for the project (e.g. Desktop or Documents).
2. Create a new folder, for example **Website**:
   - **Windows:** Right‑click → New → Folder → name it `Website`.
   - **Mac/Linux:** In Terminal: `mkdir Website` then `cd Website`.
3. Put **README2.md** inside this folder (copy or move it there).

---

## Step 3: Create the file structure and add the code from README2.md

README2.md is a reference: it contains the code for each file, but it does **not** create the files for you. You must create each file and paste the correct code from README2.md.

### 3.1 Create the `app` folder

- Inside **Website**, create a folder named **app**.

### 3.2 Create each file and copy its code

Open README2.md and find each section below. Copy **only the code inside the code block** (between the triple backticks) into the new file. Do not copy the file path line or the backticks.

| # | Create this file        | In README2.md, find the section titled |
|---|-------------------------|----------------------------------------|
| 1 | `app/page.tsx`         | `## app/page.tsx`                      |
| 2 | `app/layout.tsx`       | `## app/layout.tsx`                    |
| 3 | `app/globals.css`      | `## app/globals.css`                   |
| 4 | `next.config.mjs`      | `## next.config.mjs`                   |
| 5 | `tailwind.config.ts`   | `## tailwind.config.ts`                |
| 6 | `postcss.config.mjs`   | `## postcss.config.mjs`                |
| 7 | `tsconfig.json`        | `## tsconfig.json`                     |
| 8 | `package.json`         | `## package.json`                      |
| 9 | `.eslintrc.json`       | `## .eslintrc.json`                    |

**How to create a file:**

- **Windows:** Right‑click in the folder → New → Text Document → name it exactly as in the table (e.g. `page.tsx`). Rename so it has the correct extension (e.g. `.tsx`, `.json`, `.mjs`, `.css`). Open with a text editor (e.g. Notepad, VS Code) and paste the code.
- **Mac/Linux:** You can use a text editor (TextEdit, VS Code, etc.) and save as the exact filename in the correct folder.
- **Any system:** Using an editor like **VS Code** or **Cursor**: right‑click the folder in the sidebar → New File → type the full filename (e.g. `app/page.tsx`) and paste the code from README2.md.

**Important:**

- File names and extensions must match exactly (e.g. `page.tsx` not `page.txt`).
- `app/page.tsx`, `app/layout.tsx`, and `app/globals.css` go inside the **app** folder. The rest go in the **root** of the Website folder (same level as README2.md).
- For `.eslintrc.json`, the name starts with a dot. Some systems hide “dot files”; you may need to enable “Show hidden files” or create it from the terminal: `touch .eslintrc.json` then open and paste the code.

---

## Step 4: Add the carousel images (public folder)

The homepage shows a carousel with 6 images. The code expects them in a **public** folder.

1. Inside **Website**, create a folder named **public**.
2. Add 6 image files named exactly:
   - `carousel-1.png`
   - `carousel-2.png`
   - `carousel-3.png`
   - `carousel-4.png`
   - `carousel-5.png`
   - `carousel-6.png`

**Option A – You have the original project**

- Copy the entire **public** folder from the original project into **Website**. It should already contain `carousel-1.png` … `carousel-6.png`.

**Option B – You don’t have the images**

- Put any 6 images (e.g. photos or placeholders) in **public** and rename them to `carousel-1.png` … `carousel-6.png`. The site will run; you can replace them later with the correct pictures.

---

## Step 5: Install dependencies and run the website

1. Open a terminal (Command Prompt, PowerShell, or Terminal).
2. Go to the project folder:
   ```bash
   cd path/to/Website
   ```
   Replace `path/to/Website` with the actual path (e.g. `cd Desktop/Website` or `cd ~/Documents/Website`).
3. Install dependencies (this uses `package.json` from README2.md):
   ```bash
   npm install
   ```
   Wait until it finishes. It may take 1–2 minutes.
4. Start the development server:
   ```bash
   npm run dev
   ```
5. When you see something like “Ready in …” and “Local: http://localhost:3003”, open a browser and go to:
   **http://localhost:3003**

You should see the Thái Sport homepage. To stop the server, press **Ctrl+C** in the terminal.

---

## Step 6: If something goes wrong

- **“node not found” or “npm not found”**  
  Install Node.js (Step 1) and restart the terminal.

- **“Cannot find module …”**  
  Make sure you created all 9 files from the table in Step 3 and that you ran `npm install` in the **Website** folder.

- **Carousel shows broken images**  
  Check that the **public** folder exists and contains `carousel-1.png` … `carousel-6.png` (Step 4).

- **Port 3003 already in use**  
  Another app is using that port. Either close that app or change the port in `package.json`: in the `"dev"` script, replace `3003` with another number (e.g. `3004`), then run `npm run dev` again and open `http://localhost:3004`.

- **Build or run errors**  
  Double‑check that:
  - Every file name and path matches the table (e.g. `app/page.tsx` with code from README2.md).
  - You didn’t accidentally include the section title or the markdown code block markers (triple backticks) inside the file.

---

## Summary checklist

- [ ] Node.js and npm installed (`node -v` and `npm -v` work).
- [ ] Project folder created (e.g. **Website**) with README2.md inside.
- [ ] **app** folder created.
- [ ] All 9 files created and code pasted from README2.md (app/page.tsx, app/layout.tsx, app/globals.css, next.config.mjs, tailwind.config.ts, postcss.config.mjs, tsconfig.json, package.json, .eslintrc.json).
- [ ] **public** folder created with `carousel-1.png` … `carousel-6.png`.
- [ ] `npm install` run in the Website folder.
- [ ] `npm run dev` run; browser opened to **http://localhost:3003**.

Once all steps are done, the website will work on the other computer using only README2.md and (if possible) the carousel images.
