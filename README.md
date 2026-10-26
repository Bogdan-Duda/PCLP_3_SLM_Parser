# Analizator de Telemetrie de Rețea (SLM Parser)

O aplicație desktop dezvoltată în Python care utilizează un model de limbaj de dimensiuni reduse (SmolLM) rulat 100% local pentru a parsa și structura ieșirile nestructurate ale comenzilor de rețea din terminal (ex. `traceroute`, `ifconfig`, `netstat`).

Aplicația aplică **decodare constrânsă (Grammar-Constrained Decoding)** pentru a garanta extragerea datelor într-un format JSON valid, fără a depinde de servicii API externe, respectând cerințele cursului PCLP.

## Arhitectura Proiectului

Proiectul respectă principiul separării logicii de interfața grafică.

*   `main.py` - Punctul de intrare în aplicație.
*   `gui/` - Conține interfața grafică (ex. Tkinter/CustomTkinter), unde utilizatorul introduce textul brut și vizualizează datele extrase.
*   `logic/` - Conține motorul de parsare (încărcarea modelului SLM, aplicarea schemelor Pydantic/Gramaticilor pentru formatare).
*   `storage/` - Gestionează persistența datelor. Istoricul parsărilor și metricile sunt salvate local într-o bază de date **SQLite** (sau fișier JSON).
*   `tests/` - Conține cele (minimum) 5 teste automate pentru validarea logicii, a tratării erorilor și a bazei de date.
*   `Documentatie_proiect.docx` - Documentația detaliată, scenariile GUI și explicațiile privind instrumentele utilizate.

## Cerințe și Instalare

Proiectul folosește un mediu virtual (`.venv`) pentru a izola dependențele (`requirements.txt`), conform specificațiilor cursului.

### 1. Crearea și activarea mediului virtual
```bash
python -m venv .venv

# Pentru Windows:
.venv\Scripts\activate

# Pentru Linux / macOS:
source .venv/bin/activate
```

### 2. Instalarea pachetelor externe
```bash
pip install -r requirements.txt
```

## Rulare

Pentru a porni aplicația cu interfața grafică:
```bash
python main.py
```

## Testare

Proiectul include teste automate (ex. via `pytest` sau `unittest`) care validează validarea JSON-ului, funcționarea locală a bazei de date și comportamentul la intrări invalide.
Pentru a rula testele:
```bash
pytest tests/
# sau
python -m unittest discover tests/
```

## Observații Evaluare PCLP
*   **Fără API-uri externe:** Modelul (SmolLM/Qwen) rulează strict local (CPU), conform cerințelor.
*   **Tratare erori:** Intrările goale sau invalide sunt gestionate prin fallback-uri sigure, fără a bloca interfața.
*   Contribuțiile individuale și indicarea surselor / instrumentelor AI folosite la generarea codului (dacă există) sunt detaliate în fișierul `Documentatie_proiect.docx`.
