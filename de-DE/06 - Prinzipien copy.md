# Prinzipien

## DRY

DRY steht für "Don't Repeat Yourself" und ist ein Prinzip, das besagt, dass jede Information in einem System nur einmal vorhanden sein sollte.

* Wenn Code dupliziert wird, wird er schwerer zu warten und zu ändern.
* Fehler sind auch doppelt vorhanden und müssen an mehreren Stellen behoben werden.

## KISS

KISS steht für "Keep It Simple, Stupid" und ist ein Prinzip, das besagt, dass ein System so einfach wie möglich sein sollte.

## EUHM

EUHM steht für "Easy to use, hard to misuse" und ist ein Prinzip, das besagt, dass ein System einfach zu verwenden sein sollte, aber schwer falsch zu verwenden.

* nil sollte nicht zurückgegeben werden, wenn ein Fehler auftritt.
* nil kann als Eingabe verwendet werden, ohne dass ein Fehler auftritt.
* Falsche Eingaben führen nicht zu unerwarteten Ergebnissen.

## FF

FF steht für "Fail Fast" und ist ein Prinzip, das besagt, dass ein System so schnell wie möglich fehlschlagen sollte.

* Fehler sollten so früh wie möglich erkannt und Exceptions ausgelöst werden.
* Aufrufer sollten Exceptions nicht schlucken, sondern sie behandeln oder einfach weitergeben.

## YAGNI

YAGNI steht für "You Ain't Gonna Need It" und ist ein Prinzip, das besagt, dass keine Funktionalität hinzugefügt werden sollte, die nicht benötigt wird.

* Es ist besser, Funktionalität hinzuzufügen, wenn sie benötigt wird, anstatt sie im Voraus zu implementieren.
* Diese Funktionen verursachen Arbeit und benötigen Tests, Wartung und Dokumentation.

## SOLID
ignore

## 