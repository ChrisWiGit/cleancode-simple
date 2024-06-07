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

### Beispiel

```pascal
program DIPExample;

{$MODE OBJFPC}

uses
  SysUtils;

type
  IDatabase = interface
    procedure SaveData(const Data: string);
  end;

  TSQLDatabase = class(TInterfacedObject, IDatabase)
  public
    procedure SaveData(const Data: string);
  end;

  TNoSQLDatabase = class(TInterfacedObject, IDatabase)
  public
    procedure SaveData(const Data: string);
  end;

  TReportGenerator = class
  private
    FDatabase: IDatabase;
  public
    constructor Create(ADatabase: IDatabase);
    procedure GenerateReport;
  end;

{ TSQLDatabase }

procedure TSQLDatabase.SaveData(const Data: string);
begin
  Writeln('Saving data to SQL database: ', Data);
end;

{ TNoSQLDatabase }

procedure TNoSQLDatabase.SaveData(const Data: string);
begin
  Writeln('Saving data to NoSQL database: ', Data);
end;

{ TReportGenerator }

constructor TReportGenerator.Create(ADatabase: IDatabase);
begin
  FDatabase := ADatabase;
end;

procedure TReportGenerator.GenerateReport;
begin
  // Generate some report content
  FDatabase.SaveData('Report Content');
end;

var
  ReportGenerator: TReportGenerator;
  Database: IDatabase;
begin
  // Use SQL Database
  Database := TSQLDatabase.Create;
  ReportGenerator := TReportGenerator.Create(Database);
  try
    ReportGenerator.GenerateReport;
  finally
    ReportGenerator.Free;
  end;

  // Use NoSQL Database
  Database := TNoSQLDatabase.Create;
  ReportGenerator := TReportGenerator.Create(Database);
  try
    ReportGenerator.GenerateReport;
  finally
    ReportGenerator.Free;
  end;
end.



```