# claude-skills

[English](README.md) · **Türkçe**

Claude Code ve `npx skills` destekleyen diğer AI ajanları için yazdığım skill'ler.

## Skill'ler

| Skill | Ne yapar |
|---|---|
| [orchestration](skills/orchestration/SKILL.md) | Büyük işleri bağımsız parçalara böler, paralel arka plan subagent'larıyla çalıştırır, her sonucu doğrular ve tek bir cevapta birleştirir. Çok bileşenli özellikler, geniş araştırmalar ve incelemeler için. |
| [apple-design](skills/apple-design/SKILL.md) | Apple'ın tasarım ve arayüz kodlama standartları, platformdan bağımsız: boşluk, hedef boyutları, tipografi, renk ve kontrast, hareket, bileşen davranışları, arayüz metinleri, girdi, uygulama kalıpları ve bunların kodda uygulanışı. Web, Flutter, React Native, Electron, Tauri ve SwiftUI için. |

## Yapı

```
skills/                     tek başına çalışan skill'ler, her biri kendi klasöründe
  orchestration/
    SKILL.md
  apple-design/
    SKILL.md
    references/             ayrıntılı kurallar, gerektiğinde okunur
.claude-plugin/
  marketplace.json          bu repoyu Claude Code'a marketplace olarak tanıtır
  plugin.json               skills/ altındaki tüm skill'leri paketleyen "furkan-skills" plugin'i
```

Her skill bir klasördür ve içinde şu frontmatter ile başlayan bir `SKILL.md` bulunur:

```markdown
---
name: skill-adi            # zorunlu: klasör adıyla aynı; a-z, 0-9 ve tek tire; en fazla 64 karakter
description: Ne yapar ve ne zaman kullanılmalı.   # zorunlu: en fazla 1024 karakter
license: MIT               # opsiyonel
compatibility: Python 3 gerekir.                  # opsiyonel, sadece özel bir gereksinim varsa (en fazla 500 karakter)
metadata:                  # opsiyonel, string → string
  author: furkansenturk
  version: "1.0.0"
---
```

Format [Agent Skills spesifikasyonuna](https://agentskills.io/specification) uyar. `SKILL.md` 500 satırın altında kalır. Uzun dokümanlar `references/`, yardımcı scriptler `scripts/`, şablon ve veri dosyaları `assets/` altına konur. Dosya yolları skill klasörüne göre yazılır. 100 satırı aşan referans dosyalarının başında içindekiler listesi bulunur.

## Kurulum

### Seçenek 1: `npx skills` (Claude Code, Cursor, Codex vb.)

```bash
npx skills add furkansenturk/claude-skills                          # hepsi
npx skills add furkansenturk/claude-skills --skill apple-design     # tek skill
```

### Seçenek 2: Claude Code plugin

```
/plugin marketplace add furkansenturk/claude-skills
/plugin install furkan-skills@claude-skills   # skills/ altındaki tüm skill'ler
```

### Seçenek 3: Elle

```bash
git clone https://github.com/furkansenturk/claude-skills
cp -r claude-skills/skills/* ~/.claude/skills/
```

## Yeni skill ekleme

1. `skills/` altında skill adıyla bir klasör aç ve içine `SKILL.md` koy (frontmatter yukarıda).
2. Yukarıdaki tabloya hem `README.md` hem `README.tr.md` içinde ekle.
3. Commit et, push et.

## Lisans

[MIT](LICENSE).

`apple-design` skill'i Apple'ın Human Interface Guidelines'ını kendi cümleleriyle özetler. Apple Inc. ile bağlantılı değildir ve Apple tarafından onaylanmamıştır. Apple ve ilgili adlar Apple Inc.'in ticari markalarıdır.
