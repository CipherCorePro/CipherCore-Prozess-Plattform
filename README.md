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
## 10. Abgrenzung zu realen Umgebungen (Simulationsmodus vs. Echtbetrieb)

Dieses Kapitel beschreibt den Unterschied zwischen der Simulationsumgebung, die in diesem Handbuch und der Anwendung dargestellt wird, und einer echten Produktionsumgebung.

**Wichtiger Hinweis:** Viele Funktionen der CipherCore Prozess-Plattform, wie sie in diesem Handbuch beschrieben werden, sind *Simulationen*. Dies dient dazu, die Konzepte und Möglichkeiten der Plattform zu demonstrieren, ohne echte Datenverbindungen oder sensible Operationen durchzuführen.

### 10.A. Simulationsmodus (Standard)

Der Simulationsmodus ist die Standardbetriebsart der Anwendung.  Er zeichnet sich durch folgende Merkmale aus:

*   **Datenabruf:** Anstelle von echten API-Verbindungen zu externen Diensten (Nachrichten, soziale Medien, etc.) werden *Dummy-Funktionen* verwendet. Diese Funktionen (z.B. `fetch_dummy_news_data`) liefern vorab definierte, statische Daten.  Es findet *keine* Kommunikation mit externen Servern statt (mit Ausnahme der Gemini API, siehe unten).
*   **Netzwerklatenz:** Die Funktion `time.sleep()` wird verwendet, um die Verzögerungen zu simulieren, die bei realen Netzwerkoperationen auftreten würden.
*   **Echtzeitdaten:** Der Begriff "Echtzeit" bezieht sich im Simulationsmodus auf das regelmäßige Abrufen der statischen Dummy-Daten und deren Aktualisierung im Cache.
*   **Quanten-inspirierte Optimierung:** Die "Optimierung" ist eine Demo-Implementierung von Simulated Annealing. Sie operiert auf den simulierten Daten und Diagrammstrukturen.
*   **Gemini API:** Die Gemini API-Integration ist *real*, aber die Nutzung sollte unter dem Gesichtspunkt der Testumgebung erfolgen.  Verwende Testdaten und erwarte keine Ergebnisse in Produktionsqualität.
*   **Infrastruktur-Bedürfnisse:** Der Abschnitt zu Infrastruktur-Bedürfnissen ist ein Platzhalter und hat im Simulationsmodus keine Funktion.
* **Automation-Skripte:** Derzeit sind alle Automations-Skripte deaktiviert.

### 10.B. Einsatz in der Produktivumgebung (Erweiterte Konfiguration)

Um die CipherCore Prozess-Plattform in einer Produktionsumgebung einzusetzen, sind *erhebliche* Anpassungen und Erweiterungen erforderlich.  Dies ist *nicht* der Standard-Anwendungsfall und erfordert tiefgreifende Kenntnisse der Plattform und der beteiligten Technologien.

**Wichtige Hinweise und Schritte für den Produktivbetrieb:**

1.  **Echte Datenquellen:**
    *   Ersetze die Dummy-Funktionen (z.B., `fetch_dummy_news_data`) durch *echte* API-Clients, die mit den entsprechenden Diensten kommunizieren.
    *   Implementiere *sichere* Authentifizierungs- und Autorisierungsmechanismen für alle externen Verbindungen.
    *   Beachte die Ratenbegrenzungen (Rate Limits) und Fehlerbehandlungsrichtlinien der jeweiligen APIs.

2.  **Echte API-Schlüsselverwaltung (Sicherheitskritisch):**
    *   Speichere API-Schlüssel *niemals* im Klartext im Code oder im Session State.
    *   Verwende sichere Umgebungsvariablen oder einen dedizierten Secret Manager (z.B. HashiCorp Vault, AWS Secrets Manager, Azure Key Vault).
    *   Implementiere Mechanismen zur Schlüsselrotation und zum Widerruf von Schlüsseln.

3.  **Sichere Agenten-Skriptausführung:**
    *   Die im Handbuch beschriebene Sicherheitsvorkehrungen für die Agenten-Skriptausführung sind für eine Demo-Umgebung ausreichend, aber *nicht* für eine Produktionsumgebung mit unvertrautem Code.
    *   Erwäge den Einsatz von Containerisierung (z.B. Docker) oder anderen Isolationsmechanismen (z.B. WebAssembly) für eine stärkere Kapselung und Kontrolle.
    *   Implementiere eine umfassende Überwachung und Protokollierung aller ausgeführten Skripte.

4.  **Echte Quanten-inspirierte Optimierung:**
    *   Ersetze die Simulated Annealing Demo durch eine geeignete Optimierungslösung für den spezifischen Anwendungsfall.
    *   Dies kann die Integration von Bibliotheken wie D-Wave Leap oder anderen Optimierungsframeworks erfordern.

5. **Automatisierungs-Skripte (Erweiterte Sicherheitsaspekte):**
    *   Vor der Aktivierung von Automatisierungs-Skripten sind *umfassende* Sicherheitsprüfungen und Risikoanalysen erforderlich.
    *   Implementiere strikte Zugriffskontrollen und Validierungsmechanismen.
    *   Stelle sicher, dass die Skripte keine sicherheitskritischen Aktionen ohne explizite Autorisierung durchführen können.

6.  **Infrastruktur:**
    *   Plane die benötigte Infrastruktur (Server, Datenbanken, Netzwerkkonfiguration) sorgfältig.
    *   Berücksichtige Skalierbarkeit, Ausfallsicherheit und Sicherheitsanforderungen.
    *   Die Infrastruktur muss den Anforderungen der echten Datenquellen und der Optimierungsalgorithmen entsprechen.

7.  **Sicherheitsüberprüfungen:**
    *   Führe regelmäßige Sicherheitsaudits und Penetrationstests durch, um Schwachstellen zu identifizieren und zu beheben.
    *   Implementiere ein umfassendes Monitoring und Logging zur Erkennung von Sicherheitsvorfällen.

8. **Datenschutz:**
    * Stelle sicher, dass alle anwendbaren Datenschutzbestimmungen (z.B. DSGVO) eingehalten werden.
    * Implementiere geeignete Maßnahmen zur Datenverschlüsselung, Anonymisierung und Zugriffskontrolle.

**Zusammenfassend lässt sich sagen, dass der Übergang von der Simulation in den Echtbetrieb eine komplexe Aufgabe ist, die erhebliche Investitionen in Sicherheit, Infrastruktur und Entwicklung erfordert.**

---

## 11. Glossar

| Begriff                        | Erklärung                                                                                                                                                                                                                                                                                                  |
| :------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Gemini API**                 | Eine Programmierschnittstelle (API) von Google, die Zugriff auf fortschrittliche KI-Modelle (Large Language Models, LLMs) bietet. Diese Modelle können für Aufgaben wie Texterstellung, Code-Generierung, Übersetzung und mehr verwendet werden.                                                        |
| **Quanten-inspirierte Optimierung** | Eine Klasse von Optimierungsalgorithmen, die von Prinzipien der Quantenmechanik inspiriert sind, aber auf klassischen Computern ausgeführt werden. Ein Beispiel ist Simulated Annealing.                                                                                                                |
| **Asynchrones Fetching**        | Eine Technik in der Programmierung, bei der Daten von einem Server abgerufen werden, ohne den Haupt-Thread der Anwendung zu blockieren. Dies ermöglicht es der Anwendung, reaktionsfähig zu bleiben, während im Hintergrund auf Daten gewartet wird. `aiohttp` ist eine Bibliothek für asynchrone HTTP-Aufrufe. |
| **Simulated Annealing**          | Ein probabilistischer Optimierungsalgorithmus, der vom Abkühlprozess von Metallen inspiriert ist. Er wird verwendet, um gute (aber nicht unbedingt optimale) Lösungen für komplexe Optimierungsprobleme zu finden.                                                                                   |
| **Session State**               | Eine Funktion von Streamlit, die es ermöglicht, Daten *temporär* im Speicher zu speichern, solange die Benutzersitzung aktiv ist. Diese Daten sind *nicht* persistent und gehen verloren, wenn die Sitzung beendet wird.                                                                             |
| **Graphviz**                   | Eine Open-Source-Software zur Visualisierung von Graphen (Netzwerken). Sie wird verwendet, um Diagramme aus einer textuellen Beschreibung (DOT-Sprache) zu erzeugen.                                                                                                                                   |
| **Caching**                    | Eine Technik, bei der häufig verwendete Daten temporär gespeichert werden, um den Zugriff darauf zu beschleunigen. In diesem Fall wird ein Cache verwendet, um (simulierte) Echtzeitdaten zwischenzuspeichern und so die Performance zu verbessern.                                                    |
| **Dummy-Funktionen**           | Funktionen, die anstelle von echten API-Aufrufen verwendet werden, um den Datenabruf zu simulieren. Sie liefern vordefinierte, statische Daten.                                                                                                                                                       |
| **Namespace**                  | In der Programmierung ein Bereich, in dem Bezeichner (z.B. Variablennamen) eindeutig sein müssen. Ein isolierter Namespace verhindert Namenskonflikte und schützt vor unbeabsichtigten Zugriffen auf globale Variablen.                                                                               |
| **`__builtins__`**            | Ein spezielles Attribut in Python, das Zugriff auf die eingebauten Funktionen und Konstanten der Sprache bietet. Im Kontext der sicheren Skriptausführung wird dieser Zugriff eingeschränkt, um potenziell gefährliche Operationen zu verhindern.                                                        |
| **DOT-Sprache**                | Die textuelle Beschreibungssprache, die von Graphviz verwendet wird, um Graphen zu definieren. Sie besteht aus Knoten, Kanten und Attributen.                                                                                                                                                             |
| **Ratenbegrenzung (Rate Limit)** | Eine Beschränkung der Anzahl von Anfragen, die ein Client innerhalb eines bestimmten Zeitraums an eine API senden darf. Dies dient dazu, die Server vor Überlastung zu schützen.                                                                                                                         |
| **Secret Manager**             | Ein Dienst oder eine Software, die zur sicheren Speicherung und Verwaltung von Geheimnissen (z.B. API-Schlüsseln, Passwörtern) verwendet wird. Beispiele sind HashiCorp Vault, AWS Secrets Manager und Azure Key Vault.                                                                                     |
| **Containerisierung**          | Eine Technologie, die es ermöglicht, Anwendungen und ihre Abhängigkeiten in isolierten Containern zu verpacken und auszuführen. Docker ist eine weit verbreitete Containerisierungsplattform.                                                                                                                |
| **WebAssembly (Wasm)**          | Ein Binärcodeformat, das es ermöglicht, Code in verschiedenen Programmiersprachen im Webbrowser auszuführen. Es bietet eine sichere und effiziente Möglichkeit, Code in einer isolierten Umgebung auszuführen.                                                                                             |
