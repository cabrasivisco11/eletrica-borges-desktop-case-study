# Technology and architecture

| Layer | Technology | Documented responsibility |
| --- | --- | --- |
| Desktop shell | Electron 44 | Windows application lifecycle, secure renderer configuration, native dialogs, and local packaging. |
| Interface | React, TypeScript, Vite | Customers, catalog, quotation editor, results, settings, and responsive layout. |
| Boundary | Electron preload and restricted IPC | Exposes selected operations to the renderer; main-process checks guard writes and external navigation. |
| Persistence | Node's SQLite API | Local commercial records, migrations, backup, and restore. Data lives outside the installation folder. |
| Documents | Electron/PDF and print workflow | A4 quotation output and the visible Windows print dialog. |
| Licensing | Ed25519 signature verification | Offline, device-bound licenses; signing tools and private material are excluded from the distributed application. |
| Packaging | electron-builder, NSIS | Windows x64 installer and uninstall settings that retain user data. |

```text
React renderer
    │ selected requests
    ▼
Restricted preload / IPC
    │
    ▼
Electron main process ── SQLite in user data
    ├── PDF and print dialog
    ├── backup and restore
    ├── external WhatsApp link (optional network access)
    └── offline license verification
```

The packaged app loads its compiled UI locally and does not need a development server for core work. An optional WhatsApp action opens an external URL for a valid customer phone number; it does not send a message automatically. The presence of local-first architecture is not a claim that a physically disconnected customer-PC test has passed.

Security settings documented in the original project include `contextIsolation`, `nodeIntegration: false`, sandboxing, constrained IPC, sender validation, and blocked in-app navigation. This is an architecture description, not an independent security certification.
