Збірка форку з запіненими залежностями. Усе вбудовано в один файл, під час встановлення нічого не тягнеться з npm.

## 1. Завантажити й перевірити

```bash
gh release download {{TAG}} -R {{REPO}} -D asc-mcp-{{TAG}} && cd asc-mcp-{{TAG}}
shasum -a 256 -c SHA256SUMS
gh attestation verify asc-mcp-{{TAG}}.tgz -R {{REPO}}
gh attestation verify heimdall-asc-{{TAG}}.mcpb -R {{REPO}}
```

Якщо хоч одна перевірка впала — не встановлювати.

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
