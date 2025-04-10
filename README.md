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

- onchange event での検索実行などは backend 負荷が大きいため、
  import { useDebouncedCallback } from 'use-debounce';
  const handleSearch = useDebouncedCallback((term) => {
    ...
  }, 300);
  と useDebouncedCallback で call する関数を定義すると、指定の時間間隔(300ms?)
  連続して関数が呼ばれないようにしてくれる。

- app/lib/definitions.ts に input 用の定義がある。
  string, number, 'man' | 'woman' などが使える
  validation library は Zod で行っている

- amount type は coerce によって validate 時に number に変換されている

- 更新後に `revalidatePath('/dashboard/invoices');` することで
  /dashboard/invoices が最新の情報を fetch することが可能
  さらに `redirect('/dashboard/invoices');` でリダイレクトも可能

- url parameter はディレクトリで表現するらしく、`invoices/[id]/edit/page.tsx`
  と [foo] でディレクトリを作成する

- invoices.id は uuidv4 なので url に uuid が入る

- app/ui/invoices/table.tsx        - UpdateInvoice component
  app/ui/invoices/buttons.tsx      - /dashboard/invoices/${id}/edit link href
  app/dashboard/[id]/edit/page.tsx - Form component
  app/ui/invoices/edit-form.tsx    - EditInvoiceForm()
  app/lib/actions.ts               - updateInvoice()
  という遷移で画面が表示、更新される

- DB fetch 系の関数は大体 `app/lib/data.ts` に定義されており、こいつがモデル層っぽい
  ふるまいをするようになっているが、一部直接 sql 書かれたりもしている(action.ts 等)

- http://localhost:3000/dashboard/invoices/2e94d1ed-d220-449f-9f11-f0bbceed9645/edit
  のような存在しないid の url へアクセスすると、
  1. dashboard/invoices/error.tsx を表示する
  2. page.tsx で notFound() を call していれば、edit/not-found.tsx を表示する。

- package.json に script: { "lint": "next lint" } を追加して pnpm lint を
  実行すると静的解析してくれる

- chapter15 で `% pnpm i next-auth@beta` して NextAuth.js を追加
  `openssl rand -base64 32` して結果を .env に貼り付け

- どの layout.js, page.js に対しても metadata object を定義することにより
  meta 要素を head に付与することが出来る
  app/layout.js に書いた metadata が一番強く、その下の page.js に書くと、
  部分的に override 出来る。

  app/layout.js を title: {template: '%s | bar', default:'foo'} とし、
  hogehoge/page.js で title:{ 'hogehoge' } とすると %s に hogehoge を代入することが出来る

- tutorial 的な要素として mv するんだけど、
  favicon.ico, opengraph-image.png は /public ではなく /app に配置するのが正解？
</pre>
