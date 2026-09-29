Збірка форку з запіненими залежностями. Усе вбудовано в один файл, під час встановлення нічого не тягнеться з npm.

## 1. Завантажити й перевірити

```bash
V={{TAG}}
B=https://github.com/{{REPO}}/releases/download/$V
mkdir asc-mcp-$V && cd asc-mcp-$V
curl -fsSL --remote-name-all $B/asc-mcp-$V.tgz $B/heimdall-asc-$V.mcpb $B/SHA256SUMS
shasum -a 256 -c SHA256SUMS
```

Обидва рядки мають закінчитись на `OK`, інакше не встановлювати.

Якщо встановлено `gh`, можна ще перевірити, що файли зібрав CI саме з цього тегу:

```bash
gh attestation verify asc-mcp-$V.tgz -R {{REPO}}
gh attestation verify heimdall-asc-$V.mcpb -R {{REPO}}
```

## 2a. Claude Code

```bash
npm install -g ./asc-mcp-{{TAG}}.tgz
asc-mcp setup
```

`setup` кладе `.p8` у macOS Keychain і реєструє вибрані профілі. Після нього файл `.p8` можна видалити з диска.

## 2b. Claude Desktop

Двічі клікнути `heimdall-asc-{{TAG}}.mcpb`, вказати профіль і шлях до `.p8`. Файл ключа тримати з правами `600`.

## Не робити

- `npx @erayendes/asc-mcp ...` та `npm update -g` — це upstream з npm, без наших пінів.
- Не ділитись `.p8` у чатах і не комітити його.
