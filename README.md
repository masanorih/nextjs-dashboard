## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

<pre>
MEMO:
- pnpm devで開発 serverを起動することが出来る
  pnpm は npm で install
  % sudo npm install -g pnpm
  npm は apt で install
  % sudo apt install npm

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
</pre>
