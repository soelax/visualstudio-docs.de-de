---
title: Analysieren der CPU-Auslastungsdaten (verwalteter Code)
description: Messen der App-Leistung in C# und Visual Basic mithilfe des Diagnosetools für die CPU-Auslastung
ms.custom: mvc
ms.date: 08/06/2018
ms.topic: quickstart
helpviewer_keywords:
- Profiling Tools, quick start
- Diagnostics Tools, CPU Usage
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 05dbbf5bc6e13b36e5918a880d0a767968a78f30
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703858"
---
# <a name="quickstart-analyze-cpu-usage-data-in-visual-studio-managed-code"></a>Schnellstart: Analysieren der CPU-Auslastungsdaten in Visual Studio (verwalteter Code)

Visual Studio enthält viele leistungsstarke Features, mit denen Sie Leistungsprobleme in Ihrer Anwendung besser analysieren können. In diesem Thema werden einige der grundlegenden Funktionen erläutert. Außerdem betrachten wir das Tool, mit dem Leistungsengpässe aufgrund hoher CPU-Auslastung erkannt werden können. Die Diagnosetools werden für die .NET-Entwicklung in Visual Studio, darunter ASP.NET, sowie für die native/C++-Entwicklung unterstützt.

Der Diagnosehub bietet Ihnen viele weitere Optionen zum Ausführen und Verwalten Ihrer Diagnosesitzung. Wenn das hier beschriebene **CPU-Auslastungs-Tool** nicht die benötigten Daten zurückgibt, gibt es andere [Tools zur Profilerstellung](../profiling/profiling-feature-tour.md), mit denen sie andere hilfreiche Informationen erhalten. In vielen Fällen kann der Leistungsengpass Ihrer Anwendung durch etwas anderes als die CPU ausgelöst werden, z.B. durch den Speicher, das Rendern der Benutzeroberfläche oder die Anforderungszeit des Netzwerks. Der Diagnosehub bietet Ihnen viele andere Optionen zum Aufzeichnen und Analysieren dieser Art von Daten.

Windows 8 und höher ist erforderlich, um die Profilerstellungstools mit dem Debugger auszuführen (Fenster **Diagnosetools**). Unter Windows 7 und höher können Sie das Post-Mortem-Tool [Leistungsprofiler](../profiling/profiling-feature-tour.md) verwenden.

## <a name="create-a-project"></a>Erstellen eines Projekts

1. Klicken Sie in Visual Studio auf **Datei** > **Neues Projekt**.

2. Klicken Sie unter **Visual C#** oder **Visual Basic** auf **Windows-Desktop** und dann im mittleren Bereich auf **Konsolen-App (.NET Framework)**.

    Wenn Ihnen die Projektvorlage **Konsolenanwendung** nicht angezeigt wird, klicken Sie im linken Bereich des Dialogfelds **Neues Projekt** auf den Link **Visual Studio-Installer öffnen**. Der Visual Studio-Installer wird gestartet. Wählen Sie die Workload **.NET-Desktopentwicklung** aus, und klicken Sie anschließend auf **Ändern**.

3. Geben Sie einen Namen wie **MyProfilerApp** ein, und klicken Sie auf **OK**.

    Visual Studio erstellt daraufhin das Projekt.

2. Öffnen Sie die Datei *Program.cs*, und ersetzen Sie den gesamten Code durch den folgenden:

    ```csharp
    using System;
    using System.Threading;
    public class ServerClass
    {
        const int MIN_ITERATIONS = int.MaxValue / 1000;
        const int MAX_ITERATIONS = MIN_ITERATIONS + 10000;

        long m_totalIterations = 0;
        readonly object m_totalItersLock = new object();
        // The method that will be called when the thread is started.
        public void DoWork()
        {
            Console.WriteLine(
                "ServerClass.InstanceMethod is running on another thread.");

            var x = GetNumber();
        }

        private int GetNumber()
        {
            var rand = new Random();
            var iters = rand.Next(MIN_ITERATIONS, MAX_ITERATIONS);
            var result = 0;
            lock (m_totalItersLock)
            {
                m_totalIterations += iters;
            }
            // we're just spinning here
            // and using Random to frustrate compiler optimizations
            for (var i = 0; i < iters; i++)
            {
                result = rand.Next();
            }
            return result;
        }
    }

    public class Simple
    {
        public static void Main()
        {
            for (int i = 0; i < 200; i++)
            {
                CreateThreads();
            }
        }
        public static void CreateThreads()
        {
            ServerClass serverObject = new ServerClass();

            Thread InstanceCaller = new Thread(new ThreadStart(serverObject.DoWork));
            // Start the thread.
            InstanceCaller.Start();

            Console.WriteLine("The Main() thread calls this after "
                + "starting the new InstanceCaller thread.");

        }
    }
    ```

    ```vb
    Imports System
    Imports System.Threading

    Namespace MyProfilerApp
        Public Class ServerClass
            Const MIN_ITERATIONS As Integer = Integer.MaxValue / 1000
            Const MAX_ITERATIONS As Integer = MIN_ITERATIONS + 10000

            Private m_totalIterations As Long = 0
            ReadOnly m_totalItersLock As New Object()
            ' The method that will be called when the thread is started.
            Public Sub DoWork()
                Console.WriteLine("ServerClass.InstanceMethod is running on another thread.")

                Dim x = GetNumber()
            End Sub

            Private Function GetNumber() As Integer
                Dim rand = New Random()
                Dim iters = rand.[Next](MIN_ITERATIONS, MAX_ITERATIONS)
                Dim result = 0
                SyncLock m_totalItersLock
                    m_totalIterations += iters
                End SyncLock
                ' we're just spinning here
                ' and using Random to frustrate compiler optimizations
                For i As Integer = 0 To iters - 1
                    result = rand.[Next]()
                Next
                Return result
            End Function
        End Class

        Public Class Simple
            Public Shared Sub Main()
                For i As Integer = 0 To 199
                    CreateThreads()
                Next
            End Sub
            Public Shared Sub CreateThreads()
                Dim serverObject As New ServerClass()

                Dim InstanceCaller As New Thread(New ThreadStart(AddressOf serverObject.DoWork))
                ' Start the thread.
                InstanceCaller.Start()

                Console.WriteLine("The Main() thread calls this after " + "starting the new InstanceCaller thread.")

            End Sub
        End Class
    End Namespace
    ```

    > [!NOTE]
    > Stellen Sie in Visual Basic sicher, dass das Startobjekt auf `Sub Main` festgelegt ist (**Eigenschaften** > **Anwendung** > **Startobjekt**).

## <a name="step-1-collect-profiling-data"></a>Schritt 1: Sammeln von Profilerstellungsdaten

1. Legen Sie in Ihrer App zuerst einen Haltepunkt auf diese Codezeile in der `Main`-Funktion fest:

    `for (int i = 0; i < 200; i++)`

    oder für Visual Basic:

    `For i As Integer = 0 To 199`

    Legen Sie einen Haltepunkt fest, indem Sie in den Bundsteg links neben der Codezeile klicken.

2. Legen Sie als Nächstes einen weiteren Haltepunkt auf die schließende Klammer am Ende der `Main`-Funktion fest:

     ![Haltepunkte für die Profilerstellung festlegen](../profiling/media/quickstart-cpu-usage-breakpoints.png "Set breakpoints for profiling")

    > [!TIP]
    > Durch das Festlegen von zwei Haltepunkten können Sie die Datensammlung auf die Teile des Code begrenzen, die Sie analysieren möchten.

3. Das Fenster **Diagnosetools** wird bereits angezeigt, es sei denn, Sie haben es deaktiviert. Klicken Sie auf **Debuggen** > **Windows** > **Diagnosetools anzeigen**, um das Fenster erneut aufzurufen.

4. Klicken Sie auf **Debuggen** > **Debugging starten** (oder auf **Start** auf der Symbolleiste oder auf **F5**).

     Wenn das Laden der Anwendung abgeschlossen ist, wird die Ansicht **Zusammenfassung** der Diagnosetools angezeigt.

5. Aktivieren Sie, während der Debugger angehalten ist, die Sammlung von CPU-Auslastungsdaten, indem Sie auf **CPU-Profilerstellung aufzeichnen** klicken. Öffnen Sie anschließend die Registerkarte **CPU-Auslastung**.

     ![Diagnosetools ermöglichen die CPU-Profilerstellung](../profiling/media/quickstart-cpu-usage-summary.png "Diagnostics Tools Enable CPU Profiling")

     Wenn die Datensammlung aktiviert ist, zeigt die Schaltfläche für das Aufzeichnen einen roten Kreis an.

     Wenn Sie auf **CPU-Profilerstellung aufzeichnen** klicken, zeichnet Visual Studio auf, welche Funktionen ausgeführt werden und wie lange dies dauert. Außerdem stellt das Programm ein Zeitachsendiagramm bereit, mit dem Sie bestimmte Segmente der Samplingsitzung genauer betrachten können. Diese gesammelten Daten können jedoch nur angezeigt werden, wenn die Anwendung an einem Haltepunkt angehalten wird.

6. Drücken Sie **F5**, um die App bis zum zweiten Haltepunkt auszuführen.

     Jetzt verfügen Sie über Leistungsdaten für Ihre Anwendung, die speziell für den Codebereich gelten, der zwischen den beiden Haltepunkten liegt.

     Der Profiler beginnt, Threaddaten vorzubereiten. Warten Sie, bis dieser Vorgang abgeschlossen ist.

     Das CPU-Auslastungstool zeigt den Bericht unter der Registerkarte **CPU-Auslastung** an.

     An diesem Punkt können Sie beginnen, die Daten zu analysieren.

## <a name="step-2-analyze-cpu-usage-data"></a>Schritt 2: Analysieren der CPU-Auslastungsdaten

Beginnen Sie bei der Datenanalyse am besten mit der Liste der Funktionen unter „CPU-Auslastung“, stellen Sie fest welche Funktionen die meisten Aufgaben ausführen, und betrachten Sie die einzelnen Funktionen näher.

1. Untersuchen Sie in der Liste der Funktionen die Funktionen, die am meisten Aufgaben ausführen.

     ![Diagnosetools Registerkarte CPU-Auslastung](../profiling/media/quickstart-cpu-usage-cpu.png "DiagToolsCPUUsageTab")

    > [!TIP]
    > Die Auflistung der Funktionen beginnt mit der Funktion, die die meisten Aufgaben ausführt (sie sind nicht in der Reihenfolge der Aufrufe gelistet). Dadurch können Sie schnell feststellen, welche Funktionen am längsten ausgeführt werden.

2. Doppelklicken Sie in der Funktionsliste auf die `ServerClass::GetNumber`-Funktion.

    Dabei wird die Ansicht **Aufrufer/Aufgerufener** im linken Bereich geöffnet.

    ![Diagnosetools Ansicht Aufrufer-Aufgerufener](../profiling/media/quickstart-cpu-usage-caller-callee.png "DiagToolsCallerCallee")

    In dieser Ansicht wird die ausgewählte Funktion in der Überschrift und im Feld **Aktuelle Funktion** angezeigt (in diesem Beispiel `GetNumber`). Die Funktion, die die aktuelle Funktion aufgerufen hat, wird links unter **Calling Function** (Aufrufende Funktion) angezeigt, und alle Funktionen, die von der aktuellen Funktion aufgerufen wurden werden im Feld **Called Functions** (Aufgerufene Funktionen) auf der rechten Seite angezeigt. (Sie können beide Felder auswählen, um die aktuelle Funktion zu ändern.)

    In dieser Ansicht wird Ihnen die Gesamtzeit (ms) und der Prozentsatz der gesamten Ausführungszeit der App angezeigt, den die Funktion bis zum Abschluss eingenommen hat.

    Unter **Funktionsrumpf** wird ebenso die Gesamtzeit (und der Prozentsatz der Zeit) angezeigt, die im Funktionsrumpf aufgewendet wurde. Die Zeit, die in aufrufenden und aufgerufenen Funktionen aufgewendet wurde, ist nicht enthalten. (In dieser Abbildung wurden 2856 von 2863 ms im Funktionsrumpf aufgewendet, und die verbleibende Zeit (<20 ms) wurde im von dieser Funktion aufgerufenen externen Code aufgewendet). Die aktuellen Werte unterscheiden sich je nach Umgebung.

    > [!TIP]
    > Hohe Werte unter **Funktionsrumpf** deuten auf einen Leistungsengpass in der Funktion selbst hin.

## <a name="next-steps"></a>Nächste Schritte

- [Analysieren der Speicherauslastung](../profiling/memory-usage.md), um Leistungsengpässe zu erkennen
- [Analysieren der CPU-Auslastung](../profiling/cpu-usage.md) für weitere Informationen zum CPU-Auslastungs-Tool
- Analysieren der CPU-Auslastung, auch ohne Debugger oder dass eine ausgeführte App als Ziel gesetzt wird: Weitere Informationen finden Sie unter [Sammeln von Profilerstellungsdaten ohne das Debuggen](../profiling/running-profiling-tools-with-or-without-the-debugger.md#collect-profiling-data-without-debugging) in [Ausführen von Profilerstellungstools mit oder ohne den Debugger](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

## <a name="see-also"></a>Siehe auch

- [Profilerstellung in Visual Studio](../profiling/index.md)
- [Einführung in Profilerstellungstools](../profiling/profiling-feature-tour.md)
