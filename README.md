# aspace-theme-ja

ArchivesSpace の公開画面（PUI）のための、日本語向けの見た目のプラグインです。
CSS だけで動き、画面の HTML（ERB）は書き換えません。

- 淡いグレーの地に白いカード、上端に固定される 1 段のヘッダー
- 大きな検索欄、絞り込みはチップ
- 資料の項目は「項目名｜値」の 2 段組
- 外部のサーバーから文字を読み込みません（端末に入っている日本語の文字を使います）

ArchivesSpace v4.2.1 で確認しています。

## 入れ方

```sh
cd /path/to/archivesspace/plugins
git clone https://github.com/nakamura196/aspace-theme-ja.git ja_theme
```

`config/config.rb` の `AppConfig[:plugins]` に `ja_theme` を足し、ArchivesSpace を再起動します。

```ruby
AppConfig[:plugins] = ['local', 'ja_theme']
```

フォルダ名は `ja_theme` にしてください。設定に書く名前と同じである必要があります。

画面の言葉を日本語にするのは、このプラグインの役目ではありません（`AppConfig[:locale] = :ja` と、訳の上書き用のプラグインで行います）。

## 色や文字を館ごとに変える

このプラグインのファイルは書き換えず、館用のプラグインを 1 つ作って変数だけを上書きします。

ArchivesSpace は、すべてのプラグインの `public/views/layout_head.html.erb` を、`AppConfig[:plugins]` に並べた順に読み込みます。
そのため、後ろに並べたプラグインの値が勝ちます。

```
plugins/my_theme/public/views/layout_head.html.erb
```

```erb
<style>
  :root {
    --c-accent: #2292ca;
    --c-accent-dark: #17709d;
    --c-accent-light: #39a9dd;
    --c-accent-soft: #e7f3fa;
    --c-accent-line: #bfdcee;
    --c-focus-ring: 0 0 0 3px rgba(34, 146, 202, .18);
    --c-hero-top: #eaf4fa;
    --c-hero-glow: rgba(34, 146, 202, .14);
  }
</style>
```

```ruby
AppConfig[:plugins] = ['local', 'ja_theme', 'my_theme']
```

Web フォントを使いたいときも、同じファイルに `<link>` を足します。

### 変数の一覧

| 種類 | 変数 |
|---|---|
| 文字 | `--c-font` |
| 差し色 | `--c-accent` `--c-accent-dark` `--c-accent-light` `--c-accent-soft` `--c-accent-line` `--c-on-accent` `--c-focus-ring` |
| トップの帯 | `--c-hero-top` `--c-hero-glow` |
| 文字の濃淡 | `--c-text` `--c-sub` `--c-muted` `--c-placeholder` `--c-disabled` |
| 面 | `--c-bg` `--c-surface` `--c-soft` `--c-segment-bg` `--c-segment-hover` `--c-header-bg` |
| 罫線・強調 | `--c-line` `--c-line-strong` `--c-mark` |
| 角丸 | `--c-radius` `--c-radius-sm` `--c-radius-lg` `--c-radius-pill` `--c-btn-radius` `--c-action-radius` |
| 影 | `--c-shadow` `--c-shadow-hover` `--c-shadow-pop` `--c-shadow-modal` |
| 幅 | `--c-max` |

## English

A CSS-only theme for the ArchivesSpace Public User Interface, designed for Japanese-language sites.
Clone it into `plugins/ja_theme` and add `ja_theme` to `AppConfig[:plugins]`.
To customise colours or fonts, create another plugin whose `public/views/layout_head.html.erb` overrides the `--c-*` CSS variables in `:root`, and list it after `ja_theme`.
Tested with ArchivesSpace v4.2.1.

## ライセンス

MIT License。作成: 中村 覚（東京大学） / Satoru Nakamura (The University of Tokyo)
