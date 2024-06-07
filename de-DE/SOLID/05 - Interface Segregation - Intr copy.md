# Interface Segregation Principle (ISP)

Das Interface Segregation Principle besagt, dass eine Klasse nicht gezwungen sein sollte, Methoden zu implementieren, die sie nicht benötigt.

D.h. Interfaces sollten spezifisch für die Klassen sein, die sie implementieren.


## Beispiel (Pascal)

### Schlechtes Beispiel

```pascal
program ISPExample;

{$MODE OBJFPC}

type
  IWorker = interface
    procedure Work;
    procedure TakeBreak;
  end;

  TManager = class(TInterfacedObject, IWorker)
  public
    procedure Work;
    procedure TakeBreak;  // Manager muss diese Methode implementieren, obwohl er sie nicht benötigt
  end;

  TDeveloper = class(TInterfacedObject, IWorker)
  public
    procedure Work;
    procedure TakeBreak; // Developer muss diese Methode implementieren, obwohl er sie nicht benötigt
  end;

{ TManager }

procedure TManager.Work;
begin
  Writeln('Manager is working.');
end;

procedure TManager.TakeBreak;
begin
  Writeln('Manager is taking a break.');
end;

{ TDeveloper }

procedure TDeveloper.Work;
begin
  Writeln('Developer is writing code.');
end;

procedure TDeveloper.TakeBreak;
begin
  Writeln('Developer is taking a break.');
end;

var
  Worker: IWorker;
begin
  Worker := TManager.Create;
  Worker.Work;
  Worker.TakeBreak;

  Worker := TDeveloper.Create;
  Worker.Work;
  Worker.TakeBreak;
end.

```