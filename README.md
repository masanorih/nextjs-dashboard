## Next.js App Router Course - Starter

https://nextjs.org/learn が途中で github への登録を求めてくるので作成したチュートリアル。

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

<pre>
MEMO:
- Ubuntu 24.04.2 LTS on WSL2 での環境構築手順
  npm は apt で install
  % sudo apt install npm

  pnpm は npm で install
  % sudo npm install -g pnpm

  開発環境を起動する
  % pnpm run dev

- 他環境で新たに git clone して開発する場合の注意点

  chapter10. でカナリヤ版を入れたので他環境で開発環境を立ち上げるには以下が必要かも
  % pnpm install next@canary
  現状
      "next": "15.3.0-canary.24",
  が入る

  vercel の postgresql の .env がリポジトリにはないので
  https://nextjs.org/learn/dashboard-app/setting-up-your-database
  の手順で local に作成する必要がある

- /app/layout.tsx に css import を書くと、global に css を設定可能
  import '@/app/ui/global.css';

- 上記 global.css で base, components, utilities の @tailwind を宣言してる

- import path を @ から始めることで app root からの path を表現出来るみたい
  next 謹製のライブラリは @なしで
  import Link from 'next/link';
  と import 出来る

- Tailwind を利用して className に css プロパティを記述することが出来る
  <main className="flex min-h-screen flex-col p-6">

- app/hogehoge/page.tsx を生やすことで /hogehoge でアクセス可能なページを
  追加していくことが出来る
  app/foo/bar/page.tsx みたいにネストすることも出来る

- RootLayout は全ての基底になる特別なレイアウトで必ず一つ必要
  app/layout.tsx で定義されている

- a tag で link すると完全な再読み込みが実行されるので、Link component を使う
  Link component は prod環境では prefetch を行う模様

- postgres module の sql() は Promise を返すので `await Promise.all(q1, q2, ...)` で
  パラレルにクエリ発行が可能

- app/dashboard/(hogehoge)/ とカッコでディレクトリを作ると特別？と見なされる
  app/dashboard/ に置いたものとみなされる？

- app/dashboard/ 配下に url に対応するページを配置して、
  app/ui/dashboard/ 配下に内容物(コンポーネント)を配置していく

- 部分的なプリレンダリングを行う Partial Prerendering は
  next.config.ts で
  experimental: {
    ppr: 'incremental'
  }
  して
  layout.tsx で
  export const experimental_ppr = true;
  すればいいだけなので簡単。Next.js 14 で投入された新機能な点に注意が必要
</pre>
