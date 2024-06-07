# Least astonishment

Das Gesetz der geringsten Überraschung besagt, dass die Implementierung einer Klasse oder Methode so sein sollte, dass sie für andere Entwickler so wenig überraschend wie möglich ist.

## Beispiele

* Methoden sollten so implementiert sein, dass sie das tun was ihr Name verspricht.
  * calculateTotalAmountOfItems sollte den Gesamtbetrag der Artikel berechnen und nicht z.B. die Differenz.
* Methoden sollten so implementiert sein, dass sie keine Seiteneffekte haben.
  * Keine Methode sollte eine Datei löschen, wenn sie `calculateTotalAmountOfItems` heißt.
  * Werte sollten nicht verändert werden, wenn die Methode `getFullName` heißt.
  * globale Variablen sollten nicht verändert werden, wenn die Methode `printDocument` heißt.
* Methoden sollten so implementiert sein, dass sie keine Ausnahmen werfen, wenn dies nicht erwartet wird.
  * Eine Methode, die `getFullName` heißt, sollte keine `FileNotFoundException` werfen.
  * Eine Methode, die `calculateTotalAmountOfItems` heißt, sollte keine `NullPointerException` werfen.
  * Eine Methode, die `printDocument` heißt, sollte keine `NetworkException` werfen.

## Schlechtes Beispiel

```pascal
{
  Liefert den Namen des Benutzer zurück.
  Wenn der Benutzer nicht existiert, wird nil zurückgegeben.
}
function getFullName(user: User): String;
begin
  if user = nil then
  begin
    user.FirstName := 'John';
    result := '';
    exit;
  end;
    
  Result := user.title + ' ' + user.LastName + ' ' + user.FirstName;
  Result := user.title + ' ' + user.LastName + ' ' + user.FirstName;
end;
```

