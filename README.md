# Git Flow / GitHub Flow 操作紀錄

本專案用來練習 Git 與 GitHub 的基本協作流程，包含：

1. 建立分支（Branch）
2. 合併分支（Merge）
3. Fork 專案
4. 建立 Pull Request

---

## 1. 建立分支（Branch）

首先從 `main` 建立一個新的開發分支 `developGitBranch`：

```bash
git switch -c developGitBranch
```

建立 `gitBranch.md` 檔案後，確認 Git 狀態：

```bash
git status
```

將檔案加入暫存區：

```bash
git add gitBranch.md
```

建立 Commit：

```bash
git commit -m "add gitBranch.md"
```

最後將新的分支 Push 到 GitHub：

```bash
git push -u origin developGitBranch
```

完成後，GitHub Repository 中就會同時存在 `main` 與 `developGitBranch` 分支。

流程：

```text
main
 └── developGitBranch
       └── add gitBranch.md
```

---

## 2. 合併分支（Merge）

完成 `developGitBranch` 的修改後，先切換回 `main`：

```bash
git switch main
```

同步 GitHub 上的最新內容：

```bash
git pull origin main
```

接著將 `developGitBranch` 合併回 `main`：

```bash
git merge developGitBranch
```

最後將合併完成的 `main` Push 到 GitHub：

```bash
git push origin main
```

完成後，原本只存在於 `developGitBranch` 的 `gitBranch.md` 就會出現在 `main` 中。

流程：

```text
main
 │
 └── developGitBranch
          │
          └── 修改與 Commit
                    │
                    ▼
                  Merge
                    │
                    ▼
                   main
```

---

## 3. Fork 專案

接著練習 GitHub 的 Fork 功能。

首先在 GitHub 上進入 Organization 的母專案：

```text
yang-organization/git-example
```

使用 GitHub 網頁右上方的 **Fork** 功能，將 Repository Fork 到自己的 GitHub 帳號。

Fork 完成後：

```text
母專案：
yang-organization/git-example

        ↓ Fork

個人專案：
ChunYang0808/git-example
```

接著設定本機 Git Remote。

將原本的 `origin` 改名為 `upstream`：

```bash
git remote rename origin upstream
```

將自己的 Fork 設定為新的 `origin`：

```bash
git remote add origin git@github.com:ChunYang0808/git-example.git
```

使用以下指令確認 Remote：

```bash
git remote -v
```

設定完成後：

- `origin`：`ChunYang0808/git-example`，自己的 Fork
- `upstream`：`yang-organization/git-example`，Organization 的母專案

接著建立 `ChunYang0808Fork.md`，並提交修改：

```bash
git add ChunYang0808Fork.md
git commit -m "add ChunYang0808Fork.md"
git push origin main
```

此時修改會先被 Push 到自己的 Fork，而不是直接修改 Organization 的母專案。

---

## 4. Pull Request

將修改 Push 到自己的 Fork 後，在 GitHub 上進入：

```text
ChunYang0808/git-example
```

點選：

```text
Contribute
→ Open pull request
```

建立 Pull Request 時設定：

```text
來源：
ChunYang0808/git-example:main

        ↓ Pull Request

目標：
yang-organization/git-example:main
```

確認沒有 Conflict 後，建立 Pull Request：

```text
Create pull request
```

最後使用：

```text
Merge pull request
→ Confirm merge
```

將自己 Fork 中的修改合併回 Organization 的母專案。

---

# Git 流程說明

## Branch / Merge 流程

本次先從 `main` 建立 `developGitBranch`，在開發分支中新增檔案並建立 Commit，完成後再將分支 Merge 回 `main`。

```text
main
 ↓
建立 developGitBranch
 ↓
修改檔案
 ↓
git add
 ↓
git commit
 ↓
git push
 ↓
切換回 main
 ↓
git merge
 ↓
main
```

這種方式可以讓開發工作先在獨立分支進行，完成後再整合回主要分支，避免直接在 `main` 上進行所有修改。

---

## Fork / Pull Request 流程

Fork 則是將 Organization 的 Repository 複製一份到自己的 GitHub 帳號。

修改自己的 Fork 後，再透過 Pull Request 請求將修改合併回母專案。

```text
Organization 母專案
yang-organization/git-example
        │
        │ Fork
        ▼
個人 Repository
ChunYang0808/git-example
        │
        │ 修改檔案
        ▼
Commit
        │
        ▼
Push
        │
        ▼
Pull Request
        │
        ▼
Merge
        │
        ▼
Organization 母專案
```

這種流程適合多人協作或沒有母專案直接寫入權限的情況，開發者可以先在自己的 Fork 中修改，再透過 Pull Request 提交變更。

---

## 本次練習結果

本次實際完成：

- [x] 建立 `developGitBranch` 分支
- [x] 在分支新增 `gitBranch.md`
- [x] 將 `developGitBranch` 合併回 `main`
- [x] Fork Organization Repository 到個人帳號
- [x] 設定 `origin` 與 `upstream`
- [x] 在個人 Fork 新增 `ChunYang0808Fork.md`
- [x] Push 修改到個人 Fork
- [x] 建立 Pull Request
- [x] 將 Pull Request Merge 回 Organization Repository