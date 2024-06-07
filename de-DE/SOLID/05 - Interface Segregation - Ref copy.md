# Interface Segregation Principle (ISP)

Das Interface Segregation Principle besagt, dass eine Klasse nicht gezwungen sein sollte, Methoden zu implementieren, die sie nicht benötigt.

D.h. Interfaces sollten spezifisch für die Klassen sein, die sie implementieren.


## Beispiel (Pascal)

### Beispiel

```pascal
program ISPExample;

{$MODE OBJFPC}

type
  IWork = interface
    procedure Work;
  end;

  ITakeBreak = interface
    procedure TakeBreak;
  end;

  TManager = class(TInterfacedObject, IWork, ITakeBreak)
  public
    procedure Work;
    procedure TakeBreak;
  end;

  TDeveloper = class(TInterfacedObject, IWork)
  public
    procedure Work;
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

var
  Worker: IWork;
  BreakTaker: ITakeBreak;
begin
  Worker := TManager.Create;
  Worker.Work;
  
  if Supports(Worker, ITakeBreak, BreakTaker) then
    BreakTaker.TakeBreak;

  Worker := TDeveloper.Create;
  Worker.Work;
  
  if Supports(Worker, ITakeBreak, BreakTaker) then
    BreakTaker.TakeBreak
  else
    Writeln('This worker does not take breaks.');
end.


```