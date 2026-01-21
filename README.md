<p align="center">
  <img src="https://img.shields.io/badge/🔧-Debug%20Tools-FF6B6B?style=for-the-badge" alt="Debug Tools"/>
</p>

<h1 align="center">DirtyTag-dogana</h1>

<p align="center">
  <strong>Webapp di Debugging e Diagnostica Sistema</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-1.0-blue?style=flat-square" alt="Version"/>
  <img src="https://img.shields.io/badge/status-development-yellow?style=flat-square" alt="Status"/>
  <img src="https://img.shields.io/badge/stack-HTML%20%7C%20JS%20%7C%20Airtable%20API-orange?style=flat-square" alt="Stack"/>
</p>

---

## 📋 Overview

**DirtyTag-dogana** è una webapp di debugging per il sistema DirtyTag 3.0. Fornisce strumenti diagnostici per ispezionare record, verificare stati e testare connessioni API durante lo sviluppo e il troubleshooting.

---

## 🎯 Funzionalità

### Core Features

| Feature | Descrizione |
|---------|-------------|
| **🔍 Record Inspector** | Visualizzazione dettagliata campi Airtable |
| **📊 Status Checker** | Verifica stati pipeline per SKU |
| **🔗 API Tester** | Test connessioni Airtable/Drive |
| **📝 Log Viewer** | Visualizzazione log operazioni |
| **🔄 Field Updater** | Modifica diretta campi per test |
| **📁 Drive Explorer** | Navigazione cartelle Google Drive |

### Use Cases

| Scenario | Tool |
|----------|------|
| Record bloccato in pipeline | Status Checker |
| Verifica dati dopo workflow | Record Inspector |
| Test nuove credenziali | API Tester |
| Fix manuale campo | Field Updater |
| Verifica foto esistenti | Drive Explorer |

---

## 🛠️ Tech Stack

| Componente | Tecnologia |
|------------|------------|
| **Frontend** | HTML5, CSS3, Vanilla JavaScript |
| **Database** | Airtable API |
| **Storage** | Google Drive API |
| **Auth** | Airtable Personal Access Token |
| **Hosting** | GitHub Pages |

---

## 📊 Database Access

### Basi Airtable Accessibili

| Base | ID | Descrizione |
|------|-----|-------------|
| **DirtyTag 3.0** | `apptD8GSxN3vhhivI` | Sistema principale |
| **DirtyTag 2.0** | `apptPbWnDkDkKEpFV` | Legacy (migrazione) |

### Tabelle Principali

| Tabella | Ruolo | Operazioni |
|---------|-------|------------|
| `INVENTARIO` | Prodotti | Read/Write |
| `PROCESS_QUEUE` | Coda migrazione | Read/Write |
| `CONTABILITÀ` | Movimenti | Read |
| `LOG_PIPELINE` | Log | Read |
| `RAW` | Cartelle Drive | Read |

---

## 🔧 Strumenti Debug

### 1. Record Inspector

Visualizza tutti i campi di un record Airtable:

```
┌─────────────────────────────────────────────────────────────────┐
│  🔍 Record Inspector                                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  SKU: [MF-2411        ]  [🔍 Search]                            │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ Field                    │ Value                    │ Type  ││
│  ├─────────────────────────────────────────────────────────────┤│
│  │ SKU                      │ MF-2411                  │ text  ││
│  │ Brand                    │ [rec123...]              │ link  ││
│  │ Product_Status           │ AI_GENERATED             │ select││
│  │ AI_Quality_Check         │ PENDING                  │ select││
│  │ RAW_Ready_Trigger        │ false                    │ bool  ││
│  │ AI_Pending_Trigger       │ false                    │ bool  ││
│  │ ...                      │ ...                      │ ...   ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### 2. Status Checker

Verifica lo stato pipeline di un prodotto:

```
Pipeline Status for MF-2411:

✅ RAW_Status: READY
✅ RAW_FolderID: 1abc...
✅ AI_Mode_Selected: MANI
⏳ Product_Status: AI_GENERATED
⏳ AI_Quality_Check: PENDING
❌ Listing_Status: NOT_PUBLISHED

Triggers:
  RAW_Ready_Trigger: false ✓
  AI_Pending_Trigger: false ✓
  Listing_Ready_Trigger: false ✓

Next Step: Awaiting AI Quality Review
```

### 3. API Tester

Test connessioni e credenziali:

```
┌─────────────────────────────────────────────────────────────────┐
│  🔗 API Tester                                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Airtable Token: [pat...••••••••••]  [Test Connection]          │
│                                                                  │
│  Results:                                                        │
│  ✅ Auth: Valid                                                  │
│  ✅ Base Access: apptD8GSxN3vhhivI                              │
│  ✅ Read: OK (fetched 1 record)                                 │
│  ✅ Write: OK (test field updated)                              │
│                                                                  │
│  Latency: 234ms                                                  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### 4. Field Updater

Modifica diretta campi (⚠️ usare con cautela):

```
┌─────────────────────────────────────────────────────────────────┐
│  ✏️ Field Updater                                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Record ID: [recABC123...]                                      │
│  Table: [INVENTARIO ▼]                                          │
│                                                                  │
│  Field: [AI_Pending_Trigger ▼]                                  │
│  Value: [1]                                                      │
│                                                                  │
│  [⚠️ Update Field]                                              │
│                                                                  │
│  ⚠️ Warning: Direct field updates bypass workflow logic.        │
│     Use only for debugging/recovery.                            │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### 5. Log Viewer

Visualizza log da LOG_PIPELINE:

```
┌─────────────────────────────────────────────────────────────────┐
│  📝 Pipeline Logs                                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Filter: [All ▼] SKU: [________] [🔍 Search]                    │
│                                                                  │
│  2026-01-21 09:45:23 | W3 | MF-2411 | SUCCESS | AI generated   │
│  2026-01-21 09:44:12 | W2 | MF-2411 | SUCCESS | RAW validated  │
│  2026-01-21 09:43:01 | W1 | MF-2411 | SUCCESS | Migrated       │
│  2026-01-21 09:30:45 | W3 | CG-2960 | ERROR   | Template miss  │
│  ...                                                             │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Setup & Deploy

### Prerequisiti

- Account GitHub
- Airtable Personal Access Token con scope FULL:
  - `data.records:read`
  - `data.records:write`
  - `schema.bases:read`
  - `schema.bases:write` (per alcuni test)

### Deploy su GitHub Pages

```bash
# Clone repository
git clone https://github.com/FedericoLuigiDOrsi/DirtyTag-dogana.git

# Il file index.html è già configurato
# GitHub Pages serve automaticamente da branch main
```

### Configurazione Token

1. Apri la webapp
2. Inserisci il token Airtable nel campo dedicato
3. Il token viene salvato in `localStorage` del browser

⚠️ **Nota Sicurezza:** Questa webapp ha accesso in scrittura. Usa token dedicati per debugging, non token di produzione.

---

## ⚠️ Avvertenze

### Uso Responsabile

| ⚠️ Warning | Descrizione |
|------------|-------------|
| **Field Updates** | Le modifiche dirette bypassano la logica workflow |
| **Trigger Resets** | Resettare trigger può causare loop o blocchi |
| **Production Data** | Ogni modifica impatta dati reali |

### Best Practices

1. **Backup** — Annota valori originali prima di modificare
2. **Test First** — Usa record di test quando possibile
3. **Single Changes** — Modifica un campo alla volta
4. **Verify After** — Controlla stato dopo ogni modifica

---

## 🔧 Troubleshooting Comune

### Scenari Debug Tipici

| Problema | Diagnosi | Fix |
|----------|----------|-----|
| Record bloccato | Check triggers tutti FALSE | Set trigger appropriato = 1 |
| Foto non generate | Check AI_Pending_Trigger | Set = 1 se RAW_PROCESSED |
| Listing non creato | Check Listing_Ready_Trigger | Set = 1 se AI_APPROVED |
| Migrazione fallita | Check PROCESS_QUEUE status | Reset Migrate_Trigger |

### Reset Pipeline SKU

Per resettare completamente un SKU:

```javascript
// Campi da resettare
{
  "Product_Status": "RAW_READY",
  "RAW_Ready_Trigger": 1,
  "AI_Pending_Trigger": 0,
  "AI_Quality_Check": "",
  "AI_Front_Image_Link": "",
  "AI_Back_Image_Link": "",
  "Listing_Ready_Trigger": 0,
  "Listing_Status": ""
}
```

---

## 📚 Documentazione Correlata

| Documento | Contenuto |
|-----------|-----------|
| [TROUBLESHOOTING.md](https://github.com/FedericoLuigiDOrsi/dirtytag-system/blob/main/TROUBLESHOOTING.md) | Guida problemi comuni |
| [ERROR_CODES.md](https://github.com/FedericoLuigiDOrsi/dirtytag-system/blob/main/ERROR_CODES.md) | Catalogo errori |
| [STATUS_VALUES.md](https://github.com/FedericoLuigiDOrsi/dirtytag-system/blob/main/STATUS_VALUES.md) | Valori status validi |
| [TRIGGER_SCHEMAS.md](https://github.com/FedericoLuigiDOrsi/dirtytag-system/blob/main/TRIGGER_SCHEMAS.md) | Pattern trigger |

---

## 🔗 Links

| Risorsa | URL |
|---------|-----|
| **Webapp Live** | https://federicoluigidorsi.github.io/DirtyTag-dogana/ |
| **Sistema Principale** | https://github.com/FedericoLuigiDOrsi/dirtytag-system |
| **AI Support Chat** | https://notebooklm.google.com/notebook/7b62519e-9fbf-4d40-bf47-2f43c0fd0b28 |

---

## 📄 License

Proprietario — Tutti i diritti riservati.

---

## 👤 Author

**Federico Luigi D'Orsi** — [@FedericoLuigiDOrsi](https://github.com/FedericoLuigiDOrsi)
