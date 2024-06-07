# Open Closed Principle (OCP)

Das Open Closed Principle besagt, dass eine Klasse offen für Erweiterungen sein sollte, aber geschlossen für Modifikationen. 

Das bedeutet, dass eine Klasse durch Ableitung erweitert werden sollte, anstatt den bestehenden Code zu ändern.

## Beispiel (Pascal)

### Beispiel

```pascal
program OCPExample;

uses
  SysUtils, Classes;

type
  TMessageProcessor = class
  public
    procedure ProcessMessage(const Message: string); virtual; abstract;
  end;

  TEmailProcessor = class(TMessageProcessor)
  public
    procedure ProcessMessage(const Message: string); override;
  end;

  TSMSProcessor = class(TMessageProcessor)
  public
    procedure ProcessMessage(const Message: string); override;
  end;

  TMessageHandler = class
  private
    FProcessors: TList;
  public
    constructor Create;
    destructor Destroy; override;
    procedure AddProcessor(Processor: TMessageProcessor);
    procedure HandleMessage(ProcessorClass: TClass; const Message: string);
  end;

{ TEmailProcessor }

procedure TEmailProcessor.ProcessMessage(const Message: string);
begin
  Writeln('Processing Email: ', Message);
end;

{ TSMSProcessor }

procedure TSMSProcessor.ProcessMessage(const Message: string);
begin
  Writeln('Processing SMS: ', Message);
end;

{ TMessageHandler }

constructor TMessageHandler.Create;
begin
  FProcessors := TList.Create;
end;

destructor TMessageHandler.Destroy;
begin
  FProcessors.Free;
  inherited;
end;

procedure TMessageHandler.AddProcessor(Processor: TMessageProcessor);
begin
  FProcessors.Add(Processor);
end;

procedure TMessageHandler.HandleMessage(ProcessorClass: TClass; const Message: string);
var
  I: Integer;
  Processor: TMessageProcessor;
begin
  for I := 0 to FProcessors.Count - 1 do
  begin
    Processor := TMessageProcessor(FProcessors[I]);
    if Processor.ClassType = ProcessorClass then
    begin
      Processor.ProcessMessage(Message);
      Exit;
    end;
  end;
  Writeln('No processor found for the specified class');
end;

var
  Handler: TMessageHandler;
begin
  Handler := TMessageHandler.Create;
  try
    Handler.AddProcessor(TEmailProcessor.Create);
    Handler.AddProcessor(TSMSProcessor.Create);
    
    Handler.HandleMessage(TEmailProcessor, 'Hello via Email');
    Handler.HandleMessage(TSMSProcessor, 'Hello via SMS');
  finally
    Handler.Free;
  end;
end.


```