# ojochiの案内所

Astro で作成した静的サイトです。
個人HPを「案内所」として構成し、`Home / Profile / Works / お散歩` の4ページで案内します。

公開URL: https://ojochi510510-oss.github.io/

## ローカル起動手順

```bash
npm install
npm run dev
```

本番ビルド確認:

```bash
npm run build
npm run preview
```

## コンテンツ更新方法

サイト内の文章や導線は `src/data/site.ts` にまとめています。

- `siteMeta`: サイト名とイントロ
- `works`: Works ページと Home のプレビューに表示する内容
- `noteThemes`: Home に表示する note の案内
- `osanpoEntries`: お散歩ページと Home の記録表示
- `profileSections`: Profile ページの本文構成
- `updates`: Home 下部の更新欄
- `noteConfig.url`: note の外部URL

更新欄は次のような配列を増やすだけで差し替えできます。

```ts
export const updates = [
  {
    date: "2026.03.09",
    title: "案内所としての構成に整えました",
    description: "人となり、制作、note への入口が先に見えるよう、導線を整理しました。",
  },
];
```

## GitHub Pages 設定手順（ユーザーサイト）

このリポジトリは `ojochi510510-oss.github.io` を想定しています。
GitHub Actions が `gh-pages` 以外のブランチへの push をトリガーに `dist/` を build し、`gh-pages` ブランチのルートへデプロイします。

1. GitHub リポジトリの `Settings` -> `Pages` を開く
2. `Source` で `Deploy from a branch` を選択
3. `Branch` は `gh-pages`、`Folder` は `/(root)` を選択

`gh-pages` ブランチは Actions の初回成功後に自動生成されます。

補足:
- `Settings` -> `Actions` -> `General` の `Workflow permissions` は `Read and write permissions` を推奨します（`GITHUB_TOKEN` で `gh-pages` へ push するため）。
- `gh-pages` は生成物置き場です。手動コミットやPR対象にしない運用にしてください。

## Astro 設定について

`astro.config.mjs` には以下を設定しています。

- `site: "https://ojochi510510-oss.github.io"`

`base` は設定していません。
ユーザーサイト（`https://ojochi510510-oss.github.io/`）はルート配信のため、`/profile` や `/works` をそのまま使えます。
将来 Project Pages（例: `https://<user>.github.io/<repo>/`）へ変更する場合のみ `base` の設定が必要です。
