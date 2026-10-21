# GitHub и Obsidian: командная работа

## Рекомендуемая модель
Хранить Markdown, Canvas и допустимые публичные источники в отдельном **private** репозитории; `main` — только прошедшие review изменения. Участники создают свои ветки `legal/...`, `tech/...`, `product/...` и открывают Pull Request.

### Добавить участников
Личный репозиторий: **Settings → Collaborators → Add people**, найти GitHub-аккаунт, отправить приглашение. После принятия участник сможет клонировать репозиторий, создавать и отправлять ветки. У личного private-репозитория права collaborators в общем случае **write**, без отдельной роли read-only.

Более гибко: создать GitHub **Organization**, перенести/создать там репозиторий и выдать нужные роли **Read / Triage / Write / Maintain / Admin**. Для авторов изменений обычно достаточно **Write**, право Admin не требуется.

### Защита main
**Settings → Rules → Rulesets** (либо Branches → Branch protection rule): для `main` по возможности включить обязательный Pull Request, ревью, запрет force push и удаления. Условия доступности/применения защиты различаются в зависимости от тарифа и видимости репозитория — перепроверить в UI.

### Локальный цикл
```bash
git clone <URL-РЕПОЗИТОРИЯ>
cd <ПАПКА>
git switch -c product/customer-interviews
# изменить файлы в Obsidian
git add .
git commit -m "docs(product): add interview guide"
git push -u origin product/customer-interviews
```
Далее открыть Pull Request → дождаться ревью → Merge. Перед новой задачей: `git switch main && git pull`.

### Важно
Права на **ветки** не означают автоматической изоляции: участник с Write обычно может изменять и чужие незащищённые ветки. Защищается прежде всего `main`; для строгой изоляции нужны отдельные репозитории/политики доступа.

Документация: https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization ; https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets
