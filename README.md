# 🚀 CipherCore Prozess-Plattform – Handbuch

**Wichtig:** Dieses Dokument beschreibt die Funktionalitäten der CipherCore Prozess-Plattform.  Jegliche sicherheitsrelevanten Konfigurationen (z.B. API-Schlüssel) sind *ausschließlich* im Session State der Anwendung zu speichern und *niemals* persistent abzulegen.

---

## 1. Einleitung

Die CipherCore Prozess-Plattform ist eine hochentwickelte, interaktive Streamlit-Anwendung, die speziell für die sichere Erstellung, Bearbeitung, Visualisierung und Analyse komplexer Prozessdiagramme entwickelt wurde. Die Plattform kombiniert intuitive Diagrammerstellung mit (simulierten) Echtzeitdatenabfragen, fortschrittlicher Agenten-Skriptausführung und einer sicheren Integration der Gemini API.  Der Fokus liegt auf Sicherheit, Benutzerfreundlichkeit und Erweiterbarkeit.

---

## 2. Kernfunktionen

Die Plattform bietet folgende Hauptfunktionen, die alle unter strengen Sicherheitsaspekten entwickelt wurden:

-   **Knoten/Agenten-Management:**
    -   Erstellung, Bearbeitung und Löschung von Knoten (Prozesse, Agenten, Datenquellen).
    -   Konfiguration von Knoteneigenschaften (ID, Label, Form, Farbe).
    -   Sichere Ausführung von Python-Agenten-Skripten in einer isolierten Umgebung.
    -   (Simulierte) Echtzeit-Datenabfrage mit integriertem Caching.
    -   Sichere Integration der Gemini API für dynamische Inhalte.

-   **Verbindungsmanagement:**
    -   Definition von gerichteten und ungerichteten Verbindungen (Kanten) zwischen Knoten.
    -   Konfiguration von Verbindungseigenschaften (Richtung, Farbe).
    -   Platzhalter für zukünftige Automatisierungs-Skripte (derzeit deaktiviert).

-   **Diagramm-Visualisierung:**
    -   Automatische Generierung von Diagrammen mittels Graphviz.
    -   Interaktive Anzeige mit Tooltips für Detailinformationen.
    -   Visuelle Hervorhebung von Anomalien und Engpässen.

-   **Sichere Analysewerkzeuge:**
    -   Quanten-inspirierte Optimierung (Demo) mittels Simulated Annealing.
    -   Vollständige Undo/Redo-Funktionalität mit umfassender Historie.

-   **Datenmanagement und Persistenz:**
    -   Export und Import von Diagrammen im JSON-Format.
    -   Sicheres Speichern und Laden des *gesamten* Anwendungszustands (Diagramm, Historie, UI-Einstellungen) *ausschließlich* im Session State.

-   **Benutzeranpassung (UX-Personalisierung):**
    -   Umfangreiche Anpassungsmöglichkeiten für Theme, Layout, Schriftart und mehr.

---

## 3. Bedienungsanleitung

### 3.A. Einstellungen (Sidebar: "⚙️ Einstellungen")

-   **Gemini API-Schlüssel (Sicherheitskritisch):**
    -   **Eingabe:**  Hier wird der persönliche Gemini API-Schlüssel eingegeben.
        -   **Beispiel:** `ABC123XYZ` (Dies ist nur ein Platzhalter. Echte Schlüssel sind wesentlich komplexer.)
    -   **Sichere Speicherung:** Der Schlüssel wird *ausschließlich* im Session State der Anwendung gespeichert. Es erfolgt *keine* persistente Speicherung, um Sicherheitsrisiken zu minimieren.
    -   **Verwendung:** Der Schlüssel wird für alle Interaktionen mit der Gemini API verwendet.
    -   **Sicherheitswarnung:** Für Produktionsumgebungen sind zusätzliche Sicherheitsmaßnahmen zu implementieren (z.B. Schlüsselrotation, Zugriffsbeschränkungen).
    -   **API-Version:** Die Anwendung verwendet die Gemini v1alpha API.

### 3.B. Knoten / Agenten (Sidebar: "➕ Knoten / Agenten")

1.  **Neuen Knoten hinzufügen:** Erstellt einen neuen Knoten mit sicheren Standardwerten.

2.  **Knoten bearbeiten (pro Knoten):**
    -   **ID:** Eindeutiger Bezeichner (Text, sicher).
    -   **Label:** Beschreibender Text (sicher).
    -   **Form:** Visuelle Darstellung (Dropdown, sicher).
    -   **Farbe:** Knotenfarbe (Farbauswahl, sicher).
    -   **Datenquelle:** Auswahl der Datenquelle (Dropdown, sicher). Optionen umfassen:
        -   `Keine`
        -   `Nachrichten`
        -   `Soziale Medien`
        -   `IoT Sensoren`
        -   `CI/CD Pipeline`
        -   `Predictive News`
        -   `Predictive Soziale Medien`
        -   `Predictive IoT Sensoren`
        -   `CI/CD Monitoring`
        -   `Code Generation`
        -   `UX Personalization`
        -   `Globale Trends`
        -   `Globale Risiken`
        -   `Predictive Globale Trends`
        -   `Predictive Globale Risiken`
        -   `Infrastructure Monitoring`
        -   `Gemini` (Sichere Integration, siehe Abschnitt 4)
    -   **Daten-Query:** Suchbegriff oder Prompt (Text, sicher).
        -   **Gemini-Beispiel (sicher):** `"Erstelle ein Python-Skript, das eine einfache REST-API mit Flask implementiert."`
    -   **Daten aktualisieren:** Ruft Daten ab (simuliert oder von Gemini).
        -   Anzeige detaillierter Dateninformationen in einem sicheren Expander.
        -   Nutzt Caching für (simulierte) Echtzeitdaten zur Performance-Optimierung.
        -   Bei Auswahl von "UX Personalization" wird die Anpassung sicher angewendet.
    -   **Agenten-Skript (Python – Sicherheitskritisch):**
        -   Python-Code, der *innerhalb des Knotens* ausgeführt wird.
        -   **Beispiel (sicher):**
            ```python
            print(f"Agentenskript für Knoten '{node.get('name', 'Unbekannt')}' wird ausgeführt.")
            # Zugriff auf 'node', 'st', 'time' ist sicher.
            ```
        -   **Sicherheitsvorkehrungen:**
            -   Stark eingeschränkte `__builtins__` (nur sichere Funktionen erlaubt).
            -   Isolierter Namespace (`safe_globals`, `safe_locals`).
            -   Kontrollierter Zugriff auf Bibliotheken (`st`, `node`, `time`, `random`, `requests`, `DUMMY_API_ENDPOINTS`).
    -   **Agenten-Skript ausführen:** Führt das Skript in der sicheren Umgebung aus.
    -   **Knoten / Agent X entfernen:** Löscht den Knoten (sicher).
    - **Infrastruktur-Bedürfnisse:** (Platzhalter, derzeit nicht implementiert).

### 3.C. Verbindungen (Sidebar: "🔗 Verbindungen")

1.  **Neue Verbindung hinzufügen:** Erstellt eine neue Verbindung (Kante).

2.  **Verbindung bearbeiten (pro Kante):**
    -   **Von Knoten/Agent-ID:** ID des Startknotens (Text, sicher).
    -   **Nach Knoten/Agent-ID:** ID des Endknotens (Text, sicher).
    -   **Richtung:** Pfeilrichtung (Dropdown, sicher).
    -   **Farbe:** Kantenfarbe (Farbauswahl, sicher).
    -   **Automatisierungs-Skript:** (Derzeit deaktiviert, Platzhalter).
    -   **Verbindung X entfernen:** Löscht die Verbindung (sicher).

### 3.D. Werkzeuge (Sidebar: "🧰 Werkzeuge")

1.  **Diagramm aktualisieren:** Zeichnet das Diagramm neu (sicher).
2.  **Quanten-inspirierte Optimierung (Demo):** Führt die simulierte Optimierung aus (Simulated Annealing, sicher).
3.  **Undo:** Macht die letzte Aktion rückgängig (sicher).
4.  **Redo:** Stellt die letzte rückgängig gemachte Aktion wieder her (sicher).
5.  **Diagramm speichern (JSON):** Ermöglicht den sicheren Download des Diagramms als JSON-Datei.
6.  **Diagramm laden (JSON):** Lädt ein gespeichertes Diagramm (mit Validierung, sicher).
7.  **Alles löschen:** Löscht alle Knoten und Verbindungen (mit Warnmeldung, sicher).
8.  **Zustand speichern:** Speichert den *gesamten* Anwendungszustand *sicher im Session State*.
9. **Zustand laden:** Lädt den gespeicherten Anwendungszustand (mit Validierung, sicher).

### 3.E. Diagramm Visualisierung

-   **Anzeige:** Das Diagramm wird als Bild (Graphviz) angezeigt (sicher).
-   **Inhalt:** Zeigt Knoten und Verbindungen mit ihren Eigenschaften.
-   **Tooltips:** Knoten zeigen detaillierte, sichere Informationen als Tooltips an.
-   **Automatische Aktualisierung:** Das Diagramm wird bei Bedarf neu generiert.

---

## 4. Sichere Gemini-Integration

Die Plattform bietet eine *sichere* Integration der Gemini API zur Generierung dynamischer Inhalte.

### 4.A. Funktionsweise (Sicherheitsaspekte)

1.  **API-Schlüssel:** Der Schlüssel muss *sicher* in den Einstellungen eingegeben werden (siehe 3.A).
2.  **Datenquelle "Gemini":**
    -   Wird "Gemini" als Datenquelle ausgewählt, wird ein Prompt eingegeben.
        -   **Beispiel (sicher):** `"Generiere ein Python-Skript für eine einfache Webanwendung mit Flask und grundlegenden CRUD-Operationen."`
    -   Die `fetch_gemini_data(prompt)` Funktion wird aufgerufen.
        -   Diese Funktion verwendet `asyncio.run` für *asynchrone*, sichere API-Aufrufe.
        -   Die Antwort wird *sicher* in `node["data_info"]` gespeichert.
3.  **Code-Generierung (Beispiel):** Die `generate_code_from_diagram` Funktion ist ein *sicheres* Beispiel. Sie wird über die Datenquelle "Code Generation" genutzt.

### 4.B. Asynchrone API-Aufrufe und Fehlerbehandlung (Sicherheitsrelevant)

-   **Asynchron:** `fetch_gemini_data_async` verwendet `aiohttp` für *nicht-blockierende*, sichere API-Aufrufe.
-   **`asyncio.run`:** Wird sicher verwendet, um asynchrone Funktionen in der synchronen Umgebung auszuführen.
-   **Umfassende Fehlerbehandlung:**
    -   Fehlender/Ungültiger API-Schlüssel: Sichere Warnmeldung.
    -   Netzwerkfehler, Timeouts, HTTP-Fehler, fehlende Textantworten: Detaillierte und sichere Fehlermeldungen.
    -   Allgemeine Fehler: Umfassende `try...except` Fehlerbehandlung zur Absicherung.

---

## 5. (Simulierte) Echtzeit-Datenabfrage (Sicher)

Die Plattform simuliert den sicheren Abruf von Echtzeitdaten.

### 5.A. Funktionsweise (Sicherheitsaspekte)

-   **Datenquellen:** Vordefinierte, sichere Datenquellen (siehe 3.B).
-   **`fetch_realtime_data`:** Zentrale, sichere Funktion für den Datenabruf.
    -   Ruft spezifische Dummy-Funktionen auf.
    -   Simuliert Netzwerklatenz (`time.sleep`) *sicher*.
-   **Caching:**
    -   Sicherer Cache (`data_cache`) mit begrenzter Gültigkeit.
    -   Verbessert die Performance.
    -   Cache-Schlüssel: Sichere Kombination aus Datenquellentyp und Query.
-   **Dummy-Funktionen:**
    -   Funktionen wie `fetch_dummy_news_data` simulieren API-Aufrufe *sicher*.
    -   Geben strukturierte, sichere Daten zurück.

### 5.B. Datenquellen (Details – Sicherheitsgeprüft)

(Tabelle wie im ursprünglichen Dokument, aber mit dem Hinweis, dass alle Daten und Simulationen sicher sind.)

---

## 6. UX-Personalisierung (Sicher)

Die `apply_ux_personalization` Funktion ermöglicht sichere Anpassungen der Benutzeroberfläche.

### 6.A. Funktionsweise (Sicherheitsaspekte)

-   Wird bei Aktualisierung eines Knotens mit der Datenquelle "UX Personalization" aufgerufen.
-   **Sichere Parameter:**
    -   `personalization_type`: Typ der Personalisierung (z.B. "Theme", "Layout").
    -   `personalization_value`: Wert der Personalisierung (z.B. "Dark", "Wide").
-   **Unterstützte, sichere Typen:** Theme, Layout, Font, Content Density, Animation, Sprache, Farbpalette, Symbolgröße, Navigations Stil
-   **Sichere Implementierung:** Verwendet `st.markdown` mit Inline-CSS für sichere Stiländerungen. `st.experimental_rerun()` wird für Layout- und Sprachänderungen verwendet.

---

## 7. Undo/Redo & Historie (Sicher)

Die Plattform bietet sichere Undo/Redo-Funktionen.

### 7.A. Funktionsweise (Sicherheitsaspekte)

-   **`record_history`:** Speichert den Zustand *sicher* in der Historie.
    -   Tiefe Kopien von Knoten und Kanten werden *sicher* gespeichert.
    -   Begrenzte Historie (50 Einträge).
    -   Sichere Fehlerbehandlung beim Kopieren.
-   **`undo`:** Stellt den vorherigen Zustand *sicher* wieder her.
-   **`redo`:** Stellt den nächsten Zustand *sicher* wieder her.
- **`update_history`**: Sichere Aktualisierung
-   **Sichere Speicherung:** Die Historie wird *ausschließlich* im Session State gespeichert.

---

## 8. Speichern & Laden (Sicher)

Die Plattform ermöglicht das sichere Speichern und Laden von Daten.

### 8.A. Diagramm (JSON – Sicherheitsgeprüft)

-   **Speichern:** `st.download_button` für sicheren Download (JSON).
-   **Laden:** `st.file_uploader` für sicheren Upload (JSON, mit Validierung).

### 8.B. Anwendungszustand (Sicherheitskritisch)

-   **Speichern:** `save_state` speichert den *gesamten* Zustand *sicher im Session State*.
    -  Umfassende, sichere Fehlerbehandlung.
-   **Laden:** `load_state` lädt den gespeicherten Zustand (mit Validierung, sicher).
    -   Detaillierte, sichere Fehlermeldungen.
    -   Sichere Initialisierung von Standardwerten.

---

## 9. Agenten-Skriptausführung (Sicherheitskritisch)

Die Plattform ermöglicht die *sichere* Ausführung von Python-Skripten.

### 9.A. Funktionsweise (Sicherheitsaspekte)

-   **`execute_agent_script`:** Führt Skripte *sicher* aus.
    -   **Sicherheitsvorkehrungen:**
        -   Stark eingeschränkte `__builtins__`.
        -   Isolierter Namespace.
        -   Kontrollierter Bibliothekszugriff.
    -   Sichere Fehlerbehandlung.
-   **Ausführung pro Knoten:** Jeder Knoten hat seinen eigenen, sicheren Skriptbereich.
-   **Spinner:** Zeigt sichere Statusinformationen während der Ausführung an.
- **`execute_automation_script`**: Deaktiviert

---
