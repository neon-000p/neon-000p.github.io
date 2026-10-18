# neon-000p.github.io

[AkariEN](https://neon-000p.github.io/toeic-app/) の Google ログイン用のリポジトリ。

AkariEN は Firebase Authentication でログインする。ログインの受け渡しを Firebase 既定の
`toeic-daily-7cea5.firebaseapp.com` で行うと、iPad・iPhone（Safari も Chrome も中身は WebKit）が
ドメインをまたぐ受け渡しを遮り、ログインしても結果がアプリに届かない。
そこで受け渡し用のファイルをアプリと同じドメイン（`neon-000p.github.io`）の `__/auth/` に置き、
アプリの `authDomain` をこのドメインにしている。

- `__/auth/` は Firebase が配るファイルの写し。`.github/workflows/firebase-auth.yml` が取り寄せて
  コミットする（週1回と手動）。手で書き換えない
- `__/firebase/init.json` は Firebase Hosting を使っていないため向こうに無いので、手で置いている
  （中身は AkariEN の `core.js` の `FIREBASE` と同じ、公開されてよい値）
- GitHub Pages は拡張子の無いファイルを HTML として返さないので、`handler` と `iframe` は
  `.html` を付けて置く。`/__/auth/handler` で開くと `handler.html` が返る
- `_` で始まるフォルダを公開するため `.nojekyll` を置いている
- Google Cloud Console の OAuth クライアントに、承認済みのリダイレクト URI として
  `https://neon-000p.github.io/__/auth/handler` を登録してある必要がある

参考: https://firebase.google.com/docs/auth/web/redirect-best-practices （Option 3）
