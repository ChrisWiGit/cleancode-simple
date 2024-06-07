# Single Responsibility Principle

Es besagt, dass eine Klasse nur eine Verantwortlichkeit haben sollte. 

```pascal
uses
  SysUtils, Classes;

type
  TFileProcessor = class
  public
    procedure ProcessFile(const FileName: string);
  end;

procedure TFileProcessor.ProcessFile(const FileName: string);
var
  FileContent: TStringList;
  Line: string;
begin
  // Datei einlesen
  FileContent := TStringList.Create;
  try
    FileContent.LoadFromFile(FileName);
  except
    on E: Exception do
    begin
      Writeln('Fehler beim Lesen der Datei: ', E.Message);
      Exit;
    end;
  end;

  // Inhalte parsen und ausgeben
  for Line in FileContent do
  begin
    // Hier könnte eine komplexere Parsing-Logik stehen
    Writeln('Gelesene Zeile: ', Line);
  end;

  FileContent.Free;
end;

var
  Processor: TFileProcessor;
begin
  Processor := TFileProcessor.Create;
  try
    Processor.ProcessFile('example.txt');
  finally
    Processor.Free;
  end;
end.

```

### Lösung


```pascal
program SRPExample;

uses
  SysUtils, Classes;

type
  TFileProcessor = class
  public
    procedure ProcessFile(const FileName: string);
  end;

procedure TFileProcessor.ProcessFile(const FileName: string);
var
  FileContent: TStringList;
  Line: string;
begin
  // Datei einlesen
  FileContent := TStringList.Create;
  try
    FileContent.LoadFromFile(FileName);
  except
    on E: Exception do
    begin
      Writeln('Fehler beim Lesen der Datei: ', E.Message);
      Exit;
    end;
  end;

  // Inhalte parsen und ausgeben
  for Line in FileContent do
  begin
    // Hier könnte eine komplexere Parsing-Logik stehen
    Writeln('Gelesene Zeile: ', Line);
  end;

  FileContent.Free;
end;

var
  Processor: TFileProcessor;
begin
  Processor := TFileProcessor.Create;
  try
    Processor.ProcessFile('example.txt');
  finally
    Processor.Free;
  end;
end.

```
