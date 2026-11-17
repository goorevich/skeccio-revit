# Skeccio for Revit

Connects Autodesk Revit 2024 and Revit 2026 to [Skeccio](https://skeccio.com): the model open in Revit works with your
Skeccio project. This repository is where the add-in is downloaded; Skeccio itself is developed elsewhere.

## Download

Stable version: [0.5.2](https://github.com/goorevich/skeccio-revit/releases/latest).

Preview: [1.0.0](https://github.com/goorevich/skeccio-revit/releases/tag/v1.0.0), build `e30de6c`. Local reading starts automatically; **Edit** permits changes to the active document, and changing documents ends Edit. Runtime verification in both Revit 2024 and 2026 is still pending, so this is a pre-release. The instructions below describe stable 0.5.2; for 1.0.0, use the README included in its archive.

Two editions; install one of them.

| Edition | For | Contains |
| --- | --- | --- |
| `Skeccio-for-Revit-<version>.zip` | Everyone | The Revit add-in only (DLL files), no program file (.exe) |
| `Skeccio-for-Revit-Agents-<version>.zip` | People who also let AI assistants on their computer (Claude Code, Codex) work in Revit | The same add-in plus `Skeccio.Mcp.exe`, a local MCP program with its own .NET runtime |

## Install

1. Close Revit.
2. Unzip the download (all files).
3. Double-click `Install.cmd`. It copies the `Skeccio.bundle` folder to
   `%APPDATA%\Autodesk\ApplicationPlugins\Skeccio.bundle`, for this Windows user only, without administrator rights.
   It is a short, readable script; you can also copy that folder yourself.
4. Start Revit. Revit asks about an add-in whose publisher it cannot verify: choose **Always Load**.
5. Tab **Skeccio**: **Connect**, then **Account** to sign in and choose your project.

## Sign in

The add-in connects to skeccio.com directly; no browser or extension is needed.

- **Work email** (your organization's domain): the **team password**, then the six-digit code skeccio.com emails you
  (valid 30 minutes) — the same as signing in on the site.
- **Other accounts**: your Skeccio email or username and password.

Then choose the project from the list. Changing project later (Account, Project) needs no password; the site ends a
sign-in after 30 days. Local AI assistants (agents edition) need no Skeccio account at all.

`Skeccio.bundle` is Autodesk's standard application-bundle format (`PackageContents.xml`); one folder serves Revit 2024
and 2026. To remove: close Revit and run `Uninstall.cmd`, or delete that folder.

## What it does and never does

- Works only after you press **Connect**; Revit starts disconnected every time.
- Your password is not kept. Windows Credential Manager keeps this computer's own token for your Skeccio project and
  your sign-in; **Sign out** in Account removes both here and on the site.
- Never saves, synchronizes with central or upgrades a model by itself.
- Changes a model only while **Allow changes** is on in Account, one Undo step at a time.
- The agents edition adds a Windows named pipe for your own Windows user only; it opens no network port. Requests and
  results are journaled in `%LOCALAPPDATA%\Skeccio\Revit\journal`.

## Connect an AI assistant (agents edition)

The program is `%APPDATA%\Autodesk\ApplicationPlugins\Skeccio.bundle\Contents\Mcp\Skeccio.Mcp.exe` (MCP over stdio,
no arguments). For Claude Code:

```
claude mcp add skeccio-revit -- "%APPDATA%\Autodesk\ApplicationPlugins\Skeccio.bundle\Contents\Mcp\Skeccio.Mcp.exe"
```

In Revit press **Connect** first; one Revit per Windows user is connected at a time.

## Notes

- The files are not code-signed yet, so Revit and Windows show them as coming from an unverified publisher.
- Questions: [skeccio.com](https://skeccio.com).

Copyright © 2026 Skeccio. All rights reserved.
