Fibonacci-Uhr (Fobinacci_Uhr)

Dieses kleine Windows Forms Projekt zeigt eine Fibonacci-basierte Uhr.

Funktionen:
- Anzeige der aktuellen Uhrzeit (lblLiveTime), automatisch aktualisiert per Timer.
- Manuelle Einstellung der Stunden und Minuten per NumericUpDown-Steuerelemente.
- Schaltfläche zum Setzen der Zeit manuell (Set Time) und Start/Stop für automatische Aktualisierung.

Wichtig:
- In InitializeComponent wird die Variable `components` initialisiert, damit Timer sauber über das Designer-Container-Pattern verwaltet werden.
- Bei Bedarf wird der Timer dynamisch angelegt, wenn der Nutzer automatische Aktualisierung startet.

Build & Run:
- Öffne die Lösung in Visual Studio und starte das Projekt.

Anpassungen:
- Die Minuten-Inkremente können in Form1.Designer.cs geändert werden.
- Die UI-Strings sind aktuell auf Englisch; können bei Bedarf ins Deutsche angepasst werden.