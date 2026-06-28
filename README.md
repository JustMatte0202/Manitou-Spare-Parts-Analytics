# Spare Parts Availability Analytics — Power BI (Manitou Group)

Progetto di **Business Intelligence / Data Analysis** end-to-end realizzato in Power BI, focalizzato sull'**after-sales** (ricambi) di Manitou Group. Il progetto traduce un'esigenza di business reale in un set di KPI azionabili e tre dashboard interattive.

> ⚠️ **Nota sui dati.** I dati **finanziari e strategici** di Manitou citati nel progetto sono **reali e pubblici** (risultati annuali, mix ricavi Prodotti/Servizi, ripartizione geografica). Il **dataset operativo** (ordini ricambi e magazzino) è **simulato** e modellato fedelmente sulla struttura reale dell'azienda (gamme prodotto, brand, segmenti geografici), perché i dati interni non sono pubblici. È un progetto di portfolio a scopo dimostrativo, non affiliato a Manitou.

## Anteprime

| Executive Overview | Disponibilità | Inventario |
|---|---|---|
| ![Overview](screenshots/01-overview.png) | ![Disponibilità](screenshots/02-disponibilita.png) | ![Inventario](screenshots/03-inventario.png) |

---

## Contesto di business

Il piano strategico **"LIFT" (2025-2030)** di Manitou punta a far crescere fortemente i ricavi da servizi e ricambi. Questa crescita dipende da un prerequisito operativo: **avere il pezzo giusto, al momento giusto, nel posto giusto**. Un ricambio non disponibile significa macchina ferma dal cliente (Vehicle Off Road), insoddisfazione e ricavo che scivola verso ricambi non originali.

Il progetto risponde alla domanda: *dove perdiamo disponibilità ricambi, quanto ci costa, e su quali codici/categorie intervenire per primi?*

## Le tre dashboard

1. **Executive Overview** — trend ricavi ricambi, mix ordini Stock vs VOR (urgenti), ricavo per regione, KPI di sintesi.
2. **Disponibilità (Service Level)** — Fill Rate, OTIF, Fill Rate VOR, fill rate per categoria, e **matrice degli SKU critici per Revenue at Risk** (lista d'intervento prioritaria).
3. **Inventario & Capitale Immobilizzato** — rotazione stock, giorni di copertura, valore giacenza per mese/categoria e **capitale immobilizzato** (stock con copertura > 180 giorni) per gamma e classe ABC.

## Stack tecnico

- **Power BI Desktop** (modello, report, tema personalizzato)
- **DAX** — ~40 misure (fill rate, OTIF, revenue at risk, rotazione, ABC, time intelligence, capitale immobilizzato)
- **Power Query / ETL** — import e pulizia dei CSV
- **Data modeling** — schema a stella (9 tabelle: 6 dimensioni + 3 fact)
- **Data visualization** — formattazione condizionale, slicer per pagina, tema brand

## Struttura del repository

```
.
├── powerbi/    # File Power BI (.pbix) del report completo
├── data/       # 9 CSV sorgente (modello a stella) — separatore ";", UTF-8
├── dax/        # Tutte le misure DAX in formato testo
├── theme/      # Tema Power BI in stile Manitou (JSON)
├── docs/       # Documento di progetto + guida alla costruzione del report
└── screenshots/ # Anteprime delle dashboard
```

## Come aprire il progetto

1. Apri `powerbi/Manitou_Spare_Parts_Analytics.pbix` con **Power BI Desktop** (gratuito).
2. Se i dati non si caricano, aggiorna il percorso della cartella `data/` da *Trasforma dati → Impostazioni origine dati*.
3. Il file `dax/misure_DAX.txt` documenta tutte le misure; `theme/Manitou_Theme.json` è il tema applicato.

## Modello dati (schema a stella)

| Tabella | Tipo | Contenuto |
|---|---|---|
| `dim_date` | Dim. | Calendario giornaliero 2024-2025 |
| `dim_region` | Dim. | 4 segmenti geografici Manitou |
| `dim_product_family` | Dim. | 8 gamme prodotto (Manitou/Gehl/Mustang) |
| `dim_part_category` | Dim. | 10 categorie ricambio |
| `dim_part` | Dim. | ~880 SKU con classe ABC, mover class, criticità |
| `dim_dealer` | Dim. | Concessionari per regione e tier |
| `fact_parts_orders` | Fact | ~51.700 righe d'ordine ricambi |
| `fact_inventory_snapshot` | Fact | ~21.000 snapshot mensili di magazzino |
| `fact_financials_real` | Fact | Dati finanziari **reali** (contesto) |

---

**Autore:** Matteo Dominici
**Strumenti:** Power BI · DAX · Power Query · Data Modeling
