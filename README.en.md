# astrbot_plugin_pokepro — Advanced Poke Plugin

[简体中文](README.md) · [繁體中文](README.zh-TW.md) · **English**

An AstrBot poke-interaction plugin. Being poked can trigger randomly weighted actions: poke back, LLM reply, QQ face, image meme, mute or custom command. It also supports active pokes, keyword triggers and scheduled pokes, with configurable probabilities and responses.

**Requires AstrBot v4.13.0+** to load correctly. Find `astrbot_plugin_pokepro` in the AstrBot plugin market to install.

## Basic configuration

| Setting | Purpose | Default |
| --- | --- | --- |
| `on_poke` | Global poke listener | `true` |
| `poke_cd` | Per-user cooldown in seconds | `10` |
| `group_poke_cd` | Group-level cooldown (`0` disables) | `0` |
| `follow_prob` | Chance to poke alongside another user | `0.1` |

Each response action has a `weight`; its probability is **action weight / sum of enabled action weights**.

| Action | Main settings | Defaults |
| --- | --- | --- |
| `antipoke` | `weight`, `max_times` (random 1–N) | `10`, `5` |
| `llm` | `weight`, `template` with `{username}` | `10`, `"{username} 戳了你一下..."` |
| `face` | `weight`, `pool` of QQ face IDs, `max_copy_count` | `10`, `[1,11,14...]`, `3` |
| `meme` | `weight`, local image `pool` | `10`, `[]` |
| `ban` | `weight`, `duration`, `delta`, `ban_template`, `ban_fail_template` | `10`, `60` sec, `30` sec, no template |
| `command` | `weight`, command `pool` | `10`, see configuration |

## Active pokes and scheduling

| Setting | Meaning | Default |
| --- | --- | --- |
| `poke_max_times` | Maximum times for `戳 @person count`, excluding admins | `5` |
| `poke_interval` | Poke spacing, seconds | `0.5` |
| `poke_keywords` | Automatic poke trigger keywords | `[笨蛋, 人机, 机器人, bot]` |
| `scheduler.enabled` | Enable scheduled pokes | `true` |
| `scheduler.cron` | Minute hour day month weekday | `"30 22 * * *"` |
| `scheduler.target` | List of `groupID:QQID` targets | `["-199:-101"]` |
| `scheduler.times` | Pokes per scheduled event | `1` |

## Commands (retain original Chinese syntax)

| Command | Effect |
| --- | --- |
| Being poked | Triggers weighted reply actions |
| `戳 @XXX` | Poke a user, optionally specify a count such as `戳 3@张三` |
| `戳我` | Poke yourself |
| `戳全体成员` | Poke all members; for groups over 200, randomly choose 200 |

**README translations do not add English command aliases or change configuration keys.**

## Contributing and licensing limitations

Stars, issue reports, feature requests and pull requests are welcome. The original README lists the feedback QQ group as `-199`.

**Critical upstream license warning:** This repository is a fork of [Zhalslar/astrbot_plugin_pokepro](https://github.com/Zhalslar/astrbot_plugin_pokepro). The upstream repository **does not contain a LICENSE file** (`UNLICENSED_UPSTREAM`). The GPL-3.0 file in this fork **cannot license original upstream code on the original author's behalf**, nor can this fork unilaterally relicense that code. Do not redistribute, package or incorporate upstream-derived portions unless the author grants permission or independent provenance is established. Retain upstream authorship; this fork's license does not grant rights to third-party assets or dependencies.
