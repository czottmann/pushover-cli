# pushover-cli

A CLI for sending [Pushover](https://pushover.net/) notifications. Forked from [aaronfagan/pushover-cli](https://github.com/aaronfagan/pushover-cli). Not an official Pushover tool.

## Install

With [mise](https://mise.jdx.dev/):

```bash
mise use github:czottmann/pushover-cli
```

Or grab the script from the [releases page](https://github.com/czottmann/pushover-cli/releases) and drop it somewhere on your `$PATH`.

## Usage

```bash
pushover --message "hello"
```

Run `pushover --help` for the full option list.

## Tokens

You need a Pushover **user key** and **application API token** from <https://pushover.net/>.

Each token is resolved from the first source that has it. There is no fallback chaining: if you pass `--user` on the command line and set `PUSHOVER_APP_TOKEN` in the environment, the user key comes from the flag and the app token comes from the env var.

1. CLI flags: `--user KEY` / `--token TOKEN`
2. Environment variables: `PUSHOVER_USER_KEY` / `PUSHOVER_APP_TOKEN`
3. Global config file: `~/.config/pushover-cli/global.env`

### Global config file

`~/.config/pushover-cli/global.env` is plain text:

```
PUSHOVER_USER_KEY="your-user-key"
PUSHOVER_APP_TOKEN="your-app-token"
```

Lock it down:

```bash
mkdir -p ~/.config/pushover-cli
chmod 700 ~/.config/pushover-cli
touch ~/.config/pushover-cli/global.env
chmod 600 ~/.config/pushover-cli/global.env
```
