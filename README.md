# Extended and User-Oriented Versioning (ExuoVer)

![ExuoVer Logo](./assets/dark_x512.png)

ExuoVer is a versioning specification for software whose users are people: games, general applications, content mods, and similar projects. It moves the meaning of a version number away from API compatibility and toward what a user has to do when they update.

**Current version: [ExuoVer 2.0.0](./ExuoVer.md)** · [Changelog](./CHANGELOG.md) · [All versions](./docs) · [License](./LICENSE)

The normative text is in Simplified Chinese. Translations are informative only.

## 中文

「扩展并面向用户的版本号规范」（ExuoVer）面向以人为受众的软件：游戏、通用应用、内容模组等。它把版本号的语义从"接口是否兼容"移到"用户更新时需要做什么"。

**当前版本：[ExuoVer 2.0.0](./ExuoVer.md)** · [变更日志](./CHANGELOG.md) · [历史版本](./docs) · [许可证](./LICENSE)

规范文本以简体中文为准，其他语言的译本仅供参考，与中文原文冲突时以中文原文为准。

## At a glance

- Core: `X.Y.Z` or `X.Y.Z.A`, where X is Major, Y is Minor, Z is Patch and A is Tweak.
- Optional build label: `-` followed by 1–64 lowercase letters or digits, as in `2.0.0-exp` or `1.4.1.2-202611030015`.
- The build label never affects precedence and may be reused freely. It is not a pre-release version.
- Tweak 0 is omitted, so `1.4.2` and `1.4.2.0` are the same version; `1.4.2` is canonical.
- Each segment states what the user must do: migrate (Major), discover (Minor), nothing (Patch), nothing noticeable (Tweak).

## Versions

| Version | Chinese (normative) | English (informative) |
| --- | --- | --- |
| 2.0.0 | [ExuoVer.md](./ExuoVer.md) | [docs/2.0.0/english.md](./docs/2.0.0/english.md) |
| 1.0.0 | [docs/1.0.0/chinese.md](./docs/1.0.0/chinese.md) | [docs/1.0.0/english.md](./docs/1.0.0/english.md) |

Archived copies under `docs/` are frozen and are never edited.

## License

[Creative Commons Attribution-ShareAlike 4.0 International](./LICENSE)
