# Dependency Inversion Principle

Das Dependency Inversion Principle besagt, dass High-Level-Module nicht von Low-Level-Modulen abhängen sollten. 

Beide sollten von Abstraktionen abhängen. 

Abstraktionen sollten nicht von Details abhängen. Details sollten von Abstraktionen abhängen.

Kurzes Beispiel:

Ein Modul benötigt eine Datenbankverbindung. Diese Verbindung ist eine Detailinformation und im Abstraktionslayer tiefer liegend als das Modul selbst.

1. App
2. Modul
3. Datenbankverbindung



## Beispiel (Pascal)

### Schlechtes Beispiel

```pascal
program DIPExample;

{$MODE OBJFPC}

uses
  SysUtils;

type
  TSQLDatabase = class
  public
    procedure SaveData(const Data: string);
  end;

  TReportGenerator = class
  private
    FDatabase: TSQLDatabase;
  public
    constructor Create;
    destructor Destroy; override;
    procedure GenerateReport;
  end;

{ TSQLDatabase }

procedure TSQLDatabase.SaveData(const Data: string);
begin
  Writeln('Saving data to SQL database: ', Data);
end;

{ TReportGenerator }

constructor TReportGenerator.Create;
begin
  FDatabase := TSQLDatabase.Create;
end;

destructor TReportGenerator.Destroy;
begin
  FDatabase.Free;
  inherited Destroy;
end;

procedure TReportGenerator.GenerateReport;
begin
  // Generate some report content
  FDatabase.SaveData('Report Content');
end;

var
  ReportGenerator: TReportGenerator;
begin
  ReportGenerator := TReportGenerator.Create;
  try
    ReportGenerator.GenerateReport;
  finally
    ReportGenerator.Free;
  end;
end.


```