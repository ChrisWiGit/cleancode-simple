# Komplexität von Methode

Die Komplexität einer Methode kann durch die Anzahl der Verantwortlichkeiten, die sie hat, gemessen werden.

Je mehr Verantwortlichkeiten eine Methode hat, desto komplexer ist sie.

Die sogenannte zyklomatische Komplexität ist eine Metrik, die die Anzahl der möglichen Pfade durch eine Methode misst.

Je mehr if-else-Blöcke, Schleifen und Verzweigungen eine Methode hat, desto höher ist ihre zyklomatische Komplexität.

Auch mehrere exit-Punkte in einer Methode erhöhen die Komplexität.

## Beispiele für komplexe Methoden

```pascal
procedure CalculateAbsoluteAmountOfItems(items: array of Integer): Integer;
var
  i: Integer;
  total: Integer;
begin
  if (items <> nil) and (Length(items) > 0) then
    total := 0;
    // hier wird die Summe der Elemente berechnet
    for i := 0 to Length(items) - 1 do
    begin
      if items[i] > 0 then
      begin
        total := total + items[i];
      end
      else
      begin
        total := total - items[i];
      end;
    end;
    Result := total;
  end else begin
    Result := 0;
  end;
end;
```

## Lösungen

* Methode aufteilen
* Jeder Kommentar, der eine Verantwortlichkeit beschreibt, kann eine separate Methode sein
* Bedingungen in Variablen extrahieren
* Schleifen in separate Methoden extrahieren
* Bedingungen, die eine nil-Prüfung machen als Guard-Klauseln verwenden

## Beispiel für refaktorisierte Methode

```pascal
function CalculateAbsoluteAmountOfItems(items: array of Integer): Integer;
var
  i: Integer;
  total: Integer;
begin
  if (items = nil) or (Length(items) = 0) then
  begin
    // Guard-Klausel
    Result := 0;
    Exit;
  end;

  for i := 0 to Length(items) - 1 do
  begin
    total := total + CalculateItemAmount(items[i]);
  end;

  Result := 
end;

function CalculateItemAmount(item: Integer): Integer;
begin
  // Guard-Klausel
  if item > 0 then
  begin
    Result := item;
    Exit;
  end
  
  Result := -item;
end;
```